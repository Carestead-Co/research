<!-- SPDX-License-Identifier: CC-BY-4.0 -->

# Scripture research, class A: statistical and constraint models

**Status:** Pre-registration, 2026-10-20. Tracks are built in the order below.
Each track's results go into its own dated report next to this file. A change
to a method, threshold or switch below made AFTER a target result was seen is
recorded in that report as a deviation, with its reason.

**What this is.** A research project, not a product feature. It asks the Bible
questions that are decidable in principle from evidence: who wrote a text,
whether a passage belongs to its book, when events happened, and whether two
genealogies can both stand. It does not ask what a text means or whether it is
true; those questions (classes B and C) are out of scope. Nothing here ships to
the Herald panel or reads tenant data. ADR 0168 (reference tools) is therefore
not engaged; if a result ever feeds a product, it is decided then.

**Where the code is.** `flock-scripture-import research <track>`
(`apps/api-server/src/bin/scripture_import/research.rs` and its `research/`
modules). Every track prints a Markdown report and writes no database.

## Rules every track follows

1. **Pinned inputs only.** Datasets come from `data/scripture/manifest.toml`,
   public domain or CC BY 4.0, verified by sha256. Hand-encoded tables (the
   chronology and genealogy data) are committed under `data/scripture/research/`,
   and every row cites the verse it was read from.
2. **Deterministic.** The same inputs, switches and seed give the same bytes.
   Random procedures use the seeded generator in
   `flock_core::scripture_connections::eval` and print their seed.
3. **Every assumption is a switch, and every report shows results across its
   switches.** Example switches: accession versus non-accession year counting;
   the crescent-visibility threshold; whether two same-named people are one
   person. No setting is a hidden default.
4. **Validate before the target.** Each track runs its validation first, on
   synthetic data and then on cases whose answer is known. Only a method that
   passes its pre-registered bar is applied to the target; a method that fails
   is reported as failed, and the target is not scored by it.
5. **The price of "the text is wrong here" is a parameter.** Wherever a model
   may treat a number in the text as corrupted, that costs a stated amount, and
   the report shows how the answer moves as the cost changes. Readers who hold
   the text inerrant and readers who do not then read the same table.

## Track 1: foundation (the research corpus)

`research corpus`. The tagged New Testament from the pinned STEPBible TAGNT
files as one token stream: a base Strong's number, STEPBible's grammar code and
the surface word per token, in canonical order. Function lemmas are KEPT; the
Gospel-connections ranker drops them, but writing-style models live on them.
Edition rule: a verse's NA27/28 words, or its TR words for a verse with none
(Mark 16:9-20 and John 7:53-8:11, which NA28 double-brackets). The report prints
the size per book and a fingerprint (sha256 of the stream) that every later
report cites. On the current pins: 137,589 tokens in 27 books, 40 fallback
verses.

## Track 2: writing style (Hebrews; Mark 16:9-20; John 7:53-8:11)

### Questions

* **2a.** Is Hebrews Pauline?
* **2b.** Which New Testament author group is Hebrews closest to, with
  "none of them" as an allowed answer?
* **2c.** Does Mark 16:9-20 depart from the vocabulary of Mark 1:1-16:8 more
  than any stretch of Mark does from the rest of Mark?
* **2d.** Does John 7:53-8:11 fit John's vocabulary or Luke's better?

### Author groups (training classes)

| Group | Books |
|---|---|
| Paul (undisputed) | Rom, 1Cor, 2Cor, Gal, Phil, 1Thess, Phlm |
| Luke | Luke, Acts |
| Johannine | John, 1John, 2John, 3John |
| Matthew | Matt |
| Mark | Mark (without 16:9-20) |
| Peter | 1Pet |
| James | Jas |
| Revelation | Rev |

Eph, Col, 2Thess, the Pastorals, 2Pet, Jude and Hebrews are never training
data. John's Gospel excludes 7:53-8:11.

### Features and units

* **F1:** relative frequencies of the 150 most frequent lemmas in the New
  Testament (counted over all tokens).
* **F2:** relative frequencies of the 100 most frequent grammar codes,
  truncated to their first two hyphen-separated fields (`V-2AAP-NSM` becomes
  `V-2AAP`).
* **Units:** consecutive 1,000-token chunks within a book; a remainder of 500
  or more tokens is its own chunk, otherwise it joins the last chunk. Hebrews
  (4,954 tokens) gives 5 chunks.

### Methods

* **M1, Cosine Delta.** Z-score each feature over all training chunks. An
  author's profile is the mean z-vector of its chunks. Distance is 1 minus the
  cosine similarity.
* **M2, General Impostors.** For a questioned text X (the mean z-vector of
  its chunks) and candidate group A: 1,000 rounds (seed 20261020), each
  sampling half the features. Each round draws 5 chunks of A and 5 impostor
  chunks, with replacement, and scores when X's best cosine similarity to the
  drawn A chunks beats its best similarity to the drawn impostors. Impostors
  are the chunks of every other group. The score is the share of winning
  rounds. The z-scores are fit on the training chunks of the experiment at
  hand, never on X.
* **Amended before any target run (2026-10-20).** The first draft compared
  A's mean profile with every impostor chunk. A mean is smoother than a
  single chunk, and a group with many chunks offers more chances to win, so
  the draft favoured large groups and profiles over chunks. Drawing the same
  number of chunks on each side compares like with like. Ties for theta (see
  below) go to the highest maximizing threshold.

### Validation (run first) and the bar

* **V2a, leave one book out.** For each undisputed Pauline letter, rebuild
  Paul's profile without it and score it against Paul (positives). Negatives
  are Jas, 1Pet and 1John scored against Paul, with each one's own group
  removed from the impostors and the profiles.
* **V2b.** Acts scored against a Luke profile built from Luke alone.
* **V2c, chunk length.** V2a repeated at 500 and 2,000 tokens, reported
  alongside.
* **Bar:** with F1 + F2 at 1,000 tokens, M2's area under the ROC curve over
  V2a's positives and negatives is at least 0.90. The threshold theta is fixed
  at the value maximizing balanced accuracy on V2a. V2b's score is at least
  theta. If the bar fails, 2a and 2b are reported as "method not validated"
  and not answered.

### Target scoring

* **2a:** M2's score for Hebrews against Paul, compared with theta, and its
  percentile among V2a's positives and among its negatives.
* **2b:** M2's score against every group. "None of them" when every score is
  below theta. M1's distances are reported beside it.

### 2c and 2d: short passages

Each passage is about 170 to 190 tokens, too short for 2a's method. The
statistic instead is **vocabulary novelty**: the share of a passage's lemma
types, proper names excluded, that occur nowhere else in the comparison text.
A proper name is a noun whose grammar code ends in `-P` (person) or `-L`
(place), or is indeclinable `N-PRI`; titles (`-T`, such as "Christ") stay in.
(Amended before any target run: the first draft named only `N-PRI`, which
misses every declined name.)

* **Null distribution:** every window of the same token length that starts at a
  verse boundary in the comparison book (the passage removed), each scored
  against the book minus that window.
* **p-value:** (1 + windows at least as novel) / (1 + windows).
* **Pre-registered reading:** 2c, "departs" if p < 0.01. 2d, "fits Luke better
  than John" if its novelty is significant against John (p < 0.01) and not
  against Luke (p at least 0.05), and conversely.
* **Power check (run first):** plant 200 seeded windows of the passage's
  length taken from one book into another (Luke into Mark, Mark into Luke,
  Luke into John, John into Luke). The detection rate at p < 0.01 is the test's
  power. Below 0.5, the passage results are reported as underpowered.

## Track 2b: short-passage style with power (Mark 16:9-20; John 7:53-8:11)

**Status:** pre-registered 2026-10-20, before any code for it was written or
any target scored. Run once the same day, unchanged:
[scripture-research-results-style-short-2026-10-20.md](scripture-research-results-style-short-2026-10-20.md).
Track 2's passage tests were underpowered for Mark
(planted Luke windows detected 10% of the time) and for John against Luke
(0.5%), because lemma novelty uses one bit of each token: "seen before or
not". Track 2b asks the same two questions with statistics that use more of
each token: how often the function words occur, and how the grammar codes
follow each other. It is held to the same planted-window power floor. The
name is the programme's, not track 2's question 2b (Hebrews).

`research style-short`. It reads the track 1 corpus and nothing else.

### Questions

* **M.** Does Mark 16:9-20 (169 tokens) depart from the style of the rest of
  Mark more than a same-length stretch of Mark does?
* **J.** Does John 7:53-8:11 (193 tokens) fit John's style or Luke's better?

### Token streams

Every token becomes one symbol in each of two streams. "The counting corpus"
is the New Testament with both disputed passages removed.

* **FW, function words with content masked.** A token is a *function token*
  when its grammar code's first hyphen field is one of `T`, `CONJ`, `PREP`,
  `PRT`, `ADV`, `COND`, `INJ`, `P`, `R`, `D`, `I`, `X`, `F`, `S`, `C`, `K` or
  `Q` (article, conjunction, preposition, particle, adverb, conditional,
  interjection and the pronoun classes). A function token whose lemma has at
  least 20 function tokens in the counting corpus is its lemma (`L:G2532`).
  Every other token is its first grammar field (`P:N`, `P:V`, `P:A`, or a rare
  function word's class). Content is masked, so a passage's subject matter
  cannot carry the score; Mark's `καί` and `εὐθύς`, Luke's `δέ` and John's
  `οὖν` can.
* **GR, grammar codes.** Track 2's F2 truncation, the code's first two hyphen
  fields (`V-2AAP-NSM` becomes `V-2AAP`).

### Models

* *The book model B* of a host book: its tokens with the disputed passage
  removed, counted along its token list. When a window of the host is scored
  (the null), B is fit on the book **minus that window**: the window's
  symbols and every bigram touching them are removed.
* *The reference model R:* the books of track 2's eight author groups, minus
  the host's group, and minus the donor's group in a power check; bigrams are
  counted within each book. R is what "New Testament Greek in general" looks
  like to the test.
* *Unigrams* are add-0.5 smoothed over the stream's alphabet in the counting
  corpus. *Bigrams* are Witten-Bell smoothed, backing off to that unigram:
  `P(b after a) = (c(a,b) + T(a) P(b)) / (c(a) + T(a))`, where `T(a)` is the number
  of distinct symbols seen after `a`, and `P(b after a) = P(b)` when `a` was never
  seen. Neither has a tuned constant.

### Candidate statistics (larger means more foreign)

| # | Name | Statistic for a window w of n tokens |
|---|---|---|
| S1 | FW profile divergence | 2 sum over symbols s of o_s ln(o_s / (n P_B(s))), FW unigrams (a G-statistic against B) |
| S2 | GR profile divergence | the same over GR unigrams |
| S3 | FW bigram ratio | mean over w's n - 1 internal bigrams (a, b) of ln P_R(b after a) minus ln P_B(b after a), FW stream |
| S4 | GR bigram ratio | the same, GR stream |
| S5 | combined | S3 + S4 |

S1 and S2 measure how far the window's profile is from its book's. S3 to S5
ask whether the window fits Greek in general better than it fits its book:
a construction rare everywhere cancels out, and only rarity *in this book*
counts. S4 is the "grammar-code n-gram surprisal under a book model fit
without the passage", made relative to R.

### The null, the p-value and the reading

* *Null:* every window of the passage's token length that starts at a verse
  boundary of the host book (the disputed passage removed), each scored
  against B fit without it, as in track 2.
* *p-value:* (1 + windows at least as extreme) / (1 + windows), one-sided.
* *Reading (track 2's):* M, "departs" if p < 0.01. J, "fits Luke better than
  John" if p < 0.01 against John and p at least 0.05 against Luke, and
  conversely; otherwise "does not separate John from Luke". The report
  also states whether each p < 0.01 survives a Bonferroni correction over the
  three tests (p < 0.0033); that line is descriptive, the reading is the
  uncorrected one, as in track 2.

### Choosing one statistic, without the targets

Only one statistic is applied to the passages, so there is no correction for
five candidates. It is chosen on a **selection study** that never reads
Mark 16:9-20 or John 7:53-8:11 (removed from every stream) and never plants
into or out of Mark, Luke or John, the power gate's books; they appear only
inside R:

* Planted windows Matthew into Acts and Acts into Matthew, each at 169 and at
  193 tokens: four cells, 200 windows each, seeds `20261020 + 100 + i`
  (i = 0..3 in that order).
* A planted window starts at a verse boundary of the donor (its disputed
  passages removed), chosen uniformly; it is scored against the whole host,
  with R built without the host's and the donor's groups, against the
  host's null under that same R. It is detected when p < 0.01.
* **The chosen statistic** is the one with the highest mean detection rate
  over the four cells; a tie goes to the lower number.
  The passages are scored by it alone. The other candidates' passage p-values
  are never computed.

### The power gate (run after selection, before the passages)

* Planted windows, 200 each, seeds `20261020 + 200 + i`, by the selection
  study's planting rule, with the chosen statistic:
  * i = 0, Luke into Mark at 169 tokens: gates M.
  * i = 1, Luke into John at 193: gates J against John.
  * i = 2, John into Luke at 193, and i = 3, Mark into Luke at 193: gate J
    against Luke, which takes the lower of the two.
* **Power below 0.5 means "underpowered"**, and that test's p is printed but
  not read. Track 2's Mark into Luke pair was at 169 tokens; here it is at
  193, the length of the only test against Luke.
* The power is conservative by construction: the planted text's own author
  group is left out of R, so the donor is an author the test has never seen.
  The passages are scored with R holding every group but the host's.
* Every candidate's gate power is printed beside the chosen one's. That row
  is descriptive: it decides nothing and reads no target.

### What breaks the inference

* **Edition.** Both passages are read from the TR (track 1); every null window
  is NA27/28 text. If the TR's spelling or particles differ systematically
  from NA's, a passage looks foreign because of its edition. The report
  cannot separate the two; a departure is read with that caveat.
* **Genre inside a book.** The null holds every kind of stretch the book has,
  narrative and discourse alike, so a narrative passage is compared with the
  book's own narrative among the rest. A book with little narrative would make
  a narrative passage look foreign; John has enough.
* **A positive answer is not authorship.** "Departs from Mark" says the
  passage's function words or grammar are unlike Mark's beyond the book's
  own variation. It does not say who wrote it.

## Track 2c: Mark 16:9-20 against texts that did not copy Mark

**Status:** pre-registered 2026-10-20, before any code for it was written and
before its target was scored. Run once the same day, unchanged:
[scripture-research-results-style-mark-2026-10-20.md](scripture-research-results-style-mark-2026-10-20.md)
(underpowered, power 0.280). The name is the programme's, not track 2's
question 2c. Track 2b's test of Mark was underpowered (planted Luke windows
detected 8.5% of the time). Its report gave the reason: Luke copied Mark, so
a planted Luke window is often Mark's own text, and the reference model for
Mark held Matthew and Luke, which both absorbed Mark. Track 2c asks 2b's
question M again with the design that report named. The donors and the
reference are texts that did not copy Mark. Everything else is 2b's,
unchanged.

`research style-mark`. It reads the track 1 corpus and nothing else.

### Question

* **M.** Does Mark 16:9-20 (169 tokens) depart from the style of the rest of
  Mark more than a same-length stretch of Mark does, when "Greek in general"
  is modelled only by texts that did not copy Mark?

### What is reused from 2b, unchanged

* The FW and GR streams, the counting corpus (the New Testament without both
  disputed passages; it only decides which function lemmas keep a symbol and
  the smoothing alphabets), add-0.5 unigrams and Witten-Bell bigrams.
* The book model B: Mark without 16:9-20, and for a null window, without that
  window too.
* The null: every 169-token window starting at a verse boundary of Mark (the
  passage removed), scored against B fit without it. The p-value is
  (1 + windows at least as extreme) / (1 + windows), one-sided. Alpha 0.01.
* **The statistic is S5** (FW bigram ratio plus GR bigram ratio), as chosen
  by 2b's selection study. There is no new selection. 2b's gate table already
  printed every candidate's power for Luke into Mark, so a selection made now
  would be made by someone who had seen how each candidate behaves in Mark.
  Fixing S5 removes that freedom.
* 200 planted windows per donor, the power floor 0.5, and 2b's planting rule:
  a window starts at a verse boundary of the donor, chosen uniformly, and is
  scored against the whole host. Its p comes from the host's null under the
  same reference model.

### What changes: the reference and the donors

* **The reference R** is track 2's author groups Paul, Johannine, Peter,
  James and Revelation. That is the eight groups minus Mark, Matthew and
  Luke. The Luke group goes whole, Acts with it: Acts has no Markan source
  material, but its author rewrote Mark in the Gospel. With the whole group
  out, R holds no text by anyone who copied Mark. And for the Acts donor, the
  gate then uses exactly the R the passage is scored with. As in 2b, a
  gate pair also removes the donor's own group. So the Paul donor's R is
  Johannine, Peter, James and Revelation, and the Revelation donor's is Paul,
  Johannine, Peter and James. Hebrews belongs to no group and removes nothing.
* **The donors**, 200 windows of 169 tokens each, seeds `20261020 + 300 + i`:
  * i = 0, **Acts.** Narrative, the nearest in genre to the passage
    (appearances, a commission, signs, an ascension). It carries no Markan
    blocks. Shared authorship with Luke may carry some Markan phrasing into
    it, which makes it a harder donor, not an easier one.
  * i = 1, **Paul**, the seven undisputed letters as one pool. A window
    starts uniformly over the pooled verse boundaries and stays inside its
    letter. All seven were written before Mark, so none can have copied it.
  * i = 2, **Hebrews.** No literary relation to Mark.
  * i = 3, **Revelation.** No literary relation to Mark.
* **Not donors.** Matthew and Luke copied Mark. John is left out because
  whether John knew Mark is disputed. 1 Peter and James are short, and they
  are part of R.
* **The gate is the lowest of the four donors' powers.** Below 0.5 the test
  is "underpowered", and its p is printed but not read. Every donor's power
  is printed.

### The reading

* **Powered and p < 0.01: "departs from Mark".** Power does not affect this
  reading's validity. The null is Mark's own windows, so the false-alarm rate
  is 1% whatever the donors were. The departure says that the passage's
  function words and grammar fit non-Synoptic Greek better than they fit
  Mark, beyond Mark's own variation.
* **Powered and p at least 0.01: "no departure detected".** This is NOT
  "Mark wrote it", and the report's verdict line says so. See the first
  limit below.
* **Underpowered.** Then S5 cannot tell Mark from Greek that shares neither
  Mark's sources nor, mostly, its genre. That is a stronger negative than
  2b's: at 169 tokens, this statistic cannot answer M at all.
* **Descriptive lines.** Bonferroni over the two style tests of M, 2b's and
  this one (p < 0.005); 2b's was not read, but it was run. Then a
  sensitivity run: the gate and the passage repeated with R also
  without the Johannine group (the same seeds), for readers who hold that
  John knew Mark. It decides nothing.

### Limits, and how they shape the reading

* **The power is an optimistic bound.** The donors are less like Mark
  16:9-20 than its real author would be if that author was not Mark: that
  author wrote a Gospel ending, while the donors are a history, letters, a
  homily and an apocalypse. The letters and Hebrews differ from Mark in
  genre as well as in hand, and much of their power is genre. So a powered
  gate is necessary, not sufficient, for reading "no departure" as evidence.
  A later writer imitating Gospel narrative would be detected less often than
  any donor here, by an amount this design cannot measure. Acts, the nearest
  in genre, is printed beside the gate so the reader can see how much the
  floor rests on it.
* **The compilation hypothesis is not tested.** One case for a later ending
  is that it summarises Luke 24, Acts, Matthew and John. R has no Matthew or
  Luke-Acts, so phrasing borrowed from them earns no credit as "general
  Greek". Track 2c asks only whether the passage is unlike Mark in ways that
  non-Synoptic Greek explains. A non-departure therefore says nothing against
  compilation from the other Gospels.
* **What was seen first.** 2b's S5 result for M, p = 0.094 (statistic 0.387,
  null median 0.090, with R holding Matthew and Luke), was printed before
  this design was written. So were the design's two changes, named in 2b's
  report as "what would change the answer". The safeguard is that only the
  reference and the donors change, and both follow from one stated rule: no
  text that copied Mark. The statistic, null, length, alpha, floor and trial
  count are 2b's. Under this R the passage's statistic has not been computed.
