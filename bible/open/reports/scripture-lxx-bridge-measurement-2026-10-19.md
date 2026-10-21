# LXX bridge measurement (2026-10-19)

The measurement behind open question 1 of
herald-scripture-connections.md:
which public-domain or CC BY source can build phase 2's Hebrew-to-Greek
equivalence table (section 5.2), and does its Greek let the quotation flag
(5.3) fire. It was measured offline, with no product code and nothing loaded.
The owner accepted the recommendation and the slice plan below on
2026-10-19; the pins themselves land in phase 2's slice 1.

## Erratum (phase 2 slice 3, 2026-10-19)

The importer's reimplementation of B3's alignment (`connections --lxx`)
found a case bug in the measurement's TVTMS script: it folded a numbered
book's code to `1sa`, which never matched Brenton's `1Sa`. So no TVTMS test
on 1-2 Samuel, 1-2 Kings or 1-2 Chronicles ever held, and those books kept
Brenton's own numbering. With that one line fixed, the measurement's own
script gives exactly the importer's figures: 4,921 TVTMS rows pass (not
4,492), 4,288 Brenton verses are renumbered (not 3,899), 22,640 are paired
with a TAHOT verse (99.4%, not 22,603 and 99.2%), and 22,609 TAHOT verses
are covered (97.2%, not 22,574 and 97.1%). The importer also keeps the TAGNT
rows that carry a versification alternate (`Rev.12.18(13.1)`), which the
measurement's pattern skipped, and breaks a tie between two lemmas of one
form toward the lower number: 399,678 tokens by form (85.3%) and 432,582
with the prefix fallback (92.3%). It corrects TVTMS's expanded rows for
Malachi 3:22-24 to its condensed table. The precision and coverage tables
below were computed on the uncorrected alignment. Slice 4 re-measures them
on the importer's own.

**Re-measured (phase 2 slice 4).** `flock-scripture-import bridge` fits B3
on the importer's alignment and lemmatization, with the Hebrew read as slice
2 loads it (the object marker `H0853` dropped; Joshua 21:36-37's restored
words kept), after the 2026-10-20 TVTMS audit (#3373) and its by-hand rows (#3381): 22,683 verse pairs. On the 99 gold pairs B3 (IBM 1) scores
exactly the table's figures below: P@1 1.00 common, 0.94 rare, 0.98 all, and
hit@3 1.00. P@3 is 0.37 common and 0.35 rare, within a hundredth of the
measurement's (the shipped table also keeps no candidate under t(g | h) =
0.05). The two misses at rank
1 are near-synonyms (σῦκον for συκῆ, ἄστρον for ἀστήρ). The B1 internals
below are reproduced exactly.

## Inputs

All files were downloaded into a scratch directory with the owner's approval
on 2026-10-19 and parsed with `python3 -I`. Nothing was committed.