* **Edition and authorship**, as in 2b. The passage is TR text and Mark's
  windows are NA27/28. "Departs from Mark" does not say who wrote the passage.

## Track 3: chronology as constraint solving

### 3a. The divided monarchy

* **Data:** `data/scripture/research/kings.tsv` (each reign's stated length and
  verse) and `synchronisms.tsv` (each "in the Nth year of X, Y became king"
  statement, plus the cross-kingdom events), transcribed from the BSB with
  every row citing its verse.
* **Model:** an integer start year per reign. Under a counting method, a reign
  of L years started in year s has its year n in s + n - 1 (non-accession, the
  accession year counted as year 1) or in s + n (accession).
* **Costs:**

  | Item | Cost | Notes |
  |---|---|---|
  | Successor starts in its predecessor's last year | 0 | |
  | Co-regency (successor starts earlier) | `c_coregency` | Up to 24 years |
  | Interregnum (successor starts later) | `c_gap` | Up to 12 years |
  | Reign length read as corrupted | `c_emend` | |
  | Synchronism not met | `c_emend` | It is a textual correction too |

* **Solver:** exact dynamic programming over the accession events in the
  order Kings narrates them. The state is the current start year in each
  kingdom.
* **Anchors (hard constraints):**
  * Ahab reigning in 853 BC (Qarqar).
  * Jehu reigning in 841 BC (tribute to Shalmaneser III).
  * Menahem reigning in 738 BC (tribute to Tiglath-pileser III).
  * Hoshea's 9th year in 723 or 722 BC (the fall of Samaria).
  * Hezekiah's 14th year in 701 BC (Sennacherib).
  * Zedekiah's accession in 597 BC (Babylonian Chronicle).
  * Zedekiah's 11th year in 587 BC or 586 BC, a switch.
* **Switches:**
  * Counting-method profiles: both kingdoms accession; both non-accession;
    Israel non-accession and Judah accession; and Thiele's era-by-era
    profile.
  * Costs: `c_emend` in {1, 3, 10}, with `c_coregency` = `c_gap` = 1.
  * The 587/586 anchor.
* **Validation:** 100 synthetic chronologies of the same shape with known
  dates. Derive their synchronisms and lengths, corrupt k in {0, 1, 2, 3} of
  them, and solve. **Bar:** exact recovery of every start year in at least 95%
  of cases with k at most 2, and the corrupted items flagged with at least
  0.9 precision.
* **Reported:**
  * the minimum-cost solution per switch setting, with its dates;
  * every co-regency, interregnum and emendation it needs;
  * how many solutions tie at that minimum.
* **Derived:** the date the literal "480th year" of 1 Kgs 6:1 gives for the
  Exodus, under each solution. The symbolic reading (12 x 40) is reported as
  undated.
* **Implementation details** (fixed in the code before the first run, and
  recorded here after it):
  * Events follow the verse of each reign's formula in Kings. The two first
    kings start together.
  * A reign "ends" in the year its successor starts. Under a co-regency or
    interregnum, it ends at its stated end instead. A "reigning in" anchor
    must fall within that span.
  * An emended length lets a reign run up to 80 years.
  * Identical claims made in two verses count once.
  * A statement whose other king is no longer on the throne at the later
    accession, or that gives no regnal year, cannot be held in the DP state
    (2 Kgs 15:30, 2 Chr 16:1). It is scored on each solution but does not
    steer it.
  * The synthetic chronologies shuffle the real lengths within each kingdom,
    with no co-regencies or gaps, and use Thiele's counting. Each accession
    gets one synchronism, and the anchors keep their real shape. A
    corruption moves a length or a synchronism by 1 to 10 years.
  * "Exact" means a unique optimum equal to the truth.

### 3b. The Passion week

* **Astronomy:**
  * Mean new moons with Meeus's (1998, ch. 49) periodic terms.
  * Delta T from the Espenak-Meeus polynomial.
  * Solar longitude for the vernal equinox (Meeus ch. 25).
* **Crescent visibility:** first evening at Jerusalem when the moon's age at
  sunset is at least A hours, A in {15, 20, 24, 30} (the visibility switch). Nisan
  1 begins at that sunset, so Nisan 14 runs from sunset 13 days later. Nisan is
  the first month whose 15th falls on or after the vernal equinox.
* **Years:** AD 26 to 36, Pilate's tenure.
* **Hypotheses:**
  * Synoptic: the crucifixion Friday is Nisan 15.
  * Johannine: the crucifixion Friday is Nisan 14.
  * Jaubert: the Last Supper on the Tuesday evening of the Qumran 364-day
    calendar.
* **Validation:**
  * The new-moon routine must reproduce Meeus's worked example 49.a
    (1977 February, JDE 2443192.65118) within 0.0001 days.
  * The model must find the published Johannine candidates, Friday 7 April
    AD 30 and Friday 3 April AD 33, at A = 20 hours.
* **Reported:** per year and per A, the Julian date and weekday of Nisan 14,
  and which hypotheses each year admits.

## Track 4: genealogies as a graph with hypotheses