| Bridge | File | Source | Bytes | sha256 (first 12) | Licence |
|---|---|---|---|---|---|
| B1, B3 | TBESG, TBESH (lexicons) | STEPBible-Data `Lexicons/` at commit `ed476a8e` (2026-10-17) | 4,736,912; 3,288,045 | `312f723d7b8e`; `464dccadd95f` | CC BY 4.0 (repository README) |
| B3 | TAHOT x4, TAGNT x2 | STEPBible-Data `Translators Amalgamated OT+NT/`, same commit | 70,208,913; 30,128,964 | per file, kept with the notes | CC BY 4.0 |
| B3 | TVTMS | STEPBible-Data `Versification/`, same commit | 5,790,928 | `63058e0f2020` | CC BY 4.0 |
| B3 | `grcbrent_usfm.zip` (Brenton's Septuagint, no Strong's tags) | ebible.org, live file dated 2026-10-18 | 1,725,661 | `bc414101e94f` | Public domain (ebible.org/grcbrent/copr.htm) |
| B2 | `bsb_tables.tsv` (BSB word to Strong's alignment) | bereanbible.com, dated 2026-07-31 | 85,525,373 | `09bbee6f9fe4` | **Unclear**: berean.bible/terms.htm dedicates the BSB "texts" to the public domain (CC0), but no page names the translation tables |

TBESG also carries Apostolic Bible Polyglot numbers (G6100-G9979, "Extra Greek
from Apostolic Bible Project"). Nothing here reads them: B1 uses only entries
below G6100, which are Abbott-Smith (1922, public domain) as digitized by
STEPBible.

## What was built

* **B1, curated.** Each TBESG entry's `[in LXX ... for <Hebrew>]` note is
  parsed, and each pointed Hebrew word is mapped to an H number through
  TBESH's lemma column. A word is matched pointed first (cantillation stripped,
  vowels kept), and vowel-stripped only as a fallback. A homograph goes to its
  most frequent H number in TAHOT. Rank is the order of mention in the note.
* **B2, English pivot.** P(G|H) = sum over English words e of P(e|H) P(G|e),
  from the BSB tables' English column (stop-worded, plural-stripped).
* **B3, statistical.** Brenton is lemmatized by surface-form lookup from TAGNT
  (accents, breathings and case stripped, final sigma folded, movable nu
  restored). Its verses are aligned to TAHOT's English-numbered verses by
  TVTMS's expanded table, whose identifying tests are evaluated against
  Brenton itself. 2 Esdras 11-23 is renumbered Nehemiah 1-13 first. IBM
  Model 1 (6 EM iterations, a NULL source) gives t(G|H). Dice over verse
  co-occurrence is reported beside it.
* **Combinations.** B1R is B1 with each homograph resolved by B3's t(G|H)
  instead of frequency. COMBO puts B1's seeds first, then B3's order. BOOST
  keeps B3's order and doubles a B1 seed's weight.

Every candidate list is restricted to NT lemmas (the target is Gospel
pericopes) and drops the function lemmas the quotation rule drops (articles,
conjunctions, particles, pronouns, prepositions, the copula, negatives).

**No NT quotation pair is an input to any bridge.** B3 reads only the OT
(Brenton x TAHOT). The NT enters only as a table of word forms. B1 reads
Abbott-Smith's per-lemma LXX notes, not its NT references. B2 is not
leak-free: the BSB translators' English for an NT quotation may echo their
English for its OT source, which is a diffuse leak into set B.

## Results

### Alignment and lemmatization (B3)

| Measure | Value |
|---|---|
| Brenton verses (canonical books; Greek Esther left out) | 22,785 |
| Verses renumbered by TVTMS | 3,899 |
| Brenton verses paired with a TAHOT verse | 22,603 (99.2%) |
| TAHOT verses covered | 22,574 of 23,259 (97.1%) |
| Greek / Hebrew tokens per pair, median; pairs outside 0.5-3 | 1.59; 1.2% |
| Brenton tokens lemmatized, TAGNT form lookup | 85.3% (399,626 of 468,516) |
| ... plus a prefix fallback for unseen inflections | 92.3% |
| The fallback, leave-one-out on 9,693 NT hapax forms | answers 64.9%, correct 87.2% of those |

Two gaps are in the data, not the method. Brenton's Jeremiah follows LXX
chapter order but fails TVTMS's identifying tests, so its plain "Greek" rows
are applied untested; Brenton's chapters 29-30 split Edom differently from
Rahlfs and are left unaligned. The 14.7% of tokens the lookup misses are
mostly proper names, LXX-only vocabulary and inflections the NT never uses
(ἀμνούς, for example).

### B1 internals

| Measure | Value |
|---|---|
| TBESG entries below G6100 | 5,607 |
| ... with an `[in LXX ...]` note | 3,638 |
| ... with at least one Hebrew word mapped to an H number | 2,978 |
| Hebrew words in the notes | 4,697 |
| ... matched pointed and unique / pointed but ambiguous | 3,458 (73.6%) / 690 (14.7%) |
| ... matched only vowel-stripped: unique / ambiguous | 121 / 275 |
| ... unmatched | 153 (3.3%) |
| Vowel-stripped as the only key: matched words that are ambiguous | 2,900 of 4,544 (63.8%) |
| TBESH consonantal keys that are homographs | 1,161 of 4,353 (26.7%) |
| Homographs B3 resolves differently from "most frequent" | 194 of 945 |

Vowel stripping alone is not usable: two thirds of the notes' words become
ambiguous. Pointed matching cuts that to 15%, and frequency still misresolves
some. The headline case: Abbott-Smith's note for ποιμαίνω names רָעָה, whose
pointed form is shared by "to pasture" (H7462) and "evil" (H7451), and
frequency picks "evil", so B1 cannot answer ra'ah -> poimaino.

### Coverage of Gospel Greek lemma types

A Greek lemma counts as covered when it is in some Hebrew lemma's top 5 (for
B1, when its note maps any Hebrew). "Content" excludes the function lemmas and
proper names: 2,625 of 2,925 Gospel lemma types.