* **Data:** `data/scripture/research/genealogies.tsv` (the lines) and
  `genealogy-people.tsv` (candidate identities across them), transcribed from
  the BSB.
  It covers Matt 1:1-16, Luke 3:23-38, Ruth 4:18-22, 1 Chr 2-3, Gen 5 and 11,
  the Zerubbabel statements (Ezra 3:2, Hag 1:1, and 1 Chr 3:19's Pedaiah) and
  the kings of Judah from 1-2 Kings. Every row cites its verse. Person identity
  across lines is a switch, never an assumption.
* **Validation first:** align Matthew's kings (Matt 1:7-11) to the kings of
  Judah by sequence alignment. **Bar:** it finds exactly the omissions of
  Ahaziah, Joash, Amaziah and Jehoiakim, with no false positive.
* **Hypotheses:**

  | Id | Hypothesis |
  |---|---|
  | H1 | Africanus's levirate (Joseph natural son of Jacob, legal son of Heli) |
  | H2 | Luke gives Mary's line |
  | H3 | Matthew's royal-legal line with Luke's natural line, Matthew's and Luke's Shealtiel and Zerubbabel the same men (a levirate or adoption at Shealtiel) |
  | H4 | As H3, but Luke's Shealtiel and Zerubbabel are different men of the same names |

* **Scored per hypothesis:**
  * the assumptions it needs, counted by kind (identity merges, legal or
    levirate links, omitted generations);
  * the plausibility of each line's generation count over its anchored time
    span (David about 1000 BC, the exile 597 BC, the birth of Jesus about
    5 BC). Generation length is modelled as normal with mean 30 years and
    standard deviation 7, truncated to 15 to 60.
* **The decidable claims are consistency and assumption count.** Which
  hypothesis is historically true is not claimed.
* **Implementation details** (fixed in the code before the first run, and
  recorded here after it):
  * **Conflicts.** A conflict is a person whose sources name different
    fathers.
  * **Omissions.** An omission covers a conflict when one stated father is an
    ancestor of the other, within three generations, in some source.
  * **Consistency.** Every other conflict needs an assumption that names it.
  * **The identity switch.** H1 and H2 do not speak to it, so they are scored
    under both settings.
  * **Anchors.** The exile anchors Jeconiah's generation. Under "same men",
    Luke's Neri, Shealtiel's other father, stands in that generation.
  * **Tail probability.** Each span's p is two-sided, from the exact
    convolution of whole-year generation lengths.
  * **Calibration, added after the first run and descriptive only.** The
    same prior is applied to the attested royal line of 1 Chr 3.

## Track 5: manuscript family trees (stemmatics)

* **Benchmark:** no published artificial tradition has a usable licence (the
  Helsinki Parzival, Notre Besoin and Heinrichi sets state none or restrict
  use), so the benchmark is generated here. The generator draws a random
  copying tree of 20 to 40 witnesses, some exemplars lost, and 500 variation
  units. Each copy changes a unit with probability mu and adopts a second
  exemplar's readings with probability kappa (contamination); a change may
  coincide with another copy's change with probability rho.
* **Methods:**
  * neighbour joining over pairwise disagreement;
  * maximum parsimony by stepwise addition and nearest-neighbour
    interchange.
* **Metric:** the normalized Robinson-Foulds distance between the true and
  inferred trees over the observed witnesses.
* **Bar:** at mu = 0.02, kappa = 0 and rho = 0.05, the mean normalized
  Robinson-Foulds distance over 50 traditions is 0.25 or less. The report shows
  how the distance degrades as kappa rises.
* **Application:**
  * *The data:* the Münster INTF NTVMR transcriptions (CC BY 4.0, per
    manuscript, through its API), pinned by sha256 like every other input,
    after the owner approves the download list.
  * *The question:* given a tree built from the variation units OUTSIDE the
    passage, is the passage's presence at the root (in the archetype) or its
    absence the more parsimonious history?
  * *What breaks the inference:* the gain of a twelve-verse block is one
    event, but a loss can come from a lost final leaf. So the report states the
    parsimony counts under equal costs and under a switch that makes loss
    cheaper than gain.
  * *If the data is not available,* the report says so and stops after
    validation.
* **Implementation details.** The generator's details were fixed before the
  validation run. Everything about the application was fixed before the
  application ran.
  * *Generator:*
    * Each new copy has a uniformly random earlier exemplar.
    * The total is the observed count plus half again. The archetype and a
      random third of all copies are lost.
    * Contamination takes each unit from a random second exemplar with
      probability kappa.
    * A coincident change reuses one of that unit's earlier non-archetype
      readings.
  * *Metric:* normalized RF is |A xor B| / (|A| + |B|) over the observed
    witnesses' splits. The true copying tree is not binary.
  * *Diagnostic,* added after the validation run: the share of true splits
    each builder recovers.
  * *Witnesses:* every Greek continuous-text manuscript that the NTVMR
    catalogue lists as containing Mark 16:8, or John 7:52, and dates to
    AD 1000 or earlier. P66 and P75 are added for John. Each must have a
    published transcription of Mark 15-16, or John 7-8.
  * *First hand only.* Corrections, notes, running titles and editorial
    supplements are skipped. A word with lost letters is dropped: it gives
    no reading, and the base words and gaps a lost stretch spans are missing
    data, never an omission (made explicit before merge, after review).
  * *Spelling folds* the itacisms ει/ι, αι/ε, οι/υ, η/ι and ω/ο, then
    nu-movable (a movable ν supplied where Greek may drop it: -σι, ἐστί, a
    third-person -ε, so no real ν is lost).
  * *Variation units:* for each verse outside the passage, the most common
    folded form is the base. Each witness is aligned to it by longest common
    subsequence, with adjacent unmatched words paired as substitutions. Each
    base word gives one unit and each gap between base words gives another.
    A unit is kept only when at least two readings each have two witnesses.
  * *Placed witnesses:* those attesting at least 30% of the units.
  * *Presence states:*
    * Present: words of the passage stand between the verses before and
      after its place. For Mark, that means after 16:8.
    * Absent: the text runs on past that place with no lacuna marked.
    * Otherwise undecidable, which is missing data.
  * *The root:* Sankoff parsimony of the presence character with the root
    on each edge. The report tallies the edges favouring presence, absence or
    a tie, and for neighbour joining gives the result at the midpoint root.
  * *The cost switch:* loss costs a third of gain (gain 3, loss 1).

## Track 5b: where the adultery story stood (a multistate location)

**Status:** pre-registered 2026-10-20. Not implemented and not run.
**Too thin to run under the licence rule** (see the data section). The data
was measured from NTVMR catalogue and search metadata. The approved fetch
then measured each file's licence, and every IGNTP-owned file fails the CC BY
or public domain rule.

### Question

In the Greek manuscripts John 7:53-8:11 has no fixed home. Most carry it
after John 7:52. Others carry it after John 7:36, after John 21:25, after
Luke 21:38 (family 13) or after Luke 24:53, and the earliest lack it. Given a
tree built from the text OUTSIDE the passage, which history is the most
parsimonious: the passage at one of those places in the archetype, then
moved, or absent from the archetype and then inserted, possibly more than
once?

* *The archetype* is the latest common ancestor of the placed witnesses: the
  root of the extant Greek tradition, not the autograph.
* *Why track 5 cannot answer it.* Track 5 reads only John 7-8, so a witness
  carrying the passage after Luke 21:38 scores as "absent". Its presence
  character is binary, so "present elsewhere" cannot be said. Its AD 1000
  cutoff removes the later relocating witnesses (family 13, 225). Its
  INTF-only source removes the early ones: 1582 (AD 948) has no INTF
  transcription of John 7, 8 or 21, and 565 (IX) none of John 7 (measured;
  565's John 8 and 21 are pending).

### Witnesses

* Every Greek continuous-text manuscript (NTVMR docID 10000-39999: papyri,
  majuscules and minuscules; lectionaries are out) that the catalogue lists as
  containing John 7:52 and that has an admitted transcription of John 7 and
  John 8. There is no date cutoff. P66 and P75 stay in, as in track 5.
* John 7-8 places the witness on the tree. John 21, Luke 21 and Luke 24 are
  read only to find the passage, for every witness that has them.
* **Two sources, by the owner's ruling (2026-10-20).** The NTVMR holds
  transcriptions under owners.
  * *The INTF's own:* the API's default owner, `PUBLISHED`, as in track 5.
    It is asked for by OMITTING `userName`.
  * *The IGNTP's:* owner `IGNTP`. Many more witnesses carry these, and the
    default fetch does not return them.
  * *One per chapter, chosen by the catalogue's owner counts, never by what
    a fetch returns.* For each witness and chapter, `transcript/exists`
    gives each owner's page count. The INTF's file is used where its count is
    above zero; otherwise the IGNTP's, where its count is.
  * *Fetched by owner.* An IGNTP fetch names its owner (`&userName=IGNTP`).
    An INTF fetch omits `userName`. The ledger records the owner either way.
  * *Deviation, before any run (2026-10-20).* This rule first said every
    fetch names its owner, with `&userName=PUBLISHED` for the INTF. Named,
    that owner returns zero pages: 33's John 7 counts 2 INTF pages with
    `userName` omitted and 0 with it named. So the INTF is asked for unnamed,
    which is what track 5 did. The choice of owner still comes from the
    counts, and the INTF is fetched only where its count is above zero, so
    the 036 case (unnamed text where the INTF count is zero) cannot be
    chosen.
  * *Why not by text.* The default fetch returned text for 036's John 7
    under an INTF header, although 036 has no INTF pages of John 7, only
    IGNTP ones. Choosing by "has text" would record that file as the INTF's,
    read the licence from the wrong header, and put an IGNTP transcription
    into the INTF-only switch.
  * *A fetch that disagrees with the counts* (text where its owner's count is
    zero) is reported and excluded, not reassigned.
  * *A chosen file that comes back empty* (a count above zero, no text: the
    045 case in track 5) falls back to the other owner if its count is above
    zero. Otherwise the chapter counts as untranscribed. Either way, the
    report lists it.
* **Admission is per file, by licence.** A file is admitted only if its TEI
  header's `availability` states CC BY (any version) or public domain.
  * The licence is recorded in the ledger row.
  * `data/scripture/ATTRIBUTION.md` credits the IGNTP when the first
    IGNTP-owned file is pinned.
  * A file with any other licence, or none, is excluded. The report lists it
    by document, chapter and the licence text found.
* First hand only, as in track 5. A corrector's insertion (1333's
  supplement after Luke 24:53 is the known case) is not the first hand's
  location. Marginal text is skipped. Doubt marks (obeli, asterisks) are
  ignored: a first hand that copies the passage with an obelus carries it.

### The location character

Each witness gets the SET of states its transcribed chapters allow:

| State | The passage stands... |
|---|---|
| `J7.52` | after John 7:52 (the standard place) |
| `J7.36` | after John 7:36 |
| `J21.25` | after John 21:25 |
| `L21.38` | after Luke 21:38 |
| `L24.53` | after Luke 24:53 |
| `other` | anywhere else, coded only when the reader finds it there |
| `absent` | at none of the five places |

* *Found:* passage words stand, in page order, after the place's verse. The
  set is that one state.
* *Ruled out, inside a book:* a place is ruled out where its chapter is
  transcribed and the text runs on past it unbroken (track 5's absence rule:
  no lacuna, no lost text at the place). This covers `J7.52`, `J7.36` and
  `L21.38`.
* *Ruled out, at a book's end* (`J21.25`, `L24.53`). No later verse of the
  same book follows, so the reader reads on in page order from the book's
  last verse.
  * End matter between the last verse and the passage does not stop the
    reading: a subscription, a title, a scholion (family 1 explains the
    passage's new place in one), a chapter list or a blank.
  * *Found takes precedence.* Passage words anywhere in that stretch make
    the place found, whatever end matter comes before them.
  * The place is ruled out when the next book's first verse with text, or
    the end of the codex, comes first. Nothing may be lost, untranscribed or
    illegible along the way.
  * The reading stops after four pages past the one holding the last verse.
    If neither the next book nor the codex's end is reached by then, or a page
    on the way is untranscribed or lost, the place stays open.
  * So every end-of-book chapter is fetched with up to four following pages
    (see the download list).
* *Open:* a place whose chapter is not transcribed, or is lost at the place,
  stays in the set, and so does `absent` whenever no place is found.
  * A witness that lacks the passage after 7:52 and 7:36 but has no
    transcribed John 21 or Luke is `{J21.25, L21.38, L24.53, absent}`.
  * A transcribed John 21 that rules out its place leaves
    `{L21.38, L24.53, absent}`.
* *Undecidable:* a set holding all six open states (the five places and
  `absent`) is missing data. It is not placed and does not count toward the
  run threshold.
* *`other` is never an open state.* It is coded only for a witness whose
  passage the reader actually finds somewhere else. An open set holds only
  the five places and `absent`, so `absent` means "at none of the five read
  places". If `other` were open wherever `absent` is, the two would tie at
  every root under equal costs, and no method could choose between them.

**Location is read in page order, never from verse ids.** The INTF labels a
relocated passage with John's verse ids wherever it stands: the catalogue
search below found 13's Luke 21 page when asked for pages carrying John 8.
Track 5's reader orders a witness's verses by those ids within the files it
joins, so it would score 13 as present after John 7:52. The 5b reader joins
pages in the manuscript's page order and takes the last verse with text
before the passage's first word as its place.

* *Fetching for that:* every chapter is fetched with `fullPage=true`, so a
  page that holds both Luke 21:38 and the passage comes whole. Pages shared by
  two chapter files are read once.
* *A check before the run:* if the `fullPage` TEI does not carry its page
  ids, the implementation fetches by `pageID` instead, and the download list
  goes back to the owner.

### The tree

Exactly track 5's machinery, reused:

* the collation (longest-common-subsequence alignment to the most common
  folded form; a unit is kept when two readings have two witnesses each);
* the `[lost]` and `[damaged]` handling (lost text and the gaps it spans are
  missing data, never an omission);
* the spelling folds (the itacisms, then nu-movable);
* the 30% attestation floor for placed witnesses;
* neighbour joining and maximum parsimony, both reported.

Units come from John 7:1-52 and 8:12-59, as in track 5. **Switch:** add units
from John 21, Luke 21 and Luke 24 (the passage removed), where witnesses have
them. A witness without those chapters is missing there.

### The root: Sankoff over seven states

Sankoff parsimony of the location character with the root on every edge, as
in track 5 but multistate. A leaf's cost is 0 for each state in its set.

**Costs, all three reported:**

| Switch | Gain (`absent` to a place) | Loss (a place to `absent`) | Move (place to place) |
|---|---|---|---|
| Equal | 1 | 1 | 1 |
| Cheap loss (track 5's switch) | 3 | 1 | 3 |
| Cheap move | 3 | 1 | 1 |

*Cheap move* is the lectionary hypothesis: a scribe who already has the
passage relocates it to where the lection sequence puts it, at no more cost
than dropping it.

**Reported, per tree and cost switch:**

* the least-cost root state at the neighbour-joining midpoint root, with the
  root cost of every state;
* the tally of root edges by their uniquely best state, and ties;
* the root-cost gap between `absent` and `J7.52`, the two hypotheses that
  matter most, at the midpoint root and over all edges;
* the events in one best reconstruction at the midpoint root: gains, losses
  and moves, by place.

### Validation, registered before any run

Track 5's generated-tradition benchmark, extended with a **moving block**.

* *The traditions:* track 5's generator, unchanged: mu = 0.02, rho = 0.05,
  500 units, a third of all copies lost. The observed witness count is
  matched to the application's placed witness count (or 40, if more).
* *The block:* a location state carried down the true copying tree. At each
  copy it changes with probability q = 0.05:
  * from a place: lost (probability 1/2) or moved to one of the other four
    places (1/2, uniformly);
  * from `absent`: gained at `J7.52` (0.6) or at each other place (0.1).
  * Under contamination, a copy takes the block's state from its second
    exemplar with probability kappa, as it takes the units.
* *Two scenarios, 100 traditions each* (seeds from 20261021):
  * **P:** the archetype carries the passage at `J7.52`.
  * **A:** the archetype lacks it (late, floating insertion).
* *The observed sets:* each observed witness is paired, in turn, with one of
  the application's witnesses, and coded by the application's own rule.
  * *The paired witness's decidable places:* the places the real reader
    could decide for that witness, either found or ruled out. That means
    the chapter is transcribed and not lost at the place. For `J21.25` and
    `L24.53` it also means the following pages reach the next book or the
    codex's end, as the end-of-book rule requires.
  * If the true state is one of those places, the set is that place.
  * Otherwise, `absent` included, the set is every place NOT decidable for
    that witness, plus `absent`.
  * So a true `L21.38` paired with a witness without Luke is coded
    `{L21.38, L24.53, absent}`. Add `J21.25` if that witness's John 21 is
    missing, or its pages after 21:25 do not reach John's end. The benchmark
    has the data's blind spots and never knows more than the reader would.
* *Metric:* the share of traditions in which the method's answer is the true
  archetype state. The archetype here is what the application means by it:
  the block's state at the latest common ancestor of the observed witnesses
  in the true copying tree, not the generator's root. The answer is the
  least-cost midpoint root state for neighbour joining, and the edge-tally
  majority for parsimony; a tie is scored wrong. The generator never produces `other`, and `other` is never an
  open state, so the bar cannot be failed by a tie the design builds in.
* **Bar:** under equal costs at kappa = 0, the share is 0.80 or more in
  scenario P AND in scenario A, **for neighbour joining at the midpoint
  root**. That is the registered primary builder: it gives one root and one
  answer. Parsimony's edge tally is reported beside it and decides nothing.
  A method that is right only when the answer is "present at 7:52" fails. The
  report shows kappa = 0.1, both cost switches and q = 0.02 and 0.10 beside
  it. Track 5's Robinson-Foulds score is printed as a diagnostic, not a bar.
* *If neighbour joining fails the bar,* the application is descriptive only,
  as in track 5, whatever parsimony scores.

### When the data is too thin to run

The application runs only if, after the approved fetch, every one of these
holds. If one fails, the report prints the counts and stops after
validation:

1. at least 20 placed witnesses whose state set is not undecidable (not all
   six open states);
2. at least two places other than `J7.52`, each the found state of at least
   two placed witnesses (otherwise the character is binary, and track 5
   already answers it);
3. at least five placed witnesses with `J7.52` ruled out.

### What breaks the inference

* **The lectionary moves the block sideways.** The passage was read as a
  separate lection, and family 13's place after Luke 21:38 follows a lection
  sequence. A move that comes from a lectionary, not the exemplar, is
  horizontal transmission, which a tree does not model. The kappa row and the
  cheap-move switch measure how much this can move the answer; they cannot
  remove it.
* **The sample is what was transcribed.** Published transcriptions follow
  editorial projects (the ECM's Luke and John, the IGNTP's John, family
  studies), not a random draw. A clade nobody transcribed is invisible, and
  its location with it.
* **The archetype is not the autograph.** The Old Latin, Syriac and Coptic
  versions and the church fathers bear on the passage's history and are
  outside this method by design.
* **One tree for the whole book.** Block mixture (a manuscript copied from
  different exemplars in different books) is real. The John 7-8 tree may not
  be the Luke tree. The extra-chapters switch is the check.
* **The verse-id trap above.** The reader is wrong if it ever uses verse
  ids, not page order, to place the passage.
* **`absent` means "at none of the five places".** A witness that carries
  the passage at an unread place, on a page nobody looked at, is coded
  `absent`. The report says so wherever `absent` wins.
* **Two transcribers, one collation.** The INTF and the IGNTP follow the same
  TEI guidelines but are different teams. A difference in convention (how a
  supplied letter, an abbreviation or a correction is marked) could group
  witnesses by transcriber, not by text. **Switch:** the trees and the root
  analysis are also run on the INTF-owned witnesses alone, and the report
  shows both. The report also tallies units where the two sources' witnesses
  split cleanly, as a diagnostic.

### Data: what the catalogue says (measured 2026-10-20)

**How it was measured.** Only catalogue and search metadata were read; no
transcription was downloaded.
* *The run.* This machine was refused by `ntvmr.uni-muenster.de` after its
  first probes, so the owner had the measurement run from another
  environment. It used a stdlib Python script: `selftest`, then `meta`.
* *The self-test.* The script began by checking seven values measured
  directly here before the refusal: four INTF page counts, one IGNTP page
  count, and two pages known to carry the passage (05's John 8 and 13's
  Luke 21). All seven matched.
* *A first run was discarded.* It asked for the INTF's pages as
  `userName=PUBLISHED`, which the API answers with zero (see the deviation in
  Witnesses).
* *The outputs.* `availability.json` (sha256 `66330de03248`) and the
  download list below (sha256 `140758a5be6f`) are kept outside the repo,
  with the session notes.

**The catalogue.** Greek continuous-text manuscripts (docID 10000-39999):

| Verse | Catalogue lists it |
|---|---|
| John 7:52 | 884 |
| John 7:36 | 508 |
| John 21:25 | 1,013 |
| Luke 21:38 | 500 |
| Luke 24:53 | 1,090 |

**The witnesses.**
* *Candidates:* 215 manuscripts have a transcription, by either owner, of at
  least one of the five chapters.
* *The pool before the licence rule: 114.* These have both John 7 and
  John 8 and are listed for John 7:52. 98 others lack John 7 or 8, and 3 have them but are not
  listed for John 7:52.
* *By owner:* 11 of the 114 are INTF-owned for John 7-8 (P66, P75, 01, 03,
  05, 038, 13, 69, 18, 33 and 045), and 103 are IGNTP-owned.
* *Other chapters:* 95 have John 21, 16 have Luke 21 and 21 have Luke 24.

**Where the passage stands: the catalogue against published scholarship.**
* *The sources.* Metzger's placements are from *A Textual Commentary on the
  Greek New Testament* (2nd ed., 1994), on John 7:53-8:11, read through
  secondary quotations. They are to be checked against the NA28 or UBS5
  apparatus before the run. J. Knust and T. Wasserman, *To Cast the First
  Stone* (Princeton, 2019), treat the relocations.
* *What "the catalogue" means here.* The column below is the catalogue's own
  page index, the verses the INTF says each page holds. It is evidence of
  where the passage stands, not a reading of the text: the reader decides
  that at the run.

| State | Metzger | The catalogue, for witnesses in the pool |
|---|---|---|
| `J7.36` | 225 | 225 has no transcription of any of the five chapters |
| `J21.25` | 1, 565, 1076, 1570, 1582 | **1:** the page after John 21:25 is indexed "John 7:53; John 8:1-11" and is IGNTP-transcribed. **1582:** the two pages after it are indexed as John's subscription, then 7:53 to 8:7, both IGNTP-transcribed. **565:** the page after 21:25 is indexed John 1:1-17, not the passage, and is untranscribed. 1076 and 1570 have no transcription of these chapters. Outside Metzger's list, 1029's page after 21:25 is indexed as the passage but is untranscribed |
| `L21.38` | family 13 | **13 and 69:** INTF Luke 21 pages indexed as Luke 21:36-38 (13) or 21:26-38 (69), followed by 7:53 and 8:1-11. 124, 346, 543 and 826 have IGNTP Luke 21, so the reader decides them. 828 and 983 have no Luke 21 |
| `L24.53` | none in the first hand (1333's supplement is a corrector's) | 1333 has no transcription of these chapters |
| `J7.52` ruled out | P66, P75, 01, 03, 038, 33 (track 5's reading) | all six are in the pool, now INTF-owned |

**Two facts about the API that the reader must respect.**
* *A search hit is not presence.* A search for the passage's verse ids hits
  the 7:52 page of witnesses that lack the passage (01, 03, P66, P75, 038,
  33). Their stored transcriptions apparently carry empty markers for the
  verses they omit. Only the reader's own rule (passage words in page order)
  decides presence.
* *IGNTP-owned pages are not searchable.* The same search returned nothing on
  any IGNTP-owned page, including 1's and 1582's pages that the catalogue
  indexes as the passage. For IGNTP witnesses, location is known only once
  their files are read.

**End-of-book coverage.** The end-of-book rule needs the pages after John
21:25 and Luke 24:53.
* *John 21 (95 witnesses).*
  * 3 have the passage there by the catalogue's index (1, 1582, 1029).
  * 8 reach the next book on transcribed pages, so their place can be ruled
    out.
  * For 12, the next book's pages are untranscribed.
  * For 62, four following pages carry no catalogue index at all. These stay
    open at `J21.25`.
  * 10 have no index for the page holding 21:25.
* *Luke 24 (21 witnesses).* 11 reach the next book on transcribed pages, 7 on
  untranscribed ones, and 3 find no index.
* *So most witnesses keep `J21.25` open.* The validation codes its generated
  witnesses by these same gaps, so the bar measures the method with this
  blindness built in.

**The licences, measured at fetch (2026-10-20).** The owner approved the list
below, and the fetch ran from the same environment as the measurement.
* *Where it stopped.* The server returned HTTP 500 four times on file 162
  (173's John 7, IGNTP), so the fetch stopped there. All 71 INTF files were
  among the 161 fetched.
* *Every IGNTP file failed the licence rule.*
  * 87 state "Creative Commons Attribution-ShareAlike 3.0 Unported License
    CC-BY-SA-NC". That is ShareAlike, and tagged non-commercial.
  * 2 more are non-commercial ShareAlike.
  * 1 has no `availability` element.
  * None states plain CC BY or public domain.
* *Not every INTF file passed either.*
  * 56 state plain CC BY 4.0.
  * 11 have no `availability` element. All are 045's, and each is an empty
    stub of 77 to 88 bytes.
  * 4 state "All rights reserved by the INTF": single pages of 05, 038 and
    18 (two).
* *The admitted set, verified 2026-10-20.* `report_only.py` admitted 56 files,
  all INTF and all "Creative Commons Attribution 4.0 Unported License". Each
  file's bytes and sha256 match its manifest row. They cover 13 witnesses,
  but only 10 have John 7-8: P66, P75, 01, 03, 05, 038, 13, 69, 18 and 33.
  019, 1 and 22 have Luke 21 and 24 only. 13's John 7 and John 8 files are
  byte-identical, a single page.
* *The rule stands.* The owner kept CC BY or public domain (2026-10-20). So
  no IGNTP-owned file is admitted, and the 233 IGNTP files never fetched
  would add nothing. The fetch is not resumed.

**The run threshold, re-read with the licence rule applied:**

1. *At least 20 placed witnesses:* **NOT MET.** Only INTF files can be
   admitted, and the admitted set reaches John 7-8 in only 10 witnesses: P66,
   P75, 01, 03, 05, 038, 13, 69, 18 and 33. 045's INTF files are empty stubs.
2. *Two non-standard places, each found in at least two placed witnesses:*
   **NOT MET.**
   * `L21.38` keeps 13 and 69: their Luke 21 files are admitted.
   * `J21.25` loses 1 and 1582, which are IGNTP-owned.
3. *At least five placed witnesses with `J7.52` ruled out:* at most met.
   Track 5's six are all INTF-owned, and their John 7-8 files are admitted.

**Reading:** **track 5b is too thin to run.** Under the licence rule the
owner set, the admitted transcriptions reach John 7-8 in 10 witnesses, against
the threshold's 20. Only one non-standard place (family 13, after Luke 21:38)
would be populated.
* *What the report does.* As registered, the 5b report prints these counts
  and stops after validation.
* *What would change it.* A licence change by the IGNTP; new CC BY
  transcriptions published by the INTF; or a ruling to admit ShareAlike
  files. The last is a legal question, because the IGNTP files are also
  tagged non-commercial.

### The download list (approved 2026-10-20; fetch stopped, licence-limited)

The owner approved this list on 2026-10-20. The fetch, its stop at file 162
and the licence results are above. Only files that pass the licence rule are
brought into the cache; nothing is committed. The admitted INTF files get a
pinned ledger, by sha256, in the PR that implements the track.

The full list is `data/scripture/research/ntvmr-5b-download-list.tsv`, one row
per file: document, siglum, item, owner, URL and estimated bytes.

| | Files | Estimated bytes |
|---|---|---|
| John 7 | 114 (11 INTF, 103 IGNTP) | 2.88 MB |
| John 8 | 114 (11 INTF, 103 IGNTP) | 3.12 MB |
| John 21 | 95 (8 INTF, 87 IGNTP) | 1.61 MB |
| Luke 21 | 16 (12 INTF, 4 IGNTP) | 0.29 MB |
| Luke 24 | 21 (13 INTF, 8 IGNTP) | 0.50 MB |
| Pages after a book's end | 34 (16 INTF, 18 IGNTP) | 0.14 MB |
| **Total** | **394 files from 114 witnesses** | **8.55 MB** |

* *URL forms.* Chapters are fetched as
  `https://ntvmr.uni-muenster.de/community/vmr/api/transcript/get/?docID=<doc>&indexContent=<chapter>&fullPage=true&format=teiraw`,
  and single pages with `pageID=<page>` in place of `indexContent` and
  `fullPage`.
  * An INTF file has no owner parameter.
  * An IGNTP file adds `&userName=IGNTP`.
* *Bytes are estimates:* track 5's measured means for John 7 (25.3 KB) and
  John 8 (27.4 KB), other chapters scaled by word count, and 4 KB a page. The
  exact bytes and sha256 are pinned with the admitted files.

## Track 5c: collapsed trees, then dated roots

**Status:** part 1 pre-registered 2026-10-20, before any run of it, and run
the same day. Part 2 (dated roots) was registered in its own section after
part 1's run and before its own.

### Part 1: a validated builder (collapse unsupported branches)

**Why.** Track 5's builders recovered every true split at kappa = 0 and still
failed the bar (mean normalized RF 0.272 against 0.25). The error was the
splits a binary tree must invent where one exemplar was copied several times:
the true copying tree is not binary, and RF counts each forced resolution as
a wrong split. That diagnosis was read from the generated benchmark, never
from the manuscripts. Part 1 tests the remedy its results doc named: collapse
the branches the data does not support, then score.

**The collapse rule (the only one this track tries).**

* *Supported:* an internal branch (both ends internal nodes) is supported when
  contracting it raises the tree's exact parsimony length, so at least one
  variation unit changes on it in every most parsimonious reconstruction.
* *Contracted:* every other internal branch. Contracting a branch merges its
  two ends into one node; leaf branches are never contracted.
* *Order:* internal branches are visited once, in ascending order of their
  `(lower node, higher node)` ids, and each is tested against the tree as
  contracted so far. One pass suffices: contracting more branches never lowers
  a tree's length, so a branch found supported stays supported.
* *Length:* exact Sankoff parsimony per unit with unit change costs, which is
  exact on multifurcating nodes; missing data costs nothing. On a binary tree
  it equals track 5's Fitch length.
* *Branch lengths:* a contracted branch's length is dropped (it is zero), and
  every other branch keeps its builder's length. The neighbour-joining
  midpoint root is taken on the collapsed tree.
* *Both builders* (track 5's neighbour joining and parsimony, unchanged) are
  collapsed by the same rule against the same matrix.
* *Not a retune.* No support threshold, bootstrap or alternative rule is
  tried in this track. If the rule fails the bar, that is the result.

**Validation, the same benchmark and bar as track 5.**

* *Traditions:* track 5's generator and seeds, unchanged (50 traditions per
  row, 20-40 observed witnesses, a third of all copies lost, 500 units,
  mu = 0.02, rho = 0.05, seeds from 20261020).
* *Metric:* normalized RF, |A xor B| / (|A| + |B|) over the observed
  witnesses' splits, now with A the collapsed tree's splits. A star tree
  scores 1, so collapsing everything cannot pass.
* **Bar:** at kappa = 0, the mean normalized RF of a collapsed builder is
  0.25 or less. Each builder is judged separately, and only a builder that
  passes is validated for the application.
* *The kappa degradation curve:* kappa = 0, 0.05, 0.1 and 0.2, as in track 5.
* *Diagnostics (decide nothing):* the share of true splits each collapsed
  builder keeps (recall), the share of its splits that are true (precision),
  the uncollapsed RF beside it, and the kappa = 0 benchmark rerun with the
  observed witness count fixed at each application's placed count (21 for
  Mark, 8 for John on track 5's data), because 8 is below the benchmark's
  range.

**Application, exactly track 5's except the trees.**

* The same pinned NTVMR transcriptions (`data/scripture/research/ntvmr.tsv`,
  no new download), reader, damage handling, spelling folds, collation, 30%
  attestation floor and presence character.
* The same root analysis: Sankoff parsimony of the presence character with
  the root on each branch of the collapsed tree, tallied as favouring
  presence, absence or a tie, and for neighbour joining the root costs at
  the collapsed tree's midpoint root. Both cost switches (equal; loss a third
  of gain).
* The report also gives each collapsed tree's count of internal branches,
  and whether the passage's absent witnesses form a clade on it.
* *If a collapsed builder passes the bar,* its rows are validated and the
  application is no longer descriptive-only for that builder. If it fails,
  its rows stay descriptive, as in track 5.
* *What it still does not weigh:* a witness's age. Part 2 registers that.

### Part 2: dated roots (a witness's age as evidence)

**Status:** pre-registered 2026-10-20, after part 1's run and before any
run of part 2. Amended the same day, after the validation run and before
any application run, in two ways. The date source is narrowed to the one
named below. The range-sensitivity analysis was added. Neither touches the
validation or its bar, and both are marked *(amended)*.

**Why.** Tracks 5 and 5c weigh every witness alike and root the tree by
parsimony alone. Scholars weigh most heavily what that leaves out: the
oldest witnesses (01 and 03 for Mark) lack the passage. Part 2 lets each
witness's date place the root, then asks the same presence question.

**The model: root-to-tip regression.** This is the standard way to root a
tree from tip dates: TempEst (Rambaut, Lam, Carvalho and Pybus, *Virus
Evolution* 2016). A copy made later sits more copyings, and so more
changes, from the archetype. Its distance from the root should therefore
grow with its date.

* *The tree:* part 1's collapsed neighbour-joining tree, with its branch
  lengths. Neighbour joining is the only builder here: parsimony's tree has
  no branch lengths to regress.
* *Candidate roots:* on every branch, 100 interior positions, at
  (i + 0.5) / 100 of its length for i = 0..99. A branch of length zero
  still gets them; they are all the same point.
* *The dated root:* the candidate with the largest Pearson correlation r
  between the placed witnesses' dates and their distances from it. A tie
  goes to the earliest branch in `(lower, higher)` id order, then the lowest
  position.
* *No temporal signal:* if the best r is 0 or less, the method gives no
  answer. The report says so, and validation scores it wrong.
* *The answer:* the presence character's least-cost state with the root on
  the dated root's branch (track 5's Sankoff, both cost switches). A tie is
  no answer.
* *Reported beside it:* the best r, the slope (changes per unit per
  century), the archetype date the line implies (where the distance is
  zero), and the root costs of both states.

**Dates (the data).**

* *The table:* a committed TSV, `data/scripture/research/witness-dates.tsv`,
  with one row per placed witness. Each row holds the date as its source
  states it (a century, two centuries, "ca. 200" or a year), the earliest
  and latest year that statement allows, and the source it was transcribed
  from. Facts only, cited; no text is copied.
* *The source (amended):* one source only, the INTF's Kurzgefasste Liste
  as the NTVMR catalogue gives it. No other source fills a row, not even
  one that relays the INTF. Until the catalogue answers (it refused
  connections on 2026-10-20), the table is empty. The report then stops
  after validation, as track 5b waits.
* *Year rules:* a century N runs from 100(N - 1) to 100N - 1 (IV is
  300-399). "N/N+1" spans both centuries. "ca. Y" is Y - 25 to Y + 25. A
  year is itself.
* **Dates are ranges, not points.** The midpoint of each witness's range is
  the primary point. The switch to every witness's earliest year, then to
  every witness's latest year, is reported beside it.
* **Range sensitivity (amended):** 1,000 draws, seeded from 20261022. Each
  draw dates every witness independently and uniformly within its own range
  (whole years), then runs the dated root. The report gives the share of
  draws whose answer is present, absent or a tie, or that had no temporal
  signal, under each cost switch. It also gives the share of draws whose
  root lands on the midpoint run's branch. An answer that holds in less
  than 90% of draws is reported as sensitive to the dates.

**Validation, registered before any run.**

* *Traditions:* part 1's generator, unchanged (mu = 0.02, rho = 0.05,
  500 units, a third of copies lost, the archetype lost). The observed
  witness count is fixed at each application's placed count: 21 for Mark,
  8 for John. 100 traditions per scenario, seeds from 20261022.
* *Copy dates:* the archetype is dated AD 100. Each copy is dated its
  exemplar's date plus a gap drawn uniformly from 20 to 100 years.
* *Dated as palaeography dates:* each observed witness is given only its
  century, as the range that century allows, so the method sees what the
  Liste would give.
* *The passage:* a presence state carried down the true copying tree.
  * Scenario **P**: the generator's archetype has it.
  * Scenario **A**: the generator's archetype lacks it.
  * At each copy, the state is first taken from the second exemplar with
    probability kappa, as the units are. Then it flips with probability
    q = 0.05: a loss if present, a gain if absent.
  * The dates and states come from a second generator seeded from the same
    seed, so part 1's traditions are unchanged.
* *Truth:* the state at the latest common ancestor of the observed
  witnesses in the true copying tree, as track 5b defines the archetype.
* *Metric:* the share of traditions whose answer is the true state. No
  answer counts as wrong.
* **Bar, per passage:** at that passage's witness count, under equal costs,
  at kappa = 0 and q = 0.05, the dated root's share is **0.80 or more in
  scenario P AND in scenario A**. A method that is right only when the
  answer is "present" fails. The passage's dated rows are validated only if
  its own bar passes. If it fails, they are descriptive, as in track 5.
* *Beside it, deciding nothing:*
  * the same share for part 1's undated answer, the collapsed NJ tree at
    its midpoint root, so the report shows whether the dates help;
  * the cheap-loss costs;
  * kappa = 0.1;
  * q = 0.02 and q = 0.10;
  * the share of traditions in which both states occur among the observed
    witnesses.

**What breaks the inference.**

* *A clock is assumed.* Root-to-tip regression assumes changes pile up at a
  roughly steady rate per century. A careful scriptorium (or a careless
  one) breaks that, and so does a late copy of a much older exemplar. The
  validation's random copy gaps model only the second.
* *Palaeographic dates are estimates* to a century or two. The year switch
  shows how far that moves the root.
* *Contamination* bends root-to-tip distances as it bends the tree. The
  kappa row shows how far.
* *Still only the extant Greek witnesses,* as in track 5: the versions and
  the fathers bear on the archetype and are outside the method.

## Track 6: chiastic structure (Hebrew and Greek only)

**Status:** pre-registered 2026-10-20 (#3402). Implemented in #3404 as
`flock-scripture-import research chiasm`. The pre-run amendments below were
committed before the validation run; only the data check (the reader's own
check) was run before them. Nothing was downloaded for it beyond the pinned
files. Run 2026-10-20 and, with the inclusio table added and a reader
fix for split Hebrew verses, on 2026-10-21:
[scripture-research-results-chiasm-2026-10-21.md](scripture-research-results-chiasm-2026-10-21.md)
(validated; T1 the flood passes at Holm p = 0.0049, T2a, T2b and T4 do not;
6a finds parallel, not mirror, order).

### Questions

A chiasm is a run of material repeated in mirror order around a centre:
A B C | C' B' A'. This track asks where the repeated words of the Hebrew
and Greek text fall in mirror order more often than their content alone
predicts.

* **6a (confirmatory, aggregate).** Within one verse or clause pair, do
  repeated words prefer mirror order to parallel order (A B | A' B'), beyond
  chance? It is asked separately of Hebrew poetry, Hebrew narrative, the
  prophets and the Greek New Testament.
* **6b (confirmatory, named passages).** At each named target, at its
  registered extent and centre: does mirror order beat both parallel order
  and the permutation null? The gold items and negative controls are
  validation, not 6b. Their p's are printed but tested by the bars below,
  not answered here. A word-scale gold item cannot reach significance (see
  the arithmetic), and its p is never read as evidence against it.
* **6c (exploratory).** A scan of every window in both testaments, reported
  with false discovery rate q-values. Nothing found here is a claim until a
  later registration names it.

**Original languages only, by the owner's ruling.** A translation moves words
to suit its own grammar, and it renders one lemma by several words or several
lemmas by one. A mirror found in English is mostly the translator's.

### The arithmetic that shapes this design

The null keeps each half's content and shuffles its order. Take k repeated
lemmas, each used once on each side of the centre. Under the null, the right
side's order is a random permutation of the left side's. The chance of an
exact mirror is 1/k!:

| k | 2 | 3 | 4 | 5 | 6 | 8 | 10 |
|---|---|---|---|---|---|---|---|
| P(exact mirror) | 0.5 | 0.17 | 0.042 | 0.0083 | 0.0014 | 2.5e-5 | 2.8e-7 |

So **no micro-chiasm can be significant on its own.** Gen 9:6 has k = 3 and
Mark 2:27 has k = 2, and each is a perfect mirror. Under any null that keeps
their words, a perfect mirror is still what one shuffle in 6 (or in 2) gives.
The evidence that micro-chiasm is a real device lies in how often it recurs,
which is 6a. Three consequences are registered here, before any run:

1. **The gold set validates structure, not significance.** The bar asks
   whether the detector finds each gold item's published centre and pairs
   (B1). It does not ask for each to reach the FDR. A bar of "gold recall at
   the FDR" would fail on arithmetic alone, before the method was tested.
2. **The scan can find only long mirrors.** With m windows, the first
   Benjamini-Hochberg rejection needs p of about q/m. For example, with
   m = 10^5 and q = 0.10, that is 10^-6, which takes about k = 10 exact
   mirror pairs. The discrete screening below (Tarone 1990; Gilbert 2005)
   drops windows that cannot reach a small p, so the effective m is smaller.
   It is still the planted-chiasm power (B2), measured in the real scan,
   that says what the scan can see.
3. **The named targets are tested as a family of their own** (Holm across the
   target list), never inside the scan's FDR.

### Units

**Hebrew (TAHOT).** The pinned TAHOT keeps the full Masoretic cantillation.
Its Hebrew column is "full Hebrew including pointing, cantillation and
punctuation" (the file header), and a check on cached rows confirms it. In
Gen 9:6, word 3 (הָֽ/אָדָ֔ם) carries zaqef qatan (U+0594), word 4 tipcha
(U+0596) and word 6 (יִשָּׁפֵ֑ךְ) atnach (U+0591). Sof pasuq is split off as
its own tagged element (`\׃`, H9016), and so is maqaf (`\־`, H9014). Accents
are read from the whole word, prefix and suffix segments included. They come
from TAHOT's raw Hebrew column, never from a cleaned surface form.

* *Rows read:* the ones the lemma loader reads (`L` and `Q`, with `R` as a
  fallback). `K` rows (Ketiv) are never read, because their pointing is
  Tyndale's, not the Masoretes'. `X` rows (words retroverted from the LXX)
  are left out: they are Greek evidence written in Hebrew.
* *Prose books (the 18 accent system):* the dividers have two levels.
  * Level 1 is atnach (U+0591), with sof pasuq ending the verse.
  * Level 2 is segolta (U+0592), shalshelet (U+0593), zaqef qatan
    (U+0594), zaqef gadol (U+0595) and tipcha (U+0596).
* *Job 3:2-42:6, Psalms and Proverbs (the poetic system):*
  * Level 1 is oleh we-yored and atnach. Oleh we-yored is ole (U+05AB) on a
    word, with merkha (U+05A5) on that word or the next. When a verse has
    both, oleh we-yored makes the main division and atnach divides the rest.
  * There is no level 2 in version 1. In this system U+0596 is dehi and
    U+0597 serves two different rebia accents, so the prose level 2 does not
    carry over, and its own hierarchy is not registered.
  * The prose frame of Job (1:1-3:1 and 42:7-17) uses the prose rules.
* *A level-1 unit* runs from one level-1 divider to the next: a verse half,
  or a third in a poetic verse that has both dividers. A verse with no
  level-1 divider is one unit. Psalm titles (TAHOT verse 0) are units of
  their own.
* *Level-2 units* split a level-1 unit at its level-2 dividers. They are the
  centres for the word scale (below), and a switch for the unit scale.

**Greek (TAGNT).** The tokens are track 1's research corpus (NA27/28 words,
with TR words only for the two double-bracketed passages). A clause ends at a
token whose word ends in a comma, a full stop, ano teleia (TAGNT writes
U+00B7, as in Mark 2:27's `αὐτοῖς·`; U+0387 is also accepted) or a question
mark (`;` U+003B or U+037E). The ¶ paragraph mark is not a divider.

* **The punctuation comes from the raw TAGNT word column** (the Greek before
  its parenthesised transliteration), read for the same tokens track 1
  selects. It cannot come from the corpus's `surface` field:
  `strongs::clean_surface` trims every non-letter at both ends, so that
  field has no punctuation at all.

* **The Greek units are editorial.** The manuscripts are largely
  unpunctuated, so a clause boundary is a modern editor's judgement. Which
  edition TAGNT's punctuation follows is to be read from its header at
  implementation and stated in the report. Every Greek result carries this
  flag.
* **Switch:** Greek units are whole verses instead, which are a different
  editor's divisions. A Greek result that holds under only one of the two
  divisions is reported as division-dependent.

**The data check (run first).** The report prints, per book:

* how many verses have each divider;
* how many verses have no level-1 divider;
* the mean unit length, in words;
* the Greek punctuation counts by character.

It then checks the gold items' units against the expectations written below
(for example, Gen 9:6a, words 1-6, has level-2 dividers after words 3 and
4 and its atnach on word 6; only the dividers named are checked, so 9:6b's
own zaqef and tipcha do not count as a mismatch). A mismatch stops the run
before validation, because the reader is wrong.

### Matching

* **The key is the base Strong's number** (`strongs::base_strongs`, which
  folds STEPBible's extended letters, so H0120G is H0120). Two words match
  when their keys are equal.
* **Roots are not in the pinned data, so version 1 matches lemmas only.**
  TAHOT tags each word with a lemma number, not a root. TBESH has a
  "uStrong" column that joins variant spellings and Aramaic equivalents, but
  it does not join a root family: לֵב (H3820A) and לֵבָב (H3824), both
  "heart", each map to themselves (measured). That costs Isa 6:10 one of its
  three pairs (below).
  * *Switch v1u:* keys are TBESH's uStrong numbers. This is cheap, but it
    does not rescue the heart pair.
  * *Version 2 (root matching)* needs a new pinned source that gives each
    lemma's root, with a licence check and the owner's approval of the
    download. A candidate is the OpenScriptures Hebrew lexicon, whose licence
    must be confirmed before it is proposed. Nothing here depends on it.
* **The stop lists are the scripture connections lists, reused unchanged.**
  * *Hebrew:* `strongs::is_stop_lemma`, which is STEPBible's H9000-range
    morphemes (the article, prefixed conjunctions and prepositions, pronoun
    suffixes) and the object marker H0853.
  * *Greek:* `scripture_connections::FUNCTION_LEMMAS`, the wider 63-number
    list. It holds the article, conjunctions, particles, pronouns,
    prepositions, the copula, the negatives, πᾶς, τις, ὡς and καθώς.
  * *The asymmetry is deliberate and stated.* The Hebrew list keeps free
    particles such as כִּי, לֹא, אֶל and עַל, and the Greek list drops their
    equivalents. IDF prices the Hebrew ones low.
  * *Switch "Hebrew wide":* the Hebrew list also drops every base number
    whose TBESH Morph type is Prep, Conj, Part, Neg, Cond, PerP, DemP, Intg
    or Art. The rule is fixed here, and the list it yields is printed.
* **Weights.** A key's weight is its IDF, ln(N / df). The documents are
  verses and the corpus is the testament the key comes from (the Hebrew OT,
  the Greek NT, or Brenton for the side check). *Switch:* every weight is 1.
* **Not matched in version 1:** synonyms, antonyms, word pairs (such as "heart"
  with "mind", or "first" with "last"), a compound with its simplex
  (καταπατέω with πατέω), and a pronoun with its referent. A chiasm built
  from these is invisible to version 1, and the gold set says where.

### The statistic

One statistic serves two scales. A **window** is a sequence of elements split
by a **centre** into a left and a right side. An odd centre element, if
there is one, belongs to neither side and is never matched.

* **The word scale (micro-chiasm).** The elements are the content tokens of
  one window, in order.
  * *Hebrew:* **each divider is its own test, with one window and one
    centre.** For a level-1 divider, the window is the whole verse. For a
    level-2 divider, the window is the level-1 unit that holds it. The
    centre is that divider. A verse with several dividers gives several
    tests, and no test takes a maximum over centres, so each has one
    well-defined within-side null.
  * *Greek:* the window is two adjacent clauses of one sentence (between
    full stops or question marks), with the centre between them.
* **The unit scale (passage chiasm).** The elements are units, each
  carrying its set of keys.
  * *The scan:* every run of n consecutive level-1 units within one book,
    for n = 4 to 24. An even n has its centre between the halves, and an
    odd n has the middle unit as its centre.
  * *A named passage* uses its registered extent and centre. When the
    source's centre spans several units (Lev 24:19-20, a clause of Amos
    5:8), those units together are the centre element. They are never
    matched, and the sides are the units before and after them. A centre
    that falls inside a unit makes that whole unit the centre element. A
    named passage's two sides need not have the same number of units.

**Matches.** A match is a left element and a right element that share a key.
At the word scale its weight is the key's IDF. At the unit scale it is the
sum of the IDF of every key the two units share.

**Mirror and parallel.** Take two matches, (i1, j1) and (i2, j2), with i on
the left and j on the right.

* They are **mirror-ordered** when (i1 - i2) and (j1 - j2) have opposite
  signs: the earlier left element pairs with the later right one, so the
  pairs nest around the centre.
* They are **parallel-ordered** when the signs agree: the pairs cross, as in
  A B | A' B'.
* They are **tied** when they share an element. A tied pair adds nothing to
  either side.

Over all pairs of matches:

* M is the sum of w1 * w2 over the mirror-ordered pairs, and P is the same
  sum over the parallel-ordered ones.
* **T = (M - P) / (M + P)** runs from -1 (pure parallel) through 0 to +1
  (pure mirror). T is 0 when M + P = 0.
* R, the repetition mass, is the sum of all match weights. It is reported
  as context and never scored.

**Why this answers the brief.**

* Parallel poetry gives P > M and T < 0, so it cannot score as chiasm.
* Unordered repetition, such as a refrain, puts its pairs in ties or
  splits them evenly between M and P. It gives T near 0, however large R is.
* A mirror is credited only for order. How much repetition there is enters
  only through how improbable that order is under the null.

**Inclusio is a separate, simpler detector.** It asks whether a window's
first and last units share a key whose IDF is at or above the corpus median.
It prints its own table, enters no score and is never tested.

### The null and multiple testing

* **The primary null is a within-side permutation.** The order of the
  elements is shuffled within the left side, and separately within the right
  side. The centre element stays put, and every element keeps its content.
  * *Why within-side.* A shuffle across the whole window would also reward
    the repeats for falling on both sides of the centre, which is
    repetition, not order. The within-side shuffle holds which repeats
    straddle the centre fixed, so T is tested on order alone. M + P is fixed
    under it, so testing T and testing M - P give the same p.
  * *Switch:* the whole-window shuffle the first brief named, with the
    centre element fixed. It is reported beside the primary null, but **no
    direction is claimed for it.** T is a ratio, so a shuffle that leaves
    only two keys straddling the centre reaches T = +1 easily.
    * For an exact mirror of k = 3, its p is 1/15, against 1/6 within
      sides.
    * For k = 4 it is about 0.35, against 1/24.
    The two nulls answer different questions: order given the straddle,
    and straddle and order together.
* **T depends only on the matched elements.** It reads only the relative
  order of elements that carry at least one match. Shuffling the unmatched
  elements changes nothing. So the null's distinct outcomes number
  L_m! * R_m!, where L_m and R_m are the matched elements on each side.
  Both criteria below use those counts, not the window's length.
* **The p-value.**
  * *Exact* when L_m! * R_m! <= 9!, enumerated over the relative orders of
    the matched elements. The p is (orderings with
    T >= observed) / (all orderings), where the observed ordering is one of
    them. For an exact mirror of k distinct keys, this gives 1/k!.
  * *Sampled* otherwise: (1 + draws with T >= observed) / (1 + B), with
    B = 99,999 seeded draws (seed 20261022). The report states the floor,
    1/(B + 1).
  * *Escalation, so the floor never decides the result.* A sampled
    window with fewer than 10 exceedances is re-run at B = 10^7 (floor
    about 1e-7). If it still has fewer than 10, it is re-run at B = 10^9
    (floor about 1e-9). Each stage has its own seed (20261022, then
    20261027, then 20261028), and the p reported is the last stage's.
    Only the few windows near their floor reach the later stages.
* **The minimum attainable p** is used only for screening.
  * *Exact windows:* the null probability of the window's largest
    achievable T.
  * *Sampled windows:* a lower bound, 1 / (L_m! * R_m!), raised to the
    final escalation floor (1e-9) when that is larger. A window with few
    matched elements therefore has a large bound and is screened out, however
    long it is.
  * Both are computed from the match structure alone, without looking at
    the order. A lower bound keeps more windows in m than the exact value
    would, so the screen stays valid, just more conservative.
  * *The bound that follows:* with the 1e-9 floor, a window can survive the
    screen at q = 0.10 while the screened m stays below about 10^8. The
    report prints the screened m for each testament and scale, so a reader
    can see whether that held.
* **6c, the scan (exploratory).**
  * *Screening (Tarone 1990):* a window whose minimum attainable p cannot
    meet the Benjamini-Hochberg threshold is removed from m before
    Benjamini-Hochberg runs. This is Gilbert's (2005) modified procedure for
    discrete tests.
  * *FDR:* q = 0.10, run separately per testament and per scale.
  * *Switch:* Benjamini-Yekutieli. Overlapping windows are dependent, and
    Benjamini-Hochberg under that dependence is assumed, not proven.
* **6b, the named targets (confirmatory).** The targets are one family,
  with Holm's correction at alpha = 0.05.
  * *The gold items* are scored by B1 (structure) only.
  * *The negative controls* are scored by B4, on the raw p, and are never
    Holm-adjusted.
  * Neither enters a Holm family.
* **6a, the aggregate test (confirmatory).**
  * *The eligible windows:* every Hebrew level-1 test (a verse at one of
    its level-1 dividers, so a poetic verse with both dividers gives two)
    and every Greek clause pair, provided it has at least one pair of
    matches that is not tied.
  * *The statistic:* mean T over the eligible windows of a group. Under the
    null its expected value is 0.
  * *The null:* one shuffle per draw serves every window. Each draw
    shuffles the tokens within each level-1 unit (Hebrew) or clause
    (Greek) once, and scores every eligible window from that same draw.
    B = 9,999 draws, seed 20261023. The test is one-sided.
    * *Why one shared draw.* Windows overlap. A Greek clause sits in two
      adjacent clause pairs, and a poetic verse with both dividers is two
      tests on the same words. Independent shuffles would break the
      correlation between their T values and make the null too narrow.
    * For a prose verse and a Greek clause pair, the units are exactly the
      window's sides. For a poetic verse with both dividers, the shuffle
      is finer than either window's sides, which is a stricter null than
      the per-window one; the report states it.
  * *The groups:*
    * Hebrew poetry: the poetic-system books, plus Lamentations and Song
      of Songs.
    * The prophets: Isaiah to Malachi, excluding Lamentations.
    * Hebrew narrative: Genesis to 2 Kings, without its poems. The poems
      are Gen 49:2-27, Exod 15:1-18, Num 23-24, Deut 32:1-43, Deut
      33:2-29, Judg 5, 1 Sam 2:1-10, 2 Sam 1:19-27 and 2 Sam 22.
    * The Greek New Testament.
  * *The reading:* "mirror is preferred" in a group when p < 0.01 and the
    mean T is positive. Poetry against narrative is reported as the
    difference in mean T, with a 95% bootstrap interval that resamples
    verses, not windows (1,000 resamples, seed 20261024).
  * *Grammar is a known cause, reported apart.* Hebrew moves its verb
    between clauses (verb first in one line, verb last in the next), and
    that alone yields mirror order. The report splits the 6a statistic by
    the matched keys' part of speech: verb pairs, noun pairs, and mixed.
    Mirror order among verbs may be grammar rather than rhetoric, and the
    test cannot tell the two apart.

### Validation (run first) and the bar

**V1, the gold set.** These are widely accepted micro-chiasms, each with a
cited source (see Sources and checks), checked against TAHOT and TAGNT for
whether version 1 can see them. Each is run at its registered extent, with
a test at every centre the rules give that extent.

| Item | Scale | Keys version 1 can match | Visible? | Citation |
|---|---|---|---|---|
| Gen 9:6a | word; window words 1-6 (to the atnach); centre the zaqef qatan after word 3 | sheds H8210, blood H1818, man H0120: a perfect mirror, k = 3. The test at the tipcha after word 4 also gives T = +1 (shed and blood still nest, and the second adam has no right match) | yes | verified |
| Isa 6:10 | word; centre atnach on word 8 | ears H0241 and eyes H5869, in mirror order. "Heart" is לֵב H3820 then לְבָבוֹ H3824, a different number | partly: 2 of 3 pairs | verified |
| Lev 24:13-23 | unit; centre the talion law, 24:19-20 | the repeated legal terms (strike, life, beast, man, put to death, sojourner and native), as Willis lays them out | yes, if the units fall as expected | verified |
| Amos 5:5 (from 5:4-6) | word; window the verse; centre its atnach (expected after "do not cross over to Beersheba"; the data check confirms it) | Bethel and Gilgal: Bethel, Gilgal before the centre, then Gilgal, Bethel after it, k = 2. Beersheba stands unpaired before the centre | yes | pending |
| Mark 2:27 | word; centre the comma after ἐγένετο | σάββατον G4521 and ἄνθρωπος G0444, in mirror order (διά and οὐ are stop lemmas) | yes, k = 2 | pending |
| Matt 7:6 | word | none: no content lemma recurs. The mirror is in the referents: dogs (A), swine (B), trample (B'), turn and tear (A') | **no**: out of version 1's reach | pending |

* **The Amos item is scored at the word scale only.** The mirror the source
  describes lies inside 5:5, below the unit scale's resolution. The frame
  (seek and live, 5:4b and 5:6a) is reported but not scored: "seek" also
  stands in 5:5a and Bethel again in 5:6b, so at the unit scale those
  matches tie or cross the frame.
* **Citation status.** "Verified" means a scholarly source naming the
  passage as a chiasm was read for this registration (see Sources and
  checks). "Pending" means it was not.
  * Mark 2:27 is called an antimetabole only in popular sources so far.
  * Matt 7:6 and Amos 5:4-6 have scholarly citations from an index or a
    title, but the text itself was not read.
  * A pending item joins the recall denominator only if its source is read
    and quoted in the implementation PR, before any run. Otherwise it is
    run and reported, but it does not count. The denominator is frozen when
    the implementation PR opens.
* **Recovered** means three things:
  * the test at the published centre gives T > 0;
  * no other test in the same window has a higher T (a tie counts as
    recovered, so Gen 9:6a's equal T at the tipcha does not fail it);
  * at least two of the published lexical pairs are among that test's
    matches, in mirror order.
* **Matt 7:6 is kept as a registered blind spot.** It is run and reported,
  but it is outside the recall denominator, because no lemma method can see
  it. The same holds for any chiasm of synonyms or referents.

**V2, negative controls.** These are plainly parallel or repetitive
passages. Mirror order must not be found at their extent. Each has a
registered scale and centre, as the gold items do.

* *Matt 7:7-8* (ask, seek, knock, then the one who asks, seeks, knocks):
  * *Test:* unit scale with Greek clause units. The centre is the verse
    boundary between 7:7 and 7:8, with no centre element.
  * *Expectation:* parallel order, so T <= 0. Under TAGNT's clause units
    it is probably 0, not -1: if 7:8 is one clause, every match to the right
    falls in that one unit, and the pairs all tie. That is still a pass.
* *Ps 24:7-10* (the "lift up your heads, O gates" strophes): parallel
  repetition.
  * *Test:* unit scale. The centre is the verse boundary between 24:8 and
    24:9.
* *Ps 136:1-9* (a refrain in every verse): unordered repetition.
  * *Test:* unit scale. The units of 136:5 are the centre element.
* *Matt 7:24-27* (the wise and foolish builders): a long lexical parallel
  that can fail. Hear, do, house, rain, rivers, winds and fall recur in the
  same order.
  * *Test:* unit scale with Greek clause units. The centre is the verse
    boundary between 7:25 and 7:26, with no centre element.
  * *Expectation:* T clearly negative.
* *Luke 6:37* (judge not ... condemn not ... forgive): each lemma repeats
  inside its own clause pair, which is repetition.
  * *Test:* word scale. Every clause pair within the verse's sentences is
    a test, centred between its two clauses.
  * *To pass,* every one of those tests must pass B4.

**V3, planted chiasms in real text.** This measures power and false alarms
in the real scan.

* *The hosts:* windows of n = 8, 12 and 16 level-1 units, plus the bar's
  n* (below) when it is not already one of them. They are drawn from the
  corpus (seed 20261025). The groups are Hebrew prose, Hebrew poetry and
  Greek, kept separate.
  * k* and n* come from the unplanted scan's screened m. That is a
    property of the corpus, known before any plant is made, so adding the
    n* hosts is part of the registered design, not a deviation.
* *A planted mirror* of k pairs, for k = 2 to min(n/2, 12):
  * pair d (d = 1..k) gets a lemma from the corpus's middle IDF band (the
    25th to 75th percentile of content lemmas) that is absent from the
    window;
  * that lemma replaces one unmatched content token in the left unit at
    distance d from the centre, and one in the right unit at distance d.
* *A planted parallel* uses the same lemmas, with the right side in
  parallel order. *Planted repetition* puts one lemma into every unit.
* *The run:* 100 plants per cell. Each plant replaces its host. The
  windows that overlap it are recomputed, and the testament's whole
  screened Benjamini-Hochberg is rerun.
* *Hosts are clean.* A host is drawn only from windows that overlap no
  window with q <= 0.10 in the unplanted scan, and not from a gold item,
  control or target.
* *Detected* means a window with q <= 0.10 whose centre is within one unit
  of the planted centre and which covers at least half the planted window.
  That window must also not have had q <= 0.10 in the unplanted scan.

**The bar** (all of it registered before any run):

* **B1:** at least 80% of the gold items in the frozen denominator are
  recovered, rounded up. That is the visible items with a verified
  citation; Matt 7:6 is never among them. With today's three (Gen 9:6,
  Isa 6:10, Lev 24:13-23), all three must be recovered. With five, four
  must be.
* **B2 is set by a rule, not by a fixed k.** A fixed k could fail on
  arithmetic alone, the trap B1 avoids. For each group:
  * m_s is the screened m of the scan the group's plants are detected in:
    the Hebrew Old Testament's unit-scale scan for Hebrew prose and
    Hebrew poetry alike, and the Greek New Testament's for Greek. It is
    never a smaller per-group count, because detection faces the whole
    testament's threshold;
  * k* is the smallest k with 1/k! <= 0.01 * q / m_s, so that a perfect
    mirror of k* pairs is a hundred times below the first Benjamini-Hochberg
    threshold;
  * n* = max(16, 2 * min(k*, 12)), so n* <= 24, the scan's own limit.
  * *The bar:* at (k*, n*), planted mirrors are detected at q <= 0.10 with
    power of at least 0.80. The full power curve over k and n is printed
    beside it.
  * *A cap:* when k* > 12, the report says that the group's scan cannot
    see a mirror of fewer than 12 lemma pairs at the registered FDR. That
    is a property of the corpus size, stated here in advance. The scan is
    labelled underpowered, and nothing else is stopped.
  * V3's grid always contains the bar's cell: (k*, n*) when k* <= 12, and
    (12, 24) under the cap, where n* = 24.
* **B3:** at the same (k*, n*), planted parallels and planted repetition
  are each detected in at most 5% of plants. When k* > 12 (the cap), B3 is
  evaluated at (12, 24), which is n* in that case and so is planted. That
  keeps the false-alarm bar evaluable while B2 reads underpowered.
* **B4:** every negative control has a raw p >= 0.10 at its extent, under
  the primary null. It is never Holm-adjusted: an adjustment would make a
  "must not be significant" test easier to pass. Matt 7:7-8 and Luke 6:37 test the handling of ties and
  single matches (they should give T = 0 and cannot be called mirror).
  The order logic is tested by Ps 24:7-10, Ps 136:1-9 and Matt 7:24-27.
* **6a's own power check:** in each 6a group, 5% of the eligible windows
  are re-planted from parallel to mirror order. The test must detect that
  at p < 0.01 in at least 80% of 200 plants (seed 20261026). Otherwise
  that group's 6a result is reported as underpowered.

**What a failure means.**

* **The unplanted scan is computed before V3 but kept sealed.** V3 needs
  two things from it: its screened m (for k*) and the mask of windows with
  q <= 0.10 (for clean hosts). Only those two are read. Its candidate
  list and q-values are written to a sealed file and are neither printed
  nor read until the bar passes.
* If B1, B3 or B4 fails, the method is not validated. 6b's targets are not
  run, the sealed scan is never opened or reported, and the failure is the
  result.
* If only B2 fails in a group, that group's scan is printed as a ranking,
  labelled "underpowered at the registered FDR". Its q-values still print,
  but the label says what they cannot show.
* No threshold, list or switch above is changed after a validation result
  is seen. A change is a deviation, recorded in the results with its reason.

### Targets (named and disputed; run only after the bar)

The targets are kept apart from the gold set. Each is a published chiastic
reading that other scholars dispute, and the registered extent and centre are
the proposer's. Each is run at that extent and centre, at the unit scale. Its
p follows the general rule: exact when L_m! * R_m! <= 9!, otherwise sampled
with the registered escalation. The family is corrected with Holm.

* **T1. The flood, Gen 6:10-9:19, centred on 8:1** ("God remembered
  Noah").
  * *Proposer:* Wenham (1978), a palistrophe in which the day counts (7,
    40, 150, then 150, 40, 7) and the movements into and out of the ark
    mirror each other.
  * *Critic:* Emerton (1987, 1988), who argues that the pattern is imposed
    on a text that combines two sources.
  * *Why it is a hard test:* the passage repeats "ark", "waters" and
    "days" throughout. That is heavy repetition, which this statistic must
    not reward. It is longer than 24 units, so only this named test may
    examine it.
* **T2. Babel, Gen 11:1-9, at two centres:** 11:5 (Fokkelman 1975;
  Wenham 1987) and 11:6 (van Wolde 1994).
  * *The dispute* is where the centre lies. Putrawan, Noya and Negoro
    (2022) weigh the proposals and prefer a scenic parallel reading to the
    palistrophe.
  * *Both centres are tested.* The report gives both, and it ranks them
    only by T and p.
* **T3. Amos 5:1-17, centred on "YHWH is his name" (end of 5:8).**
  * *Proposer:* de Waard (1977).
  * *The dispute* is the centre and the extent. Bliese (2003) puts the
    centre at 5:16-17, and Won Lee asks whether the centre must be the
    thematic peak. Neither venue has been verified yet. Both must be read
    and cited in the implementation PR before T3 runs, or T3 is dropped and
    the drop is recorded.
* **T4. The Johannine prologue, John 1:1-18, centred on 1:12b.**
  * *Proposer:* Culpepper (1980).
  * *Critics:* Staley (1986) proposes a competing concentric scheme, and
    Coloe (1997) finds the pairing of 1:1-2 with 1:6-8 forced.
  * This is the only Greek target, so it carries the editorial-units flag.
* **T5. The Benedictus, Luke 1:68-79.**
  * *Proposer:* Vanhoye (1965-66).
  * *Critic:* Auffret (1978) critiques it systematically, and Rousseau
    (1986) proposes two further structures.
  * *Not run until its centre is fixed.* Vanhoye's centre has not been read
    for this registration. It must be transcribed from the article in the
    implementation PR, before any run, or T5 is dropped and the drop is
    recorded.

Each proposer's pairs are written into the implementation PR before any run.
They are used only for the report's side-by-side comparison of "the
proposer's pairs" against "the detector's matched pairs". They never enter
the statistic, which sees only the text.

### Output

Each candidate (gold, control, target, or a scan window with q <= 0.10)
prints:

* **Where:** the reference range and the scale. The centre is given as a
  reference plus the divider's name (for example, "Gen 9:6, zaqef qatan
  after word 3"), or as the centre unit.
* **The matched pairs:** for each pair, the left and right references, the
  key, its lemma and gloss (from the lexicon table the importer already
  writes), and its IDF. They are listed from the centre outward, with each
  marked mirror or parallel against its neighbours.
* **The scores:** n, k, M, P, T and R.
* **The test:** p, how it was computed (exact, or sampled with B), the
  minimum attainable p, and q or the Holm-adjusted p. It is also given under
  the whole-window switch.
* **Flags:** Greek units are editorial; division-dependent; inclusio present
  (from the separate table); the LXX side check's result.

**No row says "chiasm".** The wording is fixed: "mirror order exceeds
parallel order and the permutation null at q = ..." or "... does not". A
scholar's chiasm can be thematic, and this test cannot say whether it is.

### The LXX side check (a test of the translation)

This is optional and decides nothing. For each Hebrew gold item, each
Hebrew target, and each Hebrew scan candidate with q <= 0.10, the same
verses are read in Brenton's LXX lemmas, which are already loaded and mapped
to the standard verses through TVTMS. The Greek rules are used: the
punctuation units, the Greek stop list, and IDF over Brenton. The report
shows T and p beside the Hebrew result.

* **It is labelled a test of the translation.** It asks whether the
  translators kept the mirror. It is not evidence about the Hebrew, and a
  mirror that is lost there takes nothing away from the Hebrew result.
* *The inherited error.* Brenton's lemmas are inferred from surface forms
  through TAGNT. On NT forms seen once, the prefix fallback is right 87.2%
  of the time, and unknown words stay unmatched. So a lost pair may be the
  lookup, not the translator. The report counts the unknown words in each
  window.

### Limits

* **Book-scale ring composition is out of scope.** Leviticus as a ring
  (Douglas), or a whole Gospel arranged concentrically, rests on themes, and
  a lemma statistic can neither find nor test it. Windows stop at 24 units;
  only a named target may be longer.
* **Lemma identity is not literary identity.** A writer's mirror may use
  synonyms, antonyms or referents (Matt 7:6), or the same root in another
  lemma (Isa 6:10's heart). Version 1 misses all of these, and its recall
  is a floor.
* **The accents are the Masoretes' reading,** fixed around the 9th to 10th
  centuries AD. Units built from them measure chiasm under that
  segmentation, which is old and careful but not the author's.
* **The Greek clauses are a modern editor's** (see Units).
* **Grammar makes mirrors.** See 6a: verb movement in Hebrew parallelism
  makes mirror order without rhetorical intent.
* **A significant mirror shows that the order is not chance.** It does not
  show that an author designed it, or what it means. Those questions are
  class B.

### Pre-run amendments (implementation, 2026-10-20)

Each of these was decided and committed before any validation result was
seen. They settle what the registration left open, record what it could not
do, and answer the three low-severity advisories that #3402's last review
left open.

**What the registration required before the run.**

* **The frozen B1 denominator is three:** Gen 9:6a, Isa 6:10 and Lev
  24:13-23, so B1 needs all three. No pending source was read before this
  PR opened. Amos 5:5 and Mark 2:27 are run and reported but not counted.
  Matt 7:6 stays the blind spot.
* **The published keys for the recovery rule:**
  * Gen 9:6: H8210, H1818 and H0120.
  * Isa 6:10: H0241 and H5869 (H3820 and H3824 are listed too, but they
    cannot match each other).
  * Lev 24, Willis's terms: strike H5221, life H5315, beast H0929, man
    H0120 and H0376, put to death H4191, sojourner H1616 and native H0249.
  * Amos 5:5: H1008 and H1537.
  * Mark 2:27: G4521 and G0444.
* **T3 is dropped.** Bliese (2003) and Won Lee could not be found in a
  readable form. **T5 is dropped.** Vanhoye's article could not be read, so
  its centre could not be transcribed. Both drops are as registered.
* **The proposers' pairs are display only**, and their provenance is
  stated because none of the proposers' texts was read here:
  * T1 uses the registration's own description (the 7-, 40- and 150-day
    counts, and the entry into and exit from the ark), mapped to verses.
  * T2 at 11:5 uses Wenham's (1987) pairs as they are widely reproduced.
  * T4 uses Culpepper's pairs as they are widely reproduced.

**The three open advisories.**

* **The Holm family.** Each centre tested is one hypothesis, and a dropped
  target leaves the family. The family is therefore four tests: T1, T2 at
  11:5, T2 at 11:6 and T4.
* **6a after a failed bar.** 6a follows rule 4, as 6b does. If B1, B3 or B4
  fails, 6a is not answered and its result is not printed. Its power check
  is validation, so it prints either way.
* **The cap wording.** When k* > 12, the report says that no mirror the scan
  can hold (at most 12 pairs in 24 units) meets the bar's margin at the
  registered FDR.

**The named centres, under "a centre inside a unit is that unit".**

* T1's centre, "God remembered Noah", lies in 8:1a (the level-1 unit of
  words 1-13, to the atnach). That unit is the centre element, and 8:1b
  stands on the right.
* T2's first centre, "the LORD came down to see", lies in 11:5a. That unit
  is the centre element, and 11:5b ("which the sons of man built") stands on
  the right.
* T2's second centre (van Wolde) is the units of 11:6.
* T4's 1:12b is TAGNT's clause "ἔδωκεν ... γενέσθαι," (words 5-10).
* The data check confirms each of these splits before validation runs.

**Readings of the units and matching.**

* **A name TAHOT splits over two words** (`{H1008G}+` then `{H1008G}`,
  Bethel; Beersheba) is one token. Without this, Amos 5:5's Bethel would
  count twice.
* **Oleh we-yored** divides after its merkha word.
* **A Psalm title** is one unit and gives no word-scale test.
* **A named passage's units are cut within its extent.** A Greek clause
  that crosses the extent's edge ends there.
* **The Greek word scale under the verse switch** pairs adjacent verses.
* **Recovery at the unit scale.** A unit-scale named passage has one
  centre, so the "no other test is higher" condition holds trivially. For a
  Greek word-scale item, the tests in the window are the clause pairs inside
  the extent.
* **The groups.** "Genesis to 2 Kings" is in English order, so it includes
  Ruth. Job's prose frame is in no 6a group, and Daniel is among the
  prophets. V3's "Hebrew poetry" is 6a's poetry group, and "Hebrew prose" is
  every other Hebrew verse.
* **A data fact corrected.** The pinned TAGNT writes ano teleia as U+0387
  (4,665 times) and never as U+00B7, the reverse of what the Units section
  says. Both were registered as dividers, so nothing changes.

**The computation, which changes no registered quantity.**

* **Exact ties.** Weights are fixed point at 1/4096 nat.
* **The sampled stream** is SplitMix64. Every window uses the stage's seed,
  and draw t starts at the state seed + t c gamma, where c is the number of
  random numbers one draw uses. This is reproducible and does not depend on
  threads.
* **An exact window that can never pass the screen is not enumerated.** When
  the screen's cut q/K, computed on lower bounds, is below 1/9!, no exact
  window can be screened in under its exact minimum p either. Its p is then
  not needed.
* **V3's detection stops a window's draws early, without changing any
  rejection.** It stops once the window's p is known to exceed the largest
  threshold BH could use after the plant, and only when the window would
  not escalate. A test checks this against a full rerun.
* **V3's planting:**
  * hosts are drawn uniformly from the clean starts within one book and
    group;
  * a planted lemma replaces a random token whose key does not occur on the
    host's other side;
  * the middle IDF band is the 25th to 75th percentile, by nearest rank;
  * parallels are planted at every mirror cell, and repetition once per
    host size.
* **6a's re-planting** reorders a selected window's matched tokens inside
  their own shuffle units. They are put in descending order of their left
  partners' mean position. The units' contents are unchanged, so the null
  draws are shared.
* **The whole-window column** is exact when (L + R)! <= 9!. Otherwise it is
  stage 1 only (B = 99,999, floor about 1e-5): it is never tested.
* **Where the switches apply.** The scan runs under the primary setting,
  plus BY and the Greek verse division for the division flag. The other
  switches apply to the gold items, the controls, the targets and 6a. The
  level-2 unit switch applies to unit-scale items only.
* **The word scale has a scan of its own.** It covers the Hebrew divider
  tests and the Greek clause pairs, with its own screen and FDR.
* **The LXX side check:**
  * a Brenton verse goes under its first standard verse;
  * a word the lookup cannot read is no token, and it is counted;
  * a Hebrew centre inside a verse becomes that verse's Greek units;
  * a word-scale item shows its highest-T clause pair.

### Sources and checks

Checked on 2026-10-20. **Read** means the text tying the source to the
passage was read. **Cited** means the source was found only as a reference
in a source that was read, or in a published index of chiasmus studies; the
page given is that reference's.

* **Gold**
  * *Gen 9:6:* J.W. Welch, "Narrating Homicide Chiastically", *BYU Studies
    Quarterly* 59 supplement (2020), 151-176 (read: lays out 9:6 as
    A B C C' B' A'). U. Cassuto, *A Commentary on the Book of Genesis* II,
    127 (cited).
  * *Isa 6:10:* D.W. Parry, "Chiasmus in the Text of Isaiah: MT Isaiah
    versus the Great Isaiah Scroll", *BYU Studies Quarterly* 59 supplement
    (2020), 107-127 (read).
  * *Lev 24:13-23:* T.M. Willis, "Blasphemy, Talion, and Chiasmus: The
    Marriage of Form and Content in Lev 24,13-23", *Biblica* 90 (2009),
    68-74 (read: talion at the centre). Also cited:
    * J. Milgrom, *Leviticus 23-27* (AB 3B), 2130 ("long been recognized");
    * G.J. Wenham, *Leviticus* (NICOT, 1979), 312;
    * J.W. Welch, "Chiasmus in Biblical Law", *Jewish Law Association
      Studies* IV (1990), 8.
  * *Amos 5:4-6:* J. de Waard, "The Chiastic Structure of Amos V 1-17",
    *VT* 27 (1977), 170-177. The title and bibliographic details were
    confirmed, but the text was not read. **Pending.**
  * *Mark 2:27:* no scholarly source was read; only popular sources call it
    an antimetabole. **Pending.**
  * *Matt 7:6:* N.W. Lund, *Chiasmus in the New Testament* (1942), 32 (cited
    from an index). Which clause pairs with the dogs and which with the swine
    is itself disputed. **Pending.**
* **Targets**
  * *T1:* G.J. Wenham, "The Coherence of the Flood Narrative", *VT* 28
    (1978), 336-348. J.A. Emerton, "An Examination of Some Attempts to
    Defend the Unity of the Flood Narrative in Genesis", *VT* 37 (1987) and
    *VT* 38 (1988), 1-21 (the 1987 pages to confirm).
  * *T2:* J.P. Fokkelman, *Narrative Art in Genesis* (1975), 11-45 (cited).
    G.J. Wenham, *Genesis 1-15* (WBC 1, 1987), 235-236 (cited). E. van
    Wolde, *Words Become Worlds* (1994), 86-89 (cited). B.K. Putrawan,
    L.B.J. Noya and A.P. Negoro, "Centripetal-centrifugal Forces in the
    Tower of Babel Narrative (Gen 11:1-9)", *Old Testament Essays* 35/2
    (2022) (read).
  * *T3:* de Waard (above); Bliese (2003) and Won Lee (venues pending).
  * *T4:* R.A. Culpepper, "The Pivot of John's Prologue", *NTS* 27 (1980),
    1-31 (abstract read). J.L. Staley, *CBQ* 48 (1986), 241-263 (cited).
    M.L. Coloe, "The Structure of the Johannine Prologue and Genesis 1",
    *Australian Biblical Review* 45 (1997), 40-55 (cited).
  * *T5:* A. Vanhoye, "Structure du Benedictus", *NTS* 12 (1965-66),
    382-389; P. Auffret, "Note sur la structure littéraire de Lc 1,68-79",
    *NTS* 24 (1978); both read through F. Rousseau, "Les Structures de
    Benedictus (Luc 1.68-79)", *NTS* 32 (1986), 268-282 (abstract read).
* **Criteria for a chiasm,** which the report's discussion uses and the
  statistic does not:
  * J.W. Welch, "Criteria for Identifying and Evaluating the Presence of
    Chiasmus", *Journal of Book of Mormon Studies* 4/2 (1995), 1-14;
  * C. Blomberg, "The Structure of 2 Corinthians 1-7", *Criswell
    Theological Review* 4 (1989), 3-20 (nine criteria, 5-7).
* **Computational prior art**
  * M. Dubremetz and J. Nivre ranked English candidates for the ABBA
    figure by features:
    * NAACL CLfL workshop (2015), 23-31;
    * NoDaLiDa (2017), 37-45;
    * *Frontiers in Digital Humanities* 5 (2018).
    They treat it as a ranking problem, not a verdict, as this track does.
  * H. McGovern, H. Sirin and T. Lippincott, "Computational Discovery of
    Chiasmus in Ancient Religious Text", NAACL 2025 (arXiv:2501.10739),
    is the closest prior art. It scores the Hebrew Bible by embedding
    similarity and reports precision at k against annotations.
    * *How this track differs:* it matches lemmas, not meanings, so the
      matched pairs can be shown. It also asks for order beyond a
      permutation null, not for similarity. The two are complementary.
      Embedding similarity sees synonyms that version 1 misses, but it
      cannot separate mirror order from repetition without a null like
      this one.
  * Y.T. Radday, "Chiasmus in Hebrew Biblical Narrative", in J.W. Welch
    (ed.), *Chiasmus in Antiquity* (1981), 50-117 (cited). It is an early
    statistical study, and 6a's groups allow a comparison with it.
* **The multiple-testing methods**
  * R.E. Tarone, "A Modified Bonferroni Method for Discrete Data",
    *Biometrics* 46 (1990).
  * P.B. Gilbert, "A Modified False Discovery Rate Multiple-Comparisons
    Procedure for Discrete Data", *Statistics & Probability Letters* 75
    (2005).

## Track 6r: chiastic structure with repetition weighed once

**Status:** pre-registered 2026-10-21, before any code for it was written.
The owner ruled on its four open choices the same day, each as drafted: the
shared weight (not one-to-one keys), T1 alone, 6a not asked again, and 200
plants per repetition cell. Track 6 has been run, and its
results were read before this was written:
[scripture-research-results-chiasm-2026-10-21.md](scripture-research-results-chiasm-2026-10-21.md).
Track 6r changes one thing, the match weight, so that a key repeated many
times weighs as one pair. It then asks again the one confirmatory question
whose reading that change could alter, T1. Everything else is track 6's,
unchanged.

`research chiasm-norm`. It reads track 6's pinned inputs and nothing else.

### Why

Track 6's statistic was registered on the claim that unordered repetition
"puts its pairs in ties or splits them evenly between M and P". The run showed
a case where it does not.

* **The evidence.** V3 printed planted-repetition detection for every host
  size, though B3 read only n = 24. At smaller hosts the rates were high: in
  Hebrew prose 0.72 at n = 8, 0.50 at 12 and 0.19 at 16, against 0.03 at 24.
* **The mechanism.** A detection may come from a window longer than its host.
  Repetition planted in a short host then sits at the centre of that longer
  window, a block of matches between every left unit and every right unit
  near the centre. Every match in the window's outer units nests around that
  block. Each such nesting is a mirror-ordered pair of matches, and the
  within-side shuffle, which scatters the block, does not reproduce it.
* **Why it matters.** T1 passed in track 6 at a small effect (T = 0.055), and
  the flood repeats "day", "water", "earth" and "ark" around 8:1. Track 6
  cannot tell whether T1's mirror excess is order or that repeated core.
  Nor can it for the scan's hits, whose strongest stretches are formulaic
  legal and list material.

### What is reused from track 6, unchanged

* The data, the reader (with run 4's fix for split Hebrew verses), the units,
  the keys, the stop lists, the IDF and every switch track 6 registered.
* Mirror, parallel and tied pairs of matches; M, P and T; the within-side
  null and its exact and sampled p, with the same escalation and seeds
  (20261022, 20261027, 20261028); the Tarone screen, BH and BY at q = 0.10;
  the scan's windows and sealing; the LXX side check.
* The gold set, the frozen B1 denominator (Gen 9:6a, Isa 6:10, Lev
  24:13-23), the negative controls and B4.
* V3's hosts, plants, groups, detection rule and seeds (20261025), and B2.
* T1's extent and centre: Gen 6:10-9:19, centred on the unit that holds 8:1a.
* **The seeds are track 6's on purpose.** The only difference between the
  two runs is then the weight, so a figure that moves, moved because of it.

### What changes: the match weight

* **Each key's weight is shared among its occurrences.** In a test, let a_c
  be the number of left elements that carry key c, and b_c the number of
  right elements. A match between a left element and a right element weighs
  the sum, over the keys they share, of IDF(c) / (a_c * b_c). Track 6's
  weight is the same sum without the division.
* **What this does:**
  * A key that occurs once on each side keeps its full weight. That is every
    planted mirror pair, every gold item's published pair and every A ... A'
    of a chiasm in the strict sense.
  * A key's matches weigh IDF(c) in total, however often it repeats. A refrain
    or a repeated core then weighs as one pair, not as a_c * b_c pairs. If it
    sits at the centre, it is credited as one nested pair, which is what a
    single repeated word at the centre would be.
  * a_c and b_c are fixed under the within-side null, because each element
    keeps its content. So the null, its exactness rule (L_m! * R_m! <= 9!)
    and every p-value method are unchanged.
* **Fixed point.** Each key's term IDF(c) / (a_c * b_c) is quantised at 1/4096
  nat before it is summed, as track 6 quantises IDF.
* **R** is still printed, as track 6's unnormalised repetition mass, for
  context.
* **Switches (descriptive, they decide nothing):**
  * *track 6's weight*, which reproduces track 6's figures;
  * *one-to-one keys*, which keeps only the keys with a_c = b_c = 1.
* **No other weight was tried.** Nothing under the new weight has been
  computed on a target, a gold item, a control or the corpus. The only check
  made was on random synthetic windows (12 units a side, a random vocabulary,
  one lemma added to the 4 units either side of the centre), and only under
  track 6's weight, to confirm the mechanism.

### What changes: the bar

* **B1, B2 and B4** are track 6's, applied under the new weight.
* **B3 is widened.** Planted parallels at (k*, n*) are detected in at most 5%
  of plants, as before. Planted repetition must be detected in at most 5% of
  plants **at every host size in the grid** (8, 12, 16 and n*), not only at
  n*. The repetition cells draw 200 plants each; every other cell keeps 100.
  This is the gate track 6 lacked: a short repeated block inside a longer
  window is exactly what the small hosts plant.
* **A failed bar is the result.** If B1, B3 or B4 fails, T1 is not answered
  and the scan is not opened, as in track 6. A B3 failure would mean the
  weight does not separate order from a repeated core, and the report says
  so.

### What is asked

* **T1 (confirmatory, one test).** At T1's extent and centre, does mirror
  order exceed parallel order and the within-side null under the new
  weight? It passes when T > 0 and p < 0.05. It is the only target in the
  family, so there is no Holm correction.
  * *If it passes:* the flood's mirror excess is not its repeated core.
  * *If it fails:* track 6's T1 result is attributed to repetition, and
    track 6's results doc is annotated to say so.
* **Babel (T2a, T2b) and the Johannine prologue (T4)** are re-scored under
  the new weight and printed, but not tested: their track 6 answers were
  seen, so a test of them now would not be blind, and the caveat that
  motivates this track bears on a "yes", not on their "no".
* **6a is not asked again.** Track 6's answer, no mirror preference in any
  group, was seen. 6a is printed under the new weight, descriptively,
  together with the new power check below, which says whether track 6's
  "no" could have been a "yes".
* **6c, the scan (exploratory).** Computed and sealed before V3, as in track
  6, and opened only after the bar. The report also lists track 6's stretches
  (its windows at q <= 0.10, merged where they overlap) and says which still
  hold a window at q <= 0.10 and which hold none.
* **The parallel preference 6a found** stays descriptive. It was seen, so a
  test of it on this corpus would confirm a known result. Testing it needs
  text this programme has not scored.

### What changes: 6a's power check

Track 6 re-planted 5% of each group's windows into mirror order in the
observed corpus. The observed means sit far below the null (Hebrew poetry
-0.64), so no 5% plant could reach p < 0.01, and the check measured the
corpus's level, not the test's sensitivity. Track 6r plants into null
copies instead:

* each of 200 plants (seed 20261026) draws one null shuffle of the group, as
  6a's null does;
* in that shuffled corpus, 5% of the eligible windows are re-planted into
  mirror order, by track 6's re-planting rule;
* the plant is detected when that corpus's mean T has p < 0.01 against 6a's
  null (B = 9,999, seed 20261023);
* a group is powered when at least 80% of its plants are detected.

### What changes: inclusio (descriptive)

Track 6 read "the corpus median" as the median IDF over lemma types. Most
lemmas are rare, so that threshold sat high and almost nothing qualified
(Gen 9:6a's "shed", IDF 5.35, fell below it). Track 6r prints the table under
both readings: the median over lemma types, and the median over running
content words. It enters no score.

### Output

`docs/data/scripture-research-results-chiasm-norm-<date>.md`, reading first,
with the generated report embedded. Each figure that track 6 also printed is
shown beside track 6's run 4 value.

## Out of scope for class A

* **Quirinius's census and the Exodus,** beyond 3a's derived date. They have
  too few internal constraints, and the output would only restate the reading
  assumed.
* **The conquest, and everything in classes B and C.**