| Bridge | Types, raw | Tokens, raw | Types, content | Tokens, content |
|---|---|---|---|---|
| B1 (any note) | 0.659 | 0.479 | 0.728 | 0.813 |
| B2 | 0.763 | 0.437 | 0.805 | 0.947 |
| B3, IBM 1 | 0.749 | 0.435 | 0.774 | 0.939 |
| B3, Dice | 0.595 | 0.408 | 0.609 | 0.880 |
| COMBO (B1 + B3) | 0.796 | 0.441 | 0.827 | 0.952 |

Raw token coverage is low for every bridge because the article and καί are
nearly half of all Gospel tokens and are never bridged. B3's figures use the
prefix fallback; without it its content coverage is 0.661 / 0.910.

### Precision against the hand-checked sample

There are two strata (listed in the appendix): 63 common equivalences (ra'ah
-> poimaino, nephesh -> psyche) and 36 mid- and low-frequency ones (kebes ->
amnos, tselem -> eikon), which matter more to BM25 because their IDF is high.
Each was checked against the TBESH and TBESG glosses; one gold error found
that way (zakar is tagged μιμνήσκω G3403 in TAGNT, not only μνάομαι G3415)
was corrected before scoring. P@1 is "the top candidate is acceptable". P@3 is
the share of the top 3 that are acceptable; most items have one acceptable
lemma, so its ceiling is 0.39 (common) and 0.36 (rare). Hit@3 is "an
acceptable lemma is in the top 3".

| Bridge | Answered | P@1 common | P@1 rare | P@1 all 99 | P@3 common / rare | Hit@3 all 99 |
|---|---|---|---|---|---|---|
| B1 | 93 | 0.76 | 0.83 | 0.79 | 0.30 / 0.31 | 0.84 |
| B1R | 94 | 0.73 | 0.89 | 0.79 | 0.30 / 0.32 | 0.84 |
| B2 | 99 | 0.97 | 0.75 | 0.89 | 0.37 / 0.35 | 0.98 |
| **B3, IBM 1** | 99 | **1.00** | **0.94** | **0.98** | 0.38 / 0.34 | **1.00** |
| B3, Dice | 99 | 1.00 | 0.97 | 0.99 | 0.38 / 0.35 | 1.00 |
| COMBO | 99 | 0.84 | 0.94 | 0.88 | 0.35 / 0.34 | 0.95 |
| BOOST | 99 | 1.00 | 0.94 | 0.98 | 0.38 / 0.34 | 1.00 |

The brief's hypothesis, B1 as high-precision seeds, does not hold. Abbott-Smith's
order of mention is not frequency order (its top three for chayah are
ζωοποιέω, τρέφω, ζωογονέω, without ζάω); some notes name a neighbouring lemma
(ἅγιος is "chiefly for" qodesh, holiness, not qadosh) or a form TBESH spells
differently (מַיִם against TBESH's מַי; יהוה, which TBESH lists only as a
name); and homographs cost it more. Putting B1 first (COMBO) lowers P@1 from 0.98 to 0.88. B2 is
good on common words but weak on rare ones (0.75), where the English pivot
spreads mass over near-synonyms, and its licence is unclear.

### The quotation flag on Brenton's Greek

Ten formula quotations, with the OT verse's Brenton lemmas against the quoting
Gospel verse's TAGNT lemmas, function lemmas dropped as above.

| OT -> Gospel | Fires? | Longest shared run |
|---|---|---|
| Isa 40:3 -> Mark 1:3 | yes | 9 |
| Isa 53:4 -> Matt 8:17 | **no** | 0 (Matthew renders the Hebrew, not the LXX) |
| Isa 7:14 -> Matt 1:23 | yes | 5 |
| Ps 22:18 -> John 19:24 | yes | 5 |
| Ps 118:22 -> Matt 21:42 | yes | 6 |
| Deut 8:3 -> Matt 4:4 | yes | 8 |
| Hos 6:6 -> Matt 9:13 | **no** | 3 ("mercy I desire ... sacrifice"; LXX ἤ, Matthew καὶ οὐ) |
| Isa 6:9-10 -> Matt 13:14-15 | yes | 9 |
| Isa 29:13 -> Mark 7:6-7 | yes | 8 |
| Ps 110:1 -> Mark 12:36 | yes | 8 |

It fires on 8 of 10. With only articles and conjunctions dropped it also fires
on 8, but then 7 of 400 random OT verses fire against some Gospel pericope
(pronoun and preposition runs); with the wider list, 0 of 400 do.

**A lex-only sketch of set B** (5.3's rule: quoted pericopes first, then BM25
with canon-wide IDF; the shipped k1 = 1.2 and b = 0.75; folded to parallel
groups) puts the target group at rank 1 for 9 of 10 when the OT side is
Brenton's lemmas. Hos 6:6's top group is Matt 12:1-8, which quotes Hos 6:6 at
12:7 with a formula, so it is a target group under section 7. Isa 53:4 comes
second. With the OT side as bridged Hebrew (B3, top 3 per H number) it is
also 9 of 10, with Isa 53:4 at rank 8. A naive union of the two bags is no
better. Ten queries say nothing about a confidence interval; they say the 0.9
bar is reachable and where it fails: Matthew's own renderings of the Hebrew
(Isa 53:4, Hos 11:1, Mic 5:2, Zech 11:13), a large share of the
fulfilment-formula quotations.

**Reproduced (phase 2 slice 5, 2026-10-20).** The production ranker,
through `eval --quotes` on the ten pairs above, fires the flag on the same
8 and puts a target group first for 9 of 10. Two readings of this section
were settled by re-running its own script: the 9 counts Matt 12:1-8 as Hos
6:6's target group (with Matt 9:9-13 alone it is 8), and "Isa 53:4 comes
second" was the run that also dropped the wider list from BM25 (with the
narrow list, as shipped, Isa 53:4 ranks 89 in the script and 160 in the
ranker, whose IDF counts Brenton under standard verses). The quotation flag
uses the wider list on both sides, as recommended below. On the importer's
own 400 random verses one fires, on a real Septuagint phrase (Deut 13:7 in
Mark 13:27; spec 5.3), not on function words.

**Slice 7 (2026-10-20).** On the same ten, two figures from #3392: the full
ranker with the query-to-target cross-references removed reaches recall@5
0.80 (95% CI 0.50 to 1.00) under Strong's numbers, against 0.70 over English
stems; and with Matt 9:13 as Hos 6:6's only target the Matt 9 group ranks
2nd, so lex-only recall@1 is 0.80 while recall@5 holds at 0.90. The
wider-list BM25 that put Isa 53:4 second in the sketch moves it only from
160 to 23 in the production ranker and changes no recall, so it was not
adopted. On the 72 agreed set B quotations the phase 2 lex-only recall@1 is
0.71 (95% CI 0.60 to 0.81), below the English stems' 0.78: see the
evaluation report.

## Recommendation

1. **Build the bridge from B3** (IBM Model 1 over Brenton x TAHOT, aligned by
   TVTMS). It is the most precise (P@1 0.98, hit@3 1.00 on 99 pairs), leak-free
   by construction, and uses only public-domain and CC BY 4.0 inputs. Keep
   t(G|H) as the weight, the top 3 per H number above a floor.
2. **Use Brenton's Greek directly as the OT side.** For an OT verse that
   Brenton covers, its own lemma sequence is the better query: the quotation
   flag fires on it, and BM25 over it already reaches 9 of 10 in the sketch.
   The bridged Hebrew is the fallback for verses Brenton lacks (Esther, the
   unaligned Jeremiah chapters, 182 others) and a second shingle sequence for
   quotations that follow the Hebrew. It never false-fired in the probe.
3. **Keep B1 as an audit, not a seed.** B3 top-1 choices that Abbott-Smith's
   note for that Greek lemma contradicts are a reviewer's list. B1 does not
   reorder anything.
4. **Do not use B2** unless Berean confirms in writing that CC0 covers the
   translation tables. It is also weaker on rare words and not leak-free.
5. **Use the wider function-lemma list for Greek shingles**, not articles and
   conjunctions alone.

## Phase 2 slice plan

| Slice | Ships | Notes |
|---|---|---|
| 1 | Pins: TAHOT x4, TAGNT x2 and TVTMS at one STEPBible-Data commit (raw URLs at that sha are immutable); Brenton `grcbrent_usfm.zip` as a Wayback `id_` snapshot; attribution rows | The owner's dataset decision. The 7-day floor does not formally cover datasets; pinning a commit at least 7 days old matches it anyway |
| 2 | Original-language lemmas: TAGNT for the NT, TAHOT for the OT, into `herald_scripture_lemmas` (`G4166` / `H7462`) | Gospel index switches to Greek lemmas. Extended Strong's suffixes are dropped to the base number |
| 3 | Brenton lemma sequences for OT verses, mapped to standard numbering by TVTMS | Needs a migration: the table holds one sequence per verse today, so a `layer` column or a second table. Number it above `origin/release`'s high-water mark |
| 4 | `flock-scripture-import bridge`: IBM Model 1 table `herald_lxx_bridge (h, g, weight)`, deterministic (fixed iterations), plus the B1 disagreement report as a review artefact | No NT text is read except TAGNT's form table |
| 5 | Ranker: OT query = Brenton bag (bridged Hebrew where absent); quotation flag over Brenton AND bridged-Hebrew sequences; wider Greek stop list | Pure ranker change plus its tests. Built: `flock_core::scripture_connections`, with the reads, the index's bridge and Strong's as the import default (spec 5.2, 5.3) |
| 6 | Panel evidence: Greek lemmas shown with TAGNT's English gloss | Display only |
| 7 | Re-fit and re-evaluate (sets A1, B at recall@1 0.9, set C re-rating round) | Section 7. Run 2026-10-20 (report): both bars missed, constants re-fitted, `strong` off, set C round exported, not sent |

## Caveats

* The gold sample was written for this measurement and checked against the
  STEPBible glosses, not double-annotated. It is a sanity check, not a set C.
* The quotation and set B figures are 10 queries. They show feasibility and
  failure modes, not a rate.
* Brenton's Greek is the Sixtine text (after Codex Vaticanus) of his 1851
  edition; Rahlfs differs in wording and numbering in places. The ebible.org zip is rebuilt in place, hence the Wayback pin.
* The measurement scripts are not in the repository (no product code in this
  change); slice 4 reimplements B3 in the importer and must reproduce the
  figures above.

## Appendix: gold pairs

Common (63): H7462 ra'ah = G4165, G4166, G1006; H5315 nephesh = G5590; H3820
lev = G2588, G1271; H7307 ruach = G4151; H1285 berit = G1242; H2617 chesed =
G1656; H6664 tsedeq = G1343; H6662 tsaddiq = G1342; H7965 shalom = G1515;
H3068 YHWH = G2962; H430 elohim = G2316; H4428 melek = G935; H4438 malkut =
G932; H1121 ben = G5207; H1 av = G3962; H776 erets = G1093; H8064 shamayim =
G3772; H4325 mayim = G5204; H784 esh = G4442; H3899 lechem = G740; H3196 yayin
= G3631; H6629 tson = G4263; H1870 derek = G3598; H1697 davar = G3056, G4487;
H8085 shama = G191; H3045 yada = G1097, G1492; H2421 chayah = G2198; H4191 mut
= G599; H2403 chatta't = G266; H3467 yasha = G4982; H6918 qadosh = G40; H3519
kavod = G1391; H8034 shem = G3686; H5971 am = G2992; H1471 goy = G1484; H5650
eved = G1401, G3816; H4397 mal'akh = G32; H5030 navi = G4396; H3548 kohen =
G2409; H1004 bayit = G3624, G3614; H3027 yad = G5495; H5869 ayin = G3788; H6310
peh = G4750; H3117 yom = G2250; H4196 mizbeach = G2379; H2077 zevach = G2378;
H8451 torah = G3551; H4941 mishpat = G2920, G2917; H571 emet = G225; H1320
basar = G4561; H1818 dam = G129; H7451 ra = G4190, G2556; H157 ahav = G25;
H3372 yare = G5399; H1288 barak = G2127; H2142 zakar = G3415, G3403; H6213 asah
= G4160; H5414 natan = G1325; H6440 panim = G4383; H2022 har = G3735; H4057
midbar = G2048; H68 even = G3037; H2233 zera = G4690.

Mid and low frequency (36): H6754 tselem = G1504; H1823 demut = G3667; H4899
mashiach = G5547; H4886 mashach = G5548; H5162 nacham = G3870; H1319 basar
(announce) = G2097; H6299 padah = G3084; H2398 chata' = G264; H1330 betulah =
G3933; H2483 choli = G3554, G769, G3119; H7716 seh = G4263; H3532 kebes = G286;
H8384 te'enah = G4808; H1612 gephen = G288; H3754 kerem = G290; H7105 qatsir =
G2326; H4672 matsa = G2147; H1245 baqash = G2212; H2931 tame' = G169; H2889
tahor = G2513; H6883 tsara'at = G3014; H7676 shabbat = G4521; H6453 pesach =
G3957; H4682 matstsah = G106; H5104 nahar = G4215; H3220 yam = G2281; H8121
shemesh = G2246; H3394 yareach = G4582; H3556 kokab = G792; H5404 nesher =
G105; H3123 yonah = G4058; H8269 sar = G758; H8199 shaphat = G2919; H6942
qadash = G37; H7812 shachah = G4352; H5647 avad = G1398, G3000.
