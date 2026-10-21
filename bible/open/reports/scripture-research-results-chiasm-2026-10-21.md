<!-- SPDX-License-Identifier: CC-BY-4.0 -->

# Scripture research, track 6 results: chiastic structure in the Hebrew and Greek text (2026-10-21)

This is track 6 of the class A programme, run against the frozen
pre-registration in
[scripture-research-class-a.md](scripture-research-class-a.md) (track 6, PR
3402), with the pre-run amendments recorded there before validation began.
The code was committed before each run. The datasets are the pinned TAHOT,
TAGNT, TBESH, TVTMS and Brenton files; nothing new was downloaded. The
generated report is reproduced in full below the reading. Reproduce it with:

```bash
cargo run --release -p flock-api-server --bin flock-scripture-import -- research chiasm
```

It takes about four hours on an 18-core machine. The reported run is run 4
(commit c7602baf8, finished 2026-10-21); see the post-run changes.

## Reading

**No row of this report says "chiasm".** Every reading is the registered
wording: mirror order does, or does not, exceed parallel order and the
within-side permutation null. A scholar's chiasm can be thematic; this test
sees only where the same lemmas fall.

* **The method validated.** B1 (all three counted gold items recovered: Gen
  9:6a, Isa 6:10, Lev 24:13-23), B3 (planted parallels and repetition at the
  bar's cell detected 0% to 4% of the time) and B4 (every negative control at
  raw p >= 0.29; Ps 136:1-9 is the closest, at 0.293) pass. B2 passes in all three groups: planted 12-pair mirrors
  in 24-unit windows were found 83% of the time in Hebrew prose, 100% in
  Hebrew poetry and 92% in Greek. So the targets, 6a and the scan were run.
* **6b T1, the flood (Gen 6:10-9:19, centred on 8:1a): mirror order exceeds
  parallel order and the permutation null, Holm-adjusted p = 0.0049.** It is
  the only target that does. The excess is small: T = 0.055, so the weighted
  mirror pairs outweigh the parallel ones by about 12% (M 16.6 million
  against P 14.9 million nats squared, over 77 matched keys in 152 units).
  It holds under every switch (p from 0.00065 to 0.022, the weakest under
  level-2 units) and under the whole-window null (p = 0.0014). It survives
  translation: Brenton's Greek gives T = 0.039, p = 0.015. What it does not
  show is Wenham's palistrophe. The registered statistic credits any nesting
  of repeated lemmas around 8:1a, and the flood narrative repeats "day",
  "water", "earth" and "ark" throughout. See the second caveat below: a dense
  repeated core at the centre of a window scores as mirror order, so T1's
  result is "the flood's repetitions nest around 8:1a more than chance
  orders them", not "the proposer's pairs are confirmed".
* **6b T2a and T2b, Babel (Gen 11:1-9, centred on 11:5a and on 11:6): no.**
  T = -0.186 (p 0.87) and -0.078 (p 0.69): the repeated words of Babel fall
  slightly more often in parallel order. The proposers' pairs are mostly
  visible to the lemma matcher ("earth", "all", "language", "there",
  "build"), so this is not a recall failure. It is a 9-verse passage in
  which the shared lemmas do not nest.
* **6b T4, the Johannine prologue (John 1:1-18, centred on 1:12b): no.**
  T = 0.006, p = 0.48. Only 9 keys match across the centre, and the
  proposer's pairs are thematic ("what we received", 1:4-5 / 1:16, shares no
  lemma). This is the case the registration named: a thematic chiasm the
  lemma test cannot see.
* **6a: within a verse or clause pair, repeated words do not prefer mirror
  order in any group (all p = 1.0).** They prefer parallel order, strongly.
  Mean T is -0.64 in Hebrew poetry, -0.34 in the prophets, -0.35 in Hebrew
  narrative and -0.17 in the Greek New Testament. Under the null the mean is
  exactly 0 (reversing one side's order swaps M and P), so these are far in
  the lower tail. Poetry is more parallel than narrative by 0.29 (95%
  bootstrap interval 0.17 to 0.41). This is descriptive: the registered test
  is one-sided, and "parallel is preferred" was not a registered question.
  All four groups also print "underpowered (power 0.00)". That is the
  registered power check reading literally, and it is correct as far as it
  goes: re-planting 5% of the windows into mirror order cannot lift a mean
  of -0.34 above a null centred on 0. The check was written for a corpus
  near the null and does not measure what it was meant to here. 6a's
  confirmatory answer is "no", and its own check says that "no" could not
  have been "yes" by a 5% effect.
* **6c, the exploratory scan: 3,158 Hebrew windows and 27 Greek windows at
  BH q <= 0.10.** These are leads, not claims. The Hebrew windows overlap
  heavily: they merge into 451 stretches of text, and 18 windows in 9
  stretches also pass the stricter Benjamini-Yekutieli procedure. The
  strongest stretches are legal and list material: Lev 21:12-22:17, Ezek
  47:11-48:13 (the tribal allotments), Lev 3:14-4:26, Num 34:25-35:11, 2 Kgs
  3:26-4:21, Deut 2:6-24, Ezek 2:5-3:25 and Lev 23:43-25:3. That last one
  contains the gold item Lev 24:13-23, found again by the blind scan with its
  centre in Lev 24:19, inside the published centre (24:19-20). The 27 Greek windows
  fall in 13 stretches, none passes BY, and three are flagged
  division-dependent (they vanish under verse units). The word scale finds
  nothing, as the arithmetic predicted: its best attainable p's cannot reach
  the threshold.
* **Inclusio (descriptive, never tested)** is rare: 378 of 937,650 Hebrew
  windows and 117 of 370,251 Greek ones, and 2 of the 3,158 Hebrew windows
  at q <= 0.10. No gold item, control or target has one. The threshold is
  why: the code takes "the corpus median" over lemma types, as it did before
  run 2. Most lemmas are rare, so that median sits high and only a rare
  shared lemma counts. Gen 9:6a begins and ends with "shed" (IDF 5.35),
  which falls below it. A median over running words would sit far lower;
  it was not computed.
* **The LXX side check** decides nothing, but it is consistent. Lev
  24:13-23 keeps a mirror in Brenton (T 0.435, p 0.017). Of the 3,158
  Hebrew scan windows, 2,982 have a Greek test; 2,727 of those keep a
  positive T (median 0.30, against the Hebrew's higher values) and 1,891
  reach p < 0.05. The 176 with no Greek test sit where the Septuagint's
  order or extent differs from the Hebrew (Exodus 28 and 37 to 40, Jeremiah
  25, Esther 5 and 6, 1 Samuel 17, 1 Kings 13), so the verse mapping leaves
  no Greek window.
  Gen 9:6a keeps its perfect mirror (T 1.0). Isa 6:10 and Amos 5:5 lose
  theirs in translation (T 0).

### What this answers

* **Do repeated words in the Hebrew and Greek text prefer mirror order?
  No.** At the verse scale they prefer parallel order in every group, most
  of all in Hebrew poetry. That is parallelism, the best-known feature of
  Hebrew verse, showing through a test built to look for its opposite.
* **Is the flood narrative chiastic?** Its repetitions nest around 8:1a more
  than chance would order them, at a small effect size that holds across
  every registered switch and in the Septuagint. That is consistent with
  the published palistrophe and does not establish its particular pairs.
* **Babel and the Johannine prologue:** the lemma evidence does not support
  mirror order at their published centres.

## Caveats

* **Grammar makes order.** 6a's verb pairs are few (2 to 59 windows per
  group). Hebrew word order, not rhetoric, drives much of what 6a measures.
  The registration said so before the run.
* **A repeated core at a window's centre scores as mirror order (found
  after the run).** V3 printed planted-repetition detection rates for every
  host size, though B3 reads only the bar's cell, n = 24, where it passed
  (0.03, 0.04, 0.00). At smaller hosts the rates are high: in Hebrew prose
  0.72 at n = 8, 0.50 at 12 and 0.19 at 16; in poetry 0.43, 0.23 and 0.11;
  in Greek 0.16, 0.09 and 0.09. The mechanism: a qualifying window may be
  longer than its host. Repetition planted in a short host then sits at the
  centre of a longer window, and every match in the window's outer units
  nests around that repeated core. The statistic credits each such nesting
  as mirror order, and the within-side shuffle, which scatters the core,
  does not reproduce it. A toy check (12 units a side, random vocabulary,
  one lemma added to the 4 units either side of the centre) moved three
  random windows' p from 0.36, 0.83 and 0.087 to 0.091, 0.021 and 0.0005.
  So 6c's hits, and T1's, read as "mirror order, or a dense repeated core
  at the centre". The top Hebrew hit (Lev 21:19-22:5) has at its centre the
  speech formula addressed to Aaron and his sons, repeated in 21:24 and
  22:1-3. Nothing
  was changed: a statistic that separates the two is a new registration.
* **Lemma recall is a floor.** A pair the proposer saw through synonyms,
  pronouns or themes is invisible here (Matt 7:6, the registered blind spot,
  and most of T4's pairs).
* **The Greek units are editorial.** TAGNT's clause punctuation follows the
  Tyndale House GNT. Every Greek row carries that flag.
* **6a's power check cannot be met far from the null.** See the reading. A
  check that re-plants into a corpus already far below the null tests the
  corpus's level, not the method's sensitivity. A later registration should
  measure power against the null's own distribution.

## Deviations and post-run changes

* **Pre-run amendments** (recorded in the pre-registration before
  validation): the frozen B1 denominator is three; T3 and T5 were dropped,
  leaving a Holm family of four; the #3402 review's advisories (the Holm
  family size, 6a after a failed bar, the cap wording); the named centres;
  the readings of oleh we-yored, Psalm titles, `+`-joined names and U+0387.
* **Run 1 was stopped during V3 and restarted (run 2).** One thread was
  working through a chunk of 19 of the heaviest plants alone while the rest
  sat idle. Commit 8be8db594 hands the plants out one at a time, heaviest
  first. That changes only the execution order: plants are seeded by their
  index, not by the thread that runs them. Before stopping, run 1 had
  finished V1, V2 and the sealed scans. Its sealed files are byte-identical
  to run 2's (Hebrew sha256 `bf4e8dfc947500f8`, Greek `95fae450b1cb0375`),
  and none of run 1's later output was read.
* **The inclusio table was missing from run 2 and added after it (run 3).**
  The registration says the inclusio detector "prints its own table"; run 2
  only flagged inclusio on the scan's shown candidates. Commit 3432a1c81
  adds the table. It enters no score and is never tested, so it cannot move
  any registered result. Run 3 reproduced run 2 byte for byte apart from the new section: the
  three sealed files are identical, and `diff` of the two reports shows only
  the inclusio table's added lines.
* **Two reader fixes from the PR's peer review, after run 3 (run 4).**
  * *Split Hebrew verses.* TAHOT numbers each part of an English verse
    built from two Hebrew verses from 1, and the reader sorted a verse's
    words by that number alone, so the two parts interleaved. Eleven
    verses were affected: Num 26:1, 1 Sam 20:42, 1 Kgs 18:33, 20:2, 22:22
    and 22:43, 1 Chr 12:4, and the titles of Psalms 51, 52, 54 and 60.
    TAGNT has none. Commit c7602baf8 sorts by the Hebrew verse, then the
    word number. No gold item, control or target touches those verses.
  * *V3 detection when a plant lowers Tarone's K.* Exact windows newly
    screened in were left out of the rerun's known p's. This was latent:
    both scans skip exact windows (none can pass the screen), and no plant
    can move K across that line. Fixed in the same commit, with a test.
    Run 4's Greek output, which the split-verse fix cannot touch, is
    byte-identical to run 3's.
  * *An undefined 6a mean* (a class with no windows) would have read as the
    floor p; it now reads p = 1. No class was empty.

  Run 4 changed only Hebrew figures, and no verdict. The superseded run 3
  figures:

  | Figure | Run 3 | Run 4 |
  |---|---|---|
  | Hebrew scan: Tarone K = screened m | 318,869 | 318,830 |
  | Hebrew scan: windows at BH q <= 0.10 (BY) | 3,159 (18) | 3,158 (18) |
  | Hebrew sealed file sha256 | `bf4e8dfc947500f8` | `9dcfcc4f1d73f7b7` |
  | `+`-joined name continuations folded | 775 | 778 |
  | B2 Hebrew prose at (12, 24) | 0.84 | 0.83 |
  | B3 Hebrew prose: parallels, repetition | 0.01, 0.04 | 0.00, 0.03 |
  | Planted repetition, prose n = 8, 12, 16 | 0.64, 0.44, 0.23 | 0.72, 0.50, 0.19 |
  | Planted repetition, poetry n = 8, 12, 16 | 0.46, 0.29, 0.09 | 0.43, 0.23, 0.11 |
  | 6a Hebrew narrative mean T | -0.3477 | -0.3484 |
  | 6a poetry minus narrative (95% interval) | -0.2955 (-0.4138 to -0.1691) | -0.2948 (-0.4135 to -0.1684) |
  | Hebrew word-scale tests | 86,060 | 86,059 |

  The rest of V3's planted grid moved by a few plants per cell, because the
  clean-host mask and m moved, and some scan windows in 1 Sam 20-21 and
  1 Kgs 18 and 22 changed p. T1 to T4, V1, V2 and the Greek scan did not
  change.
* **Nothing else was changed after any run.** No threshold, seed, unit
  rule, stop list or item moved.

## Generated report

Generated by `flock-scripture-import research`. Inputs (datasets pinned in `data/scripture/manifest.toml`, or tables committed under `data/scripture/research/`):

* `tahot-gen-deu` sha256 `e9b8546ee48f`
* `tahot-jos-est` sha256 `195fee1dc365`
* `tahot-job-sng` sha256 `bb508af3af07`
* `tahot-isa-mal` sha256 `f3ded203d2a7`
* `tagnt-mat-jhn` sha256 `ab8eaaeb68e1`
* `tagnt-act-rev` sha256 `524e32375361`
* `tvtms` sha256 `63058e0f2020`
* `tbesh` sha256 `464dccadd95f`
* `brenton` sha256 `bc414101e94f`

### Verdicts

Registered in docs/data/scripture-research-class-a.md (Track 6, with its pre-run amendments). No row says "chiasm": the reading is only whether mirror order exceeds parallel order and the permutation null.

* B1 passes, B3 passes, B4 passes. B2: Hebrew prose passes, Hebrew poetry passes, Greek passes. The method is validated: the targets, 6a and the scan are run.
* 6b T1 (The flood, Gen 6:10-9:19, centred on 8:1a): mirror order exceeds parallel order and the permutation null at Holm-adjusted p = 0.0049.
* 6b T2a (Babel, Gen 11:1-9, centred on 11:5a): mirror order does not exceed parallel order and the permutation null at Holm-adjusted p = 1.0000.
* 6b T2b (Babel, Gen 11:1-9, centred on 11:6): mirror order does not exceed parallel order and the permutation null at Holm-adjusted p = 1.0000.
* 6b T4 (The Johannine prologue, John 1:1-18, centred on 1:12b): mirror order does not exceed parallel order and the permutation null at Holm-adjusted p = 1.0000.
* 6a Hebrew poetry: mean T -0.6432, p 1.0000: underpowered (power 0.00).
* 6a The prophets: mean T -0.3420, p 1.0000: underpowered (power 0.00).
* 6a Hebrew narrative: mean T -0.3484, p 1.0000: underpowered (power 0.00).
* 6a Greek New Testament: mean T -0.1721, p 1.0000: underpowered (power 0.00).
* 6c Hebrew OT (level-1 units): 3158 windows at q <= 0.10 (BH).
* 6c Greek NT (clause units): 27 windows at q <= 0.10 (BH).

### Run facts

Hebrew: 23261 verses, 305471 words, 8512 keys. Greek: 7958 verses, 137589 words, 5351 keys. Seeds: sampled p 20261022, 20261027, 20261028; 6a 20261023; bootstrap 20261024; V3 hosts 20261025; 6a power 20261026. Weights are IDF in fixed point (1/4096 nat).

### The data check

| Book | Verses | atnach | oleh we-yored | segolta | shalshelet | zaqef qatan | zaqef gadol | tipcha | no level-1 | words per level-1 unit |
|---|---|---|---|---|---|---|---|---|---|---|
| Gen | 1533 | 1466 | 0 | 72 | 3 | 1201 | 167 | 1533 | 67 | 6.9 |
| Exod | 1213 | 1146 | 0 | 80 | 0 | 920 | 94 | 1213 | 67 | 7.1 |
| Lev | 859 | 813 | 0 | 55 | 1 | 648 | 55 | 859 | 46 | 7.1 |
| Num | 1288 | 1151 | 0 | 96 | 0 | 913 | 106 | 1288 | 137 | 6.7 |
| Deut | 959 | 910 | 0 | 67 | 0 | 756 | 68 | 959 | 49 | 7.7 |
| Josh | 658 | 575 | 0 | 36 | 0 | 507 | 45 | 658 | 83 | 8.2 |
| Judg | 618 | 605 | 0 | 43 | 0 | 542 | 62 | 618 | 13 | 8.1 |
| Ruth | 85 | 79 | 0 | 2 | 0 | 75 | 8 | 85 | 6 | 7.9 |
| 1Sam | 810 | 796 | 0 | 40 | 0 | 722 | 68 | 810 | 14 | 8.3 |
| 2Sam | 695 | 675 | 0 | 24 | 0 | 588 | 75 | 695 | 20 | 8.1 |
| 1Kgs | 816 | 774 | 0 | 42 | 0 | 687 | 80 | 816 | 42 | 8.3 |
| 2Kgs | 719 | 706 | 0 | 47 | 0 | 604 | 70 | 719 | 13 | 8.6 |
| 1Chr | 942 | 665 | 0 | 23 | 0 | 700 | 54 | 942 | 277 | 6.7 |
| 2Chr | 822 | 778 | 0 | 66 | 0 | 694 | 90 | 822 | 44 | 8.3 |
| Ezra | 280 | 212 | 0 | 16 | 1 | 211 | 31 | 280 | 68 | 7.6 |
| Neh | 406 | 294 | 0 | 21 | 0 | 305 | 32 | 405 | 112 | 7.6 |
| Esth | 167 | 157 | 0 | 13 | 0 | 150 | 15 | 167 | 10 | 9.4 |
| Job | 1070 | 1020 | 37 | 6 | 0 | 41 | 1 | 47 | 46 | 3.9 |
| Ps | 2577 | 2305 | 302 | 0 | 0 | 0 | 0 | 0 | 229 | 3.8 |
| Prov | 915 | 903 | 27 | 0 | 0 | 0 | 0 | 0 | 10 | 3.7 |
| Eccl | 222 | 203 | 0 | 2 | 0 | 179 | 17 | 222 | 19 | 7.0 |
| Song | 117 | 86 | 0 | 1 | 0 | 108 | 6 | 117 | 31 | 6.2 |
| Isa | 1292 | 1267 | 0 | 25 | 1 | 1041 | 61 | 1292 | 25 | 6.6 |
| Jer | 1364 | 1313 | 0 | 63 | 0 | 1149 | 99 | 1364 | 51 | 8.2 |
| Lam | 154 | 67 | 0 | 1 | 0 | 133 | 1 | 154 | 87 | 7.0 |
| Ezek | 1273 | 1203 | 0 | 70 | 0 | 1064 | 128 | 1273 | 70 | 7.6 |
| Dan | 357 | 347 | 0 | 21 | 0 | 322 | 38 | 357 | 10 | 8.4 |
| Hos | 197 | 191 | 0 | 2 | 0 | 158 | 20 | 197 | 6 | 6.1 |
| Joel | 73 | 71 | 0 | 1 | 0 | 61 | 6 | 73 | 2 | 6.6 |
| Amos | 146 | 142 | 0 | 4 | 1 | 105 | 5 | 146 | 4 | 7.1 |
| Obad | 21 | 20 | 0 | 0 | 0 | 18 | 1 | 21 | 1 | 7.1 |
| Jonah | 48 | 45 | 0 | 1 | 0 | 42 | 2 | 48 | 3 | 7.4 |
| Mic | 105 | 105 | 0 | 1 | 0 | 90 | 5 | 105 | 0 | 6.6 |
| Nah | 47 | 47 | 0 | 0 | 0 | 43 | 3 | 47 | 0 | 5.9 |
| Hab | 56 | 55 | 0 | 1 | 0 | 42 | 5 | 56 | 1 | 6.0 |
| Zeph | 53 | 50 | 0 | 0 | 0 | 46 | 1 | 53 | 3 | 7.4 |
| Hag | 38 | 36 | 0 | 0 | 0 | 30 | 3 | 38 | 2 | 8.1 |
| Zech | 211 | 200 | 0 | 11 | 0 | 180 | 26 | 211 | 11 | 7.6 |
| Mal | 55 | 54 | 0 | 1 | 0 | 51 | 9 | 55 | 1 | 8.0 |

Each count is verses holding that divider at least once. 1 ole marks have no merkha on their word or the next, so make no division; 778 name continuations (a `+`-joined name's second word) were folded into the word before.

| Book | comma | full stop | ano teleia U+00B7 | ano teleia U+0387 | question U+003B | question U+037E | words per clause |
|---|---|---|---|---|---|---|---|
| Matt | 751 | 866 | 0 | 684 | 0 | 171 | 7.4 |
| Mark | 446 | 558 | 0 | 363 | 0 | 108 | 7.6 |
| Luke | 768 | 952 | 0 | 658 | 0 | 155 | 7.7 |
| John | 769 | 769 | 0 | 603 | 0 | 167 | 6.8 |
| Acts | 782 | 712 | 0 | 476 | 0 | 71 | 9.0 |
| Rom | 419 | 274 | 0 | 183 | 0 | 83 | 7.4 |
| 1Cor | 481 | 285 | 0 | 199 | 0 | 106 | 6.4 |
| 2Cor | 368 | 158 | 0 | 95 | 0 | 25 | 6.9 |
| Gal | 162 | 99 | 0 | 59 | 0 | 19 | 6.6 |
| Eph | 140 | 58 | 0 | 27 | 0 | 1 | 10.6 |
| Phil | 127 | 53 | 0 | 35 | 0 | 1 | 7.5 |
| Col | 115 | 41 | 0 | 35 | 0 | 1 | 8.2 |
| 1Thess | 84 | 43 | 0 | 37 | 0 | 3 | 8.8 |
| 2Thess | 44 | 24 | 0 | 12 | 0 | 1 | 10.0 |
| 1Tim | 164 | 67 | 0 | 26 | 0 | 1 | 6.1 |
| 2Tim | 119 | 54 | 0 | 32 | 0 | 0 | 6.0 |
| Titus | 72 | 28 | 0 | 10 | 0 | 0 | 5.9 |
| Phlm | 24 | 11 | 0 | 7 | 0 | 1 | 7.8 |
| Heb | 284 | 177 | 0 | 142 | 0 | 18 | 8.0 |
| Jas | 104 | 78 | 0 | 52 | 0 | 22 | 6.8 |
| 1Pet | 139 | 47 | 0 | 41 | 0 | 4 | 7.2 |
| 2Pet | 70 | 37 | 0 | 17 | 0 | 2 | 8.7 |
| 1John | 125 | 99 | 0 | 46 | 0 | 4 | 7.8 |
| 2John | 14 | 9 | 0 | 6 | 0 | 0 | 8.2 |
| 3John | 13 | 16 | 0 | 5 | 0 | 0 | 6.4 |
| Jude | 44 | 17 | 0 | 7 | 0 | 0 | 6.8 |
| Rev | 448 | 386 | 0 | 147 | 0 | 8 | 9.9 |

Word-final characters skipped before reading the punctuation (paragraph marks, brackets): ' ' (U+0020) 1, ']' (U+005D) 8, '¬' (U+00AC) 1, '¶' (U+00B6) 2150, '᾽' (U+1FBD) 1357.

| Expectation (written before the run) | Data |
|---|---|
| Gen 9:6 word 3 carries zaqef qatan (level 2) | holds |
| Gen 9:6 word 4 carries tipcha (level 2) | holds |
| Gen 9:6 word 6 carries atnach (so 9:6a is words 1-6) | holds |
| Isa 6:10 word 8 carries atnach | holds |
| Amos 5:5's atnach falls on "cross over" (H5674), after "do not cross over to Beersheba" | holds |
| Mark 2:27 word 9 (egeneto) ends with a comma | holds |
| Gen 8:1's first level-1 unit holds "remembered" (H2142) | holds |
| Gen 11:5's first level-1 unit holds "came down" (H3381) and the verse has two | holds |
| John 1:12 word 5 is "gave" (G1325), in its own clause | holds |

### V1: the gold set (structure only)

#### G1 Gen 9:6a (verified (Welch 2020))

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| Gen 9:6, zaqef qatan after word 3 | 6 | 3 | 60.17 | 0.00 | 1.000 | 13.50 | 0.1667 | exact (6 of 36) | 0.1667 | 0.0667 (exact (48 of 720)) |
| Gen 9:6, tipcha after word 4 | 6 | 2 | 23.35 | 0.00 | 1.000 | 9.71 | 0.5000 | exact (2 of 4) | 0.5000 | 0.4000 (exact (288 of 720)) |

Matched pairs at the published centre (Gen 9:6, zaqef qatan after word 3), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Gen 9:6 w3 | Gen 9:6 w4 | H0120 | אָדָם | man | 3.79 |  |
| Gen 9:6 w2 | Gen 9:6 w5 | H1818 | דָּם | blood | 4.37 | mirror |
| Gen 9:6 w1 | Gen 9:6 w6 | H8210 | שָׁפַךְ | pour | 5.35 | mirror |

**Recovered.** T = 1.000 at the published centre, no test higher, 3 published keys matched in mirror order.

#### G2 Isa 6:10 (verified (Parry 2020))

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| Isa 6:10, atnach after word 8 | 17 | 2 | 16.24 | 0.00 | 1.000 | 8.20 | 0.5000 | exact (2 of 4) | 0.5000 | 0.1411 (sampled, B = 99999, 14109 as high) |

Matched pairs at the published centre (Isa 6:10, atnach after word 8), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Isa 6:10 w7 | Isa 6:10 w11 | H5869 | עַ֫יִן | eye | 3.34 |  |
| Isa 6:10 w5 | Isa 6:10 w12 | H0241 | אֹ֫זֶן | ear | 4.87 | mirror |

**Recovered.** T = 1.000 at the published centre, no test higher, 2 published keys matched in mirror order.

#### G3 Lev 24:13-23 (verified (Willis 2009))

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the units of 24:19-24:20 | 18 | 20 | 5467.10 | 449.39 | 0.848 | 130.54 | 2.30e-6 | sampled, B = 10000000, 22 as high | 1.00e-9 | 6.00e-5 (sampled, B = 99999, 5 as high) |

Matched pairs at the published centre (the units of 24:19-24:20), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 24:18 w1-w4 | Lev 24:21 w1-w3 | H0929 | בְּהֵמָה | animal | 4.91 |  |
| Lev 24:18 w1-w4 | Lev 24:21 w1-w3 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:18 w1-w4 | Lev 24:21 w1-w3 | H7999 | שָׁלֵם | to complete | 5.38 | tied |
| Lev 24:18 w1-w4 | Lev 24:21 w4-w6 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:17 w7-w8 | Lev 24:21 w4-w6 | H4191 | מוּת | to die | 3.50 | tied |
| Lev 24:17 w1-w6 | Lev 24:21 w1-w3 | H5221 | נָכָה | to smite | 3.92 | parallel |
| Lev 24:17 w1-w6 | Lev 24:21 w4-w6 | H0120 | אָדָם | man | 3.79 | tied |
| Lev 24:17 w1-w6 | Lev 24:21 w4-w6 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:17 w1-w6 | Lev 24:22 w8-w11 | H3588 | כִּי | for | 1.78 | tied |
| Lev 24:16 w11-w15 | Lev 24:21 w4-w6 | H4191 | מוּת | to die | 3.50 | parallel |
| Lev 24:16 w11-w15 | Lev 24:22 w1-w7 | H1616 | גֵּר | sojourner | 5.64 | tied |
| Lev 24:16 w11-w15 | Lev 24:22 w1-w7 | H0249 | אֶזְרָח | born | 7.22 | tied |
| Lev 24:16 w1-w10 | Lev 24:21 w4-w6 | H4191 | מוּת | to die | 3.50 | parallel |
| Lev 24:16 w1-w10 | Lev 24:22 w8-w11 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 24:16 w1-w10 | Lev 24:23 w1-w14 | H7275 | רָגַם | to stone | 7.35 | tied |
| Lev 24:16 w1-w10 | Lev 24:23 w15-w22 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 24:15 w6-w12 | Lev 24:22 w8-w11 | H0430 | אֱלֹהִים | God | 2.34 | parallel |
| Lev 24:15 w6-w12 | Lev 24:22 w8-w11 | H3588 | כִּי | for | 1.78 | tied |
| Lev 24:15 w6-w12 | Lev 24:23 w1-w14 | H7043 | קָלַל | to lighten | 5.69 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H3478 | יִשְׂרָאֵל | Israel | 2.34 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w15-w22 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w15-w22 | H3478 | יִשְׂרָאֵל | Israel | 2.34 | tied |
| Lev 24:14 w14-w17 | Lev 24:23 w1-w14 | H7275 | רָגַם | to stone | 7.35 | parallel |
| Lev 24:14 w1-w13 | Lev 24:23 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 24:14 w1-w13 | Lev 24:23 w1-w14 | H3318 | יָצָא | come | 3.16 | tied |
| Lev 24:14 w1-w13 | Lev 24:23 w1-w14 | H2351 | חוּץ | outside | 4.99 | tied |
| Lev 24:14 w1-w13 | Lev 24:23 w1-w14 | H7043 | קָלַל | to lighten | 5.69 | tied |
| Lev 24:14 w1-w13 | Lev 24:23 w1-w14 | H4264 | מַחֲנֶה | camp | 4.81 | tied |
| Lev 24:13 w1-w5 | Lev 24:22 w8-w11 | H3068 | יהוה | LORD | 1.44 | parallel |
| Lev 24:13 w1-w5 | Lev 24:23 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 24:13 w1-w5 | Lev 24:23 w1-w14 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 24:13 w1-w5 | Lev 24:23 w1-w14 | H4872 | מֹשֶׁה | Moses | 3.50 | tied |
| Lev 24:13 w1-w5 | Lev 24:23 w15-w22 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 24:13 w1-w5 | Lev 24:23 w15-w22 | H4872 | מֹשֶׁה | Moses | 3.50 | tied |

**Recovered.** T = 0.848 at the published centre, no test higher, 6 published keys matched in mirror order.

#### G4 Amos 5:5 (pending (de Waard 1977 not read))

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| Amos 5:5, atnach after word 11 | 16 | 2 | 37.83 | 0.00 | 1.000 | 12.31 | 0.5000 | exact (2 of 4) | 0.5000 | 0.2345 (sampled, B = 99999, 23449 as high) |

Matched pairs at the published centre (Amos 5:5, atnach after word 11), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Amos 5:5 w5 | Amos 5:5 w13 | H1537 | גִּלְגָּל | Gilgal | 6.42 |  |
| Amos 5:5 w3 | Amos 5:5 w16 | H1008 | בֵּֽיתְ־אֵל | Bethel | 5.90 | mirror |

**Recovered (not in the denominator).** T = 1.000 at the published centre, no test higher, 2 published keys matched in mirror order.

#### G5 Mark 2:27 (pending (no scholarly source read))

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| Mark 2:27, the '·' break after word 3 | 4 | 0 | 0.00 | 0.00 | 0.000 | 0.00 | 1.0000 | exact (1 of 1) | 1.0000 | 1.0000 (exact (24 of 24)) |
| Mark 2:27, the ',' break after word 9 | 5 | 2 | 13.41 | 0.00 | 1.000 | 7.61 | 0.5000 | exact (2 of 4) | 0.5000 | 0.2000 (exact (24 of 120)) |

Matched pairs at the published centre (Mark 2:27, the ',' break after word 9), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Mark 2:27 w8 | Mark 2:27 w13 | G0444 | ἄνθρωπος | a human | 2.77 |  |
| Mark 2:27 w5 | Mark 2:27 w16 | G4521 | σάββατον | Sabbath | 4.84 | mirror |

Flag: the Greek units are editorial (TAGNT's punctuation follows the Tyndale House GNT).

**Recovered (not in the denominator).** T = 1.000 at the published centre, no test higher, 2 published keys matched in mirror order.

#### G6 Matt 7:6 (blind spot: no lemma method can see it; never counted)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| Matt 7:6, the ',' break after word 21 | 13 | 0 | 0.00 | 0.00 | 0.000 | 0.00 | 1.0000 | exact (1 of 1) | 1.0000 | 1.0000 (sampled, B = 99999, 99999 as high) |

Flag: the Greek units are editorial (TAGNT's punctuation follows the Tyndale House GNT).

The gold items under each switch (descriptive; the bar reads the primary setting):

The Hebrew wide switch drops 104 base numbers whose TBESH morph type is Prep, Conj, Part, Neg, Cond, PerP, DemP, Intg or Art: H0116, H0176, H0199, H0227, H0233, H0335, H0336, H0349, H0369, H0370, H0371, H0375, H0383, H0408, H0409, H0411, H0412, H0413, H0428, H0429, H0432, H0459, H0479, H0518, H0575, H0576, H0581, H0586, H0587, H0589, H0595, H0607, H0608, H0637, H0638, H0645, H0854, H0859, H0994, H0997, H1077, H1097, H1115, H1119, H1297, H1454, H1571, H1668, H1768, H1791, H1797, H1836, H1931, H1932, H1963, H1975, H1976, H1977, H1992, H1994, H2006, H2063, H2088, H2090, H2097, H2098, H3282, H3487, H3588, H3644, H3652, H3808, H3809, H3860, H3861, H3884, H3890, H3926, H3964, H4069, H4100, H4101, H4310, H4479, H4480, H4481, H4970, H5049, H5168, H5668, H5704, H5705, H5921, H5922, H5924, H5973, H5974, H5978, H6435, H6441, H6903, H6925, H7535, H8460.

| Item | v1u (uStrong keys) | Hebrew wide stop list | weights 1 | Greek verse units | Hebrew level-2 units |
|---|---|---|---|---|---|
| G1 Gen 9:6a | T 1.00, recovered | T 1.00, recovered | T 1.00, recovered | T 1.00, recovered | T 1.00, recovered |
| G2 Isa 6:10 | T 1.00, recovered | T 1.00, recovered | T 1.00, recovered | T 1.00, recovered | T 1.00, recovered |
| G3 Lev 24:13-23 | T 0.84, recovered | T 0.86, recovered | T 0.76, recovered | T 0.85, recovered | T 0.62, recovered |
| G4 Amos 5:5 | T 1.00, recovered | T 1.00, recovered | T 1.00, recovered | T 1.00, recovered | T 1.00, recovered |
| G5 Mark 2:27 | T 1.00, recovered | T 1.00, recovered | T 1.00, recovered | - | T 1.00, recovered |
| G6 Matt 7:6 | - | - | - | - | - |

**B1: 3 of 3 counted gold items recovered; the bar needs 3. Passes.**

### V2: the negative controls

#### C1 Matt 7:7-8

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the boundary before 7:8 | 9 | 5 | 0.00 | 186.29 | -1.000 | 24.34 | 1.0000 | exact (720 of 720) | 0.0333 | 1.0000 (exact (362880 of 362880)) |

Matched pairs at the published centre (the boundary before 7:8), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Matt 7:7 w9-w11 | Matt 7:8 w10-w13 | G0455 | ἀνοίγω | to open | 4.66 |  |
| Matt 7:7 w8 | Matt 7:8 w10-w13 | G2925 | κρούω | to knock | 6.78 | tied |
| Matt 7:7 w6-w7 | Matt 7:8 w6-w9 | G2147 | εὑρίσκω | to find/meet | 3.86 | parallel |
| Matt 7:7 w5 | Matt 7:8 w6-w9 | G2212 | ζητέω | to seek | 4.25 | tied |
| Matt 7:7 w1 | Matt 7:8 w1-w5 | G0154 | αἰτέω | to ask | 4.78 | parallel |

Flag: the Greek units are editorial (TAGNT's punctuation follows the Tyndale House GNT).

**Passes B4**: raw p 1.0000 under the primary null (never Holm-adjusted).

#### C2 Ps 24:7-10

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the boundary before 24:9 | 10 | 11 | 255.57 | 1546.35 | -0.716 | 77.11 | 0.9678 | exact (13936 of 14400) | 0.0017 | 0.9582 (sampled, B = 99999, 95819 as high) |

Matched pairs at the published centre (the boundary before 24:9), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Ps 24:8 w8-w10 | Ps 24:10 w6-w7 | H3068 | יהוה | LORD | 1.44 |  |
| Ps 24:8 w5-w7 | Ps 24:10 w6-w7 | H3068 | יהוה | LORD | 1.44 | tied |
| Ps 24:8 w1-w4 | Ps 24:9 w7-w9 | H4428 | מֶ֫לֶךְ | king | 2.49 | parallel |
| Ps 24:8 w1-w4 | Ps 24:9 w7-w9 | H3519 | כָּבוֹד | glory | 4.81 | tied |
| Ps 24:8 w1-w4 | Ps 24:10 w1-w5 | H4310 | מִי | who? | 4.22 | tied |
| Ps 24:8 w1-w4 | Ps 24:10 w1-w5 | H2088 | זֶה | this | 3.09 | tied |
| Ps 24:8 w1-w4 | Ps 24:10 w1-w5 | H4428 | מֶ֫לֶךְ | king | 2.49 | tied |
| Ps 24:8 w1-w4 | Ps 24:10 w1-w5 | H3519 | כָּבוֹד | glory | 4.81 | tied |
| Ps 24:8 w1-w4 | Ps 24:10 w8-w11 | H4428 | מֶ֫לֶךְ | king | 2.49 | tied |
| Ps 24:8 w1-w4 | Ps 24:10 w8-w11 | H3519 | כָּבוֹד | glory | 4.81 | tied |
| Ps 24:7 w7-w9 | Ps 24:9 w7-w9 | H0935 | בּוֹא | come | 2.31 | parallel |
| Ps 24:7 w7-w9 | Ps 24:9 w7-w9 | H4428 | מֶ֫לֶךְ | king | 2.49 | tied |
| Ps 24:7 w7-w9 | Ps 24:9 w7-w9 | H3519 | כָּבוֹד | glory | 4.81 | tied |
| Ps 24:7 w7-w9 | Ps 24:10 w1-w5 | H4428 | מֶ֫לֶךְ | king | 2.49 | tied |
| Ps 24:7 w7-w9 | Ps 24:10 w1-w5 | H3519 | כָּבוֹד | glory | 4.81 | tied |
| Ps 24:7 w7-w9 | Ps 24:10 w8-w11 | H4428 | מֶ֫לֶךְ | king | 2.49 | tied |
| Ps 24:7 w7-w9 | Ps 24:10 w8-w11 | H3519 | כָּבוֹד | glory | 4.81 | tied |
| Ps 24:7 w1-w6 | Ps 24:9 w1-w6 | H7218 | רֹאשׁ | head | 3.75 | parallel |
| Ps 24:7 w1-w6 | Ps 24:9 w1-w6 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 24:7 w1-w6 | Ps 24:9 w1-w6 | H6607 | פֶּ֫תַח | entrance | 5.02 | tied |
| Ps 24:7 w1-w6 | Ps 24:9 w1-w6 | H5375 | נָשָׂא | bear | 3.63 | tied |
| Ps 24:7 w1-w6 | Ps 24:9 w1-w6 | H8179 | שַׁ֫עַר | gate | 4.34 | tied |

**Passes B4**: raw p 0.9678 under the primary null (never Holm-adjusted).

#### C3 Ps 136:1-9

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the units of 136:5-136:5 | 17 | 5 | 5000.06 | 4721.93 | 0.029 | 179.45 | 0.2933 | exact (25344 of 86400) | 0.0667 | 0.3184 (sampled, B = 99999, 31841 as high) |

Matched pairs at the published centre (the units of 136:5-136:5), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Ps 136:4 w5-w7 | Ps 136:6 w5-w7 | H3588 | כִּי | for | 1.78 |  |
| Ps 136:4 w5-w7 | Ps 136:6 w5-w7 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:4 w5-w7 | Ps 136:6 w5-w7 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:4 w5-w7 | Ps 136:7 w4-w6 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:4 w5-w7 | Ps 136:7 w4-w6 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:4 w5-w7 | Ps 136:7 w4-w6 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:4 w5-w7 | Ps 136:8 w5-w7 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:4 w5-w7 | Ps 136:8 w5-w7 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:4 w5-w7 | Ps 136:8 w5-w7 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:4 w5-w7 | Ps 136:9 w6-w8 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:4 w5-w7 | Ps 136:9 w6-w8 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:4 w5-w7 | Ps 136:9 w6-w8 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:4 w1-w4 | Ps 136:7 w1-w3 | H6213 | עָשָׂה | do | 2.32 | parallel |
| Ps 136:4 w1-w4 | Ps 136:7 w1-w3 | H1419 | גַּל | large | 3.85 | tied |
| Ps 136:3 w4-w6 | Ps 136:6 w5-w7 | H3588 | כִּי | for | 1.78 | parallel |
| Ps 136:3 w4-w6 | Ps 136:6 w5-w7 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:3 w4-w6 | Ps 136:6 w5-w7 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:3 w4-w6 | Ps 136:7 w4-w6 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:3 w4-w6 | Ps 136:7 w4-w6 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:3 w4-w6 | Ps 136:7 w4-w6 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:3 w4-w6 | Ps 136:8 w5-w7 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:3 w4-w6 | Ps 136:8 w5-w7 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:3 w4-w6 | Ps 136:8 w5-w7 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:3 w4-w6 | Ps 136:9 w6-w8 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:3 w4-w6 | Ps 136:9 w6-w8 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:3 w4-w6 | Ps 136:9 w6-w8 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:2 w4-w6 | Ps 136:6 w5-w7 | H3588 | כִּי | for | 1.78 | parallel |
| Ps 136:2 w4-w6 | Ps 136:6 w5-w7 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:2 w4-w6 | Ps 136:6 w5-w7 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:2 w4-w6 | Ps 136:7 w4-w6 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:2 w4-w6 | Ps 136:7 w4-w6 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:2 w4-w6 | Ps 136:7 w4-w6 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:2 w4-w6 | Ps 136:8 w5-w7 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:2 w4-w6 | Ps 136:8 w5-w7 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:2 w4-w6 | Ps 136:8 w5-w7 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:2 w4-w6 | Ps 136:9 w6-w8 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:2 w4-w6 | Ps 136:9 w6-w8 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:2 w4-w6 | Ps 136:9 w6-w8 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:1 w5-w7 | Ps 136:6 w5-w7 | H3588 | כִּי | for | 1.78 | parallel |
| Ps 136:1 w5-w7 | Ps 136:6 w5-w7 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:1 w5-w7 | Ps 136:6 w5-w7 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:1 w5-w7 | Ps 136:7 w4-w6 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:1 w5-w7 | Ps 136:7 w4-w6 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:1 w5-w7 | Ps 136:7 w4-w6 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:1 w5-w7 | Ps 136:8 w5-w7 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:1 w5-w7 | Ps 136:8 w5-w7 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:1 w5-w7 | Ps 136:8 w5-w7 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:1 w5-w7 | Ps 136:9 w6-w8 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:1 w5-w7 | Ps 136:9 w6-w8 | H5769 | עוֹלָם | enduring | 4.03 | tied |
| Ps 136:1 w5-w7 | Ps 136:9 w6-w8 | H2617 | חֶ֫סֶד | kindness | 4.57 | tied |
| Ps 136:1 w1-w4 | Ps 136:6 w5-w7 | H3588 | כִּי | for | 1.78 | parallel |
| Ps 136:1 w1-w4 | Ps 136:7 w4-w6 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:1 w1-w4 | Ps 136:8 w5-w7 | H3588 | כִּי | for | 1.78 | tied |
| Ps 136:1 w1-w4 | Ps 136:9 w6-w8 | H3588 | כִּי | for | 1.78 | tied |

**Passes B4**: raw p 0.2933 under the primary null (never Holm-adjusted).

#### C4 Matt 7:24-27

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the boundary before 7:26 | 11 | 15 | 332.15 | 2035.27 | -0.719 | 89.41 | 0.8938 | exact (2574 of 2880) | 0.0042 | 0.8661 (sampled, B = 99999, 86609 as high) |

Matched pairs at the published centre (the boundary before 7:26), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Matt 7:25 w18-w20 | Matt 7:27 w18-w19 | G4098 | πίπτω | to collapse | 4.54 |  |
| Matt 7:25 w13-w17 | Matt 7:26 w1-w23 | G3614 | οἰκία | home | 4.54 | parallel |
| Matt 7:25 w13-w17 | Matt 7:27 w13-w17 | G3614 | οἰκία | home | 4.54 | tied |
| Matt 7:25 w1-w12 | Matt 7:27 w1-w12 | G2064 | ἔρχομαι | to come/go | 2.59 | parallel |
| Matt 7:25 w1-w12 | Matt 7:27 w1-w12 | G2597 | καταβαίνω | to come/go down | 4.58 | tied |
| Matt 7:25 w1-w12 | Matt 7:27 w1-w12 | G1028 | βροχή | rain | 8.29 | tied |
| Matt 7:25 w1-w12 | Matt 7:27 w1-w12 | G4215 | ποταμός | river | 6.21 | tied |
| Matt 7:25 w1-w12 | Matt 7:27 w1-w12 | G4154 | πνέω | to blow | 7.04 | tied |
| Matt 7:25 w1-w12 | Matt 7:27 w1-w12 | G0417 | ἄνεμος | wind | 5.61 | tied |
| Matt 7:24 w12-w22 | Matt 7:26 w1-w23 | G0435 | ἀνήρ | man | 3.71 | parallel |
| Matt 7:24 w12-w22 | Matt 7:26 w1-w23 | G3748 | ὅστις | who/which | 4.05 | tied |
| Matt 7:24 w12-w22 | Matt 7:26 w1-w23 | G3614 | οἰκία | home | 4.54 | tied |
| Matt 7:24 w12-w22 | Matt 7:26 w1-w23 | G3666 | ὁμοιόω | to liken | 6.27 | tied |
| Matt 7:24 w12-w22 | Matt 7:26 w1-w23 | G3618 | οἰκοδομέω | to build | 5.34 | tied |
| Matt 7:24 w12-w22 | Matt 7:27 w13-w17 | G3614 | οἰκία | home | 4.54 | tied |
| Matt 7:24 w1-w11 | Matt 7:26 w1-w23 | G4160 | ποιέω | to do/make | 2.74 | parallel |
| Matt 7:24 w1-w11 | Matt 7:26 w1-w23 | G0191 | ἀκούω | to hear | 2.99 | tied |
| Matt 7:24 w1-w11 | Matt 7:26 w1-w23 | G3748 | ὅστις | who/which | 4.05 | tied |
| Matt 7:24 w1-w11 | Matt 7:26 w1-w23 | G3056 | λόγος | word | 3.22 | tied |

Flag: the Greek units are editorial (TAGNT's punctuation follows the Tyndale House GNT).

**Passes B4**: raw p 0.8938 under the primary null (never Holm-adjusted).

#### C5 Luke 6:37

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| Luke 6:37, the ',' break after word 3 | 2 | 1 | 0.00 | 0.00 | 0.000 | 4.40 | 1.0000 | exact (1 of 1) | 1.0000 | 1.0000 (exact (2 of 2)) |
| Luke 6:37, the ',' break after word 10 | 2 | 1 | 0.00 | 0.00 | 0.000 | 7.60 | 1.0000 | exact (1 of 1) | 1.0000 | 1.0000 (exact (2 of 2)) |
| Luke 6:37, the ',' break after word 15 | 2 | 1 | 0.00 | 0.00 | 0.000 | 4.85 | 1.0000 | exact (1 of 1) | 1.0000 | 1.0000 (exact (2 of 2)) |

Flag: the Greek units are editorial (TAGNT's punctuation follows the Tyndale House GNT).

**Passes B4**: raw p 1.0000, 1.0000, 1.0000 under the primary null (never Holm-adjusted).

**B4: every control has p >= 0.10. Passes.**

### The unplanted unit-scale scan (sealed)

Computed before V3 and sealed: only the screened m (below) and the mask of windows with q <= 0.10 (for clean hosts) were read until the bar's verdict.

| Scan | Units | Windows | Tarone K | Screened m | Sealed file sha256 |
|---|---|---|---|---|---|
| Hebrew OT, level-1 units | 45157 | 937650 | 318830 | 318830 | `9dcfcc4f1d73f7b7` |
| Greek NT, clause units | 17982 | 370251 | 47984 | 47984 | `95fae450b1cb0375` |

### V3: planted chiasms in real text

#### Hebrew prose

k* = 12, n* = 24.

Detected share of planted mirrors by host size n (rows) and pairs k (columns), and of planted repetition:

| n | k=2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | repetition |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 8 | 0.14 | 0.19 | 0.24 | - | - | - | - | - | - | - | - | 0.72 |
| 12 | 0.13 | 0.20 | 0.28 | 0.22 | 0.40 | - | - | - | - | - | - | 0.50 |
| 16 | 0.06 | 0.18 | 0.26 | 0.23 | 0.27 | 0.52 | 0.65 | - | - | - | - | 0.19 |
| 24 | 0.04 | 0.20 | 0.17 | 0.25 | 0.30 | 0.56 | 0.76 | 0.75 | 0.78 | 0.87 | 0.83 | 0.03 |

Planted parallels detected (a false alarm):

| n | k | detected |
|---|---|---|
| 8 | 2 | 0.08 |
| 8 | 3 | 0.06 |
| 8 | 4 | 0.03 |
| 12 | 2 | 0.04 |
| 12 | 3 | 0.10 |
| 12 | 4 | 0.05 |
| 12 | 5 | 0.01 |
| 12 | 6 | 0.01 |
| 16 | 2 | 0.05 |
| 16 | 3 | 0.08 |
| 16 | 4 | 0.03 |
| 16 | 5 | 0.00 |
| 16 | 6 | 0.00 |
| 16 | 7 | 0.00 |
| 16 | 8 | 0.00 |
| 24 | 2 | 0.08 |
| 24 | 3 | 0.02 |
| 24 | 4 | 0.01 |
| 24 | 5 | 0.01 |
| 24 | 6 | 0.00 |
| 24 | 7 | 0.00 |
| 24 | 8 | 0.00 |
| 24 | 9 | 0.00 |
| 24 | 10 | 0.00 |
| 24 | 11 | 0.00 |
| 24 | 12 | 0.00 |

**B2 at (k, n) = (12, 24): power 0.83; passes. B3 there: parallels 0.00, repetition 0.03; passes.**

#### Hebrew poetry

k* = 12, n* = 24.

Detected share of planted mirrors by host size n (rows) and pairs k (columns), and of planted repetition:

| n | k=2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | repetition |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 8 | 0.06 | 0.15 | 0.27 | - | - | - | - | - | - | - | - | 0.43 |
| 12 | 0.06 | 0.18 | 0.28 | 0.36 | 0.68 | - | - | - | - | - | - | 0.23 |
| 16 | 0.03 | 0.11 | 0.14 | 0.32 | 0.53 | 0.86 | 0.95 | - | - | - | - | 0.11 |
| 24 | 0.04 | 0.16 | 0.16 | 0.34 | 0.63 | 0.88 | 0.93 | 0.98 | 1.00 | 0.99 | 1.00 | 0.04 |

Planted parallels detected (a false alarm):

| n | k | detected |
|---|---|---|
| 8 | 2 | 0.00 |
| 8 | 3 | 0.00 |
| 8 | 4 | 0.00 |
| 12 | 2 | 0.01 |
| 12 | 3 | 0.01 |
| 12 | 4 | 0.00 |
| 12 | 5 | 0.00 |
| 12 | 6 | 0.00 |
| 16 | 2 | 0.04 |
| 16 | 3 | 0.03 |
| 16 | 4 | 0.00 |
| 16 | 5 | 0.00 |
| 16 | 6 | 0.00 |
| 16 | 7 | 0.00 |
| 16 | 8 | 0.00 |
| 24 | 2 | 0.01 |
| 24 | 3 | 0.00 |
| 24 | 4 | 0.00 |
| 24 | 5 | 0.00 |
| 24 | 6 | 0.00 |
| 24 | 7 | 0.00 |
| 24 | 8 | 0.00 |
| 24 | 9 | 0.00 |
| 24 | 10 | 0.00 |
| 24 | 11 | 0.00 |
| 24 | 12 | 0.00 |

**B2 at (k, n) = (12, 24): power 1.00; passes. B3 there: parallels 0.00, repetition 0.04; passes.**

#### Greek

k* = 12, n* = 24.

Detected share of planted mirrors by host size n (rows) and pairs k (columns), and of planted repetition:

| n | k=2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | repetition |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 8 | 0.00 | 0.03 | 0.04 | - | - | - | - | - | - | - | - | 0.16 |
| 12 | 0.00 | 0.01 | 0.03 | 0.10 | 0.14 | - | - | - | - | - | - | 0.09 |
| 16 | 0.00 | 0.01 | 0.02 | 0.05 | 0.24 | 0.44 | 0.63 | - | - | - | - | 0.09 |
| 24 | 0.02 | 0.03 | 0.06 | 0.06 | 0.18 | 0.44 | 0.65 | 0.74 | 0.81 | 0.90 | 0.92 | 0.00 |

Planted parallels detected (a false alarm):

| n | k | detected |
|---|---|---|
| 8 | 2 | 0.00 |
| 8 | 3 | 0.00 |
| 8 | 4 | 0.00 |
| 12 | 2 | 0.02 |
| 12 | 3 | 0.00 |
| 12 | 4 | 0.00 |
| 12 | 5 | 0.00 |
| 12 | 6 | 0.00 |
| 16 | 2 | 0.00 |
| 16 | 3 | 0.00 |
| 16 | 4 | 0.00 |
| 16 | 5 | 0.00 |
| 16 | 6 | 0.00 |
| 16 | 7 | 0.00 |
| 16 | 8 | 0.00 |
| 24 | 2 | 0.01 |
| 24 | 3 | 0.00 |
| 24 | 4 | 0.00 |
| 24 | 5 | 0.00 |
| 24 | 6 | 0.00 |
| 24 | 7 | 0.00 |
| 24 | 8 | 0.00 |
| 24 | 9 | 0.00 |
| 24 | 10 | 0.00 |
| 24 | 11 | 0.00 |
| 24 | 12 | 0.00 |

**B2 at (k, n) = (12, 24): power 0.92; passes. B3 there: parallels 0.00, repetition 0.00; passes.**

### 6a's power check

5% of each group's eligible windows re-planted from their order to mirror order, 200 plants (seed 20261026); detected at p < 0.01.

| Group | Power | 6a reading |
|---|---|---|
| Hebrew poetry | 0.00 | underpowered |
| The prophets | 0.00 | underpowered |
| Hebrew narrative | 0.00 | underpowered |
| Greek New Testament | 0.00 | underpowered |

### The bar

B1 passes, B3 passes, B4 passes. B2: Hebrew prose passes, Hebrew poetry passes, Greek passes. The method is validated: the targets, 6a and the scan are run.

### 6b: the named targets

One Holm family of four tests at alpha = 0.05 (T3 and T5 dropped before the run; see the amendments).

| Target | Extent and centre | T | p | Holm p | Reading |
|---|---|---|---|---|---|
| T1 | The flood, Gen 6:10-9:19, centred on 8:1a | 0.055 | 0.0012 | 0.0049 | mirror order exceeds parallel order and the permutation null at Holm-adjusted p = 0.0049 |
| T2a | Babel, Gen 11:1-9, centred on 11:5a | -0.186 | 0.8742 | 1.0000 | mirror order does not exceed parallel order and the permutation null at Holm-adjusted p = 1.0000 |
| T2b | Babel, Gen 11:1-9, centred on 11:6 | -0.078 | 0.6852 | 1.0000 | mirror order does not exceed parallel order and the permutation null at Holm-adjusted p = 1.0000 |
| T4 | The Johannine prologue, John 1:1-18, centred on 1:12b | 0.006 | 0.4826 | 1.0000 | mirror order does not exceed parallel order and the permutation null at Holm-adjusted p = 1.0000 |

#### T1 The flood, Gen 6:10-9:19, centred on 8:1a

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Gen 8:1 w1 to Gen 8:1 w13 | 152 | 77 | 16608070.67 | 14870252.61 | 0.055 | 8088.92 | 0.0012 | sampled, B = 99999, 122 as high | 1.00e-9 | 0.0014 (sampled, B = 99999, 134 as high) |

Matched pairs at the published centre (the unit Gen 8:1 w1 to Gen 8:1 w13), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Gen 7:24 w5-w7 | Gen 8:3 w7-w12 | H3117 | יוֹם | day | 2.49 |  |
| Gen 7:24 w5-w7 | Gen 8:3 w7-w12 | H3967 | מֵאָה | hundred | 3.82 | tied |
| Gen 7:24 w5-w7 | Gen 8:3 w7-w12 | H2572 | חֲמִשִּׁים | fifty | 5.11 | tied |
| Gen 7:24 w5-w7 | Gen 8:4 w1-w8 | H3117 | יוֹם | day | 2.49 | tied |
| Gen 7:24 w5-w7 | Gen 8:6 w1-w4 | H3117 | יוֹם | day | 2.49 | tied |
| Gen 7:24 w5-w7 | Gen 8:10 w1-w5 | H3117 | יוֹם | day | 2.49 | tied |
| Gen 7:24 w5-w7 | Gen 8:12 w1-w5 | H3117 | יוֹם | day | 2.49 | tied |
| Gen 7:24 w5-w7 | Gen 8:13 w1-w12 | H3967 | מֵאָה | hundred | 3.82 | tied |
| Gen 7:24 w5-w7 | Gen 8:14 w1-w6 | H3117 | יוֹם | day | 2.49 | tied |
| Gen 7:24 w5-w7 | Gen 8:22 w1-w4 | H3117 | יוֹם | day | 2.49 | tied |
| Gen 7:24 w5-w7 | Gen 8:22 w5-w14 | H3117 | יוֹם | day | 2.49 | tied |
| Gen 7:24 w1-w4 | Gen 8:1 w14-w20 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | parallel |
| Gen 7:24 w1-w4 | Gen 8:1 w14-w20 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 8:1 w14-w20 | H4325 | מַי | water | 3.79 | tied |
| Gen 7:24 w1-w4 | Gen 8:3 w1-w6 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 8:3 w1-w6 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 8:3 w1-w6 | H4325 | מַי | water | 3.79 | tied |
| Gen 7:24 w1-w4 | Gen 8:3 w7-w12 | H4325 | מַי | water | 3.79 | tied |
| Gen 7:24 w1-w4 | Gen 8:4 w9-w11 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 8:5 w1-w7 | H4325 | מַי | water | 3.79 | tied |
| Gen 7:24 w1-w4 | Gen 8:7 w4-w11 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 8:7 w4-w11 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 8:7 w4-w11 | H4325 | מַי | water | 3.79 | tied |
| Gen 7:24 w1-w4 | Gen 8:8 w5-w10 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 8:8 w5-w10 | H4325 | מַי | water | 3.79 | tied |
| Gen 7:24 w1-w4 | Gen 8:9 w1-w16 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 8:9 w1-w16 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 8:9 w1-w16 | H4325 | מַי | water | 3.79 | tied |
| Gen 7:24 w1-w4 | Gen 8:11 w11-w17 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 8:11 w11-w17 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 8:11 w11-w17 | H4325 | מַי | water | 3.79 | tied |
| Gen 7:24 w1-w4 | Gen 8:13 w1-w12 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 8:13 w1-w12 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 8:13 w1-w12 | H4325 | מַי | water | 3.79 | tied |
| Gen 7:24 w1-w4 | Gen 8:14 w7-w8 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 8:17 w1-w15 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 8:17 w1-w15 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 8:17 w16-w21 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 8:17 w16-w21 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 8:19 w1-w10 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 8:19 w1-w10 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 8:22 w1-w4 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 9:1 w7-w13 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 9:2 w1-w11 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 9:2 w1-w11 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 9:7 w4-w7 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 9:10 w1-w12 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 9:10 w13-w18 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 9:11 w1-w11 | H4325 | מַי | water | 3.79 | tied |
| Gen 7:24 w1-w4 | Gen 9:11 w12-w17 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 9:13 w5-w10 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 9:14 w1-w5 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 9:14 w1-w5 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 9:15 w13-w20 | H4325 | מַי | water | 3.79 | tied |
| Gen 7:24 w1-w4 | Gen 9:16 w4-w18 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 9:16 w4-w18 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 9:17 w5-w16 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:24 w1-w4 | Gen 9:17 w5-w16 | H5921 | עַל | upon | 1.64 | tied |
| Gen 7:24 w1-w4 | Gen 9:19 w5-w8 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 7:23 w20-w25 | Gen 8:4 w1-w8 | H8392 | תֵּבָה | ark | 6.84 | parallel |

The proposer's pairs (display only; never scored) against the keys the detector matched between those verses:

| Proposer's pair | Keys matched there |
|---|---|
| 7 days (7:4, 7:10 / 8:10, 8:12) | H0776, H5921, H4325, H3117, H7651, H5146, H8392, H0413, H0935, H4480, H5750, H3588 |
| 40 days (7:17 / 8:6) | H8392, H1961, H3117, H0705 |
| 150 days (7:24 / 8:3) | H3117, H3967, H2572, H0776, H5921, H4325 |
| into the ark / out of the ark (7:7-16 / 8:15-19) | H0430, H0834, H3605, H1320, H2416, H0413, H5146, H8392, H5775, H0776, H5921, H7430, H0929, H7431, H0802, H1121, H0854, H4480 |

Under each switch:

| Switch | T | p |
|---|---|---|
| v1u (uStrong keys) | 0.054 | 0.0014 |
| Hebrew wide stop list | 0.053 | 0.0029 |
| weights 1 | 0.049 | 6.50e-4 |
| Greek verse units | 0.055 | 0.0012 |
| Hebrew level-2 units | 0.028 | 0.0218 |

#### T2a Babel, Gen 11:1-9, centred on 11:5a

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Gen 11:5 w1 to Gen 11:5 w7 | 18 | 16 | 2993.94 | 4359.85 | -0.186 | 144.63 | 0.8742 | sampled, B = 99999, 87424 as high | 3.83e-9 | 0.8944 (sampled, B = 99999, 89438 as high) |

Matched pairs at the published centre (the unit Gen 11:5 w1 to Gen 11:5 w7), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Gen 11:4 w12-w17 | Gen 11:6 w1-w11 | H3605 | כֹּל | all | 1.70 |  |
| Gen 11:4 w12-w17 | Gen 11:6 w12-w19 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:4 w12-w17 | Gen 11:8 w1-w8 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:4 w12-w17 | Gen 11:8 w1-w8 | H5921 | עַל | upon | 1.64 | tied |
| Gen 11:4 w12-w17 | Gen 11:8 w1-w8 | H6440 | פָּנֶה | before | 2.51 | tied |
| Gen 11:4 w12-w17 | Gen 11:8 w1-w8 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:4 w12-w17 | Gen 11:8 w1-w8 | H6327 | פּוּץ | to scatter | 5.86 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w1-w12 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w1-w12 | H5921 | עַל | upon | 1.64 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w1-w12 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w13-w19 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w13-w19 | H5921 | עַל | upon | 1.64 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w13-w19 | H6440 | פָּנֶה | before | 2.51 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w13-w19 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w13-w19 | H6327 | פּוּץ | to scatter | 5.86 | tied |
| Gen 11:4 w1-w11 | Gen 11:5 w8-w11 | H1129 | בָּנָה | to build | 4.21 | parallel |
| Gen 11:4 w1-w11 | Gen 11:6 w1-w11 | H0559 | אָמַר | to say | 1.68 | tied |
| Gen 11:4 w1-w11 | Gen 11:6 w1-w11 | H6213 | עָשָׂה | do | 2.32 | tied |
| Gen 11:4 w1-w11 | Gen 11:6 w12-w19 | H6213 | עָשָׂה | do | 2.32 | tied |
| Gen 11:4 w1-w11 | Gen 11:7 w1-w5 | H3051 | יָהַב | to give | 6.69 | tied |
| Gen 11:4 w1-w11 | Gen 11:8 w9-w11 | H1129 | בָּנָה | to build | 4.21 | tied |
| Gen 11:4 w1-w11 | Gen 11:8 w9-w11 | H5892 | עִיר | city | 3.22 | tied |
| Gen 11:4 w1-w11 | Gen 11:9 w1-w12 | H8034 | שֵׁם | name | 3.41 | tied |
| Gen 11:3 w1-w9 | Gen 11:6 w1-w11 | H0559 | אָמַר | to say | 1.68 | parallel |
| Gen 11:3 w1-w9 | Gen 11:7 w1-w5 | H3051 | יָהַב | to give | 6.69 | tied |
| Gen 11:3 w1-w9 | Gen 11:7 w6-w11 | H0376 | אִישׁ | man | 2.79 | tied |
| Gen 11:3 w1-w9 | Gen 11:7 w6-w11 | H7453 | רֵעַ | neighbor | 4.90 | tied |
| Gen 11:2 w4-w9 | Gen 11:7 w1-w5 | H8033 | שָׁם | there | 3.46 | parallel |
| Gen 11:2 w4-w9 | Gen 11:8 w1-w8 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:2 w4-w9 | Gen 11:8 w1-w8 | H8033 | שָׁם | there | 3.46 | tied |
| Gen 11:2 w4-w9 | Gen 11:9 w1-w12 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:2 w4-w9 | Gen 11:9 w1-w12 | H8033 | שָׁם | there | 3.46 | tied |
| Gen 11:2 w4-w9 | Gen 11:9 w13-w19 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:2 w4-w9 | Gen 11:9 w13-w19 | H8033 | שָׁם | there | 3.46 | tied |
| Gen 11:1 w6-w7 | Gen 11:6 w1-w11 | H0259 | אֶחָד | one | 3.45 | parallel |
| Gen 11:1 w1-w5 | Gen 11:6 w1-w11 | H0259 | אֶחָד | one | 3.45 | tied |
| Gen 11:1 w1-w5 | Gen 11:6 w1-w11 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:1 w1-w5 | Gen 11:6 w1-w11 | H8193 | שָׂפָה | lips | 4.95 | tied |
| Gen 11:1 w1-w5 | Gen 11:6 w12-w19 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:1 w1-w5 | Gen 11:7 w1-w5 | H8193 | שָׂפָה | lips | 4.95 | tied |
| Gen 11:1 w1-w5 | Gen 11:7 w6-w11 | H8193 | שָׂפָה | lips | 4.95 | tied |
| Gen 11:1 w1-w5 | Gen 11:8 w1-w8 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:1 w1-w5 | Gen 11:8 w1-w8 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:1 w1-w5 | Gen 11:9 w1-w12 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:1 w1-w5 | Gen 11:9 w1-w12 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:1 w1-w5 | Gen 11:9 w1-w12 | H8193 | שָׂפָה | lips | 4.95 | tied |
| Gen 11:1 w1-w5 | Gen 11:9 w13-w19 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:1 w1-w5 | Gen 11:9 w13-w19 | H3605 | כֹּל | all | 1.70 | tied |

The proposer's pairs (display only; never scored) against the keys the detector matched between those verses:

| Proposer's pair | Keys matched there |
|---|---|
| one language (1 / 9) | H0776, H3605, H8193 |
| there (2 / 8) | H0776, H8033 |
| one another; come, let us (3 / 7) | H3051, H0376, H7453 |
| build; city and tower (4 / 5b) | H1129 |

Under each switch:

| Switch | T | p |
|---|---|---|
| v1u (uStrong keys) | -0.190 | 0.8792 |
| Hebrew wide stop list | -0.152 | 0.8292 |
| weights 1 | -0.149 | 0.8616 |
| Greek verse units | -0.186 | 0.8742 |
| Hebrew level-2 units | -0.065 | 0.6921 |

#### T2b Babel, Gen 11:1-9, centred on 11:6

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the units of 11:6-11:6 | 17 | 16 | 2811.08 | 3285.48 | -0.078 | 131.37 | 0.6852 | sampled, B = 99999, 68522 as high | 2.76e-7 | 0.6640 (sampled, B = 99999, 66400 as high) |

Matched pairs at the published centre (the units of 11:6-11:6), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Gen 11:5 w8-w11 | Gen 11:7 w6-w11 | H0834 | אֲשֶׁר | which | 1.66 |  |
| Gen 11:5 w8-w11 | Gen 11:8 w9-w11 | H1129 | בָּנָה | to build | 4.21 | tied |
| Gen 11:5 w1-w7 | Gen 11:7 w1-w5 | H3381 | יָרַד | to go down | 4.21 | parallel |
| Gen 11:5 w1-w7 | Gen 11:8 w1-w8 | H3068 | יהוה | LORD | 1.44 | tied |
| Gen 11:5 w1-w7 | Gen 11:8 w9-w11 | H5892 | עִיר | city | 3.22 | tied |
| Gen 11:5 w1-w7 | Gen 11:9 w1-w12 | H3068 | יהוה | LORD | 1.44 | tied |
| Gen 11:5 w1-w7 | Gen 11:9 w13-w19 | H3068 | יהוה | LORD | 1.44 | tied |
| Gen 11:4 w12-w17 | Gen 11:8 w1-w8 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | parallel |
| Gen 11:4 w12-w17 | Gen 11:8 w1-w8 | H5921 | עַל | upon | 1.64 | tied |
| Gen 11:4 w12-w17 | Gen 11:8 w1-w8 | H6440 | פָּנֶה | before | 2.51 | tied |
| Gen 11:4 w12-w17 | Gen 11:8 w1-w8 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:4 w12-w17 | Gen 11:8 w1-w8 | H6327 | פּוּץ | to scatter | 5.86 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w1-w12 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w1-w12 | H5921 | עַל | upon | 1.64 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w1-w12 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w13-w19 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w13-w19 | H5921 | עַל | upon | 1.64 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w13-w19 | H6440 | פָּנֶה | before | 2.51 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w13-w19 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:4 w12-w17 | Gen 11:9 w13-w19 | H6327 | פּוּץ | to scatter | 5.86 | tied |
| Gen 11:4 w1-w11 | Gen 11:7 w1-w5 | H3051 | יָהַב | to give | 6.69 | parallel |
| Gen 11:4 w1-w11 | Gen 11:8 w9-w11 | H1129 | בָּנָה | to build | 4.21 | tied |
| Gen 11:4 w1-w11 | Gen 11:8 w9-w11 | H5892 | עִיר | city | 3.22 | tied |
| Gen 11:4 w1-w11 | Gen 11:9 w1-w12 | H8034 | שֵׁם | name | 3.41 | tied |
| Gen 11:3 w1-w9 | Gen 11:7 w1-w5 | H3051 | יָהַב | to give | 6.69 | parallel |
| Gen 11:3 w1-w9 | Gen 11:7 w6-w11 | H0376 | אִישׁ | man | 2.79 | tied |
| Gen 11:3 w1-w9 | Gen 11:7 w6-w11 | H7453 | רֵעַ | neighbor | 4.90 | tied |
| Gen 11:2 w4-w9 | Gen 11:7 w1-w5 | H8033 | שָׁם | there | 3.46 | parallel |
| Gen 11:2 w4-w9 | Gen 11:8 w1-w8 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:2 w4-w9 | Gen 11:8 w1-w8 | H8033 | שָׁם | there | 3.46 | tied |
| Gen 11:2 w4-w9 | Gen 11:9 w1-w12 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:2 w4-w9 | Gen 11:9 w1-w12 | H8033 | שָׁם | there | 3.46 | tied |
| Gen 11:2 w4-w9 | Gen 11:9 w13-w19 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:2 w4-w9 | Gen 11:9 w13-w19 | H8033 | שָׁם | there | 3.46 | tied |
| Gen 11:1 w1-w5 | Gen 11:7 w1-w5 | H8193 | שָׂפָה | lips | 4.95 | parallel |
| Gen 11:1 w1-w5 | Gen 11:7 w6-w11 | H8193 | שָׂפָה | lips | 4.95 | tied |
| Gen 11:1 w1-w5 | Gen 11:8 w1-w8 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:1 w1-w5 | Gen 11:8 w1-w8 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:1 w1-w5 | Gen 11:9 w1-w12 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:1 w1-w5 | Gen 11:9 w1-w12 | H3605 | כֹּל | all | 1.70 | tied |
| Gen 11:1 w1-w5 | Gen 11:9 w1-w12 | H8193 | שָׂפָה | lips | 4.95 | tied |
| Gen 11:1 w1-w5 | Gen 11:9 w13-w19 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Gen 11:1 w1-w5 | Gen 11:9 w13-w19 | H3605 | כֹּל | all | 1.70 | tied |

Under each switch:

| Switch | T | p |
|---|---|---|
| v1u (uStrong keys) | -0.074 | 0.6765 |
| Hebrew wide stop list | -0.059 | 0.6430 |
| weights 1 | -0.026 | 0.5821 |
| Greek verse units | -0.078 | 0.6852 |
| Hebrew level-2 units | -0.007 | 0.5178 |

#### T4 The Johannine prologue, John 1:1-18, centred on 1:12b

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit John 1:12 w5 to John 1:12 w10 | 40 | 9 | 1854.83 | 1832.37 | 0.006 | 95.28 | 0.4826 | sampled, B = 99999, 48262 as high | 1.00e-9 | 0.4805 (sampled, B = 99999, 48045 as high) |

Matched pairs at the published centre (the unit John 1:12 w5 to John 1:12 w10), from the centre outward:

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| John 1:12 w1-w4 | John 1:16 w1-w12 | G2983 | λαμβάνω | to take | 3.48 |  |
| John 1:11 w1-w4 | John 1:15 w12-w18 | G2064 | ἔρχομαι | to come/go | 2.59 | parallel |
| John 1:10 w5-w10 | John 1:14 w1-w9 | G1096 | γίνομαι | to be | 2.54 | parallel |
| John 1:10 w5-w10 | John 1:15 w12-w18 | G1096 | γίνομαι | to be | 2.54 | tied |
| John 1:10 w5-w10 | John 1:17 w7-w15 | G1096 | γίνομαι | to be | 2.54 | tied |
| John 1:9 w1-w13 | John 1:15 w12-w18 | G2064 | ἔρχομαι | to come/go | 2.59 | parallel |
| John 1:8 w6-w11 | John 1:15 w1-w7 | G3140 | μαρτυρέω | to testify | 4.71 | parallel |
| John 1:7 w10-w14 | John 1:12 w11-w16 | G4100 | πιστεύω | to trust (in) | 3.60 | parallel |
| John 1:7 w1-w9 | John 1:15 w1-w7 | G3140 | μαρτυρέω | to testify | 4.71 | mirror |
| John 1:7 w1-w9 | John 1:15 w12-w18 | G2064 | ἔρχομαι | to come/go | 2.59 | tied |
| John 1:6 w6-w8 | John 1:12 w11-w16 | G3686 | ὄνομα | name | 3.62 | parallel |
| John 1:6 w6-w8 | John 1:15 w1-w7 | G2491 | Ἰωάννης | John | 4.11 | tied |
| John 1:6 w1-w5 | John 1:13 w1-w16 | G2316 | θεός | God | 1.93 | parallel |
| John 1:6 w1-w5 | John 1:14 w1-w9 | G1096 | γίνομαι | to be | 2.54 | tied |
| John 1:6 w1-w5 | John 1:15 w12-w18 | G1096 | γίνομαι | to be | 2.54 | tied |
| John 1:6 w1-w5 | John 1:17 w7-w15 | G1096 | γίνομαι | to be | 2.54 | tied |
| John 1:6 w1-w5 | John 1:18 w1-w4 | G2316 | θεός | God | 1.93 | tied |
| John 1:6 w1-w5 | John 1:18 w6-w14 | G2316 | θεός | God | 1.93 | tied |
| John 1:3 w5-w12 | John 1:14 w1-w9 | G1096 | γίνομαι | to be | 2.54 | parallel |
| John 1:3 w5-w12 | John 1:15 w12-w18 | G1096 | γίνομαι | to be | 2.54 | tied |
| John 1:3 w5-w12 | John 1:17 w7-w15 | G1096 | γίνομαι | to be | 2.54 | tied |
| John 1:3 w1-w4 | John 1:14 w1-w9 | G1096 | γίνομαι | to be | 2.54 | parallel |
| John 1:3 w1-w4 | John 1:15 w12-w18 | G1096 | γίνομαι | to be | 2.54 | tied |
| John 1:3 w1-w4 | John 1:17 w7-w15 | G1096 | γίνομαι | to be | 2.54 | tied |
| John 1:2 w1-w7 | John 1:13 w1-w16 | G2316 | θεός | God | 1.93 | parallel |
| John 1:2 w1-w7 | John 1:18 w1-w4 | G2316 | θεός | God | 1.93 | tied |
| John 1:2 w1-w7 | John 1:18 w6-w14 | G2316 | θεός | God | 1.93 | tied |
| John 1:1 w13-w17 | John 1:13 w1-w16 | G2316 | θεός | God | 1.93 | parallel |
| John 1:1 w13-w17 | John 1:14 w1-w9 | G3056 | λόγος | word | 3.22 | tied |
| John 1:1 w13-w17 | John 1:18 w1-w4 | G2316 | θεός | God | 1.93 | tied |
| John 1:1 w13-w17 | John 1:18 w6-w14 | G2316 | θεός | God | 1.93 | tied |
| John 1:1 w6-w12 | John 1:13 w1-w16 | G2316 | θεός | God | 1.93 | parallel |
| John 1:1 w6-w12 | John 1:14 w1-w9 | G3056 | λόγος | word | 3.22 | tied |
| John 1:1 w6-w12 | John 1:18 w1-w4 | G2316 | θεός | God | 1.93 | tied |
| John 1:1 w6-w12 | John 1:18 w6-w14 | G2316 | θεός | God | 1.93 | tied |
| John 1:1 w1-w5 | John 1:14 w1-w9 | G3056 | λόγος | word | 3.22 | parallel |

The proposer's pairs (display only; never scored) against the keys the detector matched between those verses:

| Proposer's pair | Keys matched there |
|---|---|
| the Word with God (1-2 / 18) | G2316 |
| what came through the Word (3 / 17) | G1096 |
| what we received (4-5 / 16) | none |
| John's witness (6-8 / 15) | G3140, G2064, G2491, G1096 |
| the coming of the light; incarnation (9-10 / 14) | G1096 |
| his own (11 / 13) | none |

Flag: the Greek units are editorial (TAGNT's punctuation follows the Tyndale House GNT).

Under each switch:

| Switch | T | p |
|---|---|---|
| v1u (uStrong keys) | 0.006 | 0.4826 |
| Hebrew wide stop list | 0.006 | 0.4826 |
| weights 1 | 0.064 | 0.2812 |
| Greek verse units | -0.112 | 0.7372 |
| Hebrew level-2 units | 0.006 | 0.4826 |

### 6a: mirror order within a verse or clause pair

Mean T over each group's eligible windows (a Hebrew verse at each level-1 divider, a Greek clause pair with at least one untied pair of matches), against one shared within-unit shuffle per draw (B = 9,999, seed 20261023), one-sided. For a poetic verse with both level-1 dividers the shuffle is finer than either window's sides, a stricter null than the per-window one.

| Group | Windows | Eligible | Mean T | p | Reading |
|---|---|---|---|---|---|
| Hebrew poetry | all | 129 | -0.6432 | 1.0000 | underpowered (power 0.00) |
| Hebrew poetry | verb pairs | 2 | -0.5000 | 1.0000 | descriptive |
| Hebrew poetry | noun pairs | 22 | -0.6708 | 0.9994 | descriptive |
| Hebrew poetry | mixed | 105 | -0.6402 | 1.0000 | descriptive |
| The prophets | all | 858 | -0.3420 | 1.0000 | underpowered (power 0.00) |
| The prophets | verb pairs | 36 | -0.2722 | 0.9573 | descriptive |
| The prophets | noun pairs | 167 | -0.4221 | 1.0000 | descriptive |
| The prophets | mixed | 655 | -0.3254 | 1.0000 | descriptive |
| Hebrew narrative | all | 2183 | -0.3484 | 1.0000 | underpowered (power 0.00) |
| Hebrew narrative | verb pairs | 59 | -0.5520 | 1.0000 | descriptive |
| Hebrew narrative | noun pairs | 577 | -0.3563 | 1.0000 | descriptive |
| Hebrew narrative | mixed | 1547 | -0.3376 | 1.0000 | descriptive |
| Greek New Testament | all | 377 | -0.1721 | 1.0000 | underpowered (power 0.00) |
| Greek New Testament | verb pairs | 28 | -0.3623 | 0.9843 | descriptive |
| Greek New Testament | noun pairs | 91 | -0.0962 | 0.8485 | descriptive |
| Greek New Testament | mixed | 258 | -0.1782 | 0.9995 | descriptive |

Verb pairs are windows whose matched tokens are all verbs; Hebrew verb movement between lines makes mirror order by grammar alone, and this test cannot separate grammar from rhetoric.

Poetry minus narrative, mean T: -0.2948, 95% bootstrap interval -0.4135 to -0.1684 (1,000 resamples of verses, seed 20261024).

Under each switch that applies (descriptive):

| Switch | Group | Mean T | p |
|---|---|---|---|
| v1u (uStrong keys) | Hebrew poetry | -0.5824 | 1.0000 |
| v1u (uStrong keys) | The prophets | -0.3204 | 1.0000 |
| v1u (uStrong keys) | Hebrew narrative | -0.3340 | 1.0000 |
| Hebrew wide stop list | Hebrew poetry | -0.5911 | 1.0000 |
| Hebrew wide stop list | The prophets | -0.3269 | 1.0000 |
| Hebrew wide stop list | Hebrew narrative | -0.3663 | 1.0000 |
| weights 1 | Hebrew poetry | -0.6377 | 1.0000 |
| weights 1 | The prophets | -0.3399 | 1.0000 |
| weights 1 | Hebrew narrative | -0.3479 | 1.0000 |
| weights 1 | Greek New Testament | -0.1744 | 1.0000 |
| Greek verse units | Greek New Testament | -0.2882 | 1.0000 |

### 6c: the exploratory scan (opened)

#### Hebrew OT (level-1 units)

Screened m = 318830, Tarone K = 318830. Windows with BH q <= 0.10: 3158; with Benjamini-Yekutieli q <= 0.10: 18. Sealed file `chiasm-sealed-hebrew-units.tsv` (sha256 `9dcfcc4f1d73f7b7`).

##### 1. Lev 21:19 w8 to Lev 22:5 w16 (n = 20, centre before Lev 21:24 w7)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Lev 21:24 w7 | 20 | 19 | 16761.20 | 3588.72 | 0.647 | 233.74 | 1.30e-8 | sampled, B = 1000000000, 12 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0022, q (BY) 0.0285: mirror order exceeds parallel order and the permutation null at q = 0.0022. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 21:24 w1-w6 | Lev 21:24 w7-w10 | H0413 | אֶל | to(wards) | 1.71 |  |
| Lev 21:24 w1-w6 | Lev 21:24 w7-w10 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H4872 | מֹשֶׁה | Moses | 3.50 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H0175 | אַהֲרֹן | Aaron | 4.26 | tied |
| Lev 21:24 w1-w6 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:3 w1-w18 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:4 w1-w14 | H0175 | אַהֲרֹן | Aaron | 4.26 | tied |
| Lev 21:23 w13-w20 | Lev 22:1 w1-w5 | H3068 | יהוה | LORD | 1.44 | parallel |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H2490 | חָלַל | profane | 5.16 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w1-w12 | Lev 21:24 w7-w10 | H0413 | אֶל | to(wards) | 1.71 | parallel |
| Lev 21:23 w1-w12 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w1-w12 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:22 w5-w7 | Lev 22:2 w1-w14 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | parallel |

##### 2. Lev 21:19 w1 to Lev 22:6 w7 (n = 22, centre before Lev 21:24 w7)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Lev 21:24 w7 | 22 | 19 | 23505.58 | 5660.95 | 0.612 | 276.85 | 1.70e-8 | sampled, B = 1000000000, 16 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0022, q (BY) 0.0285: mirror order exceeds parallel order and the permutation null at q = 0.0022. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 21:24 w1-w6 | Lev 21:24 w7-w10 | H0413 | אֶל | to(wards) | 1.71 |  |
| Lev 21:24 w1-w6 | Lev 21:24 w7-w10 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H4872 | מֹשֶׁה | Moses | 3.50 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H0175 | אַהֲרֹן | Aaron | 4.26 | tied |
| Lev 21:24 w1-w6 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:3 w1-w18 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:4 w1-w14 | H0175 | אַהֲרֹן | Aaron | 4.26 | tied |
| Lev 21:23 w13-w20 | Lev 22:1 w1-w5 | H3068 | יהוה | LORD | 1.44 | parallel |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H2490 | חָלַל | profane | 5.16 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w1-w12 | Lev 21:24 w7-w10 | H0413 | אֶל | to(wards) | 1.71 | parallel |
| Lev 21:23 w1-w12 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w1-w12 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:22 w5-w7 | Lev 22:2 w1-w14 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | parallel |

##### 3. Lev 21:19 w8 to Lev 22:6 w7 (n = 21, centre the unit Lev 21:24 w7)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Lev 21:24 w7 | 21 | 19 | 15857.43 | 3401.07 | 0.647 | 228.43 | 2.60e-8 | sampled, B = 1000000000, 25 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0022, q (BY) 0.0285: mirror order exceeds parallel order and the permutation null at q = 0.0022. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 |  |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H4872 | מֹשֶׁה | Moses | 3.50 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H0175 | אַהֲרֹן | Aaron | 4.26 | tied |
| Lev 21:24 w1-w6 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:3 w1-w18 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:4 w1-w14 | H0175 | אַהֲרֹן | Aaron | 4.26 | tied |
| Lev 21:23 w13-w20 | Lev 22:1 w1-w5 | H3068 | יהוה | LORD | 1.44 | parallel |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H2490 | חָלַל | profane | 5.16 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w1-w12 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 | parallel |
| Lev 21:23 w1-w12 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w1-w12 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:22 w5-w7 | Lev 22:2 w1-w14 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | parallel |
| Lev 21:22 w5-w7 | Lev 22:3 w1-w18 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | tied |
| Lev 21:22 w5-w7 | Lev 22:4 w1-w14 | H0398 | אָכַל | to eat | 3.50 | tied |
| Lev 21:22 w5-w7 | Lev 22:4 w1-w14 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | tied |

##### 4. Ezek 47:21 w1 to Ezek 48:12 w7 (n = 22, centre before Ezek 48:6 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Ezek 48:6 w1 | 22 | 16 | 96162.33 | 51495.14 | 0.303 | 653.91 | 2.70e-8 | sampled, B = 1000000000, 26 as high | 1.00e-9 | 0.0017 (sampled, B = 99999, 171 as high) |

q (BH) 0.0022, q (BY) 0.0285: mirror order exceeds parallel order and the permutation null at q = 0.0022. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H5921 | עַל | upon | 1.64 |  |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H0669 | אֶפְרַ֫יִם | Ephraim | 4.95 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H5921 | עַל | upon | 1.64 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H5921 | עַל | upon | 1.64 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w9-w27 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w9-w27 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w9-w27 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w9-w27 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w9-w27 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:10 w1-w22 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:10 w1-w22 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:6 w1-w10 | H5921 | עַל | upon | 1.64 | parallel |
| Ezek 48:4 w1-w10 | Ezek 48:6 w1-w10 | H0259 | אֶחָד | one | 3.45 | tied |

##### 5. Lev 24:15 w1 to Lev 25:1 w7 (n = 19, centre the unit Lev 24:19 w6)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Lev 24:19 w6 | 19 | 20 | 4845.83 | 428.77 | 0.837 | 115.26 | 9.70e-8 | sampled, B = 1000000000, 96 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0047, q (BY) 0.0627: mirror order exceeds parallel order and the permutation null at q = 0.0047. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 24:19 w1-w5 | Lev 24:20 w10-w16 | H5414 | נָתַן | give | 2.55 |  |
| Lev 24:19 w1-w5 | Lev 24:20 w10-w16 | H3971 | מוּם | blemish | 7.11 | tied |
| Lev 24:19 w1-w5 | Lev 24:22 w8-w11 | H3588 | כִּי | for | 1.78 | tied |
| Lev 24:18 w5-w7 | Lev 24:20 w1-w9 | H8478 | תַּחַת | under | 3.95 | parallel |
| Lev 24:18 w1-w4 | Lev 24:21 w1-w3 | H0929 | בְּהֵמָה | animal | 4.91 | mirror |
| Lev 24:18 w1-w4 | Lev 24:21 w1-w3 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:18 w1-w4 | Lev 24:21 w1-w3 | H7999 | שָׁלֵם | to complete | 5.38 | tied |
| Lev 24:18 w1-w4 | Lev 24:21 w4-w6 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:17 w7-w8 | Lev 24:21 w4-w6 | H4191 | מוּת | to die | 3.50 | tied |
| Lev 24:17 w1-w6 | Lev 24:20 w10-w16 | H0120 | אָדָם | man | 3.79 | parallel |
| Lev 24:17 w1-w6 | Lev 24:21 w1-w3 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:17 w1-w6 | Lev 24:21 w4-w6 | H0120 | אָדָם | man | 3.79 | tied |
| Lev 24:17 w1-w6 | Lev 24:21 w4-w6 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:17 w1-w6 | Lev 24:22 w8-w11 | H3588 | כִּי | for | 1.78 | tied |
| Lev 24:16 w11-w15 | Lev 24:21 w4-w6 | H4191 | מוּת | to die | 3.50 | parallel |
| Lev 24:16 w11-w15 | Lev 24:22 w1-w7 | H1616 | גֵּר | sojourner | 5.64 | tied |
| Lev 24:16 w11-w15 | Lev 24:22 w1-w7 | H0249 | אֶזְרָח | born | 7.22 | tied |
| Lev 24:16 w1-w10 | Lev 24:21 w4-w6 | H4191 | מוּת | to die | 3.50 | parallel |
| Lev 24:16 w1-w10 | Lev 24:22 w8-w11 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 24:16 w1-w10 | Lev 24:23 w1-w14 | H7275 | רָגַם | to stone | 7.35 | tied |
| Lev 24:16 w1-w10 | Lev 24:23 w15-w22 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 24:16 w1-w10 | Lev 25:1 w1-w7 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 24:15 w6-w12 | Lev 24:22 w8-w11 | H0430 | אֱלֹהִים | God | 2.34 | parallel |
| Lev 24:15 w6-w12 | Lev 24:22 w8-w11 | H3588 | כִּי | for | 1.78 | tied |
| Lev 24:15 w6-w12 | Lev 24:23 w1-w14 | H7043 | קָלַל | to lighten | 5.69 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H3478 | יִשְׂרָאֵל | Israel | 2.34 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w15-w22 | H1121 | בֵּן | child | 1.85 | tied |

##### 6. Lev 21:20 w1 to Lev 22:5 w16 (n = 19, centre the unit Lev 21:24 w7)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Lev 21:24 w7 | 19 | 19 | 12678.12 | 2876.06 | 0.630 | 208.07 | 1.07e-7 | sampled, B = 1000000000, 106 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0047, q (BY) 0.0627: mirror order exceeds parallel order and the permutation null at q = 0.0047. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 |  |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H4872 | מֹשֶׁה | Moses | 3.50 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H0175 | אַהֲרֹן | Aaron | 4.26 | tied |
| Lev 21:24 w1-w6 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:3 w1-w18 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:4 w1-w14 | H0175 | אַהֲרֹן | Aaron | 4.26 | tied |
| Lev 21:23 w13-w20 | Lev 22:1 w1-w5 | H3068 | יהוה | LORD | 1.44 | parallel |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H2490 | חָלַל | profane | 5.16 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w1-w12 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 | parallel |
| Lev 21:23 w1-w12 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w1-w12 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:22 w5-w7 | Lev 22:2 w1-w14 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | parallel |
| Lev 21:22 w5-w7 | Lev 22:3 w1-w18 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | tied |
| Lev 21:22 w5-w7 | Lev 22:4 w1-w14 | H0398 | אָכַל | to eat | 3.50 | tied |
| Lev 21:22 w5-w7 | Lev 22:4 w1-w14 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | tied |

##### 7. Ezek 47:22 w1 to Ezek 48:11 w16 (n = 20, centre before Ezek 48:6 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Ezek 48:6 w1 | 20 | 15 | 88620.57 | 51215.31 | 0.267 | 641.19 | 1.09e-7 | sampled, B = 1000000000, 108 as high | 1.00e-9 | 0.0028 (sampled, B = 99999, 279 as high) |

q (BH) 0.0047, q (BY) 0.0627: mirror order exceeds parallel order and the permutation null at q = 0.0047. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H5921 | עַל | upon | 1.64 |  |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H0669 | אֶפְרַ֫יִם | Ephraim | 4.95 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:6 w1-w10 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H5921 | עַל | upon | 1.64 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H5921 | עַל | upon | 1.64 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w9-w27 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w9-w27 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w9-w27 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w9-w27 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w9-w27 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:10 w1-w22 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:10 w1-w22 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:6 w1-w10 | H5921 | עַל | upon | 1.64 | parallel |
| Ezek 48:4 w1-w10 | Ezek 48:6 w1-w10 | H0259 | אֶחָד | one | 3.45 | tied |

##### 8. Lev 24:14 w14 to Lev 25:1 w7 (n = 20, centre before Lev 24:19 w6)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Lev 24:19 w6 | 20 | 20 | 5431.09 | 528.38 | 0.823 | 122.61 | 1.62e-7 | sampled, B = 1000000000, 161 as high | 1.00e-9 | 2.00e-5 (sampled, B = 99999, 1 as high) |

q (BH) 0.0047, q (BY) 0.0627: mirror order exceeds parallel order and the permutation null at q = 0.0047. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 24:19 w1-w5 | Lev 24:20 w10-w16 | H5414 | נָתַן | give | 2.55 |  |
| Lev 24:19 w1-w5 | Lev 24:20 w10-w16 | H3971 | מוּם | blemish | 7.11 | tied |
| Lev 24:19 w1-w5 | Lev 24:22 w8-w11 | H3588 | כִּי | for | 1.78 | tied |
| Lev 24:18 w5-w7 | Lev 24:20 w1-w9 | H8478 | תַּחַת | under | 3.95 | parallel |
| Lev 24:18 w1-w4 | Lev 24:21 w1-w3 | H0929 | בְּהֵמָה | animal | 4.91 | mirror |
| Lev 24:18 w1-w4 | Lev 24:21 w1-w3 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:18 w1-w4 | Lev 24:21 w1-w3 | H7999 | שָׁלֵם | to complete | 5.38 | tied |
| Lev 24:18 w1-w4 | Lev 24:21 w4-w6 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:17 w7-w8 | Lev 24:21 w4-w6 | H4191 | מוּת | to die | 3.50 | tied |
| Lev 24:17 w1-w6 | Lev 24:20 w10-w16 | H0120 | אָדָם | man | 3.79 | parallel |
| Lev 24:17 w1-w6 | Lev 24:21 w1-w3 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:17 w1-w6 | Lev 24:21 w4-w6 | H0120 | אָדָם | man | 3.79 | tied |
| Lev 24:17 w1-w6 | Lev 24:21 w4-w6 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:17 w1-w6 | Lev 24:22 w8-w11 | H3588 | כִּי | for | 1.78 | tied |
| Lev 24:16 w11-w15 | Lev 24:21 w4-w6 | H4191 | מוּת | to die | 3.50 | parallel |
| Lev 24:16 w11-w15 | Lev 24:22 w1-w7 | H1616 | גֵּר | sojourner | 5.64 | tied |
| Lev 24:16 w11-w15 | Lev 24:22 w1-w7 | H0249 | אֶזְרָח | born | 7.22 | tied |
| Lev 24:16 w1-w10 | Lev 24:21 w4-w6 | H4191 | מוּת | to die | 3.50 | parallel |
| Lev 24:16 w1-w10 | Lev 24:22 w8-w11 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 24:16 w1-w10 | Lev 24:23 w1-w14 | H7275 | רָגַם | to stone | 7.35 | tied |
| Lev 24:16 w1-w10 | Lev 24:23 w15-w22 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 24:16 w1-w10 | Lev 25:1 w1-w7 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 24:15 w6-w12 | Lev 24:22 w8-w11 | H0430 | אֱלֹהִים | God | 2.34 | parallel |
| Lev 24:15 w6-w12 | Lev 24:22 w8-w11 | H3588 | כִּי | for | 1.78 | tied |
| Lev 24:15 w6-w12 | Lev 24:23 w1-w14 | H7043 | קָלַל | to lighten | 5.69 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H3478 | יִשְׂרָאֵל | Israel | 2.34 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w15-w22 | H1121 | בֵּן | child | 1.85 | tied |

##### 9. 2Kgs 3:27 w17 to 2Kgs 4:8 w20 (n = 17, centre the unit 2Kgs 4:4 w12)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit 2Kgs 4:4 w12 | 17 | 19 | 4679.04 | 1034.32 | 0.638 | 130.08 | 1.64e-7 | sampled, B = 1000000000, 163 as high | 4.92e-9 | 1.50e-4 (sampled, B = 99999, 14 as high) |

q (BH) 0.0047, q (BY) 0.0627: mirror order exceeds parallel order and the permutation null at q = 0.0047. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 2Kgs 4:4 w1-w11 | 2Kgs 4:5 w1-w7 | H5462 | סָגַר | to shut | 5.59 |  |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:5 w1-w7 | H1121 | בֵּן | child | 1.85 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:5 w1-w7 | H1157 | בַּ֫עַד | about/through/for | 5.65 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:5 w1-w7 | H1817 | דֶּ֫לֶת | door | 5.70 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:5 w8-w12 | H3332 | יָצַק | pour | 6.18 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:6 w1-w15 | H1121 | בֵּן | child | 1.85 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:6 w1-w15 | H3627 | כְּלִי | article/utensil | 4.43 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:7 w1-w12 | H0935 | בּוֹא | come | 2.31 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:7 w13-w16 | H1121 | בֵּן | child | 1.85 | tied |
| 2Kgs 4:3 w11-w14 | 2Kgs 4:6 w1-w15 | H3627 | כְּלִי | article/utensil | 4.43 | parallel |
| 2Kgs 4:3 w1-w10 | 2Kgs 4:5 w1-w7 | H1980 | הָלַךְ | went | 2.85 | parallel |
| 2Kgs 4:3 w1-w10 | 2Kgs 4:5 w1-w7 | H0854 | אֵת | with | 3.35 | tied |
| 2Kgs 4:3 w1-w10 | 2Kgs 4:6 w1-w15 | H0559 | אָמַר | to say | 1.68 | tied |
| 2Kgs 4:3 w1-w10 | 2Kgs 4:6 w1-w15 | H3627 | כְּלִי | article/utensil | 4.43 | tied |
| 2Kgs 4:3 w1-w10 | 2Kgs 4:7 w1-w12 | H0559 | אָמַר | to say | 1.68 | tied |
| 2Kgs 4:3 w1-w10 | 2Kgs 4:7 w1-w12 | H1980 | הָלַךְ | went | 2.85 | tied |
| 2Kgs 4:2 w13-w21 | 2Kgs 4:6 w1-w15 | H0559 | אָמַר | to say | 1.68 | parallel |
| 2Kgs 4:2 w13-w21 | 2Kgs 4:6 w1-w15 | H0369 | אַ֫יִן | nothing | 3.52 | tied |
| 2Kgs 4:2 w13-w21 | 2Kgs 4:6 w16-w17 | H8081 | שֶׁ֫מֶן | oil | 4.88 | tied |
| 2Kgs 4:2 w13-w21 | 2Kgs 4:7 w1-w12 | H0559 | אָמַר | to say | 1.68 | tied |
| 2Kgs 4:2 w13-w21 | 2Kgs 4:7 w1-w12 | H8081 | שֶׁ֫מֶן | oil | 4.88 | tied |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:5 w8-w12 | H0413 | אֶל | to(wards) | 1.71 | parallel |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:6 w1-w15 | H0559 | אָמַר | to say | 1.68 | tied |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:6 w1-w15 | H0413 | אֶל | to(wards) | 1.71 | tied |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:7 w1-w12 | H0559 | אָמַר | to say | 1.68 | tied |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:7 w1-w12 | H5046 | נָגַד | to tell | 4.21 | tied |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:8 w1-w13 | H0413 | אֶל | to(wards) | 1.71 | tied |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:8 w1-w13 | H0477 | אֱלִישָׁע | Elisha | 6.10 | tied |
| 2Kgs 4:1 w21-w28 | 2Kgs 4:7 w1-w12 | H0935 | בּוֹא | come | 2.31 | parallel |
| 2Kgs 4:1 w1-w20 | 2Kgs 4:5 w1-w7 | H1121 | בֵּן | child | 1.85 | parallel |

##### 10. 2Kgs 4:1 w1 to 2Kgs 4:8 w20 (n = 16, centre before 2Kgs 4:5 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before 2Kgs 4:5 w1 | 16 | 19 | 4679.04 | 1034.32 | 0.638 | 130.08 | 1.64e-7 | sampled, B = 1000000000, 163 as high | 4.92e-9 | 1.60e-4 (sampled, B = 99999, 15 as high) |

q (BH) 0.0047, q (BY) 0.0627: mirror order exceeds parallel order and the permutation null at q = 0.0047. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 2Kgs 4:4 w1-w11 | 2Kgs 4:5 w1-w7 | H5462 | סָגַר | to shut | 5.59 |  |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:5 w1-w7 | H1121 | בֵּן | child | 1.85 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:5 w1-w7 | H1157 | בַּ֫עַד | about/through/for | 5.65 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:5 w1-w7 | H1817 | דֶּ֫לֶת | door | 5.70 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:5 w8-w12 | H3332 | יָצַק | pour | 6.18 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:6 w1-w15 | H1121 | בֵּן | child | 1.85 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:6 w1-w15 | H3627 | כְּלִי | article/utensil | 4.43 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:7 w1-w12 | H0935 | בּוֹא | come | 2.31 | tied |
| 2Kgs 4:4 w1-w11 | 2Kgs 4:7 w13-w16 | H1121 | בֵּן | child | 1.85 | tied |
| 2Kgs 4:3 w11-w14 | 2Kgs 4:6 w1-w15 | H3627 | כְּלִי | article/utensil | 4.43 | parallel |
| 2Kgs 4:3 w1-w10 | 2Kgs 4:5 w1-w7 | H1980 | הָלַךְ | went | 2.85 | parallel |
| 2Kgs 4:3 w1-w10 | 2Kgs 4:5 w1-w7 | H0854 | אֵת | with | 3.35 | tied |
| 2Kgs 4:3 w1-w10 | 2Kgs 4:6 w1-w15 | H0559 | אָמַר | to say | 1.68 | tied |
| 2Kgs 4:3 w1-w10 | 2Kgs 4:6 w1-w15 | H3627 | כְּלִי | article/utensil | 4.43 | tied |
| 2Kgs 4:3 w1-w10 | 2Kgs 4:7 w1-w12 | H0559 | אָמַר | to say | 1.68 | tied |
| 2Kgs 4:3 w1-w10 | 2Kgs 4:7 w1-w12 | H1980 | הָלַךְ | went | 2.85 | tied |
| 2Kgs 4:2 w13-w21 | 2Kgs 4:6 w1-w15 | H0559 | אָמַר | to say | 1.68 | parallel |
| 2Kgs 4:2 w13-w21 | 2Kgs 4:6 w1-w15 | H0369 | אַ֫יִן | nothing | 3.52 | tied |
| 2Kgs 4:2 w13-w21 | 2Kgs 4:6 w16-w17 | H8081 | שֶׁ֫מֶן | oil | 4.88 | tied |
| 2Kgs 4:2 w13-w21 | 2Kgs 4:7 w1-w12 | H0559 | אָמַר | to say | 1.68 | tied |
| 2Kgs 4:2 w13-w21 | 2Kgs 4:7 w1-w12 | H8081 | שֶׁ֫מֶן | oil | 4.88 | tied |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:5 w8-w12 | H0413 | אֶל | to(wards) | 1.71 | parallel |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:6 w1-w15 | H0559 | אָמַר | to say | 1.68 | tied |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:6 w1-w15 | H0413 | אֶל | to(wards) | 1.71 | tied |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:7 w1-w12 | H0559 | אָמַר | to say | 1.68 | tied |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:7 w1-w12 | H5046 | נָגַד | to tell | 4.21 | tied |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:8 w1-w13 | H0413 | אֶל | to(wards) | 1.71 | tied |
| 2Kgs 4:2 w1-w12 | 2Kgs 4:8 w1-w13 | H0477 | אֱלִישָׁע | Elisha | 6.10 | tied |
| 2Kgs 4:1 w21-w28 | 2Kgs 4:7 w1-w12 | H0935 | בּוֹא | come | 2.31 | parallel |
| 2Kgs 4:1 w1-w20 | 2Kgs 4:5 w1-w7 | H1121 | בֵּן | child | 1.85 | parallel |

##### 11. Lev 4:6 w1 to Lev 4:17 w13 (n = 24, centre before Lev 4:12 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Lev 4:12 w1 | 24 | 21 | 35384.63 | 11863.18 | 0.498 | 345.73 | 1.70e-7 | sampled, B = 1000000000, 169 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0047, q (BY) 0.0627: mirror order exceeds parallel order and the permutation null at q = 0.0047. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 4:11 w1-w10 | Lev 4:12 w1-w18 | H5921 | עַל | upon | 1.64 |  |
| Lev 4:11 w1-w10 | Lev 4:12 w1-w18 | H3605 | כֹּל | all | 1.70 | tied |
| Lev 4:11 w1-w10 | Lev 4:12 w1-w18 | H6499 | פַּר | bullock | 5.28 | tied |
| Lev 4:11 w1-w10 | Lev 4:12 w19-w22 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:11 w1-w10 | Lev 4:13 w1-w9 | H3605 | כֹּל | all | 1.70 | tied |
| Lev 4:11 w1-w10 | Lev 4:13 w10-w18 | H3605 | כֹּל | all | 1.70 | tied |
| Lev 4:11 w1-w10 | Lev 4:14 w1-w5 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:11 w1-w10 | Lev 4:14 w6-w16 | H6499 | פַּר | bullock | 5.28 | tied |
| Lev 4:11 w1-w10 | Lev 4:15 w1-w10 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:11 w1-w10 | Lev 4:15 w1-w10 | H7218 | רֹאשׁ | head | 3.75 | tied |
| Lev 4:11 w1-w10 | Lev 4:15 w1-w10 | H6499 | פַּר | bullock | 5.28 | tied |
| Lev 4:11 w1-w10 | Lev 4:15 w11-w15 | H6499 | פַּר | bullock | 5.28 | tied |
| Lev 4:11 w1-w10 | Lev 4:16 w1-w5 | H6499 | פַּר | bullock | 5.28 | tied |
| Lev 4:10 w6-w10 | Lev 4:12 w1-w18 | H5921 | עַל | upon | 1.64 | parallel |
| Lev 4:10 w6-w10 | Lev 4:12 w19-w22 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:10 w6-w10 | Lev 4:14 w1-w5 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:10 w6-w10 | Lev 4:15 w1-w10 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:10 w6-w10 | Lev 4:16 w1-w5 | H3548 | כֹּהֵן | priest | 3.57 | tied |
| Lev 4:10 w6-w10 | Lev 4:17 w1-w5 | H3548 | כֹּהֵן | priest | 3.57 | tied |
| Lev 4:10 w1-w5 | Lev 4:13 w10-w18 | H0834 | אֲשֶׁר | which | 1.66 | parallel |
| Lev 4:10 w1-w5 | Lev 4:14 w1-w5 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Lev 4:9 w11-w17 | Lev 4:12 w1-w18 | H5921 | עַל | upon | 1.64 | parallel |
| Lev 4:9 w11-w17 | Lev 4:12 w19-w22 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:9 w11-w17 | Lev 4:14 w1-w5 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:9 w11-w17 | Lev 4:15 w1-w10 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:9 w1-w10 | Lev 4:12 w1-w18 | H5921 | עַל | upon | 1.64 | parallel |
| Lev 4:9 w1-w10 | Lev 4:12 w19-w22 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:9 w1-w10 | Lev 4:13 w10-w18 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Lev 4:9 w1-w10 | Lev 4:14 w1-w5 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:9 w1-w10 | Lev 4:14 w1-w5 | H0834 | אֲשֶׁר | which | 1.66 | tied |

##### 12. Num 34:28 w5 to Num 35:10 w13 (n = 22, centre before Num 35:5 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Num 35:5 w1 | 22 | 24 | 30696.22 | 11480.43 | 0.456 | 330.48 | 1.78e-7 | sampled, B = 1000000000, 177 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0047, q (BY) 0.0627: mirror order exceeds parallel order and the permutation null at q = 0.0047. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Num 35:4 w6-w11 | Num 35:5 w1-w25 | H5892 | עִיר | city | 3.22 |  |
| Num 35:4 w6-w11 | Num 35:5 w1-w25 | H2351 | חוּץ | outside | 4.99 | tied |
| Num 35:4 w6-w11 | Num 35:5 w1-w25 | H0520 | אַמָּה | cubit | 5.18 | tied |
| Num 35:4 w6-w11 | Num 35:5 w1-w25 | H0505 | אֶ֫לֶף | thousand | 4.09 | tied |
| Num 35:4 w6-w11 | Num 35:5 w26-w30 | H5892 | עִיר | city | 3.22 | tied |
| Num 35:4 w6-w11 | Num 35:6 w1-w14 | H5892 | עִיר | city | 3.22 | tied |
| Num 35:4 w6-w11 | Num 35:6 w15-w19 | H5892 | עִיר | city | 3.22 | tied |
| Num 35:4 w6-w11 | Num 35:7 w1-w8 | H5892 | עִיר | city | 3.22 | tied |
| Num 35:4 w6-w11 | Num 35:8 w1-w12 | H5892 | עִיר | city | 3.22 | tied |
| Num 35:4 w6-w11 | Num 35:8 w13-w20 | H5892 | עִיר | city | 3.22 | tied |
| Num 35:4 w1-w5 | Num 35:5 w1-w25 | H5892 | עִיר | city | 3.22 | parallel |
| Num 35:4 w1-w5 | Num 35:5 w26-w30 | H5892 | עִיר | city | 3.22 | tied |
| Num 35:4 w1-w5 | Num 35:5 w26-w30 | H4054 | מִגְרָשׁ | pasture | 5.82 | tied |
| Num 35:4 w1-w5 | Num 35:6 w1-w14 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Num 35:4 w1-w5 | Num 35:6 w1-w14 | H5414 | נָתַן | give | 2.55 | tied |
| Num 35:4 w1-w5 | Num 35:6 w1-w14 | H5892 | עִיר | city | 3.22 | tied |
| Num 35:4 w1-w5 | Num 35:6 w1-w14 | H3881 | לֵוִי | Levi | 4.48 | tied |
| Num 35:4 w1-w5 | Num 35:6 w15-w19 | H5414 | נָתַן | give | 2.55 | tied |
| Num 35:4 w1-w5 | Num 35:6 w15-w19 | H5892 | עִיר | city | 3.22 | tied |
| Num 35:4 w1-w5 | Num 35:7 w1-w8 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Num 35:4 w1-w5 | Num 35:7 w1-w8 | H5414 | נָתַן | give | 2.55 | tied |
| Num 35:4 w1-w5 | Num 35:7 w1-w8 | H5892 | עִיר | city | 3.22 | tied |
| Num 35:4 w1-w5 | Num 35:7 w1-w8 | H3881 | לֵוִי | Levi | 4.48 | tied |
| Num 35:4 w1-w5 | Num 35:7 w9-w11 | H4054 | מִגְרָשׁ | pasture | 5.82 | tied |
| Num 35:4 w1-w5 | Num 35:8 w1-w12 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Num 35:4 w1-w5 | Num 35:8 w1-w12 | H5414 | נָתַן | give | 2.55 | tied |
| Num 35:4 w1-w5 | Num 35:8 w1-w12 | H5892 | עִיר | city | 3.22 | tied |
| Num 35:4 w1-w5 | Num 35:8 w13-w20 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Num 35:4 w1-w5 | Num 35:8 w13-w20 | H5414 | נָתַן | give | 2.55 | tied |
| Num 35:4 w1-w5 | Num 35:8 w13-w20 | H5892 | עִיר | city | 3.22 | tied |

##### 13. Lev 21:20 w1 to Lev 22:5 w9 (n = 18, centre before Lev 21:24 w7)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Lev 21:24 w7 | 18 | 19 | 11557.96 | 2996.89 | 0.588 | 202.34 | 2.51e-7 | sampled, B = 1000000000, 250 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0055, q (BY) 0.0734: mirror order exceeds parallel order and the permutation null at q = 0.0055. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 21:24 w1-w6 | Lev 21:24 w7-w10 | H0413 | אֶל | to(wards) | 1.71 |  |
| Lev 21:24 w1-w6 | Lev 21:24 w7-w10 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H4872 | מֹשֶׁה | Moses | 3.50 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H0175 | אַהֲרֹן | Aaron | 4.26 | tied |
| Lev 21:24 w1-w6 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:3 w1-w18 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:4 w1-w14 | H0175 | אַהֲרֹן | Aaron | 4.26 | tied |
| Lev 21:23 w13-w20 | Lev 22:1 w1-w5 | H3068 | יהוה | LORD | 1.44 | parallel |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H2490 | חָלַל | profane | 5.16 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w1-w12 | Lev 21:24 w7-w10 | H0413 | אֶל | to(wards) | 1.71 | parallel |
| Lev 21:23 w1-w12 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w1-w12 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:22 w5-w7 | Lev 22:2 w1-w14 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | parallel |

##### 14. Deut 2:10 w1 to Deut 2:21 w5 (n = 20, centre before Deut 2:15 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Deut 2:15 w1 | 20 | 26 | 8925.75 | 764.05 | 0.842 | 158.00 | 2.54e-7 | sampled, B = 1000000000, 253 as high | 1.00e-9 | 5.00e-5 (sampled, B = 99999, 4 as high) |

q (BH) 0.0055, q (BY) 0.0734: mirror order exceeds parallel order and the permutation null at q = 0.0055. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Deut 2:14 w15-w26 | Deut 2:15 w1-w8 | H3068 | יהוה | LORD | 1.44 |  |
| Deut 2:14 w15-w26 | Deut 2:15 w1-w8 | H7130 | קֶ֫רֶב | among | 4.66 | tied |
| Deut 2:14 w15-w26 | Deut 2:15 w1-w8 | H4264 | מַחֲנֶה | camp | 4.81 | tied |
| Deut 2:14 w15-w26 | Deut 2:15 w9-w10 | H5704 | עַד | till | 3.03 | tied |
| Deut 2:14 w15-w26 | Deut 2:15 w9-w10 | H8552 | תָּמַם | to finish | 5.94 | tied |
| Deut 2:14 w15-w26 | Deut 2:16 w1-w9 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Deut 2:14 w15-w26 | Deut 2:16 w1-w9 | H3605 | כֹּל | all | 1.70 | tied |
| Deut 2:14 w15-w26 | Deut 2:16 w1-w9 | H0582 | אֱנוֹשׁ | human | 3.78 | tied |
| Deut 2:14 w15-w26 | Deut 2:16 w1-w9 | H4421 | מִלְחָמָה | battle | 4.32 | tied |
| Deut 2:14 w15-w26 | Deut 2:16 w1-w9 | H7130 | קֶ֫רֶב | among | 4.66 | tied |
| Deut 2:14 w15-w26 | Deut 2:16 w1-w9 | H8552 | תָּמַם | to finish | 5.94 | tied |
| Deut 2:14 w15-w26 | Deut 2:17 w1-w4 | H3068 | יהוה | LORD | 1.44 | tied |
| Deut 2:14 w1-w14 | Deut 2:15 w9-w10 | H5704 | עַד | till | 3.03 | parallel |
| Deut 2:14 w1-w14 | Deut 2:16 w1-w9 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Deut 2:14 w1-w14 | Deut 2:18 w1-w8 | H3117 | יוֹם | day | 2.49 | tied |
| Deut 2:14 w1-w14 | Deut 2:18 w1-w8 | H5674 | עָבַר | pass | 3.85 | tied |
| Deut 2:13 w8-w11 | Deut 2:18 w1-w8 | H5674 | עָבַר | pass | 3.85 | tied |
| Deut 2:13 w1-w7 | Deut 2:18 w1-w8 | H5674 | עָבַר | pass | 3.85 | tied |
| Deut 2:12 w12-w20 | Deut 2:15 w1-w8 | H3068 | יהוה | LORD | 1.44 | parallel |
| Deut 2:12 w12-w20 | Deut 2:16 w1-w9 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Deut 2:12 w12-w20 | Deut 2:17 w1-w4 | H3068 | יהוה | LORD | 1.44 | tied |
| Deut 2:12 w12-w20 | Deut 2:19 w10-w22 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Deut 2:12 w12-w20 | Deut 2:19 w10-w22 | H5414 | נָתַן | give | 2.55 | tied |
| Deut 2:12 w12-w20 | Deut 2:19 w10-w22 | H3425 | יְרֻשָּׁה | possession | 7.57 | tied |
| Deut 2:12 w12-w20 | Deut 2:20 w1-w5 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Deut 2:12 w1-w11 | Deut 2:19 w1-w9 | H1121 | בֵּן | child | 1.85 | parallel |
| Deut 2:12 w1-w11 | Deut 2:19 w10-w22 | H1121 | בֵּן | child | 1.85 | tied |
| Deut 2:12 w1-w11 | Deut 2:20 w6-w13 | H6440 | פָּנֶה | before | 2.51 | tied |
| Deut 2:12 w1-w11 | Deut 2:20 w6-w13 | H3427 | יָשַׁב | to dwell | 3.18 | tied |
| Deut 2:11 w6-w9 | Deut 2:20 w6-w13 | H7121 | קָרָא | call to | 3.52 | tied |

##### 15. Ezek 3:14 w1 to Ezek 3:24 w6 (n = 21, centre the unit Ezek 3:19 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Ezek 3:19 w1 | 21 | 21 | 10867.52 | 1627.29 | 0.740 | 181.46 | 2.66e-7 | sampled, B = 1000000000, 265 as high | 1.00e-9 | 2.00e-5 (sampled, B = 99999, 1 as high) |

q (BH) 0.0055, q (BY) 0.0734: mirror order exceeds parallel order and the permutation null at q = 0.0055. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Ezek 3:18 w14-w20 | Ezek 3:19 w10-w16 | H1931 | הוּא | he; she; it | 2.62 |  |
| Ezek 3:18 w14-w20 | Ezek 3:19 w10-w16 | H4191 | מוּת | to die | 3.50 | tied |
| Ezek 3:18 w14-w20 | Ezek 3:19 w10-w16 | H5771 | עָוֺן | crime | 4.69 | tied |
| Ezek 3:18 w14-w20 | Ezek 3:20 w1-w10 | H1931 | הוּא | he; she; it | 2.62 | tied |
| Ezek 3:18 w14-w20 | Ezek 3:20 w1-w10 | H4191 | מוּת | to die | 3.50 | tied |
| Ezek 3:18 w14-w20 | Ezek 3:20 w11-w23 | H4191 | מוּת | to die | 3.50 | tied |
| Ezek 3:18 w14-w20 | Ezek 3:20 w11-w23 | H3027 | יָד | hand | 2.78 | tied |
| Ezek 3:18 w14-w20 | Ezek 3:20 w11-w23 | H1818 | דָּם | blood | 4.37 | tied |
| Ezek 3:18 w14-w20 | Ezek 3:20 w11-w23 | H1245 | בָּקַשׁ | to seek | 4.68 | tied |
| Ezek 3:18 w14-w20 | Ezek 3:21 w1-w10 | H1931 | הוּא | he; she; it | 2.62 | tied |
| Ezek 3:18 w14-w20 | Ezek 3:22 w1-w5 | H3027 | יָד | hand | 2.78 | tied |
| Ezek 3:18 w1-w13 | Ezek 3:19 w10-w16 | H4191 | מוּת | to die | 3.50 | parallel |
| Ezek 3:18 w1-w13 | Ezek 3:20 w1-w10 | H4191 | מוּת | to die | 3.50 | tied |
| Ezek 3:18 w1-w13 | Ezek 3:20 w11-w23 | H3808 | לֹא | not | 1.77 | tied |
| Ezek 3:18 w1-w13 | Ezek 3:20 w11-w23 | H4191 | מוּת | to die | 3.50 | tied |
| Ezek 3:18 w1-w13 | Ezek 3:20 w11-w23 | H2094 | זָהַר | to warn | 7.11 | tied |
| Ezek 3:18 w1-w13 | Ezek 3:21 w1-w10 | H3808 | לֹא | not | 1.77 | tied |
| Ezek 3:18 w1-w13 | Ezek 3:21 w1-w10 | H2094 | זָהַר | to warn | 7.11 | tied |
| Ezek 3:18 w1-w13 | Ezek 3:21 w11-w18 | H2421 | חָיָה | to live | 4.51 | tied |
| Ezek 3:18 w1-w13 | Ezek 3:21 w11-w18 | H2094 | זָהַר | to warn | 7.11 | tied |
| Ezek 3:18 w1-w13 | Ezek 3:22 w6-w14 | H0559 | אָמַר | to say | 1.68 | tied |
| Ezek 3:18 w1-w13 | Ezek 3:22 w6-w14 | H1696 | דָבַר | speak | 3.10 | tied |
| Ezek 3:17 w7-w12 | Ezek 3:20 w11-w23 | H2094 | זָהַר | to warn | 7.11 | parallel |
| Ezek 3:17 w7-w12 | Ezek 3:21 w1-w10 | H2094 | זָהַר | to warn | 7.11 | tied |
| Ezek 3:17 w7-w12 | Ezek 3:21 w11-w18 | H2094 | זָהַר | to warn | 7.11 | tied |
| Ezek 3:17 w1-w6 | Ezek 3:20 w1-w10 | H5414 | נָתַן | give | 2.55 | parallel |
| Ezek 3:16 w5-w9 | Ezek 3:22 w1-w5 | H1961 | הָיָה | to be | 2.01 | mirror |
| Ezek 3:16 w5-w9 | Ezek 3:22 w1-w5 | H3068 | יהוה | LORD | 1.44 | tied |
| Ezek 3:16 w5-w9 | Ezek 3:22 w6-w14 | H0559 | אָמַר | to say | 1.68 | tied |
| Ezek 3:16 w5-w9 | Ezek 3:22 w6-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |

##### 16. Ezek 47:22 w13 to Ezek 48:12 w7 (n = 20, centre before Ezek 48:7 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Ezek 48:7 w1 | 20 | 15 | 65468.92 | 40178.32 | 0.239 | 570.49 | 2.78e-7 | sampled, B = 1000000000, 277 as high | 1.00e-9 | 0.0048 (sampled, B = 99999, 482 as high) |

q (BH) 0.0055, q (BY) 0.0734: mirror order exceeds parallel order and the permutation null at q = 0.0055. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Ezek 48:6 w1-w10 | Ezek 48:7 w1-w10 | H5921 | עַל | upon | 1.64 |  |
| Ezek 48:6 w1-w10 | Ezek 48:7 w1-w10 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:7 w1-w10 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:7 w1-w10 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:7 w1-w10 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:7 w1-w10 | H7205 | רְאוּבֵן | Reuben | 5.84 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:7 w1-w10 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:7 w1-w10 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:8 w1-w8 | H5921 | עַל | upon | 1.64 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:8 w1-w8 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:8 w1-w8 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:8 w1-w8 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:8 w1-w8 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:8 w1-w8 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:8 w9-w27 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:8 w9-w27 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:8 w9-w27 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:8 w9-w27 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:8 w9-w27 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:10 w1-w22 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:6 w1-w10 | Ezek 48:10 w1-w22 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H5921 | עַל | upon | 1.64 | parallel |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:7 w1-w10 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H5921 | עַל | upon | 1.64 | tied |
| Ezek 48:5 w1-w10 | Ezek 48:8 w1-w8 | H3220 | יָם | sea | 4.23 | tied |

##### 17. Ezek 47:21 w1 to Ezek 48:11 w7 (n = 20, centre before Ezek 48:5 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Ezek 48:5 w1 | 20 | 14 | 81604.89 | 49161.18 | 0.248 | 627.11 | 3.06e-7 | sampled, B = 1000000000, 305 as high | 1.00e-9 | 0.0043 (sampled, B = 99999, 426 as high) |

q (BH) 0.0057, q (BY) 0.0760: mirror order exceeds parallel order and the permutation null at q = 0.0057. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Ezek 48:4 w1-w10 | Ezek 48:5 w1-w10 | H5921 | עַל | upon | 1.64 |  |
| Ezek 48:4 w1-w10 | Ezek 48:5 w1-w10 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:5 w1-w10 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:5 w1-w10 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:5 w1-w10 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:5 w1-w10 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:5 w1-w10 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:5 w1-w10 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:6 w1-w10 | H5921 | עַל | upon | 1.64 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:6 w1-w10 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:6 w1-w10 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:6 w1-w10 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:6 w1-w10 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:6 w1-w10 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:6 w1-w10 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:7 w1-w10 | H5921 | עַל | upon | 1.64 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:7 w1-w10 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:7 w1-w10 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:7 w1-w10 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:7 w1-w10 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:7 w1-w10 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:7 w1-w10 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:8 w1-w8 | H5921 | עַל | upon | 1.64 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:8 w1-w8 | H3220 | יָם | sea | 4.23 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:8 w1-w8 | H5704 | עַד | till | 3.03 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:8 w1-w8 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:8 w1-w8 | H6921 | קָדִים | east | 5.90 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:8 w1-w8 | H6285 | פֵּאָה | side | 5.98 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:8 w9-w27 | H0259 | אֶחָד | one | 3.45 | tied |
| Ezek 48:4 w1-w10 | Ezek 48:8 w9-w27 | H3220 | יָם | sea | 4.23 | tied |

##### 18. Josh 17:4 w1 to Josh 17:14 w23 (n = 22, centre before Josh 17:9 w13)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Josh 17:9 w13 | 22 | 21 | 28881.71 | 12380.06 | 0.400 | 331.36 | 4.13e-7 | sampled, B = 1000000000, 412 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0073, q (BY) 0.0969: mirror order exceeds parallel order and the permutation null at q = 0.0073. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Josh 17:9 w1-w12 | Josh 17:9 w13-w19 | H1366 | גְּבוּל | boundary | 4.78 |  |
| Josh 17:9 w1-w12 | Josh 17:9 w13-w19 | H5158 | נַ֫חַל | river | 5.24 | tied |
| Josh 17:9 w1-w12 | Josh 17:9 w13-w19 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Josh 17:9 w1-w12 | Josh 17:10 w1-w7 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Josh 17:9 w1-w12 | Josh 17:10 w1-w7 | H5045 | נֶ֫גֶב | south | 5.47 | tied |
| Josh 17:9 w1-w12 | Josh 17:10 w1-w7 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Josh 17:9 w1-w12 | Josh 17:10 w1-w7 | H0669 | אֶפְרַ֫יִם | Ephraim | 4.95 | tied |
| Josh 17:9 w1-w12 | Josh 17:11 w1-w23 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Josh 17:9 w1-w12 | Josh 17:12 w1-w8 | H0428 | אֵ֫לֶּה | these | 3.51 | tied |
| Josh 17:9 w1-w12 | Josh 17:12 w1-w8 | H5892 | עִיר | city | 3.22 | tied |
| Josh 17:9 w1-w12 | Josh 17:12 w1-w8 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Josh 17:8 w5-w10 | Josh 17:9 w13-w19 | H1366 | גְּבוּל | boundary | 4.78 | parallel |
| Josh 17:8 w5-w10 | Josh 17:9 w13-w19 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Josh 17:8 w5-w10 | Josh 17:10 w1-w7 | H1366 | גְּבוּל | boundary | 4.78 | tied |
| Josh 17:8 w5-w10 | Josh 17:10 w1-w7 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Josh 17:8 w5-w10 | Josh 17:10 w1-w7 | H0669 | אֶפְרַ֫יִם | Ephraim | 4.95 | tied |
| Josh 17:8 w5-w10 | Josh 17:11 w1-w23 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Josh 17:8 w5-w10 | Josh 17:12 w1-w8 | H1121 | בֵּן | child | 1.85 | tied |
| Josh 17:8 w5-w10 | Josh 17:12 w1-w8 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Josh 17:8 w5-w10 | Josh 17:13 w1-w9 | H1121 | בֵּן | child | 1.85 | tied |
| Josh 17:8 w5-w10 | Josh 17:14 w1-w6 | H1121 | בֵּן | child | 1.85 | tied |
| Josh 17:8 w1-w4 | Josh 17:9 w13-w19 | H1961 | הָיָה | to be | 2.01 | parallel |
| Josh 17:8 w1-w4 | Josh 17:9 w13-w19 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Josh 17:8 w1-w4 | Josh 17:10 w1-w7 | H1961 | הָיָה | to be | 2.01 | tied |
| Josh 17:8 w1-w4 | Josh 17:10 w1-w7 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Josh 17:8 w1-w4 | Josh 17:11 w1-w23 | H1961 | הָיָה | to be | 2.01 | tied |
| Josh 17:8 w1-w4 | Josh 17:11 w1-w23 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Josh 17:8 w1-w4 | Josh 17:12 w1-w8 | H4519 | מְנַשֶּׁה | Manasseh | 5.16 | tied |
| Josh 17:8 w1-w4 | Josh 17:12 w9-w13 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Josh 17:8 w1-w4 | Josh 17:13 w1-w9 | H1961 | הָיָה | to be | 2.01 | tied |

##### 19. Lev 21:18 w9 to Lev 22:6 w7 (n = 23, centre the unit Lev 21:24 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Lev 21:24 w1 | 23 | 16 | 21845.04 | 6722.65 | 0.529 | 276.09 | 5.03e-7 | sampled, B = 1000000000, 502 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0080, q (BY) 0.1061: mirror order exceeds parallel order and the permutation null at q = 0.0080. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 21:23 w13-w20 | Lev 22:1 w1-w5 | H3068 | יהוה | LORD | 1.44 |  |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H2490 | חָלַל | profane | 5.16 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w1-w12 | Lev 21:24 w7-w10 | H0413 | אֶל | to(wards) | 1.71 | parallel |
| Lev 21:23 w1-w12 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w1-w12 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:23 w1-w12 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:22 w5-w7 | Lev 22:2 w1-w14 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | parallel |
| Lev 21:22 w5-w7 | Lev 22:3 w1-w18 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | tied |
| Lev 21:22 w5-w7 | Lev 22:4 w1-w14 | H0398 | אָכַל | to eat | 3.50 | tied |
| Lev 21:22 w5-w7 | Lev 22:4 w1-w14 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | tied |
| Lev 21:22 w5-w7 | Lev 22:4 w15-w25 | H4480 | מִן־ | from | 3.09 | tied |
| Lev 21:22 w1-w4 | Lev 22:2 w1-w14 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | parallel |
| Lev 21:22 w1-w4 | Lev 22:3 w1-w18 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | tied |
| Lev 21:22 w1-w4 | Lev 22:4 w1-w14 | H6944 | קֹ֫דֶשׁ | holiness | 4.11 | tied |
| Lev 21:21 w15-w22 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | parallel |
| Lev 21:21 w15-w22 | Lev 22:3 w1-w18 | H7126 | קָרַב | bring | 4.49 | tied |
| Lev 21:21 w15-w22 | Lev 22:4 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:21 w1-w14 | Lev 21:24 w7-w10 | H3605 | כֹּל | all | 1.70 | parallel |
| Lev 21:21 w1-w14 | Lev 22:1 w1-w5 | H3068 | יהוה | LORD | 1.44 | tied |

##### 20. Deut 2:10 w5 to Deut 2:21 w5 (n = 19, centre the unit Deut 2:15 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Deut 2:15 w1 | 19 | 25 | 7052.99 | 514.10 | 0.864 | 139.96 | 5.25e-7 | sampled, B = 1000000000, 524 as high | 1.00e-9 | 3.20e-4 (sampled, B = 99999, 31 as high) |

q (BH) 0.0080, q (BY) 0.1061: mirror order exceeds parallel order and the permutation null at q = 0.0080. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Deut 2:14 w15-w26 | Deut 2:15 w9-w10 | H5704 | עַד | till | 3.03 |  |
| Deut 2:14 w15-w26 | Deut 2:15 w9-w10 | H8552 | תָּמַם | to finish | 5.94 | tied |
| Deut 2:14 w15-w26 | Deut 2:16 w1-w9 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Deut 2:14 w15-w26 | Deut 2:16 w1-w9 | H3605 | כֹּל | all | 1.70 | tied |
| Deut 2:14 w15-w26 | Deut 2:16 w1-w9 | H0582 | אֱנוֹשׁ | human | 3.78 | tied |
| Deut 2:14 w15-w26 | Deut 2:16 w1-w9 | H4421 | מִלְחָמָה | battle | 4.32 | tied |
| Deut 2:14 w15-w26 | Deut 2:16 w1-w9 | H7130 | קֶ֫רֶב | among | 4.66 | tied |
| Deut 2:14 w15-w26 | Deut 2:16 w1-w9 | H8552 | תָּמַם | to finish | 5.94 | tied |
| Deut 2:14 w15-w26 | Deut 2:17 w1-w4 | H3068 | יהוה | LORD | 1.44 | tied |
| Deut 2:14 w1-w14 | Deut 2:15 w9-w10 | H5704 | עַד | till | 3.03 | parallel |
| Deut 2:14 w1-w14 | Deut 2:16 w1-w9 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Deut 2:14 w1-w14 | Deut 2:18 w1-w8 | H3117 | יוֹם | day | 2.49 | tied |
| Deut 2:14 w1-w14 | Deut 2:18 w1-w8 | H5674 | עָבַר | pass | 3.85 | tied |
| Deut 2:13 w8-w11 | Deut 2:18 w1-w8 | H5674 | עָבַר | pass | 3.85 | tied |
| Deut 2:13 w1-w7 | Deut 2:18 w1-w8 | H5674 | עָבַר | pass | 3.85 | tied |
| Deut 2:12 w12-w20 | Deut 2:16 w1-w9 | H0834 | אֲשֶׁר | which | 1.66 | parallel |
| Deut 2:12 w12-w20 | Deut 2:17 w1-w4 | H3068 | יהוה | LORD | 1.44 | tied |
| Deut 2:12 w12-w20 | Deut 2:19 w10-w22 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Deut 2:12 w12-w20 | Deut 2:19 w10-w22 | H5414 | נָתַן | give | 2.55 | tied |
| Deut 2:12 w12-w20 | Deut 2:19 w10-w22 | H3425 | יְרֻשָּׁה | possession | 7.57 | tied |
| Deut 2:12 w12-w20 | Deut 2:20 w1-w5 | H0776 | אֶ֫רֶץ | country; planet | 2.36 | tied |
| Deut 2:12 w1-w11 | Deut 2:19 w1-w9 | H1121 | בֵּן | child | 1.85 | parallel |
| Deut 2:12 w1-w11 | Deut 2:19 w10-w22 | H1121 | בֵּן | child | 1.85 | tied |
| Deut 2:12 w1-w11 | Deut 2:20 w6-w13 | H6440 | פָּנֶה | before | 2.51 | tied |
| Deut 2:12 w1-w11 | Deut 2:20 w6-w13 | H3427 | יָשַׁב | to dwell | 3.18 | tied |
| Deut 2:11 w6-w9 | Deut 2:20 w6-w13 | H7121 | קָרָא | call to | 3.52 | tied |
| Deut 2:11 w1-w5 | Deut 2:20 w1-w5 | H0637 | אַף | also | 5.24 | parallel |
| Deut 2:11 w1-w5 | Deut 2:20 w1-w5 | H7497 | רְפָאִים | Rephaim | 6.88 | tied |
| Deut 2:11 w1-w5 | Deut 2:20 w1-w5 | H2803 | חָשַׁב | count | 5.25 | tied |
| Deut 2:11 w1-w5 | Deut 2:20 w6-w13 | H7497 | רְפָאִים | Rephaim | 6.88 | tied |

##### 21. Lev 21:20 w1 to Lev 22:6 w7 (n = 20, centre before Lev 22:1 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Lev 22:1 w1 | 20 | 20 | 15011.41 | 4399.84 | 0.547 | 230.06 | 5.32e-7 | sampled, B = 1000000000, 531 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0080, q (BY) 0.1061: mirror order exceeds parallel order and the permutation null at q = 0.0080. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 21:24 w7-w10 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 |  |
| Lev 21:24 w7-w10 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w7-w10 | Lev 22:2 w1-w14 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w7-w10 | Lev 22:2 w1-w14 | H3478 | יִשְׂרָאֵל | Israel | 2.34 | tied |
| Lev 21:24 w7-w10 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w7-w10 | Lev 22:3 w1-w18 | H3605 | כֹּל | all | 1.70 | tied |
| Lev 21:24 w7-w10 | Lev 22:3 w1-w18 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w7-w10 | Lev 22:3 w1-w18 | H3478 | יִשְׂרָאֵל | Israel | 2.34 | tied |
| Lev 21:24 w7-w10 | Lev 22:4 w15-w25 | H3605 | כֹּל | all | 1.70 | tied |
| Lev 21:24 w7-w10 | Lev 22:5 w1-w9 | H3605 | כֹּל | all | 1.70 | tied |
| Lev 21:24 w7-w10 | Lev 22:5 w10-w16 | H3605 | כֹּל | all | 1.70 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H0413 | אֶל | to(wards) | 1.71 | parallel |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 21:24 w1-w6 | Lev 22:1 w1-w5 | H4872 | מֹשֶׁה | Moses | 3.50 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 21:24 w1-w6 | Lev 22:2 w1-w14 | H0175 | אַהֲרֹן | Aaron | 4.26 | tied |
| Lev 21:24 w1-w6 | Lev 22:3 w1-w18 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 21:24 w1-w6 | Lev 22:3 w1-w18 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 21:24 w1-w6 | Lev 22:4 w1-w14 | H0175 | אַהֲרֹן | Aaron | 4.26 | tied |
| Lev 21:23 w13-w20 | Lev 22:1 w1-w5 | H3068 | יהוה | LORD | 1.44 | parallel |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H3808 | לֹא | not | 1.77 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w1-w14 | H2490 | חָלַל | profane | 5.16 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:2 w15-w20 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H6942 | קָדַשׁ | consecate | 5.03 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w1-w18 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 21:23 w13-w20 | Lev 22:3 w19-w24 | H3068 | יהוה | LORD | 1.44 | tied |

##### 22. Lev 24:14 w14 to Lev 24:23 w22 (n = 19, centre the unit Lev 24:19 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Lev 24:19 w1 | 19 | 17 | 3733.77 | 290.37 | 0.856 | 103.24 | 5.81e-7 | sampled, B = 1000000000, 580 as high | 1.00e-9 | 4.00e-5 (sampled, B = 99999, 3 as high) |

q (BH) 0.0080, q (BY) 0.1061: mirror order exceeds parallel order and the permutation null at q = 0.0080. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 24:18 w5-w7 | Lev 24:20 w1-w9 | H8478 | תַּחַת | under | 3.95 |  |
| Lev 24:18 w1-w4 | Lev 24:21 w1-w3 | H0929 | בְּהֵמָה | animal | 4.91 | mirror |
| Lev 24:18 w1-w4 | Lev 24:21 w1-w3 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:18 w1-w4 | Lev 24:21 w1-w3 | H7999 | שָׁלֵם | to complete | 5.38 | tied |
| Lev 24:18 w1-w4 | Lev 24:21 w4-w6 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:17 w7-w8 | Lev 24:21 w4-w6 | H4191 | מוּת | to die | 3.50 | tied |
| Lev 24:17 w1-w6 | Lev 24:20 w10-w16 | H0120 | אָדָם | man | 3.79 | parallel |
| Lev 24:17 w1-w6 | Lev 24:21 w1-w3 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:17 w1-w6 | Lev 24:21 w4-w6 | H0120 | אָדָם | man | 3.79 | tied |
| Lev 24:17 w1-w6 | Lev 24:21 w4-w6 | H5221 | נָכָה | to smite | 3.92 | tied |
| Lev 24:17 w1-w6 | Lev 24:22 w8-w11 | H3588 | כִּי | for | 1.78 | tied |
| Lev 24:16 w11-w15 | Lev 24:21 w4-w6 | H4191 | מוּת | to die | 3.50 | parallel |
| Lev 24:16 w11-w15 | Lev 24:22 w1-w7 | H1616 | גֵּר | sojourner | 5.64 | tied |
| Lev 24:16 w11-w15 | Lev 24:22 w1-w7 | H0249 | אֶזְרָח | born | 7.22 | tied |
| Lev 24:16 w1-w10 | Lev 24:21 w4-w6 | H4191 | מוּת | to die | 3.50 | parallel |
| Lev 24:16 w1-w10 | Lev 24:22 w8-w11 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 24:16 w1-w10 | Lev 24:23 w1-w14 | H7275 | רָגַם | to stone | 7.35 | tied |
| Lev 24:16 w1-w10 | Lev 24:23 w15-w22 | H3068 | יהוה | LORD | 1.44 | tied |
| Lev 24:15 w6-w12 | Lev 24:22 w8-w11 | H0430 | אֱלֹהִים | God | 2.34 | parallel |
| Lev 24:15 w6-w12 | Lev 24:22 w8-w11 | H3588 | כִּי | for | 1.78 | tied |
| Lev 24:15 w6-w12 | Lev 24:23 w1-w14 | H7043 | קָלַל | to lighten | 5.69 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H0413 | אֶל | to(wards) | 1.71 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H1696 | דָבַר | speak | 3.10 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w1-w14 | H3478 | יִשְׂרָאֵל | Israel | 2.34 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w15-w22 | H1121 | בֵּן | child | 1.85 | tied |
| Lev 24:15 w1-w5 | Lev 24:23 w15-w22 | H3478 | יִשְׂרָאֵל | Israel | 2.34 | tied |
| Lev 24:14 w14-w17 | Lev 24:23 w1-w14 | H7275 | רָגַם | to stone | 7.35 | parallel |

##### 23. Isa 44:27 w4 to Isa 45:10 w8 (n = 23, centre the unit Isa 45:5 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Isa 45:5 w1 | 23 | 10 | 2229.87 | 344.78 | 0.732 | 84.15 | 6.03e-7 | sampled, B = 1000000000, 602 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0080, q (BY) 0.1061: mirror order exceeds parallel order and the permutation null at q = 0.0080. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Isa 45:4 w6-w11 | Isa 45:5 w8-w10 | H3808 | לֹא | not | 1.77 |  |
| Isa 45:4 w6-w11 | Isa 45:5 w8-w10 | H3045 | יָדַע | to know | 3.28 | tied |
| Isa 45:4 w6-w11 | Isa 45:6 w1-w8 | H3045 | יָדַע | to know | 3.28 | tied |
| Isa 45:4 w1-w5 | Isa 45:6 w1-w8 | H4616 | מַ֫עַן | because | 4.53 | tied |
| Isa 45:3 w7-w15 | Isa 45:5 w8-w10 | H3045 | יָדַע | to know | 3.28 | parallel |
| Isa 45:3 w7-w15 | Isa 45:6 w1-w8 | H3588 | כִּי | for | 1.78 | tied |
| Isa 45:3 w7-w15 | Isa 45:6 w1-w8 | H3045 | יָדַע | to know | 3.28 | tied |
| Isa 45:3 w7-w15 | Isa 45:6 w1-w8 | H4616 | מַ֫עַן | because | 4.53 | tied |
| Isa 45:3 w7-w15 | Isa 45:6 w9-w12 | H3068 | יהוה | LORD | 1.44 | tied |
| Isa 45:3 w7-w15 | Isa 45:6 w9-w12 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Isa 45:3 w7-w15 | Isa 45:7 w9-w13 | H3068 | יהוה | LORD | 1.44 | tied |
| Isa 45:3 w7-w15 | Isa 45:7 w9-w13 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Isa 45:3 w7-w15 | Isa 45:8 w7-w16 | H3068 | יהוה | LORD | 1.44 | tied |
| Isa 45:3 w7-w15 | Isa 45:8 w7-w16 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Isa 45:3 w1-w6 | Isa 45:7 w1-w8 | H2822 | חֹ֫שֶׁךְ | darkness | 5.71 | parallel |
| Isa 45:2 w1-w5 | Isa 45:6 w9-w12 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | parallel |
| Isa 45:2 w1-w5 | Isa 45:7 w9-w13 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Isa 45:2 w1-w5 | Isa 45:8 w7-w16 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Isa 45:1 w15-w20 | Isa 45:5 w8-w10 | H3808 | לֹא | not | 1.77 | parallel |
| Isa 45:1 w15-w20 | Isa 45:8 w7-w16 | H6605 | פָּתַח | to open | 5.16 | tied |
| Isa 45:1 w1-w14 | Isa 45:6 w9-w12 | H3068 | יהוה | LORD | 1.44 | parallel |
| Isa 45:1 w1-w14 | Isa 45:7 w9-w13 | H3068 | יהוה | LORD | 1.44 | tied |
| Isa 45:1 w1-w14 | Isa 45:8 w7-w16 | H3068 | יהוה | LORD | 1.44 | tied |
| Isa 45:1 w1-w14 | Isa 45:8 w7-w16 | H6605 | פָּתַח | to open | 5.16 | tied |
| Isa 45:1 w1-w14 | Isa 45:9 w9-w17 | H0559 | אָמַר | to say | 1.68 | tied |
| Isa 45:1 w1-w14 | Isa 45:10 w1-w5 | H0559 | אָמַר | to say | 1.68 | tied |
| Isa 44:28 w7-w11 | Isa 45:9 w9-w17 | H0559 | אָמַר | to say | 1.68 | parallel |
| Isa 44:28 w7-w11 | Isa 45:10 w1-w5 | H0559 | אָמַר | to say | 1.68 | tied |
| Isa 44:28 w1-w6 | Isa 45:7 w9-w13 | H3605 | כֹּל | all | 1.70 | parallel |
| Isa 44:28 w1-w6 | Isa 45:9 w9-w17 | H0559 | אָמַר | to say | 1.68 | tied |

##### 24. Isa 44:28 w1 to Isa 45:10 w5 (n = 21, centre the unit Isa 45:5 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Isa 45:5 w1 | 21 | 10 | 2229.87 | 344.78 | 0.732 | 84.15 | 6.03e-7 | sampled, B = 1000000000, 602 as high | 1.00e-9 | 5.00e-5 (sampled, B = 99999, 4 as high) |

q (BH) 0.0080, q (BY) 0.1061: mirror order exceeds parallel order and the permutation null at q = 0.0080. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Isa 45:4 w6-w11 | Isa 45:5 w8-w10 | H3808 | לֹא | not | 1.77 |  |
| Isa 45:4 w6-w11 | Isa 45:5 w8-w10 | H3045 | יָדַע | to know | 3.28 | tied |
| Isa 45:4 w6-w11 | Isa 45:6 w1-w8 | H3045 | יָדַע | to know | 3.28 | tied |
| Isa 45:4 w1-w5 | Isa 45:6 w1-w8 | H4616 | מַ֫עַן | because | 4.53 | tied |
| Isa 45:3 w7-w15 | Isa 45:5 w8-w10 | H3045 | יָדַע | to know | 3.28 | parallel |
| Isa 45:3 w7-w15 | Isa 45:6 w1-w8 | H3588 | כִּי | for | 1.78 | tied |
| Isa 45:3 w7-w15 | Isa 45:6 w1-w8 | H3045 | יָדַע | to know | 3.28 | tied |
| Isa 45:3 w7-w15 | Isa 45:6 w1-w8 | H4616 | מַ֫עַן | because | 4.53 | tied |
| Isa 45:3 w7-w15 | Isa 45:6 w9-w12 | H3068 | יהוה | LORD | 1.44 | tied |
| Isa 45:3 w7-w15 | Isa 45:6 w9-w12 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Isa 45:3 w7-w15 | Isa 45:7 w9-w13 | H3068 | יהוה | LORD | 1.44 | tied |
| Isa 45:3 w7-w15 | Isa 45:7 w9-w13 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Isa 45:3 w7-w15 | Isa 45:8 w7-w16 | H3068 | יהוה | LORD | 1.44 | tied |
| Isa 45:3 w7-w15 | Isa 45:8 w7-w16 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Isa 45:3 w1-w6 | Isa 45:7 w1-w8 | H2822 | חֹ֫שֶׁךְ | darkness | 5.71 | parallel |
| Isa 45:2 w1-w5 | Isa 45:6 w9-w12 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | parallel |
| Isa 45:2 w1-w5 | Isa 45:7 w9-w13 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Isa 45:2 w1-w5 | Isa 45:8 w7-w16 | H0589 | אֲנִי, אָֽנֹכִ֫י | I | 3.37 | tied |
| Isa 45:1 w15-w20 | Isa 45:5 w8-w10 | H3808 | לֹא | not | 1.77 | parallel |
| Isa 45:1 w15-w20 | Isa 45:8 w7-w16 | H6605 | פָּתַח | to open | 5.16 | tied |
| Isa 45:1 w1-w14 | Isa 45:6 w9-w12 | H3068 | יהוה | LORD | 1.44 | parallel |
| Isa 45:1 w1-w14 | Isa 45:7 w9-w13 | H3068 | יהוה | LORD | 1.44 | tied |
| Isa 45:1 w1-w14 | Isa 45:8 w7-w16 | H3068 | יהוה | LORD | 1.44 | tied |
| Isa 45:1 w1-w14 | Isa 45:8 w7-w16 | H6605 | פָּתַח | to open | 5.16 | tied |
| Isa 45:1 w1-w14 | Isa 45:9 w9-w17 | H0559 | אָמַר | to say | 1.68 | tied |
| Isa 45:1 w1-w14 | Isa 45:10 w1-w5 | H0559 | אָמַר | to say | 1.68 | tied |
| Isa 44:28 w7-w11 | Isa 45:9 w9-w17 | H0559 | אָמַר | to say | 1.68 | parallel |
| Isa 44:28 w7-w11 | Isa 45:10 w1-w5 | H0559 | אָמַר | to say | 1.68 | tied |
| Isa 44:28 w1-w6 | Isa 45:7 w9-w13 | H3605 | כֹּל | all | 1.70 | parallel |
| Isa 44:28 w1-w6 | Isa 45:9 w9-w17 | H0559 | אָמַר | to say | 1.68 | tied |

##### 25. Lev 4:6 w1 to Lev 4:17 w5 (n = 23, centre the unit Lev 4:11 w11)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Lev 4:11 w11 | 23 | 16 | 26678.75 | 10732.26 | 0.426 | 311.01 | 6.31e-7 | sampled, B = 1000000000, 630 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0080, q (BY) 0.1066: mirror order exceeds parallel order and the permutation null at q = 0.0080. Flags: none.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Lev 4:11 w1-w10 | Lev 4:12 w1-w18 | H5921 | עַל | upon | 1.64 |  |
| Lev 4:11 w1-w10 | Lev 4:12 w1-w18 | H3605 | כֹּל | all | 1.70 | tied |
| Lev 4:11 w1-w10 | Lev 4:12 w1-w18 | H6499 | פַּר | bullock | 5.28 | tied |
| Lev 4:11 w1-w10 | Lev 4:12 w19-w22 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:11 w1-w10 | Lev 4:13 w1-w9 | H3605 | כֹּל | all | 1.70 | tied |
| Lev 4:11 w1-w10 | Lev 4:13 w10-w18 | H3605 | כֹּל | all | 1.70 | tied |
| Lev 4:11 w1-w10 | Lev 4:14 w1-w5 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:11 w1-w10 | Lev 4:14 w6-w16 | H6499 | פַּר | bullock | 5.28 | tied |
| Lev 4:11 w1-w10 | Lev 4:15 w1-w10 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:11 w1-w10 | Lev 4:15 w1-w10 | H7218 | רֹאשׁ | head | 3.75 | tied |
| Lev 4:11 w1-w10 | Lev 4:15 w1-w10 | H6499 | פַּר | bullock | 5.28 | tied |
| Lev 4:11 w1-w10 | Lev 4:15 w11-w15 | H6499 | פַּר | bullock | 5.28 | tied |
| Lev 4:11 w1-w10 | Lev 4:16 w1-w5 | H6499 | פַּר | bullock | 5.28 | tied |
| Lev 4:10 w6-w10 | Lev 4:12 w1-w18 | H5921 | עַל | upon | 1.64 | parallel |
| Lev 4:10 w6-w10 | Lev 4:12 w19-w22 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:10 w6-w10 | Lev 4:14 w1-w5 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:10 w6-w10 | Lev 4:15 w1-w10 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:10 w6-w10 | Lev 4:16 w1-w5 | H3548 | כֹּהֵן | priest | 3.57 | tied |
| Lev 4:10 w6-w10 | Lev 4:17 w1-w5 | H3548 | כֹּהֵן | priest | 3.57 | tied |
| Lev 4:10 w1-w5 | Lev 4:13 w10-w18 | H0834 | אֲשֶׁר | which | 1.66 | parallel |
| Lev 4:10 w1-w5 | Lev 4:14 w1-w5 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Lev 4:9 w11-w17 | Lev 4:12 w1-w18 | H5921 | עַל | upon | 1.64 | parallel |
| Lev 4:9 w11-w17 | Lev 4:12 w19-w22 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:9 w11-w17 | Lev 4:14 w1-w5 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:9 w11-w17 | Lev 4:15 w1-w10 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:9 w1-w10 | Lev 4:12 w1-w18 | H5921 | עַל | upon | 1.64 | parallel |
| Lev 4:9 w1-w10 | Lev 4:12 w19-w22 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:9 w1-w10 | Lev 4:13 w10-w18 | H0834 | אֲשֶׁר | which | 1.66 | tied |
| Lev 4:9 w1-w10 | Lev 4:14 w1-w5 | H5921 | עַל | upon | 1.64 | tied |
| Lev 4:9 w1-w10 | Lev 4:14 w1-w5 | H0834 | אֲשֶׁר | which | 1.66 | tied |

#### Greek NT (clause units)

Screened m = 47984, Tarone K = 47984. Windows with BH q <= 0.10: 27; with Benjamini-Yekutieli q <= 0.10: 0. Sealed file `chiasm-sealed-greek-clauses.tsv` (sha256 `95fae450b1cb0375`).

##### 1. Mark 8:32 w6 to Mark 9:2 w28 (n = 20, centre before Mark 8:35 w11)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Mark 8:35 w11 | 20 | 8 | 745.37 | 15.93 | 0.958 | 47.28 | 1.72e-6 | sampled, B = 1000000000, 1718 as high | 2.07e-7 | 1.90e-4 (sampled, B = 99999, 18 as high) |

q (BH) 0.0825, q (BY) 0.9367: mirror order exceeds parallel order and the permutation null at q = 0.0825. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Mark 8:35 w9-w10 | Mark 8:35 w11-w22 | G0622 | ἀπολλύω | to destroy | 4.54 |  |
| Mark 8:35 w1-w8 | Mark 8:35 w11-w22 | G5590 | ψυχή | soul | 4.45 | tied |
| Mark 8:35 w1-w8 | Mark 8:35 w24-w25 | G4982 | σῴζω | to save | 4.38 | tied |
| Mark 8:35 w1-w8 | Mark 8:36 w1-w15 | G5590 | ψυχή | soul | 4.45 | tied |
| Mark 8:35 w1-w8 | Mark 8:37 w2-w9 | G5590 | ψυχή | soul | 4.45 | tied |
| Mark 8:33 w18-w27 | Mark 8:36 w1-w15 | G0444 | ἄνθρωπος | a human | 2.77 | parallel |
| Mark 8:33 w18-w27 | Mark 8:37 w2-w9 | G0444 | ἄνθρωπος | a human | 2.77 | tied |
| Mark 8:33 w18-w27 | Mark 8:38 w18-w37 | G0444 | ἄνθρωπος | a human | 2.77 | tied |
| Mark 8:33 w18-w27 | Mark 9:1 w4-w27 | G2316 | θεός | God | 1.93 | tied |
| Mark 8:33 w1-w13 | Mark 9:1 w1-w3 | G3004 | λέγω | to speak | 1.87 | parallel |
| Mark 8:33 w1-w13 | Mark 9:1 w4-w27 | G3004 | λέγω | to speak | 1.87 | tied |
| Mark 8:33 w1-w13 | Mark 9:1 w4-w27 | G1492 | εἴδω | to perceive | 3.09 | tied |
| Mark 8:33 w1-w13 | Mark 9:2 w1-w24 | G4074 | Πέτρος | Peter | 3.97 | tied |
| Mark 8:32 w6-w13 | Mark 9:2 w1-w24 | G4074 | Πέτρος | Peter | 3.97 | tied |

##### 2. Mark 8:33 w1 to Mark 9:2 w24 (n = 18, centre before Mark 8:35 w11)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Mark 8:35 w11 | 18 | 8 | 589.17 | 15.93 | 0.947 | 43.31 | 1.22e-5 | sampled, B = 10000000, 121 as high | 1.03e-6 | 2.10e-4 (sampled, B = 99999, 20 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Mark 8:35 w9-w10 | Mark 8:35 w11-w22 | G0622 | ἀπολλύω | to destroy | 4.54 |  |
| Mark 8:35 w1-w8 | Mark 8:35 w11-w22 | G5590 | ψυχή | soul | 4.45 | tied |
| Mark 8:35 w1-w8 | Mark 8:35 w24-w25 | G4982 | σῴζω | to save | 4.38 | tied |
| Mark 8:35 w1-w8 | Mark 8:36 w1-w15 | G5590 | ψυχή | soul | 4.45 | tied |
| Mark 8:35 w1-w8 | Mark 8:37 w2-w9 | G5590 | ψυχή | soul | 4.45 | tied |
| Mark 8:33 w18-w27 | Mark 8:36 w1-w15 | G0444 | ἄνθρωπος | a human | 2.77 | parallel |
| Mark 8:33 w18-w27 | Mark 8:37 w2-w9 | G0444 | ἄνθρωπος | a human | 2.77 | tied |
| Mark 8:33 w18-w27 | Mark 8:38 w18-w37 | G0444 | ἄνθρωπος | a human | 2.77 | tied |
| Mark 8:33 w18-w27 | Mark 9:1 w4-w27 | G2316 | θεός | God | 1.93 | tied |
| Mark 8:33 w1-w13 | Mark 9:1 w1-w3 | G3004 | λέγω | to speak | 1.87 | parallel |
| Mark 8:33 w1-w13 | Mark 9:1 w4-w27 | G3004 | λέγω | to speak | 1.87 | tied |
| Mark 8:33 w1-w13 | Mark 9:1 w4-w27 | G1492 | εἴδω | to perceive | 3.09 | tied |
| Mark 8:33 w1-w13 | Mark 9:2 w1-w24 | G4074 | Πέτρος | Peter | 3.97 | tied |

##### 3. 2Cor 3:9 w1 to 2Cor 4:3 w8 (n = 24, centre before 2Cor 3:16 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before 2Cor 3:16 w1 | 24 | 8 | 3218.02 | 556.70 | 0.705 | 103.85 | 1.26e-5 | sampled, B = 10000000, 125 as high | 2.30e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 2Cor 3:15 w8-w13 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 |  |
| 2Cor 3:15 w1-w7 | 2Cor 3:16 w1-w6 | G2259 | ἡνίκα | when | 8.29 | parallel |
| 2Cor 3:14 w6-w22 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 | mirror |
| 2Cor 3:14 w6-w22 | 2Cor 3:18 w1-w9 | G0343 | ἀνακαλύπτω | to unveil | 8.29 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 | parallel |
| 2Cor 3:13 w1-w22 | 2Cor 3:18 w1-w9 | G4383 | πρόσωπον | face | 4.72 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:18 w10-w21 | G2509 | καθάπερ | just as | 6.42 | tied |
| 2Cor 3:12 w1-w7 | 2Cor 4:1 w1-w8 | G2192 | ἔχω | to have/be | 2.54 | mirror |
| 2Cor 3:11 w7-w12 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:11 w7-w12 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:11 w1-w6 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:11 w1-w6 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:10 w1-w14 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:10 w1-w14 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w8-w16 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:9 w8-w16 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w8-w16 | 2Cor 4:1 w1-w8 | G1248 | διακονία | service | 5.52 | tied |
| 2Cor 3:9 w1-w7 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:9 w1-w7 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w1-w7 | 2Cor 4:1 w1-w8 | G1248 | διακονία | service | 5.52 | tied |

##### 4. 2Thess 1:11 w1 to 2Thess 2:13 w9 (n = 21, centre the unit 2Thess 2:4 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit 2Thess 2:4 w1 | 21 | 9 | 1130.00 | 47.31 | 0.920 | 61.79 | 1.46e-5 | sampled, B = 10000000, 145 as high | 1.93e-6 | 4.20e-4 (sampled, B = 99999, 41 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 2Thess 2:3 w8-w20 | 2Thess 2:6 w1-w13 | G0601 | ἀποκαλύπτω | to reveal | 5.72 |  |
| 2Thess 2:3 w8-w20 | 2Thess 2:7 w1-w7 | G0458 | ἀνομία | lawlessness | 6.42 | tied |
| 2Thess 2:3 w8-w20 | 2Thess 2:8 w1-w22 | G0601 | ἀποκαλύπτω | to reveal | 5.72 | tied |
| 2Thess 2:2 w24-w30 | 2Thess 2:8 w1-w22 | G2962 | κύριος | lord | 2.49 | tied |
| 2Thess 2:2 w12-w23 | 2Thess 2:8 w1-w22 | G4151 | πνεῦμα | spirit/breath | 3.14 | tied |
| 2Thess 2:1 w5 to 2Thess 2:2 w11 | 2Thess 2:8 w1-w22 | G2424 | Ἰησοῦς | Jesus/Joshua | 2.20 | tied |
| 2Thess 2:1 w5 to 2Thess 2:2 w11 | 2Thess 2:8 w1-w22 | G2962 | κύριος | lord | 2.49 | tied |
| 2Thess 2:1 w5 to 2Thess 2:2 w11 | 2Thess 2:8 w1-w22 | G3952 | παρουσία | coming | 5.80 | tied |
| 2Thess 2:1 w5 to 2Thess 2:2 w11 | 2Thess 2:9 w1 to 2Thess 2:10 w9 | G3952 | παρουσία | coming | 5.80 | tied |
| 2Thess 1:12 w1-w25 | 2Thess 2:8 w1-w22 | G2424 | Ἰησοῦς | Jesus/Joshua | 2.20 | parallel |
| 2Thess 1:12 w1-w25 | 2Thess 2:8 w1-w22 | G2962 | κύριος | lord | 2.49 | tied |
| 2Thess 1:12 w1-w25 | 2Thess 2:11 w1-w15 | G2316 | θεός | God | 1.93 | tied |
| 2Thess 1:12 w1-w25 | 2Thess 2:13 w1-w9 | G2316 | θεός | God | 1.93 | tied |
| 2Thess 1:11 w1-w25 | 2Thess 2:9 w1 to 2Thess 2:10 w9 | G1411 | δύναμις | power | 4.24 | parallel |
| 2Thess 1:11 w1-w25 | 2Thess 2:11 w1-w15 | G2316 | θεός | God | 1.93 | tied |
| 2Thess 1:11 w1-w25 | 2Thess 2:13 w1-w9 | G2316 | θεός | God | 1.93 | tied |
| 2Thess 1:11 w1-w25 | 2Thess 2:13 w1-w9 | G3842 | πάντοτε | always | 5.34 | tied |

##### 5. Mark 8:32 w6 to Mark 9:2 w24 (n = 19, centre the unit Mark 8:35 w9)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Mark 8:35 w9 | 19 | 7 | 571.57 | 15.93 | 0.946 | 42.74 | 1.80e-5 | sampled, B = 10000000, 179 as high | 1.03e-6 | 4.70e-4 (sampled, B = 99999, 46 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Mark 8:35 w1-w8 | Mark 8:35 w11-w22 | G5590 | ψυχή | soul | 4.45 |  |
| Mark 8:35 w1-w8 | Mark 8:35 w24-w25 | G4982 | σῴζω | to save | 4.38 | tied |
| Mark 8:35 w1-w8 | Mark 8:36 w1-w15 | G5590 | ψυχή | soul | 4.45 | tied |
| Mark 8:35 w1-w8 | Mark 8:37 w2-w9 | G5590 | ψυχή | soul | 4.45 | tied |
| Mark 8:33 w18-w27 | Mark 8:36 w1-w15 | G0444 | ἄνθρωπος | a human | 2.77 | parallel |
| Mark 8:33 w18-w27 | Mark 8:37 w2-w9 | G0444 | ἄνθρωπος | a human | 2.77 | tied |
| Mark 8:33 w18-w27 | Mark 8:38 w18-w37 | G0444 | ἄνθρωπος | a human | 2.77 | tied |
| Mark 8:33 w18-w27 | Mark 9:1 w4-w27 | G2316 | θεός | God | 1.93 | tied |
| Mark 8:33 w1-w13 | Mark 9:1 w1-w3 | G3004 | λέγω | to speak | 1.87 | parallel |
| Mark 8:33 w1-w13 | Mark 9:1 w4-w27 | G3004 | λέγω | to speak | 1.87 | tied |
| Mark 8:33 w1-w13 | Mark 9:1 w4-w27 | G1492 | εἴδω | to perceive | 3.09 | tied |
| Mark 8:33 w1-w13 | Mark 9:2 w1-w24 | G4074 | Πέτρος | Peter | 3.97 | tied |
| Mark 8:32 w6-w13 | Mark 9:2 w1-w24 | G4074 | Πέτρος | Peter | 3.97 | tied |

##### 6. Rom 6:21 w10 to Rom 7:5 w24 (n = 23, centre the unit Rom 7:2 w15)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Rom 7:2 w15 | 23 | 9 | 3189.90 | 650.82 | 0.661 | 104.34 | 1.97e-5 | sampled, B = 10000000, 196 as high | 1.00e-9 | 2.30e-4 (sampled, B = 99999, 22 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Rom 7:2 w10-w14 | Rom 7:3 w1-w7 | G0435 | ἀνήρ | man | 3.71 |  |
| Rom 7:2 w10-w14 | Rom 7:3 w8-w11 | G0435 | ἀνήρ | man | 3.71 | tied |
| Rom 7:2 w10-w14 | Rom 7:3 w12-w16 | G0435 | ἀνήρ | man | 3.71 | tied |
| Rom 7:2 w10-w14 | Rom 7:3 w12-w16 | G0599 | ἀποθνήσκω | to die | 4.38 | tied |
| Rom 7:2 w10-w14 | Rom 7:3 w17-w29 | G0435 | ἀνήρ | man | 3.71 | tied |
| Rom 7:2 w1-w9 | Rom 7:3 w1-w7 | G0435 | ἀνήρ | man | 3.71 | parallel |
| Rom 7:2 w1-w9 | Rom 7:3 w1-w7 | G2198 | ζάω | to live | 4.16 | tied |
| Rom 7:2 w1-w9 | Rom 7:3 w8-w11 | G0435 | ἀνήρ | man | 3.71 | tied |
| Rom 7:2 w1-w9 | Rom 7:3 w12-w16 | G0435 | ἀνήρ | man | 3.71 | tied |
| Rom 7:2 w1-w9 | Rom 7:3 w17-w29 | G0435 | ἀνήρ | man | 3.71 | tied |
| Rom 7:2 w1-w9 | Rom 7:3 w17-w29 | G3551 | νόμος | law | 3.94 | tied |
| Rom 7:2 w1-w9 | Rom 7:4 w4-w18 | G3551 | νόμος | law | 3.94 | tied |
| Rom 7:2 w1-w9 | Rom 7:5 w7-w24 | G3551 | νόμος | law | 3.94 | tied |
| Rom 7:1 w8-w17 | Rom 7:3 w1-w7 | G2198 | ζάω | to live | 4.16 | parallel |
| Rom 7:1 w8-w17 | Rom 7:3 w17-w29 | G3551 | νόμος | law | 3.94 | tied |
| Rom 7:1 w8-w17 | Rom 7:4 w4-w18 | G3551 | νόμος | law | 3.94 | tied |
| Rom 7:1 w8-w17 | Rom 7:5 w7-w24 | G3551 | νόμος | law | 3.94 | tied |
| Rom 7:1 w4-w7 | Rom 7:3 w17-w29 | G3551 | νόμος | law | 3.94 | parallel |
| Rom 7:1 w4-w7 | Rom 7:4 w4-w18 | G3551 | νόμος | law | 3.94 | tied |
| Rom 7:1 w4-w7 | Rom 7:5 w7-w24 | G3551 | νόμος | law | 3.94 | tied |
| Rom 7:1 w3 | Rom 7:4 w2-w3 | G0080 | ἀδελφός | brother | 3.22 | parallel |
| Rom 6:23 w7-w19 | Rom 7:4 w4-w18 | G5547 | Χριστός | Christ | 2.77 | mirror |
| Rom 6:23 w7-w19 | Rom 7:4 w23-w26 | G2316 | θεός | God | 1.93 | tied |
| Rom 6:23 w1-w6 | Rom 7:5 w7-w24 | G0266 | ἁμαρτία | sin | 3.97 | mirror |
| Rom 6:23 w1-w6 | Rom 7:5 w7-w24 | G2288 | θάνατος | death | 4.32 | tied |
| Rom 6:22 w1-w16 | Rom 7:4 w23-w26 | G2316 | θεός | God | 1.93 | parallel |
| Rom 6:22 w1-w16 | Rom 7:5 w7-w24 | G0266 | ἁμαρτία | sin | 3.97 | tied |
| Rom 6:21 w10-w14 | Rom 7:5 w7-w24 | G2288 | θάνατος | death | 4.32 | tied |

##### 7. 2Cor 3:9 w1 to 2Cor 4:2 w30 (n = 23, centre the unit 2Cor 3:15 w8)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit 2Cor 3:15 w8 | 23 | 8 | 2665.23 | 493.74 | 0.687 | 96.26 | 2.30e-5 | sampled, B = 10000000, 229 as high | 2.30e-8 | 2.00e-5 (sampled, B = 99999, 1 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 2Cor 3:15 w1-w7 | 2Cor 3:16 w1-w6 | G2259 | ἡνίκα | when | 8.29 |  |
| 2Cor 3:14 w6-w22 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 | mirror |
| 2Cor 3:14 w6-w22 | 2Cor 3:18 w1-w9 | G0343 | ἀνακαλύπτω | to unveil | 8.29 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 | parallel |
| 2Cor 3:13 w1-w22 | 2Cor 3:18 w1-w9 | G4383 | πρόσωπον | face | 4.72 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:18 w10-w21 | G2509 | καθάπερ | just as | 6.42 | tied |
| 2Cor 3:12 w1-w7 | 2Cor 4:1 w1-w8 | G2192 | ἔχω | to have/be | 2.54 | mirror |
| 2Cor 3:11 w7-w12 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:11 w7-w12 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:11 w1-w6 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:11 w1-w6 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:10 w1-w14 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:10 w1-w14 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w8-w16 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:9 w8-w16 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w8-w16 | 2Cor 4:1 w1-w8 | G1248 | διακονία | service | 5.52 | tied |
| 2Cor 3:9 w1-w7 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:9 w1-w7 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w1-w7 | 2Cor 4:1 w1-w8 | G1248 | διακονία | service | 5.52 | tied |

##### 8. Matt 17:4 w9 to Matt 17:12 w17 (n = 20, centre before Matt 17:7 w5)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Matt 17:7 w5 | 20 | 8 | 736.39 | 63.90 | 0.840 | 46.23 | 2.67e-5 | sampled, B = 10000000, 266 as high | 1.00e-9 | 1.20e-4 (sampled, B = 99999, 11 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial; division-dependent (no window at q <= 0.10 over these words under verse units).

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Matt 17:7 w1-w4 | Matt 17:8 w1-w12 | G2424 | Ἰησοῦς | Jesus/Joshua | 2.20 |  |
| Matt 17:7 w1-w4 | Matt 17:9 w1-w11 | G2424 | Ἰησοῦς | Jesus/Joshua | 2.20 | tied |
| Matt 17:6 w1-w11 | Matt 17:7 w9-w12 | G5399 | φοβέω | to fear | 4.46 | parallel |
| Matt 17:6 w1-w11 | Matt 17:10 w1-w7 | G3101 | μαθητής | disciple | 3.48 | tied |
| Matt 17:5 w16-w25 | Matt 17:9 w12-w24 | G5207 | υἱός | son | 3.14 | parallel |
| Matt 17:5 w9-w15 | Matt 17:9 w1-w11 | G3004 | λέγω | to speak | 1.87 | parallel |
| Matt 17:5 w9-w15 | Matt 17:10 w1-w7 | G3004 | λέγω | to speak | 1.87 | tied |
| Matt 17:5 w9-w15 | Matt 17:10 w8-w17 | G3004 | λέγω | to speak | 1.87 | tied |
| Matt 17:5 w9-w15 | Matt 17:12 w1-w7 | G3004 | λέγω | to speak | 1.87 | tied |
| Matt 17:4 w20-w27 | Matt 17:10 w8-w17 | G2243 | Ἡλίας | Elijah | 5.61 | parallel |
| Matt 17:4 w20-w27 | Matt 17:11 w1-w13 | G2243 | Ἡλίας | Elijah | 5.61 | tied |
| Matt 17:4 w20-w27 | Matt 17:12 w1-w7 | G2243 | Ἡλίας | Elijah | 5.61 | tied |
| Matt 17:4 w16-w19 | Matt 17:12 w8-w17 | G4160 | ποιέω | to do/make | 2.74 | mirror |
| Matt 17:4 w14-w15 | Matt 17:12 w8-w17 | G2309 | θέλω | to will/desire | 3.69 | tied |

##### 9. Matt 17:4 w14 to Matt 17:12 w17 (n = 19, centre the unit Matt 17:7 w5)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Matt 17:7 w5 | 19 | 8 | 736.39 | 63.90 | 0.840 | 46.23 | 2.67e-5 | sampled, B = 10000000, 266 as high | 1.00e-9 | 3.60e-4 (sampled, B = 99999, 35 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial; division-dependent (no window at q <= 0.10 over these words under verse units).

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Matt 17:7 w1-w4 | Matt 17:8 w1-w12 | G2424 | Ἰησοῦς | Jesus/Joshua | 2.20 |  |
| Matt 17:7 w1-w4 | Matt 17:9 w1-w11 | G2424 | Ἰησοῦς | Jesus/Joshua | 2.20 | tied |
| Matt 17:6 w1-w11 | Matt 17:7 w9-w12 | G5399 | φοβέω | to fear | 4.46 | parallel |
| Matt 17:6 w1-w11 | Matt 17:10 w1-w7 | G3101 | μαθητής | disciple | 3.48 | tied |
| Matt 17:5 w16-w25 | Matt 17:9 w12-w24 | G5207 | υἱός | son | 3.14 | parallel |
| Matt 17:5 w9-w15 | Matt 17:9 w1-w11 | G3004 | λέγω | to speak | 1.87 | parallel |
| Matt 17:5 w9-w15 | Matt 17:10 w1-w7 | G3004 | λέγω | to speak | 1.87 | tied |
| Matt 17:5 w9-w15 | Matt 17:10 w8-w17 | G3004 | λέγω | to speak | 1.87 | tied |
| Matt 17:5 w9-w15 | Matt 17:12 w1-w7 | G3004 | λέγω | to speak | 1.87 | tied |
| Matt 17:4 w20-w27 | Matt 17:10 w8-w17 | G2243 | Ἡλίας | Elijah | 5.61 | parallel |
| Matt 17:4 w20-w27 | Matt 17:11 w1-w13 | G2243 | Ἡλίας | Elijah | 5.61 | tied |
| Matt 17:4 w20-w27 | Matt 17:12 w1-w7 | G2243 | Ἡλίας | Elijah | 5.61 | tied |
| Matt 17:4 w16-w19 | Matt 17:12 w8-w17 | G4160 | ποιέω | to do/make | 2.74 | mirror |
| Matt 17:4 w14-w15 | Matt 17:12 w8-w17 | G2309 | θέλω | to will/desire | 3.69 | tied |

##### 10. Mark 12:16 w14 to Mark 12:27 w12 (n = 24, centre before Mark 12:22 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Mark 12:22 w1 | 24 | 11 | 2513.83 | 664.84 | 0.582 | 97.19 | 3.35e-5 | sampled, B = 10000000, 334 as high | 1.00e-9 | 0.0011 (sampled, B = 99999, 112 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Mark 12:21 w1-w16 | Mark 12:22 w1-w9 | G4690 | σπέρμα | seed | 5.29 |  |
| Mark 12:21 w1-w16 | Mark 12:22 w10-w15 | G0599 | ἀποθνήσκω | to die | 4.38 | tied |
| Mark 12:20 w4-w13 | Mark 12:22 w1-w9 | G0863 | ἀφίημι | to release | 4.09 | parallel |
| Mark 12:20 w4-w13 | Mark 12:22 w1-w9 | G4690 | σπέρμα | seed | 5.29 | tied |
| Mark 12:20 w4-w13 | Mark 12:22 w10-w15 | G1135 | γυνή | woman | 3.71 | tied |
| Mark 12:20 w4-w13 | Mark 12:22 w10-w15 | G0599 | ἀποθνήσκω | to die | 4.38 | tied |
| Mark 12:20 w4-w13 | Mark 12:23 w1-w10 | G1135 | γυνή | woman | 3.71 | tied |
| Mark 12:20 w4-w13 | Mark 12:23 w11-w16 | G1135 | γυνή | woman | 3.71 | tied |
| Mark 12:20 w1-w3 | Mark 12:22 w1-w9 | G2033 | ἑπτά | seven | 4.85 | parallel |
| Mark 12:20 w1-w3 | Mark 12:23 w11-w16 | G2033 | ἑπτά | seven | 4.85 | tied |
| Mark 12:19 w2-w30 | Mark 12:22 w1-w9 | G0863 | ἀφίημι | to release | 4.09 | parallel |
| Mark 12:19 w2-w30 | Mark 12:22 w1-w9 | G4690 | σπέρμα | seed | 5.29 | tied |
| Mark 12:19 w2-w30 | Mark 12:22 w10-w15 | G1135 | γυνή | woman | 3.71 | tied |
| Mark 12:19 w2-w30 | Mark 12:22 w10-w15 | G0599 | ἀποθνήσκω | to die | 4.38 | tied |
| Mark 12:19 w2-w30 | Mark 12:23 w1-w10 | G1135 | γυνή | woman | 3.71 | tied |
| Mark 12:19 w2-w30 | Mark 12:23 w11-w16 | G1135 | γυνή | woman | 3.71 | tied |
| Mark 12:19 w2-w30 | Mark 12:26 w7-w21 | G3475 | Μωϋσῆς, Μωσῆς | Moses | 4.61 | tied |
| Mark 12:18 w11-w14 | Mark 12:26 w7-w21 | G3004 | λέγω | to speak | 1.87 | tied |
| Mark 12:18 w1-w10 | Mark 12:23 w1-w10 | G0386 | ἀνάστασις | resurrection | 5.29 | parallel |
| Mark 12:18 w1-w10 | Mark 12:26 w7-w21 | G3004 | λέγω | to speak | 1.87 | tied |
| Mark 12:17 w8-w17 | Mark 12:24 w2-w19 | G2316 | θεός | God | 1.93 | parallel |
| Mark 12:17 w8-w17 | Mark 12:26 w7-w21 | G2316 | θεός | God | 1.93 | tied |
| Mark 12:17 w8-w17 | Mark 12:26 w22-w33 | G2316 | θεός | God | 1.93 | tied |
| Mark 12:17 w8-w17 | Mark 12:27 w1-w8 | G2316 | θεός | God | 1.93 | tied |
| Mark 12:17 w3-w7 | Mark 12:24 w2-w19 | G2424 | Ἰησοῦς | Jesus/Joshua | 2.20 | parallel |
| Mark 12:17 w3-w7 | Mark 12:26 w7-w21 | G2036 | ἔπω, ἐρῶ, εἶπον | to say | 2.22 | tied |
| Mark 12:16 w14-w17 | Mark 12:26 w7-w21 | G2036 | ἔπω, ἐρῶ, εἶπον | to say | 2.22 | tied |

##### 11. Rev 9:12 w6 to Rev 10:1 w11 (n = 21, centre the unit Rev 9:18 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Rev 9:18 w1 | 21 | 14 | 2967.93 | 256.19 | 0.841 | 93.64 | 3.83e-5 | sampled, B = 10000000, 382 as high | 1.00e-9 | 5.30e-4 (sampled, B = 99999, 52 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Rev 9:17 w29-w39 | Rev 9:18 w11-w27 | G1607 | ἐκπορεύω | to depart | 5.46 |  |
| Rev 9:17 w29-w39 | Rev 9:18 w11-w27 | G4442 | πῦρ | fire | 4.72 | tied |
| Rev 9:17 w29-w39 | Rev 9:18 w11-w27 | G4750 | στόμα | mouth | 4.72 | tied |
| Rev 9:17 w29-w39 | Rev 9:18 w11-w27 | G2303 | θεῖον | sulfur | 7.04 | tied |
| Rev 9:17 w29-w39 | Rev 9:18 w11-w27 | G2586 | καπνός | smoke | 6.58 | tied |
| Rev 9:17 w29-w39 | Rev 9:19 w1-w15 | G4750 | στόμα | mouth | 4.72 | tied |
| Rev 9:17 w21-w28 | Rev 9:19 w1-w15 | G2462 | ἵππος | horse | 6.21 | tied |
| Rev 9:17 w21-w28 | Rev 9:19 w16-w27 | G2776 | κεφαλή | head | 4.78 | tied |
| Rev 9:17 w1-w20 | Rev 9:19 w1-w15 | G2462 | ἵππος | horse | 6.21 | parallel |
| Rev 9:17 w1-w20 | Rev 9:19 w16-w27 | G2192 | ἔχω | to have/be | 2.54 | tied |
| Rev 9:17 w1-w20 | Rev 10:1 w1-w11 | G1492 | εἴδω | to perceive | 3.09 | tied |
| Rev 9:16 w11-w14 | Rev 9:20 w43-w50 | G0191 | ἀκούω | to hear | 2.99 | parallel |
| Rev 9:15 w1-w24 | Rev 9:20 w1-w5 | G0444 | ἄνθρωπος | a human | 2.77 | parallel |
| Rev 9:15 w1-w24 | Rev 9:20 w6-w12 | G0615 | ἀποκτείνω | to kill | 4.73 | tied |
| Rev 9:15 w1-w24 | Rev 10:1 w1-w11 | G0032 | ἄγγελος | angel | 3.83 | tied |
| Rev 9:14 w9-w20 | Rev 10:1 w1-w11 | G0032 | ἄγγελος | angel | 3.83 | tied |
| Rev 9:13 w6 to Rev 9:14 w8 | Rev 9:19 w16-w27 | G2192 | ἔχω | to have/be | 2.54 | parallel |
| Rev 9:13 w6 to Rev 9:14 w8 | Rev 9:20 w21-w42 | G5552 | χρύσεος | golden | 6.21 | tied |
| Rev 9:13 w6 to Rev 9:14 w8 | Rev 9:20 w43-w50 | G0191 | ἀκούω | to hear | 2.99 | tied |
| Rev 9:13 w6 to Rev 9:14 w8 | Rev 10:1 w1-w11 | G0032 | ἄγγελος | angel | 3.83 | tied |
| Rev 9:13 w1-w5 | Rev 10:1 w1-w11 | G0032 | ἄγγελος | angel | 3.83 | tied |

##### 12. 2Cor 3:9 w8 to 2Cor 4:2 w30 (n = 22, centre before 2Cor 3:16 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before 2Cor 3:16 w1 | 22 | 8 | 2401.62 | 403.79 | 0.712 | 90.38 | 3.87e-5 | sampled, B = 10000000, 386 as high | 2.30e-8 | 3.00e-5 (sampled, B = 99999, 2 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 2Cor 3:15 w8-w13 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 |  |
| 2Cor 3:15 w1-w7 | 2Cor 3:16 w1-w6 | G2259 | ἡνίκα | when | 8.29 | parallel |
| 2Cor 3:14 w6-w22 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 | mirror |
| 2Cor 3:14 w6-w22 | 2Cor 3:18 w1-w9 | G0343 | ἀνακαλύπτω | to unveil | 8.29 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 | parallel |
| 2Cor 3:13 w1-w22 | 2Cor 3:18 w1-w9 | G4383 | πρόσωπον | face | 4.72 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:18 w10-w21 | G2509 | καθάπερ | just as | 6.42 | tied |
| 2Cor 3:12 w1-w7 | 2Cor 4:1 w1-w8 | G2192 | ἔχω | to have/be | 2.54 | mirror |
| 2Cor 3:11 w7-w12 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:11 w7-w12 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:11 w1-w6 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:11 w1-w6 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:10 w1-w14 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:10 w1-w14 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w8-w16 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:9 w8-w16 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w8-w16 | 2Cor 4:1 w1-w8 | G1248 | διακονία | service | 5.52 | tied |

##### 13. Mark 8:32 w1 to Mark 9:3 w6 (n = 22, centre before Mark 8:35 w11)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Mark 8:35 w11 | 22 | 9 | 835.00 | 78.69 | 0.828 | 50.50 | 4.14e-5 | sampled, B = 10000000, 413 as high | 3.83e-9 | 4.80e-4 (sampled, B = 99999, 47 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Mark 8:35 w9-w10 | Mark 8:35 w11-w22 | G0622 | ἀπολλύω | to destroy | 4.54 |  |
| Mark 8:35 w1-w8 | Mark 8:35 w11-w22 | G5590 | ψυχή | soul | 4.45 | tied |
| Mark 8:35 w1-w8 | Mark 8:35 w24-w25 | G4982 | σῴζω | to save | 4.38 | tied |
| Mark 8:35 w1-w8 | Mark 8:36 w1-w15 | G5590 | ψυχή | soul | 4.45 | tied |
| Mark 8:35 w1-w8 | Mark 8:37 w2-w9 | G5590 | ψυχή | soul | 4.45 | tied |
| Mark 8:33 w18-w27 | Mark 8:36 w1-w15 | G0444 | ἄνθρωπος | a human | 2.77 | parallel |
| Mark 8:33 w18-w27 | Mark 8:37 w2-w9 | G0444 | ἄνθρωπος | a human | 2.77 | tied |
| Mark 8:33 w18-w27 | Mark 8:38 w18-w37 | G0444 | ἄνθρωπος | a human | 2.77 | tied |
| Mark 8:33 w18-w27 | Mark 9:1 w4-w27 | G2316 | θεός | God | 1.93 | tied |
| Mark 8:33 w1-w13 | Mark 9:1 w1-w3 | G3004 | λέγω | to speak | 1.87 | parallel |
| Mark 8:33 w1-w13 | Mark 9:1 w4-w27 | G3004 | λέγω | to speak | 1.87 | tied |
| Mark 8:33 w1-w13 | Mark 9:1 w4-w27 | G1492 | εἴδω | to perceive | 3.09 | tied |
| Mark 8:33 w1-w13 | Mark 9:2 w1-w24 | G4074 | Πέτρος | Peter | 3.97 | tied |
| Mark 8:32 w6-w13 | Mark 9:2 w1-w24 | G4074 | Πέτρος | Peter | 3.97 | tied |
| Mark 8:32 w1-w5 | Mark 8:38 w1-w17 | G3056 | λόγος | word | 3.22 | parallel |

##### 14. 1Cor 15:36 w2 to 1Cor 15:43 w9 (n = 24, centre before 1Cor 15:40 w7)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before 1Cor 15:40 w7 | 24 | 4 | 4147.05 | 547.87 | 0.767 | 109.59 | 4.23e-5 | sampled, B = 10000000, 422 as high | 1.00e-9 | 3.00e-5 (sampled, B = 99999, 2 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial; division-dependent (no window at q <= 0.10 over these words under verse units).

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 1Cor 15:40 w1-w6 | 1Cor 15:40 w7-w13 | G2032 | ἐπουράνιος | heavenly | 6.15 |  |
| 1Cor 15:40 w1-w6 | 1Cor 15:40 w14-w18 | G1919 | ἐπίγειος | earthly | 7.19 | tied |
| 1Cor 15:39 w20-w22 | 1Cor 15:41 w1-w3 | G0243 | ἄλλος | another | 4.07 | mirror |
| 1Cor 15:39 w20-w22 | 1Cor 15:41 w4-w7 | G0243 | ἄλλος | another | 4.07 | tied |
| 1Cor 15:39 w20-w22 | 1Cor 15:41 w8-w11 | G0243 | ἄλλος | another | 4.07 | tied |
| 1Cor 15:39 w16-w19 | 1Cor 15:41 w1-w3 | G0243 | ἄλλος | another | 4.07 | parallel |
| 1Cor 15:39 w16-w19 | 1Cor 15:41 w4-w7 | G0243 | ἄλλος | another | 4.07 | tied |
| 1Cor 15:39 w16-w19 | 1Cor 15:41 w8-w11 | G0243 | ἄλλος | another | 4.07 | tied |
| 1Cor 15:39 w12-w15 | 1Cor 15:41 w1-w3 | G0243 | ἄλλος | another | 4.07 | parallel |
| 1Cor 15:39 w12-w15 | 1Cor 15:41 w4-w7 | G0243 | ἄλλος | another | 4.07 | tied |
| 1Cor 15:39 w12-w15 | 1Cor 15:41 w8-w11 | G0243 | ἄλλος | another | 4.07 | tied |
| 1Cor 15:39 w1-w11 | 1Cor 15:41 w1-w3 | G0243 | ἄλλος | another | 4.07 | parallel |
| 1Cor 15:39 w1-w11 | 1Cor 15:41 w4-w7 | G0243 | ἄλλος | another | 4.07 | tied |
| 1Cor 15:39 w1-w11 | 1Cor 15:41 w8-w11 | G0243 | ἄλλος | another | 4.07 | tied |
| 1Cor 15:37 w4-w12 | 1Cor 15:42 w7-w9 | G4687 | σπείρω | to sow | 5.27 | mirror |
| 1Cor 15:37 w4-w12 | 1Cor 15:43 w1-w3 | G4687 | σπείρω | to sow | 5.27 | tied |
| 1Cor 15:37 w4-w12 | 1Cor 15:43 w7-w9 | G4687 | σπείρω | to sow | 5.27 | tied |
| 1Cor 15:37 w1-w3 | 1Cor 15:42 w7-w9 | G4687 | σπείρω | to sow | 5.27 | parallel |
| 1Cor 15:37 w1-w3 | 1Cor 15:43 w1-w3 | G4687 | σπείρω | to sow | 5.27 | tied |
| 1Cor 15:37 w1-w3 | 1Cor 15:43 w7-w9 | G4687 | σπείρω | to sow | 5.27 | tied |
| 1Cor 15:36 w2-w4 | 1Cor 15:42 w7-w9 | G4687 | σπείρω | to sow | 5.27 | parallel |
| 1Cor 15:36 w2-w4 | 1Cor 15:43 w1-w3 | G4687 | σπείρω | to sow | 5.27 | tied |
| 1Cor 15:36 w2-w4 | 1Cor 15:43 w7-w9 | G4687 | σπείρω | to sow | 5.27 | tied |

##### 15. Rev 21:23 w1 to Rev 22:5 w21 (n = 23, centre the unit Rev 22:1 w11)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit Rev 22:1 w11 | 23 | 13 | 1865.28 | 150.74 | 0.850 | 76.21 | 4.28e-5 | sampled, B = 10000000, 427 as high | 3.44e-8 | 0.0013 (sampled, B = 99999, 127 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Rev 22:1 w1-w7 | Rev 22:2 w1-w8 | G4215 | ποταμός | river | 6.21 |  |
| Rev 22:1 w1-w7 | Rev 22:2 w12-w16 | G2222 | ζωή | life | 4.14 | tied |
| Rev 21:27 w1-w25 | Rev 22:2 w12-w16 | G4160 | ποιέω | to do/make | 2.74 | tied |
| Rev 21:27 w1-w25 | Rev 22:2 w12-w16 | G2222 | ζωή | life | 4.14 | tied |
| Rev 21:27 w1-w25 | Rev 22:3 w7-w17 | G0721 | ἀρνίον | lamb | 5.65 | tied |
| Rev 21:26 w1-w11 | Rev 22:2 w25-w33 | G1484 | ἔθνος | Gentile nation | 3.97 | parallel |
| Rev 21:25 w9-w13 | Rev 22:5 w1-w5 | G3571 | νύξ | night | 4.92 | mirror |
| Rev 21:24 w1-w10 | Rev 22:2 w25-w33 | G1484 | ἔθνος | Gentile nation | 3.97 | parallel |
| Rev 21:24 w1-w10 | Rev 22:5 w6-w21 | G5457 | φῶς | light | 4.85 | tied |
| Rev 21:23 w23-w28 | Rev 22:3 w7-w17 | G0721 | ἀρνίον | lamb | 5.65 | parallel |
| Rev 21:23 w23-w28 | Rev 22:5 w6-w21 | G3088 | λύχνος | lamp | 6.34 | tied |
| Rev 21:23 w16-w22 | Rev 22:3 w7-w17 | G2316 | θεός | God | 1.93 | parallel |
| Rev 21:23 w16-w22 | Rev 22:5 w6-w21 | G2316 | θεός | God | 1.93 | tied |
| Rev 21:23 w16-w22 | Rev 22:5 w6-w21 | G5461 | φωτίζω | to illuminate | 6.58 | tied |
| Rev 21:23 w1-w15 | Rev 22:5 w6-w21 | G2192 | ἔχω | to have/be | 2.54 | tied |
| Rev 21:23 w1-w15 | Rev 22:5 w6-w21 | G5532 | χρεία | need | 5.13 | tied |
| Rev 21:23 w1-w15 | Rev 22:5 w6-w21 | G2246 | ἥλιος | sun | 5.52 | tied |

##### 16. 1John 4:14 w1 to 1John 5:2 w9 (n = 24, centre before 1John 4:18 w15)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before 1John 4:18 w15 | 24 | 8 | 4089.86 | 1331.64 | 0.509 | 119.65 | 4.37e-5 | sampled, B = 10000000, 436 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 1John 4:18 w7-w14 | 1John 4:18 w15-w19 | G5401 | φόβος | fear | 5.20 |  |
| 1John 4:18 w7-w14 | 1John 4:18 w20-w27 | G0026 | ἀγάπη | love | 4.32 | tied |
| 1John 4:18 w1-w6 | 1John 4:18 w15-w19 | G5401 | φόβος | fear | 5.20 | parallel |
| 1John 4:18 w1-w6 | 1John 4:18 w20-w27 | G0026 | ἀγάπη | love | 4.32 | tied |
| 1John 4:17 w8-w15 | 1John 4:18 w15-w19 | G2192 | ἔχω | to have/be | 2.54 | parallel |
| 1John 4:17 w8-w15 | 1John 4:21 w1-w7 | G2192 | ἔχω | to have/be | 2.54 | tied |
| 1John 4:17 w1-w7 | 1John 4:18 w20-w27 | G0026 | ἀγάπη | love | 4.32 | parallel |
| 1John 4:17 w1-w7 | 1John 4:18 w20-w27 | G5048 | τελειόω | to perfect | 5.85 | tied |
| 1John 4:16 w28-w33 | 1John 4:20 w1-w12 | G2316 | θεός | God | 1.93 | mirror |
| 1John 4:16 w28-w33 | 1John 4:20 w24-w31 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w28-w33 | 1John 4:21 w8-w17 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w28-w33 | 1John 5:1 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w28-w33 | 1John 5:2 w1-w9 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w18-w27 | 1John 4:18 w20-w27 | G0026 | ἀγάπη | love | 4.32 | parallel |
| 1John 4:16 w18-w27 | 1John 4:20 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w18-w27 | 1John 4:20 w24-w31 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w18-w27 | 1John 4:21 w8-w17 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w18-w27 | 1John 5:1 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w18-w27 | 1John 5:2 w1-w9 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w14-w17 | 1John 4:18 w20-w27 | G0026 | ἀγάπη | love | 4.32 | parallel |
| 1John 4:16 w14-w17 | 1John 4:20 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w14-w17 | 1John 4:20 w24-w31 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w14-w17 | 1John 4:21 w8-w17 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w14-w17 | 1John 5:1 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w14-w17 | 1John 5:2 w1-w9 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w1-w13 | 1John 4:18 w15-w19 | G2192 | ἔχω | to have/be | 2.54 | parallel |
| 1John 4:16 w1-w13 | 1John 4:18 w20-w27 | G0026 | ἀγάπη | love | 4.32 | tied |
| 1John 4:16 w1-w13 | 1John 4:20 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w1-w13 | 1John 4:20 w24-w31 | G2316 | θεός | God | 1.93 | tied |
| 1John 4:16 w1-w13 | 1John 4:21 w1-w7 | G2192 | ἔχω | to have/be | 2.54 | tied |

##### 17. Luke 5:33 w21 to Luke 6:3 w21 (n = 24, centre before Luke 5:37 w9)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Luke 5:37 w9 | 24 | 11 | 3572.72 | 564.98 | 0.727 | 128.70 | 4.74e-5 | sampled, B = 10000000, 473 as high | 1.00e-9 | 0.0011 (sampled, B = 99999, 106 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Luke 5:37 w1-w8 | Luke 5:37 w13-w22 | G3631 | οἶνος | wine | 5.72 |  |
| Luke 5:37 w1-w8 | Luke 5:37 w13-w22 | G3501 | νέος | new | 5.94 | tied |
| Luke 5:37 w1-w8 | Luke 5:37 w13-w22 | G0779 | ἀσκός | wineskin | 7.60 | tied |
| Luke 5:37 w1-w8 | Luke 5:37 w23-w26 | G0779 | ἀσκός | wineskin | 7.60 | tied |
| Luke 5:37 w1-w8 | Luke 5:38 w1 to Luke 5:39 w7 | G3762 | οὐδείς | none | 3.58 | tied |
| Luke 5:37 w1-w8 | Luke 5:38 w1 to Luke 5:39 w7 | G3820 | παλαιός | old | 6.27 | tied |
| Luke 5:37 w1-w8 | Luke 5:38 w1 to Luke 5:39 w7 | G3631 | οἶνος | wine | 5.72 | tied |
| Luke 5:37 w1-w8 | Luke 5:38 w1 to Luke 5:39 w7 | G3501 | νέος | new | 5.94 | tied |
| Luke 5:37 w1-w8 | Luke 5:38 w1 to Luke 5:39 w7 | G0779 | ἀσκός | wineskin | 7.60 | tied |
| Luke 5:37 w1-w8 | Luke 5:39 w10-w13 | G3820 | παλαιός | old | 6.27 | tied |
| Luke 5:36 w26-w36 | Luke 5:38 w1 to Luke 5:39 w7 | G3820 | παλαιός | old | 6.27 | parallel |
| Luke 5:36 w26-w36 | Luke 5:38 w1 to Luke 5:39 w7 | G2537 | καινός | new | 5.40 | tied |
| Luke 5:36 w26-w36 | Luke 5:39 w10-w13 | G3820 | παλαιός | old | 6.27 | tied |
| Luke 5:36 w22-w25 | Luke 5:38 w1 to Luke 5:39 w7 | G2537 | καινός | new | 5.40 | parallel |
| Luke 5:36 w1-w17 | Luke 5:38 w1 to Luke 5:39 w7 | G3762 | οὐδείς | none | 3.58 | tied |
| Luke 5:36 w1-w17 | Luke 5:38 w1 to Luke 5:39 w7 | G3820 | παλαιός | old | 6.27 | tied |
| Luke 5:36 w1-w17 | Luke 5:38 w1 to Luke 5:39 w7 | G2537 | καινός | new | 5.40 | tied |
| Luke 5:36 w1-w17 | Luke 5:39 w8-w9 | G3004 | λέγω | to speak | 1.87 | tied |
| Luke 5:36 w1-w17 | Luke 5:39 w10-w13 | G3820 | παλαιός | old | 6.27 | tied |
| Luke 5:34 w20-w21 | Luke 6:2 w1-w15 | G4160 | ποιέω | to do/make | 2.74 | mirror |
| Luke 5:34 w20-w21 | Luke 6:3 w8-w13 | G4160 | ποιέω | to do/make | 2.74 | tied |
| Luke 5:34 w1-w6 | Luke 6:2 w1-w15 | G2036 | ἔπω, ἐρῶ, εἶπον | to say | 2.22 | parallel |
| Luke 5:34 w1-w6 | Luke 6:3 w1-w7 | G2036 | ἔπω, ἐρῶ, εἶπον | to say | 2.22 | tied |
| Luke 5:33 w21-w26 | Luke 5:38 w1 to Luke 5:39 w7 | G4095 | πίνω | to drink | 4.82 | parallel |
| Luke 5:33 w21-w26 | Luke 6:1 w11-w22 | G2068 | ἐσθίω | to eat | 4.97 | tied |

##### 18. 1Pet 4:8 w1 to 1Pet 4:18 w13 (n = 24, centre before 1Pet 4:13 w9)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before 1Pet 4:13 w9 | 24 | 5 | 834.98 | 184.99 | 0.637 | 54.13 | 4.96e-5 | sampled, B = 10000000, 495 as high | 1.93e-6 | 0.0012 (sampled, B = 99999, 116 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 1Pet 4:13 w1-w8 | 1Pet 4:13 w9-w18 | G5463 | χαίρω | to rejoice | 4.76 |  |
| 1Pet 4:13 w1-w8 | 1Pet 4:14 w1-w5 | G5547 | Χριστός | Christ | 2.77 | tied |
| 1Pet 4:11 w26-w37 | 1Pet 4:13 w9-w18 | G1391 | δόξα | glory | 3.98 | parallel |
| 1Pet 4:11 w26-w37 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G1391 | δόξα | glory | 3.98 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:14 w1-w5 | G5547 | Χριστός | Christ | 2.77 | parallel |
| 1Pet 4:11 w17-w25 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:16 w7-w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:16 w7-w14 | G1392 | δοξάζω | to glorify | 5.01 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:17 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:17 w18-w26 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w7-w16 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G2316 | θεός | God | 1.93 | parallel |
| 1Pet 4:11 w7-w16 | 1Pet 4:16 w7-w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w7-w16 | 1Pet 4:17 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w7-w16 | 1Pet 4:17 w18-w26 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w1-w6 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G2316 | θεός | God | 1.93 | parallel |
| 1Pet 4:11 w1-w6 | 1Pet 4:16 w7-w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w1-w6 | 1Pet 4:17 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w1-w6 | 1Pet 4:17 w18-w26 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:10 w1-w14 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G2316 | θεός | God | 1.93 | parallel |
| 1Pet 4:10 w1-w14 | 1Pet 4:16 w7-w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:10 w1-w14 | 1Pet 4:17 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:10 w1-w14 | 1Pet 4:17 w18-w26 | G2316 | θεός | God | 1.93 | tied |

##### 19. 1Pet 4:8 w10 to 1Pet 4:18 w6 (n = 22, centre before 1Pet 4:13 w9)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before 1Pet 4:13 w9 | 22 | 5 | 834.98 | 184.99 | 0.637 | 54.13 | 4.96e-5 | sampled, B = 10000000, 495 as high | 1.93e-6 | 0.0013 (sampled, B = 99999, 132 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 1Pet 4:13 w1-w8 | 1Pet 4:13 w9-w18 | G5463 | χαίρω | to rejoice | 4.76 |  |
| 1Pet 4:13 w1-w8 | 1Pet 4:14 w1-w5 | G5547 | Χριστός | Christ | 2.77 | tied |
| 1Pet 4:11 w26-w37 | 1Pet 4:13 w9-w18 | G1391 | δόξα | glory | 3.98 | parallel |
| 1Pet 4:11 w26-w37 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G1391 | δόξα | glory | 3.98 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:14 w1-w5 | G5547 | Χριστός | Christ | 2.77 | parallel |
| 1Pet 4:11 w17-w25 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:16 w7-w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:16 w7-w14 | G1392 | δοξάζω | to glorify | 5.01 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:17 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:17 w18-w26 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w7-w16 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G2316 | θεός | God | 1.93 | parallel |
| 1Pet 4:11 w7-w16 | 1Pet 4:16 w7-w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w7-w16 | 1Pet 4:17 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w7-w16 | 1Pet 4:17 w18-w26 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w1-w6 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G2316 | θεός | God | 1.93 | parallel |
| 1Pet 4:11 w1-w6 | 1Pet 4:16 w7-w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w1-w6 | 1Pet 4:17 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w1-w6 | 1Pet 4:17 w18-w26 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:10 w1-w14 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G2316 | θεός | God | 1.93 | parallel |
| 1Pet 4:10 w1-w14 | 1Pet 4:16 w7-w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:10 w1-w14 | 1Pet 4:17 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:10 w1-w14 | 1Pet 4:17 w18-w26 | G2316 | θεός | God | 1.93 | tied |

##### 20. 1Pet 4:9 w1 to 1Pet 4:17 w26 (n = 20, centre before 1Pet 4:13 w9)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before 1Pet 4:13 w9 | 20 | 5 | 834.98 | 184.99 | 0.637 | 54.13 | 4.96e-5 | sampled, B = 10000000, 495 as high | 1.93e-6 | 9.20e-4 (sampled, B = 99999, 91 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 1Pet 4:13 w1-w8 | 1Pet 4:13 w9-w18 | G5463 | χαίρω | to rejoice | 4.76 |  |
| 1Pet 4:13 w1-w8 | 1Pet 4:14 w1-w5 | G5547 | Χριστός | Christ | 2.77 | tied |
| 1Pet 4:11 w26-w37 | 1Pet 4:13 w9-w18 | G1391 | δόξα | glory | 3.98 | parallel |
| 1Pet 4:11 w26-w37 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G1391 | δόξα | glory | 3.98 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:14 w1-w5 | G5547 | Χριστός | Christ | 2.77 | parallel |
| 1Pet 4:11 w17-w25 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:16 w7-w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:16 w7-w14 | G1392 | δοξάζω | to glorify | 5.01 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:17 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w17-w25 | 1Pet 4:17 w18-w26 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w7-w16 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G2316 | θεός | God | 1.93 | parallel |
| 1Pet 4:11 w7-w16 | 1Pet 4:16 w7-w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w7-w16 | 1Pet 4:17 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w7-w16 | 1Pet 4:17 w18-w26 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w1-w6 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G2316 | θεός | God | 1.93 | parallel |
| 1Pet 4:11 w1-w6 | 1Pet 4:16 w7-w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w1-w6 | 1Pet 4:17 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:11 w1-w6 | 1Pet 4:17 w18-w26 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:10 w1-w14 | 1Pet 4:14 w7 to 1Pet 4:15 w14 | G2316 | θεός | God | 1.93 | parallel |
| 1Pet 4:10 w1-w14 | 1Pet 4:16 w7-w14 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:10 w1-w14 | 1Pet 4:17 w1-w12 | G2316 | θεός | God | 1.93 | tied |
| 1Pet 4:10 w1-w14 | 1Pet 4:17 w18-w26 | G2316 | θεός | God | 1.93 | tied |

##### 21. 2Cor 3:9 w1 to 2Cor 4:2 w16 (n = 22, centre before 2Cor 3:15 w8)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before 2Cor 3:15 w8 | 22 | 8 | 3618.00 | 740.31 | 0.660 | 111.45 | 5.11e-5 | sampled, B = 10000000, 510 as high | 3.83e-9 | 2.00e-5 (sampled, B = 99999, 1 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 2Cor 3:15 w1-w7 | 2Cor 3:16 w1-w6 | G2259 | ἡνίκα | when | 8.29 |  |
| 2Cor 3:14 w6-w22 | 2Cor 3:15 w8-w13 | G2571 | κάλυμμα | veil | 7.60 | parallel |
| 2Cor 3:14 w6-w22 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 | tied |
| 2Cor 3:14 w6-w22 | 2Cor 3:18 w1-w9 | G0343 | ἀνακαλύπτω | to unveil | 8.29 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:15 w8-w13 | G2571 | κάλυμμα | veil | 7.60 | parallel |
| 2Cor 3:13 w1-w22 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:18 w1-w9 | G4383 | πρόσωπον | face | 4.72 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:18 w10-w21 | G2509 | καθάπερ | just as | 6.42 | tied |
| 2Cor 3:12 w1-w7 | 2Cor 4:1 w1-w8 | G2192 | ἔχω | to have/be | 2.54 | mirror |
| 2Cor 3:11 w7-w12 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:11 w7-w12 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:11 w1-w6 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:11 w1-w6 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:10 w1-w14 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:10 w1-w14 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w8-w16 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:9 w8-w16 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w8-w16 | 2Cor 4:1 w1-w8 | G1248 | διακονία | service | 5.52 | tied |
| 2Cor 3:9 w1-w7 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:9 w1-w7 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w1-w7 | 2Cor 4:1 w1-w8 | G1248 | διακονία | service | 5.52 | tied |

##### 22. 2Cor 3:9 w1 to 2Cor 4:1 w8 (n = 19, centre the unit 2Cor 3:14 w23)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| the unit 2Cor 3:14 w23 | 19 | 9 | 3556.68 | 722.70 | 0.662 | 113.07 | 5.13e-5 | sampled, B = 10000000, 512 as high | 3.44e-8 | 5.00e-5 (sampled, B = 99999, 4 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 2Cor 3:14 w6-w22 | 2Cor 3:15 w1-w7 | G4594 | σήμερον | today | 5.29 |  |
| 2Cor 3:14 w6-w22 | 2Cor 3:15 w8-w13 | G2571 | κάλυμμα | veil | 7.60 | tied |
| 2Cor 3:14 w6-w22 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 | tied |
| 2Cor 3:14 w6-w22 | 2Cor 3:18 w1-w9 | G0343 | ἀνακαλύπτω | to unveil | 8.29 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:15 w1-w7 | G3475 | Μωϋσῆς, Μωσῆς | Moses | 4.61 | parallel |
| 2Cor 3:13 w1-w22 | 2Cor 3:15 w8-w13 | G2571 | κάλυμμα | veil | 7.60 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:18 w1-w9 | G4383 | πρόσωπον | face | 4.72 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:18 w10-w21 | G2509 | καθάπερ | just as | 6.42 | tied |
| 2Cor 3:12 w1-w7 | 2Cor 4:1 w1-w8 | G2192 | ἔχω | to have/be | 2.54 | mirror |
| 2Cor 3:11 w7-w12 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:11 w7-w12 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:11 w1-w6 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:11 w1-w6 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:10 w1-w14 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:10 w1-w14 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w8-w16 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:9 w8-w16 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w8-w16 | 2Cor 4:1 w1-w8 | G1248 | διακονία | service | 5.52 | tied |
| 2Cor 3:9 w1-w7 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:9 w1-w7 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w1-w7 | 2Cor 4:1 w1-w8 | G1248 | διακονία | service | 5.52 | tied |

##### 23. 2Cor 3:9 w1 to 2Cor 4:1 w10 (n = 20, centre before 2Cor 3:15 w1)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before 2Cor 3:15 w1 | 20 | 9 | 3556.68 | 722.70 | 0.662 | 113.07 | 5.13e-5 | sampled, B = 10000000, 512 as high | 3.44e-8 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| 2Cor 3:14 w6-w22 | 2Cor 3:15 w1-w7 | G4594 | σήμερον | today | 5.29 |  |
| 2Cor 3:14 w6-w22 | 2Cor 3:15 w8-w13 | G2571 | κάλυμμα | veil | 7.60 | tied |
| 2Cor 3:14 w6-w22 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 | tied |
| 2Cor 3:14 w6-w22 | 2Cor 3:18 w1-w9 | G0343 | ἀνακαλύπτω | to unveil | 8.29 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:15 w1-w7 | G3475 | Μωϋσῆς, Μωσῆς | Moses | 4.61 | parallel |
| 2Cor 3:13 w1-w22 | 2Cor 3:15 w8-w13 | G2571 | κάλυμμα | veil | 7.60 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:16 w7-w9 | G2571 | κάλυμμα | veil | 7.60 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:18 w1-w9 | G4383 | πρόσωπον | face | 4.72 | tied |
| 2Cor 3:13 w1-w22 | 2Cor 3:18 w10-w21 | G2509 | καθάπερ | just as | 6.42 | tied |
| 2Cor 3:12 w1-w7 | 2Cor 4:1 w1-w8 | G2192 | ἔχω | to have/be | 2.54 | mirror |
| 2Cor 3:11 w7-w12 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:11 w7-w12 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:11 w1-w6 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:11 w1-w6 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:10 w1-w14 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:10 w1-w14 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w8-w16 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:9 w8-w16 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w8-w16 | 2Cor 4:1 w1-w8 | G1248 | διακονία | service | 5.52 | tied |
| 2Cor 3:9 w1-w7 | 2Cor 3:18 w1-w9 | G1391 | δόξα | glory | 3.98 | parallel |
| 2Cor 3:9 w1-w7 | 2Cor 3:18 w10-w21 | G1391 | δόξα | glory | 3.98 | tied |
| 2Cor 3:9 w1-w7 | 2Cor 4:1 w1-w8 | G1248 | διακονία | service | 5.52 | tied |

##### 24. Rev 4:4 w9 to Rev 4:11 w2 (n = 20, centre before Rev 4:7 w14)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Rev 4:7 w14 | 20 | 12 | 11978.12 | 2643.94 | 0.638 | 208.50 | 5.21e-5 | sampled, B = 10000000, 520 as high | 1.00e-9 | 1.00e-5 (sampled, B = 99999, 0 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Rev 4:7 w8-w13 | Rev 4:7 w14-w22 | G2226 | ζῷον | living thing | 5.99 |  |
| Rev 4:7 w8-w13 | Rev 4:7 w23-w29 | G3664 | ὅμοιος | like | 5.27 | tied |
| Rev 4:7 w8-w13 | Rev 4:7 w23-w29 | G2226 | ζῷον | living thing | 5.99 | tied |
| Rev 4:7 w8-w13 | Rev 4:8 w1-w4 | G2226 | ζῷον | living thing | 5.99 | tied |
| Rev 4:7 w8-w13 | Rev 4:9 w1-w15 | G2226 | ζῷον | living thing | 5.99 | tied |
| Rev 4:7 w1-w7 | Rev 4:7 w14-w22 | G2226 | ζῷον | living thing | 5.99 | parallel |
| Rev 4:7 w1-w7 | Rev 4:7 w23-w29 | G3664 | ὅμοιος | like | 5.27 | tied |
| Rev 4:7 w1-w7 | Rev 4:7 w23-w29 | G2226 | ζῷον | living thing | 5.99 | tied |
| Rev 4:7 w1-w7 | Rev 4:8 w1-w4 | G2226 | ζῷον | living thing | 5.99 | tied |
| Rev 4:7 w1-w7 | Rev 4:9 w1-w15 | G2226 | ζῷον | living thing | 5.99 | tied |
| Rev 4:6 w10-w25 | Rev 4:7 w14-w22 | G2226 | ζῷον | living thing | 5.99 | parallel |
| Rev 4:6 w10-w25 | Rev 4:7 w23-w29 | G2226 | ζῷον | living thing | 5.99 | tied |
| Rev 4:6 w10-w25 | Rev 4:8 w1-w4 | G5064 | τέσσαρες | four | 5.43 | tied |
| Rev 4:6 w10-w25 | Rev 4:8 w1-w4 | G2226 | ζῷον | living thing | 5.99 | tied |
| Rev 4:6 w10-w25 | Rev 4:8 w5-w25 | G3788 | ὀφθαλμός | eye | 4.54 | tied |
| Rev 4:6 w10-w25 | Rev 4:8 w5-w25 | G1073 | γέμω | be full | 6.58 | tied |
| Rev 4:6 w10-w25 | Rev 4:9 w1-w15 | G2362 | θρόνος | throne | 5.05 | tied |
| Rev 4:6 w10-w25 | Rev 4:9 w1-w15 | G2226 | ζῷον | living thing | 5.99 | tied |
| Rev 4:6 w10-w25 | Rev 4:10 w1-w30 | G2362 | θρόνος | throne | 5.05 | tied |
| Rev 4:6 w10-w25 | Rev 4:10 w1-w30 | G5064 | τέσσαρες | four | 5.43 | tied |
| Rev 4:6 w8-w9 | Rev 4:7 w23-w29 | G3664 | ὅμοιος | like | 5.27 | parallel |
| Rev 4:6 w1-w7 | Rev 4:9 w1-w15 | G2362 | θρόνος | throne | 5.05 | mirror |
| Rev 4:6 w1-w7 | Rev 4:10 w1-w30 | G2362 | θρόνος | throne | 5.05 | tied |
| Rev 4:6 w1-w7 | Rev 4:10 w1-w30 | G1799 | ἐνώπιον | before | 4.53 | tied |
| Rev 4:5 w11-w26 | Rev 4:8 w26-w33 | G2316 | θεός | God | 1.93 | parallel |
| Rev 4:5 w11-w26 | Rev 4:9 w1-w15 | G2362 | θρόνος | throne | 5.05 | tied |
| Rev 4:5 w11-w26 | Rev 4:10 w1-w30 | G2362 | θρόνος | throne | 5.05 | tied |
| Rev 4:5 w11-w26 | Rev 4:10 w1-w30 | G1799 | ἐνώπιον | before | 4.53 | tied |
| Rev 4:5 w1-w10 | Rev 4:9 w1-w15 | G2362 | θρόνος | throne | 5.05 | parallel |
| Rev 4:5 w1-w10 | Rev 4:10 w1-w30 | G2362 | θρόνος | throne | 5.05 | tied |

##### 25. Luke 5:34 w1 to Luke 6:3 w13 (n = 22, centre before Luke 5:37 w9)

| Centre | n | k | M | P | T | R | p | how | min p | whole-window p |
|---|---|---|---|---|---|---|---|---|---|---|
| before Luke 5:37 w9 | 22 | 9 | 2901.06 | 368.00 | 0.775 | 118.90 | 5.45e-5 | sampled, B = 10000000, 544 as high | 3.44e-8 | 0.0015 (sampled, B = 99999, 145 as high) |

q (BH) 0.0969, q (BY) 1.0000: mirror order exceeds parallel order and the permutation null at q = 0.0969. Flags: Greek units are editorial.

| Left | Right | Key | Lemma | Gloss | IDF | Order |
|---|---|---|---|---|---|---|
| Luke 5:37 w1-w8 | Luke 5:37 w13-w22 | G3631 | οἶνος | wine | 5.72 |  |
| Luke 5:37 w1-w8 | Luke 5:37 w13-w22 | G3501 | νέος | new | 5.94 | tied |
| Luke 5:37 w1-w8 | Luke 5:37 w13-w22 | G0779 | ἀσκός | wineskin | 7.60 | tied |
| Luke 5:37 w1-w8 | Luke 5:37 w23-w26 | G0779 | ἀσκός | wineskin | 7.60 | tied |
| Luke 5:37 w1-w8 | Luke 5:38 w1 to Luke 5:39 w7 | G3762 | οὐδείς | none | 3.58 | tied |
| Luke 5:37 w1-w8 | Luke 5:38 w1 to Luke 5:39 w7 | G3820 | παλαιός | old | 6.27 | tied |
| Luke 5:37 w1-w8 | Luke 5:38 w1 to Luke 5:39 w7 | G3631 | οἶνος | wine | 5.72 | tied |
| Luke 5:37 w1-w8 | Luke 5:38 w1 to Luke 5:39 w7 | G3501 | νέος | new | 5.94 | tied |
| Luke 5:37 w1-w8 | Luke 5:38 w1 to Luke 5:39 w7 | G0779 | ἀσκός | wineskin | 7.60 | tied |
| Luke 5:37 w1-w8 | Luke 5:39 w10-w13 | G3820 | παλαιός | old | 6.27 | tied |
| Luke 5:36 w26-w36 | Luke 5:38 w1 to Luke 5:39 w7 | G3820 | παλαιός | old | 6.27 | parallel |
| Luke 5:36 w26-w36 | Luke 5:38 w1 to Luke 5:39 w7 | G2537 | καινός | new | 5.40 | tied |
| Luke 5:36 w26-w36 | Luke 5:39 w10-w13 | G3820 | παλαιός | old | 6.27 | tied |
| Luke 5:36 w22-w25 | Luke 5:38 w1 to Luke 5:39 w7 | G2537 | καινός | new | 5.40 | parallel |
| Luke 5:36 w1-w17 | Luke 5:38 w1 to Luke 5:39 w7 | G3762 | οὐδείς | none | 3.58 | tied |
| Luke 5:36 w1-w17 | Luke 5:38 w1 to Luke 5:39 w7 | G3820 | παλαιός | old | 6.27 | tied |
| Luke 5:36 w1-w17 | Luke 5:38 w1 to Luke 5:39 w7 | G2537 | καινός | new | 5.40 | tied |
| Luke 5:36 w1-w17 | Luke 5:39 w8-w9 | G3004 | λέγω | to speak | 1.87 | tied |
| Luke 5:36 w1-w17 | Luke 5:39 w10-w13 | G3820 | παλαιός | old | 6.27 | tied |
| Luke 5:34 w20-w21 | Luke 6:2 w1-w15 | G4160 | ποιέω | to do/make | 2.74 | mirror |
| Luke 5:34 w20-w21 | Luke 6:3 w8-w13 | G4160 | ποιέω | to do/make | 2.74 | tied |
| Luke 5:34 w1-w6 | Luke 6:2 w1-w15 | G2036 | ἔπω, ἐρῶ, εἶπον | to say | 2.22 | parallel |
| Luke 5:34 w1-w6 | Luke 6:3 w1-w7 | G2036 | ἔπω, ἐρῶ, εἶπον | to say | 2.22 | tied |

#### The word scale

| Testament | Tests | Tarone K | Screened m | q <= 0.10 |
|---|---|---|---|---|
| Hebrew OT | 86059 | 154 | 154 | 0 |
| Greek NT | 11080 | 8 | 8 | 0 |

A word-scale test holds few matched words, so its minimum attainable p is large; the arithmetic section predicted that no micro-chiasm can reach the scan's threshold on its own.

### Inclusio (a separate detector, never tested)

Whether a window's first and last units share a key whose IDF is at or above the corpus median. It enters no score and is never tested.

| Item | Inclusio | Keys |
|---|---|---|
| G1 Gen 9:6a | no |  |
| G2 Isa 6:10 | no |  |
| G3 Lev 24:13-23 | no |  |
| G4 Amos 5:5 | no |  |
| G5 Mark 2:27 | no |  |
| C1 Matt 7:7-8 | no |  |
| C2 Ps 24:7-10 | no |  |
| C3 Ps 136:1-9 | no |  |
| C4 Matt 7:24-27 | no |  |
| T1 The flood, Gen 6:10-9:19, centred on 8:1a | no |  |
| T2a Babel, Gen 11:1-9, centred on 11:5a | no |  |
| T2b Babel, Gen 11:1-9, centred on 11:6 | no |  |
| T4 The Johannine prologue, John 1:1-18, centred on 1:12b | no |  |

| Scan | Windows with inclusio | Of those at q <= 0.10 |
|---|---|---|
| Hebrew OT, level-1 units | 378 of 937650 | 2 of 3158 |
| Greek NT, clause units | 117 of 370251 | 0 of 27 |

### The LXX side check (a test of the translation)

Each Hebrew item and each Hebrew scan window with q <= 0.10, read in Brenton's lemmas by the Greek rules (clause punctuation, the Greek stop list, IDF over Brenton). Word-scale items show the clause pair with the highest T. It asks whether the translators kept the mirror; it is not evidence about the Hebrew, and a mirror lost here takes nothing from the Hebrew result. Unread words are Brenton forms the TAGNT lookup could not lemmatize: a lost pair may be the lookup, not the translator.

| Hebrew item | Hebrew T | Hebrew p | LXX tests | LXX T | LXX p | Unread words |
|---|---|---|---|---|---|---|
| G1 Gen 9:6a | 1.000 | 0.1667 | 2 | 1.000 | 0.5000 | 0 |
| G2 Isa 6:10 | 1.000 | 0.5000 | 6 | 0.000 | 1.0000 | 0 |
| G3 Lev 24:13-23 | 0.848 | 2.30e-6 | 1 | 0.435 | 0.0173 | 10 |
| G4 Amos 5:5 | 1.000 | 0.5000 | 4 | 0.000 | 1.0000 | 8 |
| T1 The flood, Gen 6:10-9:19, centred on 8:1a | 0.055 | 0.0012 | 1 | 0.039 | 0.0149 | 59 |
| T2a Babel, Gen 11:1-9, centred on 11:5a | -0.186 | 0.8742 | 1 | -0.018 | 0.5332 | 10 |
| T2b Babel, Gen 11:1-9, centred on 11:6 | -0.078 | 0.6852 | 1 | 0.022 | 0.4533 | 10 |
| scan: Lev 21:19 w8 to Lev 22:5 w16 | 0.647 | 1.30e-8 | 1 | 0.365 | 0.0082 | 15 |
| scan: Lev 21:19 w1 to Lev 22:6 w7 | 0.612 | 1.70e-8 | 1 | 0.255 | 0.0329 | 16 |
| scan: Lev 21:19 w8 to Lev 22:6 w7 | 0.647 | 2.60e-8 | 1 | 0.255 | 0.0329 | 16 |
| scan: Ezek 47:21 w1 to Ezek 48:12 w7 | 0.303 | 2.70e-8 | 1 | 0.230 | 0.0024 | 12 |
| scan: Lev 24:15 w1 to Lev 25:1 w7 | 0.837 | 9.70e-8 | 1 | 0.565 | 2.90e-4 | 8 |
| scan: Lev 21:20 w1 to Lev 22:5 w16 | 0.630 | 1.07e-7 | 1 | 0.315 | 0.0283 | 14 |
| scan: Ezek 47:22 w1 to Ezek 48:11 w16 | 0.267 | 1.09e-7 | 1 | 0.232 | 0.0031 | 10 |
| scan: Lev 24:14 w14 to Lev 25:1 w7 | 0.823 | 1.62e-7 | 1 | 0.538 | 8.50e-4 | 10 |
| scan: 2Kgs 3:27 w17 to 2Kgs 4:8 w20 | 0.638 | 1.64e-7 | 1 | 0.307 | 0.0179 | 9 |
| scan: 2Kgs 4:1 w1 to 2Kgs 4:8 w20 | 0.638 | 1.64e-7 | 1 | 0.396 | 0.0043 | 7 |
| scan: Lev 4:6 w1 to Lev 4:17 w13 | 0.498 | 1.70e-7 | 1 | 0.309 | 0.0013 | 23 |
| scan: Num 34:28 w5 to Num 35:10 w13 | 0.456 | 1.78e-7 | 1 | 0.479 | 3.70e-8 | 22 |
| scan: Lev 21:20 w1 to Lev 22:5 w9 | 0.588 | 2.51e-7 | 1 | 0.315 | 0.0283 | 14 |
| scan: Deut 2:10 w1 to Deut 2:21 w5 | 0.842 | 2.54e-7 | 1 | 0.439 | 0.0216 | 40 |
| scan: Ezek 3:14 w1 to Ezek 3:24 w6 | 0.740 | 2.66e-7 | 1 | 0.514 | 7.00e-4 | 12 |
| scan: Ezek 47:22 w13 to Ezek 48:12 w7 | 0.239 | 2.78e-7 | 1 | 0.226 | 0.0046 | 11 |
| scan: Ezek 47:21 w1 to Ezek 48:11 w7 | 0.248 | 3.06e-7 | 1 | 0.238 | 0.0022 | 11 |
| scan: Josh 17:4 w1 to Josh 17:14 w23 | 0.400 | 4.13e-7 | 1 | 0.442 | 1.66e-5 | 27 |
| scan: Lev 21:18 w9 to Lev 22:6 w7 | 0.529 | 5.03e-7 | 1 | 0.288 | 0.0120 | 17 |
| scan: Deut 2:10 w5 to Deut 2:21 w5 | 0.864 | 5.25e-7 | 1 | 0.174 | 0.2298 | 40 |
| scan: Lev 21:20 w1 to Lev 22:6 w7 | 0.547 | 5.32e-7 | 1 | 0.349 | 0.0050 | 15 |
| scan: Lev 24:14 w14 to Lev 24:23 w22 | 0.856 | 5.81e-7 | 1 | 0.555 | 0.0011 | 10 |
| scan: Isa 44:27 w4 to Isa 45:10 w8 | 0.732 | 6.03e-7 | 1 | 0.534 | 0.0025 | 9 |
| scan: Isa 44:28 w1 to Isa 45:10 w5 | 0.732 | 6.03e-7 | 1 | 0.470 | 0.0078 | 8 |
| scan: Lev 4:6 w1 to Lev 4:17 w5 | 0.426 | 6.31e-7 | 1 | 0.327 | 0.0018 | 23 |
| scan: Ezek 47:22 w13 to Ezek 48:11 w7 | 0.179 | 6.63e-7 | 1 | 0.232 | 0.0031 | 10 |
| scan: 2Kgs 14:20 w1 to 2Kgs 15:2 w15 | 0.405 | 6.89e-7 | 1 | 0.413 | 4.90e-6 | 29 |
| scan: Josh 17:3 w17 to Josh 17:15 w16 | 0.393 | 7.74e-7 | 1 | 0.367 | 3.70e-4 | 36 |
| scan: Exod 33:3 w1 to Exod 33:15 w2 | 0.430 | 8.31e-7 | 1 | 0.172 | 0.0292 | 16 |
| scan: Lev 24:12 w1 to Lev 25:1 w7 | 0.734 | 9.04e-7 | 1 | 0.417 | 0.0090 | 11 |
| scan: Lev 21:19 w1 to Lev 22:5 w16 | 0.558 | 9.05e-7 | 1 | 0.365 | 0.0082 | 15 |
| scan: Ezek 47:22 w1 to Ezek 48:10 w26 | 0.224 | 1.07e-6 | 1 | 0.160 | 0.0200 | 9 |
| scan: Lev 24:13 w1 to Lev 25:1 w7 | 0.745 | 1.16e-6 | 1 | 0.577 | 7.82e-5 | 10 |
| scan: Exod 33:3 w6 to Exod 33:14 w5 | 0.441 | 1.22e-6 | 1 | 0.172 | 0.0292 | 15 |
| scan: Lev 21:18 w9 to Lev 22:5 w16 | 0.529 | 1.30e-6 | 1 | 0.373 | 0.0029 | 16 |
| scan: Lev 24:15 w1 to Lev 24:23 w22 | 0.825 | 1.40e-6 | 1 | 0.556 | 8.10e-4 | 8 |
| scan: Num 34:29 w1 to Num 35:10 w6 | 0.406 | 1.50e-6 | 1 | 0.473 | 5.80e-8 | 20 |
| scan: 2Kgs 3:27 w17 to 2Kgs 4:9 w11 | 0.617 | 1.50e-6 | 1 | 0.388 | 8.20e-4 | 9 |
| scan: Exod 33:2 w4 to Exod 33:14 w5 | 0.391 | 1.60e-6 | 1 | 0.222 | 0.0023 | 22 |
| scan: Exod 33:3 w1 to Exod 33:14 w1 | 0.391 | 1.60e-6 | 1 | 0.222 | 0.0023 | 15 |
| scan: Josh 17:4 w1 to Josh 17:15 w16 | 0.455 | 1.60e-6 | 1 | 0.371 | 3.30e-4 | 28 |
| scan: Ezek 47:21 w1 to Ezek 48:11 w16 | 0.321 | 1.70e-6 | 1 | 0.265 | 0.0025 | 11 |
| scan: Lev 4:6 w6 to Lev 4:17 w13 | 0.455 | 1.80e-6 | 1 | 0.309 | 0.0029 | 23 |
| scan: Exod 28:14 w10 to Exod 28:25 w9 | 0.775 | 2.00e-6 | 0 | - | - | 0 |
| scan: Exod 33:3 w6 to Exod 33:15 w2 | 0.449 | 2.00e-6 | 1 | 0.172 | 0.0292 | 16 |
| scan: Lev 24:12 w3 to Lev 25:1 w7 | 0.722 | 2.00e-6 | 1 | 0.417 | 0.0090 | 11 |
| scan: Gen 47:13 w9 to Gen 47:22 w5 | 0.495 | 2.20e-6 | 1 | 0.187 | 0.0080 | 15 |
| scan: Lev 14:16 w1 to Lev 14:27 w14 | 0.316 | 2.20e-6 | 1 | 0.247 | 7.00e-4 | 30 |
| scan: Lev 24:13 w1 to Lev 25:2 w14 | 0.698 | 2.20e-6 | 1 | 0.509 | 1.29e-4 | 11 |
| scan: Josh 17:4 w21 to Josh 17:15 w16 | 0.381 | 2.20e-6 | 1 | 0.367 | 2.71e-5 | 28 |
| scan: Exod 25:28 w9 to Exod 26:1 w5 | 0.582 | 2.30e-6 | 1 | 0.519 | 3.70e-6 | 47 |
| scan: 1Chr 28:10 w1 to 1Chr 28:20 w11 | 0.650 | 2.30e-6 | 1 | 0.204 | 0.0379 | 16 |
| scan: Exod 37:15 w1 to Exod 37:26 w16 | 0.626 | 2.40e-6 | 0 | - | - | 0 |
| scan: Lev 4:5 w1 to Lev 4:16 w5 | 0.368 | 2.60e-6 | 1 | 0.234 | 0.0246 | 21 |
| scan: 2Kgs 14:20 w5 to 2Kgs 15:2 w11 | 0.397 | 2.60e-6 | 1 | 0.413 | 4.90e-6 | 29 |
| scan: Ezek 47:23 w1 to Ezek 48:11 w16 | 0.145 | 2.70e-6 | 1 | 0.056 | 0.2296 | 9 |
| scan: Lev 24:12 w3 to Lev 25:2 w14 | 0.647 | 3.00e-6 | 1 | 0.507 | 1.20e-4 | 12 |
| scan: Josh 17:3 w17 to Josh 17:14 w23 | 0.386 | 3.10e-6 | 1 | 0.440 | 1.07e-5 | 35 |
| scan: 2Kgs 14:20 w5 to 2Kgs 15:2 w15 | 0.392 | 3.10e-6 | 1 | 0.357 | 2.00e-4 | 29 |
| scan: Exod 33:3 w6 to Exod 33:13 w20 | 0.392 | 3.20e-6 | 1 | 0.222 | 0.0023 | 15 |
| scan: Num 34:28 w1 to Num 35:11 w7 | 0.372 | 3.30e-6 | 1 | 0.413 | 9.04e-7 | 24 |
| scan: Ezek 47:22 w1 to Ezek 48:12 w7 | 0.339 | 3.30e-6 | 1 | 0.234 | 0.0054 | 11 |
| scan: Lev 21:20 w8 to Lev 22:5 w9 | 0.548 | 3.40e-6 | 1 | 0.315 | 0.0283 | 14 |
| scan: Lev 24:14 w1 to Lev 25:1 w7 | 0.800 | 3.60e-6 | 1 | 0.538 | 8.50e-4 | 10 |
| scan: Num 34:27 w5 to Num 35:10 w6 | 0.487 | 3.60e-6 | 1 | 0.544 | 5.40e-6 | 23 |
| scan: 1Sam 8:10 w1 to 1Sam 8:19 w5 | 0.948 | 3.60e-6 | 1 | 0.528 | 0.0373 | 10 |
| scan: 2Kgs 4:1 w1 to 2Kgs 4:8 w13 | 0.626 | 3.70e-6 | 1 | 0.282 | 0.0436 | 7 |
| scan: Lev 21:19 w1 to Lev 22:5 w9 | 0.529 | 3.90e-6 | 1 | 0.312 | 0.0181 | 15 |
| scan: Num 34:27 w1 to Num 35:10 w6 | 0.456 | 4.00e-6 | 1 | 0.498 | 1.90e-6 | 23 |
| scan: Exod 29:39 w1 to Exod 30:3 w11 | 0.864 | 4.20e-6 | 1 | 0.630 | 1.70e-4 | 25 |
| scan: 2Chr 11:15 w6 to 2Chr 12:3 w16 | 0.585 | 4.20e-6 | 1 | 0.214 | 0.1180 | 22 |
| scan: Ezek 47:22 w1 to Ezek 48:12 w10 | 0.264 | 4.20e-6 | 1 | 0.226 | 0.0046 | 11 |
| scan: Lev 14:16 w1 to Lev 14:27 w10 | 0.312 | 4.30e-6 | 1 | 0.254 | 0.0010 | 30 |
| scan: Ezek 3:15 w1 to Ezek 3:23 w15 | 0.751 | 4.30e-6 | 1 | 0.523 | 0.0053 | 10 |
| scan: Num 34:28 w1 to Num 35:10 w13 | 0.418 | 4.40e-6 | 1 | 0.542 | 4.00e-6 | 22 |
| scan: Lev 14:15 w5 to Lev 14:27 w10 | 0.289 | 4.50e-6 | 1 | 0.199 | 0.0031 | 31 |
| scan: Lev 21:18 w9 to Lev 22:5 w9 | 0.492 | 4.50e-6 | 1 | 0.374 | 0.0053 | 16 |
| scan: Num 34:29 w5 to Num 35:10 w13 | 0.389 | 4.50e-6 | 1 | 0.402 | 3.95e-5 | 20 |
| scan: Eccl 2:24 w1 to Eccl 3:13 w12 | 0.604 | 4.60e-6 | 1 | 0.530 | 1.69e-7 | 11 |
| scan: Isa 44:26 w7 to Isa 45:10 w5 | 0.633 | 4.60e-6 | 1 | 0.550 | 1.80e-4 | 12 |
| scan: Exod 25:28 w9 to Exod 25:40 w7 | 0.587 | 4.70e-6 | 1 | 0.551 | 9.30e-6 | 44 |
| scan: Lev 24:15 w1 to Lev 24:23 w14 | 0.853 | 4.70e-6 | 1 | 0.556 | 8.10e-4 | 8 |
| scan: Lev 4:6 w1 to Lev 4:16 w5 | 0.374 | 4.90e-6 | 1 | 0.192 | 0.0585 | 21 |
| scan: Num 34:27 w5 to Num 35:10 w13 | 0.403 | 4.90e-6 | 1 | 0.544 | 5.40e-6 | 23 |
| scan: 1Chr 15:12 w7 to 1Chr 15:24 w18 | 0.676 | 4.90e-6 | 1 | 0.395 | 0.0110 | 56 |
| scan: Isa 44:27 w1 to Isa 45:10 w8 | 0.621 | 5.00e-6 | 1 | 0.516 | 2.90e-4 | 9 |
| scan: Lev 24:13 w1 to Lev 25:2 w18 | 0.634 | 5.10e-6 | 1 | 0.509 | 1.29e-4 | 11 |
| scan: Ezek 47:23 w1 to Ezek 48:10 w26 | 0.116 | 5.20e-6 | 1 | 0.049 | 0.2317 | 8 |
| scan: Josh 17:4 w1 to Josh 17:15 w21 | 0.405 | 5.30e-6 | 1 | 0.367 | 2.71e-5 | 28 |
| scan: Deut 2:11 w1 to Deut 2:21 w5 | 0.842 | 5.50e-6 | 1 | 0.221 | 0.1791 | 37 |
| scan: Exod 25:29 w1 to Exod 25:40 w7 | 0.572 | 5.70e-6 | 1 | 0.442 | 3.90e-4 | 41 |
| scan: Lev 21:19 w8 to Lev 22:5 w9 | 0.570 | 5.70e-6 | 1 | 0.365 | 0.0082 | 15 |
| scan: Exod 25:29 w1 to Exod 26:1 w5 | 0.648 | 5.90e-6 | 1 | 0.307 | 0.0123 | 44 |
| scan: Lev 4:5 w6 to Lev 4:17 w5 | 0.382 | 5.90e-6 | 1 | 0.208 | 0.0166 | 23 |
| scan: Song 5:2 w5 to Song 5:12 w5 | 0.467 | 5.90e-6 | 1 | 1.000 | 0.1667 | 26 |
| scan: Lev 21:20 w8 to Lev 22:5 w16 | 0.489 | 6.10e-6 | 1 | 0.395 | 0.0027 | 14 |
| scan: Ezek 3:13 w11 to Ezek 3:24 w6 | 0.656 | 6.10e-6 | 1 | 0.497 | 4.50e-4 | 14 |
| scan: Exod 33:4 w1 to Exod 33:14 w1 | 0.408 | 6.30e-6 | 1 | 0.167 | 0.0385 | 11 |
| scan: 1Chr 28:8 w15 to 1Chr 28:20 w11 | 0.642 | 6.30e-6 | 1 | 0.114 | 0.1264 | 19 |
| scan: 1Chr 15:13 w1 to 1Chr 15:22 w9 | 0.734 | 6.60e-6 | 1 | 0.625 | 0.0819 | 46 |
| scan: Exod 37:15 w1 to Exod 37:26 w11 | 0.628 | 6.80e-6 | 0 | - | - | 0 |
| scan: 1Chr 28:11 w1 to 1Chr 28:20 w11 | 0.596 | 6.80e-6 | 1 | 0.220 | 0.0409 | 16 |
| scan: 1Kgs 2:34 w8 to 1Kgs 2:46 w10 | 0.397 | 7.00e-6 | 1 | 0.292 | 4.50e-4 | 18 |
| scan: Num 34:29 w1 to Num 35:10 w13 | 0.398 | 7.10e-6 | 1 | 0.402 | 3.95e-5 | 20 |
| scan: Jer 6:10 w1 to Jer 6:18 w3 | 0.725 | 7.20e-6 | 1 | 0.858 | 0.0222 | 14 |
| scan: Ezek 3:13 w11 to Ezek 3:24 w14 | 0.635 | 7.20e-6 | 1 | 0.522 | 2.40e-4 | 14 |
| scan: 2Kgs 14:21 w1 to 2Kgs 15:2 w15 | 0.387 | 7.30e-6 | 1 | 0.319 | 7.60e-4 | 29 |
| scan: Gen 47:13 w9 to Gen 47:21 w10 | 0.466 | 7.40e-6 | 1 | 0.324 | 3.50e-4 | 15 |
| scan: Exod 33:4 w1 to Exod 33:14 w5 | 0.443 | 7.50e-6 | 1 | 0.167 | 0.0385 | 11 |
| scan: 2Kgs 14:21 w1 to 2Kgs 15:1 w13 | 0.373 | 7.80e-6 | 1 | 0.358 | 7.39e-5 | 27 |
| scan: Exod 25:29 w1 to Exod 25:40 w2 | 0.581 | 8.10e-6 | 1 | 0.522 | 7.96e-5 | 41 |
| scan: Lev 24:12 w3 to Lev 24:23 w22 | 0.744 | 8.10e-6 | 1 | 0.354 | 0.0433 | 11 |
| scan: Eccl 2:23 w12 to Eccl 3:13 w9 | 0.567 | 8.20e-6 | 1 | 0.474 | 9.40e-8 | 14 |
| scan: Lev 21:18 w1 to Lev 22:6 w7 | 0.409 | 8.30e-6 | 1 | 0.260 | 0.0174 | 17 |
| scan: Lev 25:17 w1 to Lev 25:26 w11 | 0.586 | 8.50e-6 | 1 | 0.643 | 0.0016 | 15 |
| scan: Gen 47:13 w9 to Gen 47:21 w5 | 0.461 | 8.60e-6 | 1 | 0.324 | 3.50e-4 | 15 |
| scan: Lev 24:14 w14 to Lev 25:2 w14 | 0.683 | 8.60e-6 | 1 | 0.502 | 7.70e-4 | 11 |
| scan: Judg 1:20 w8 to Judg 1:29 w7 | 0.839 | 8.70e-6 | 1 | 0.465 | 0.0017 | 28 |
| scan: Deut 31:11 w12 to Deut 31:19 w12 | 0.670 | 8.80e-6 | 1 | 0.435 | 0.0020 | 13 |
| scan: 1Chr 15:12 w7 to 1Chr 15:24 w13 | 0.689 | 8.80e-6 | 1 | 0.395 | 0.0110 | 56 |
| scan: Exod 29:39 w6 to Exod 30:2 w10 | 0.906 | 8.90e-6 | 1 | 0.783 | 2.20e-4 | 21 |
| scan: Ezek 43:11 w1 to Ezek 43:19 w18 | 0.670 | 9.00e-6 | 1 | 0.273 | 0.0194 | 26 |
| scan: Gen 47:13 w9 to Gen 47:20 w19 | 0.461 | 9.20e-6 | 1 | 0.321 | 6.20e-4 | 14 |
| scan: Ezek 47:22 w1 to Ezek 48:11 w7 | 0.278 | 9.20e-6 | 1 | 0.254 | 0.0032 | 10 |
| scan: Ezek 47:21 w1 to Ezek 48:12 w10 | 0.304 | 9.40e-6 | 1 | 0.252 | 0.0034 | 12 |
| scan: Gen 25:22 w1 to Gen 25:32 w10 | 0.488 | 9.90e-6 | 1 | 0.409 | 0.0034 | 14 |
| scan: Ezek 3:4 w3 to Ezek 3:11 w15 | 0.717 | 9.90e-6 | 1 | 0.150 | 0.2585 | 8 |
| scan: Exod 37:15 w1 to Exod 37:25 w6 | 0.610 | 1.00e-5 | 0 | - | - | 0 |
| scan: Josh 15:9 w14 to Josh 15:21 w13 | 0.722 | 1.01e-5 | 1 | 0.510 | 8.40e-4 | 42 |
| scan: 1Chr 27:23 w1 to 1Chr 28:1 w31 | 0.393 | 1.02e-5 | 1 | -0.120 | 0.8150 | 41 |
| scan: Dan 2:33 w4 to Dan 2:42 w6 | 0.365 | 1.02e-5 | 1 | 0.339 | 0.0053 | 15 |
| scan: 2Chr 30:2 w1 to 2Chr 30:13 w13 | 0.445 | 1.03e-5 | 1 | 0.603 | 2.52e-7 | 13 |
| scan: Ezek 3:13 w1 to Ezek 3:24 w14 | 0.598 | 1.03e-5 | 1 | 0.497 | 4.50e-4 | 14 |
| scan: Ezek 47:22 w13 to Ezek 48:11 w16 | 0.240 | 1.05e-5 | 1 | 0.274 | 0.0029 | 10 |
| scan: 1Kgs 17:23 w11 to 1Kgs 18:9 w3 | 0.488 | 1.06e-5 | 1 | 0.132 | 0.0756 | 18 |
| scan: Josh 17:5 w1 to Josh 17:14 w23 | 0.324 | 1.07e-5 | 1 | 0.353 | 6.81e-5 | 26 |
| scan: Exod 33:5 w1 to Exod 33:13 w20 | 0.470 | 1.08e-5 | 1 | 0.159 | 0.0521 | 9 |
| scan: Lev 4:6 w6 to Lev 4:18 w12 | 0.415 | 1.08e-5 | 1 | 0.168 | 0.0396 | 26 |
| scan: 2Sam 18:3 w1 to 2Sam 18:12 w17 | 0.514 | 1.08e-5 | 1 | 0.062 | 0.3563 | 37 |
| scan: Ezek 47:22 w13 to Ezek 48:10 w22 | 0.130 | 1.08e-5 | 1 | 0.160 | 0.0200 | 9 |
| scan: Ezek 3:14 w4 to Ezek 3:23 w18 | 0.697 | 1.10e-5 | 1 | 0.477 | 0.0058 | 11 |
| scan: Lev 4:33 w1 to Lev 5:9 w14 | 0.442 | 1.14e-5 | 1 | 0.247 | 5.40e-4 | 26 |
| scan: Exod 39:41 w1 to Exod 40:10 w7 | 0.804 | 1.16e-5 | 1 | 0.787 | 5.07e-5 | 14 |
| scan: Dan 2:35 w22 to Dan 2:46 w13 | 0.296 | 1.16e-5 | 1 | 0.138 | 0.0911 | 23 |
| scan: Eccl 2:24 w11 to Eccl 3:14 w15 | 0.581 | 1.17e-5 | 1 | 0.491 | 5.90e-8 | 11 |
| scan: Ezek 4:17 w5 to Ezek 5:12 w10 | 0.525 | 1.17e-5 | 1 | 0.341 | 0.0025 | 23 |
| scan: Ezek 47:13 w1 to Ezek 48:1 w3 | 0.524 | 1.17e-5 | 1 | -0.225 | 0.9446 | 27 |
| scan: Exod 37:14 w5 to Exod 37:26 w11 | 0.598 | 1.18e-5 | 0 | - | - | 0 |
| scan: Ezek 5:1 w1 to Ezek 5:12 w17 | 0.562 | 1.20e-5 | 1 | 0.459 | 1.15e-5 | 20 |
| scan: Exod 37:14 w1 to Exod 37:25 w6 | 0.581 | 1.21e-5 | 0 | - | - | 0 |
| scan: 2Chr 6:3 w1 to 2Chr 6:13 w29 | 0.455 | 1.21e-5 | 1 | 0.344 | 0.0017 | 4 |
| scan: Ezek 47:20 w10 to Ezek 48:11 w16 | 0.223 | 1.21e-5 | 1 | 0.197 | 0.0033 | 13 |
| scan: Exod 30:13 w1 to Exod 30:25 w13 | 0.640 | 1.22e-5 | 1 | 0.498 | 0.0042 | 23 |
| scan: Jer 25:16 w1 to Jer 25:29 w13 | 0.531 | 1.22e-5 | 0 | - | - | 0 |
| scan: Gen 37:26 w5 to Gen 38:1 w7 | 0.608 | 1.23e-5 | 1 | 0.619 | 5.93e-5 | 16 |
| scan: Lev 25:17 w1 to Lev 25:26 w6 | 0.585 | 1.23e-5 | 1 | 0.670 | 0.0053 | 15 |
| scan: 1Chr 15:7 w3 to 1Chr 15:19 w4 | 0.450 | 1.24e-5 | 1 | 0.260 | 0.0076 | 41 |
| scan: Josh 17:4 w21 to Josh 17:14 w23 | 0.372 | 1.26e-5 | 1 | 0.442 | 1.66e-5 | 27 |
| scan: Ezek 47:21 w1 to Ezek 48:10 w22 | 0.198 | 1.26e-5 | 1 | 0.181 | 0.0148 | 10 |
| scan: Gen 47:13 w1 to Gen 47:22 w5 | 0.427 | 1.31e-5 | 1 | 0.191 | 0.0093 | 15 |
| scan: Exod 37:3 w1 to Exod 37:13 w14 | 0.522 | 1.31e-5 | 1 | 0.227 | 0.1491 | 23 |
| scan: Isa 34:14 w9 to Isa 35:9 w11 | 0.718 | 1.33e-5 | 1 | 0.486 | 7.40e-4 | 20 |
| scan: Eccl 2:24 w1 to Eccl 3:13 w9 | 0.609 | 1.34e-5 | 1 | 0.530 | 1.69e-7 | 11 |
| scan: Lev 21:14 w1 to Lev 21:24 w6 | 0.598 | 1.35e-5 | 1 | 0.320 | 0.0535 | 13 |
| scan: Deut 4:12 w1 to Deut 4:22 w9 | 0.517 | 1.35e-5 | 1 | 0.311 | 0.0177 | 7 |
| scan: Exod 25:29 w1 to Exod 26:1 w16 | 0.615 | 1.36e-5 | 1 | 0.307 | 0.0123 | 44 |
| scan: 2Kgs 3:27 w1 to 2Kgs 4:9 w14 | 0.521 | 1.36e-5 | 1 | 0.388 | 8.20e-4 | 9 |
| scan: Deut 28:65 w1 to Deut 29:5 w14 | 0.640 | 1.38e-5 | 1 | 0.551 | 0.0070 | 8 |
| scan: Exod 33:2 w1 to Exod 33:14 w1 | 0.372 | 1.39e-5 | 1 | 0.233 | 0.0180 | 22 |
| scan: Ezek 43:10 w1 to Ezek 43:19 w18 | 0.625 | 1.40e-5 | 1 | 0.290 | 0.0019 | 27 |
| scan: Dan 2:33 w4 to Dan 2:41 w27 | 0.329 | 1.40e-5 | 1 | 0.348 | 0.0278 | 13 |
| scan: 1Chr 28:9 w1 to 1Chr 28:20 w27 | 0.535 | 1.43e-5 | 1 | 0.145 | 0.0863 | 18 |
| scan: Lev 13:28 w1 to Lev 13:39 w14 | 0.204 | 1.44e-5 | 1 | 0.137 | 0.0398 | 45 |
| scan: Judg 1:19 w8 to Judg 1:29 w7 | 0.696 | 1.45e-5 | 1 | 0.291 | 0.0110 | 32 |
| scan: Isa 54:1 w1 to Isa 54:12 w6 | 0.501 | 1.47e-5 | 1 | 0.091 | 0.3856 | 16 |
| scan: Zech 4:7 w8 to Zech 5:5 w4 | 0.426 | 1.47e-5 | 1 | 0.343 | 0.0125 | 15 |
| scan: Exod 29:39 w1 to Exod 30:3 w16 | 0.693 | 1.49e-5 | 1 | 0.630 | 1.70e-4 | 25 |
| scan: Lev 4:5 w6 to Lev 4:16 w8 | 0.383 | 1.49e-5 | 1 | 0.220 | 0.0245 | 21 |
| scan: Deut 34:2 w1 to Deut 34:12 w6 | 0.543 | 1.49e-5 | 1 | 0.193 | 0.0896 | 13 |
| scan: Ezek 42:12 w9 to Ezek 43:4 w5 | 0.534 | 1.49e-5 | 1 | 0.108 | 0.1769 | 23 |
| scan: Lev 24:11 w12 to Lev 24:23 w22 | 0.756 | 1.50e-5 | 1 | 0.467 | 0.0028 | 13 |
| scan: 2Chr 11:15 w1 to 2Chr 12:2 w14 | 0.478 | 1.50e-5 | 1 | 0.383 | 0.0048 | 19 |
| scan: 1Kgs 9:1 w1 to 1Kgs 9:11 w22 | 0.385 | 1.51e-5 | 1 | 0.350 | 6.80e-4 | 15 |
| scan: 2Kgs 3:27 w1 to 2Kgs 4:9 w11 | 0.534 | 1.51e-5 | 1 | 0.272 | 0.0176 | 9 |
| scan: Ezek 47:21 w1 to Ezek 48:13 w11 | 0.236 | 1.52e-5 | 1 | 0.204 | 0.0056 | 12 |
| scan: Exod 33:3 w6 to Exod 33:15 w9 | 0.417 | 1.53e-5 | 1 | 0.243 | 0.0022 | 16 |
| scan: Josh 4:20 w10 to Josh 5:4 w5 | 0.535 | 1.53e-5 | 1 | 0.248 | 0.0625 | 15 |
| scan: 2Kgs 14:19 w7 to 2Kgs 15:2 w11 | 0.376 | 1.54e-5 | 1 | 0.394 | 7.81e-5 | 32 |
| scan: Gen 36:29 w1 to Gen 36:40 w13 | 0.483 | 1.55e-5 | 1 | 0.590 | 9.00e-8 | 43 |
| scan: Exod 33:4 w8 to Exod 33:14 w1 | 0.445 | 1.55e-5 | 1 | 0.167 | 0.0385 | 11 |
| scan: Lev 4:5 w1 to Lev 4:16 w8 | 0.334 | 1.55e-5 | 1 | 0.214 | 0.0209 | 21 |
| scan: Exod 25:28 w1 to Exod 25:40 w7 | 0.559 | 1.57e-5 | 1 | 0.551 | 9.30e-6 | 44 |
| scan: Lev 21:12 w10 to Lev 22:1 w5 | 0.545 | 1.57e-5 | 1 | 0.310 | 0.0129 | 13 |
| scan: 1Chr 28:9 w1 to 1Chr 28:20 w11 | 0.641 | 1.58e-5 | 1 | 0.145 | 0.0863 | 18 |
| scan: 2Chr 11:14 w10 to 2Chr 12:3 w6 | 0.437 | 1.58e-5 | 1 | 0.357 | 0.0038 | 24 |
| scan: Lev 21:13 w1 to Lev 22:2 w14 | 0.541 | 1.60e-5 | 1 | 0.494 | 8.60e-4 | 13 |
| scan: Exod 37:3 w1 to Exod 37:14 w9 | 0.499 | 1.61e-5 | 0 | - | - | 0 |
| scan: Deut 10:3 w10 to Deut 10:10 w9 | 0.719 | 1.61e-5 | 1 | 0.003 | 0.4783 | 16 |
| scan: Ezek 3:13 w1 to Ezek 3:24 w6 | 0.698 | 1.61e-5 | 1 | 0.108 | 0.2905 | 14 |
| scan: 1Chr 27:24 w1 to 1Chr 28:1 w31 | 0.439 | 1.62e-5 | 1 | -0.028 | 0.5635 | 40 |
| scan: 1Chr 6:26 w1 to 1Chr 6:36 w8 | 0.542 | 1.63e-5 | 1 | -0.001 | 0.6004 | 25 |
| scan: 2Sam 3:15 w1 to 2Sam 3:23 w18 | 0.238 | 1.66e-5 | 1 | 0.015 | 0.4368 | 21 |
| scan: 2Kgs 14:21 w1 to 2Kgs 15:2 w11 | 0.379 | 1.67e-5 | 1 | 0.319 | 7.60e-4 | 29 |
| scan: 2Chr 11:15 w6 to 2Chr 12:2 w14 | 0.495 | 1.68e-5 | 1 | 0.383 | 0.0048 | 19 |
| scan: Ezek 42:12 w9 to Ezek 43:3 w21 | 0.561 | 1.72e-5 | 1 | 0.106 | 0.2036 | 23 |
| scan: Gen 37:1 w6 to Gen 37:13 w11 | 0.464 | 1.73e-5 | 1 | 0.198 | 0.0268 | 14 |
| scan: Exod 15:14 w1 to Exod 15:26 w27 | 0.604 | 1.73e-5 | 1 | 0.228 | 0.0723 | 23 |
| scan: Zech 8:15 w12 to Zech 9:3 w10 | 0.403 | 1.77e-5 | 1 | 0.410 | 9.60e-4 | 10 |
| scan: Zech 8:16 w1 to Zech 9:3 w4 | 0.403 | 1.77e-5 | 1 | 0.491 | 9.32e-5 | 8 |
| scan: 1Chr 27:24 w13 to 1Chr 27:34 w10 | 0.497 | 1.78e-5 | 1 | -0.289 | 0.9667 | 36 |
| scan: Ezek 47:20 w10 to Ezek 48:12 w10 | 0.218 | 1.79e-5 | 1 | 0.196 | 0.0041 | 14 |
| scan: Lev 21:13 w1 to Lev 21:24 w10 | 0.577 | 1.83e-5 | 1 | 0.320 | 0.0535 | 13 |
| scan: Judg 1:19 w8 to Judg 1:30 w9 | 0.625 | 1.83e-5 | 1 | 0.469 | 6.81e-5 | 34 |
| scan: Ezek 48:16 w1 to Ezek 48:28 w7 | 0.454 | 1.83e-5 | 1 | 0.201 | 0.0367 | 10 |
| scan: Jer 51:16 w1 to Jer 51:26 w13 | 0.630 | 1.85e-5 | 1 | 0.360 | 0.0012 | 10 |
| scan: Exod 25:28 w1 to Exod 25:40 w2 | 0.564 | 1.87e-5 | 1 | 0.551 | 9.30e-6 | 44 |
| scan: 2Sam 14:25 w1 to 2Sam 15:2 w31 | 0.329 | 1.89e-5 | 1 | 0.593 | 2.52e-5 | 42 |
| scan: 1Chr 28:12 w1 to 1Chr 28:20 w27 | 0.540 | 1.92e-5 | 1 | 0.320 | 0.0204 | 15 |
| scan: Lev 21:20 w8 to Lev 22:4 w25 | 0.487 | 1.93e-5 | 1 | 0.269 | 0.0524 | 12 |
| scan: Isa 44:27 w1 to Isa 45:10 w5 | 0.611 | 1.94e-5 | 1 | 0.516 | 2.90e-4 | 9 |
| scan: Exod 39:41 w6 to Exod 40:10 w14 | 0.806 | 1.95e-5 | 1 | 0.740 | 7.09e-5 | 14 |
| scan: 2Chr 11:15 w6 to 2Chr 12:2 w11 | 0.493 | 1.95e-5 | 1 | 0.383 | 0.0048 | 19 |
| scan: Exod 28:14 w10 to Exod 28:24 w8 | 0.742 | 1.97e-5 | 0 | - | - | 0 |
| scan: Josh 15:10 w1 to Josh 15:22 w3 | 0.703 | 1.98e-5 | 1 | 0.497 | 3.00e-4 | 38 |
| scan: Zech 4:7 w1 to Zech 5:5 w4 | 0.392 | 2.00e-5 | 1 | 0.343 | 0.0125 | 15 |
| scan: Lev 4:33 w7 to Lev 5:9 w12 | 0.485 | 2.01e-5 | 1 | 0.247 | 5.40e-4 | 26 |
| scan: 2Chr 11:16 w1 to 2Chr 12:3 w6 | 0.559 | 2.01e-5 | 1 | 0.420 | 0.0117 | 19 |
| scan: Gen 2:16 w7 to Gen 3:2 w8 | 0.518 | 2.03e-5 | 1 | 0.460 | 3.70e-4 | 5 |
| scan: 1Kgs 13:31 w18 to 1Kgs 14:9 w6 | 0.271 | 2.04e-5 | 0 | - | - | 0 |
| scan: Isa 44:28 w7 to Isa 45:9 w17 | 0.704 | 2.04e-5 | 1 | 0.375 | 0.0450 | 7 |
| scan: Jer 3:12 w17 to Jer 3:21 w16 | 0.541 | 2.04e-5 | 1 | -0.043 | 0.6137 | 15 |
| scan: Lev 24:13 w1 to Lev 24:23 w22 | 0.747 | 2.06e-5 | 1 | 0.354 | 0.0472 | 10 |
| scan: Ezek 47:18 w18 to Ezek 48:7 w10 | 0.185 | 2.08e-5 | 1 | 0.091 | 0.0829 | 18 |
| scan: 1Chr 28:9 w22 to 1Chr 28:20 w11 | 0.544 | 2.09e-5 | 1 | 0.145 | 0.0863 | 18 |
| scan: Lev 4:32 w1 to Lev 5:8 w16 | 0.440 | 2.13e-5 | 1 | 0.185 | 0.0044 | 23 |
| scan: Exod 40:7 w1 to Exod 40:18 w13 | 0.581 | 2.14e-5 | 0 | - | - | 0 |
| scan: Exod 40:7 w1 to Exod 40:18 w16 | 0.581 | 2.14e-5 | 0 | - | - | 0 |
| scan: Lev 21:18 w9 to Lev 22:4 w25 | 0.478 | 2.14e-5 | 1 | 0.277 | 0.0345 | 14 |
| scan: Gen 47:13 w1 to Gen 47:22 w23 | 0.395 | 2.16e-5 | 1 | 0.187 | 0.0080 | 15 |
| scan: Deut 5:24 w15 to Deut 5:33 w17 | 0.311 | 2.16e-5 | 1 | 0.443 | 0.0032 | 5 |
| scan: Exod 33:2 w4 to Exod 33:13 w20 | 0.370 | 2.18e-5 | 1 | 0.233 | 0.0180 | 22 |
| scan: Lev 4:5 w6 to Lev 4:16 w5 | 0.335 | 2.20e-5 | 1 | 0.214 | 0.0209 | 21 |
| scan: Deut 21:2 w4 to Deut 21:14 w11 | 0.666 | 2.22e-5 | 1 | 0.121 | 0.3605 | 20 |
| scan: Exod 33:5 w18 to Exod 33:13 w15 | 0.443 | 2.23e-5 | 1 | 0.159 | 0.0521 | 9 |
| scan: 1Chr 27:28 w1 to 1Chr 28:5 w18 | 0.455 | 2.26e-5 | 1 | -0.367 | 0.9715 | 30 |
| scan: Judg 11:32 w8 to Judg 12:3 w14 | 0.505 | 2.27e-5 | 1 | 0.470 | 3.10e-6 | 25 |
| scan: 1Chr 5:12 w1 to 1Chr 5:25 w3 | 0.658 | 2.28e-5 | 1 | 0.552 | 0.0115 | 44 |
| scan: Isa 44:27 w4 to Isa 45:10 w5 | 0.591 | 2.29e-5 | 1 | 0.516 | 2.90e-4 | 9 |
| scan: 1Chr 28:8 w1 to 1Chr 28:20 w11 | 0.684 | 2.32e-5 | 1 | -0.228 | 0.9871 | 19 |
| scan: Lev 21:14 w9 to Lev 21:23 w20 | 0.630 | 2.34e-5 | 1 | 0.235 | 0.1290 | 13 |
| scan: Ezek 23:46 w6 to Ezek 24:8 w10 | 0.701 | 2.35e-5 | 1 | -0.178 | 0.6361 | 28 |
| scan: 1Sam 28:12 w1 to 1Sam 28:23 w16 | 0.397 | 2.38e-5 | 1 | 0.358 | 1.40e-4 | 12 |
| scan: Josh 15:10 w1 to Josh 15:21 w10 | 0.702 | 2.40e-5 | 1 | 0.507 | 5.70e-4 | 36 |
| scan: Ezek 43:10 w12 to Ezek 43:19 w18 | 0.725 | 2.40e-5 | 1 | 0.374 | 0.0016 | 27 |
| scan: Ezek 43:11 w1 to Ezek 43:19 w14 | 0.725 | 2.40e-5 | 1 | 0.273 | 0.0194 | 26 |
| scan: Deut 2:11 w1 to Deut 2:20 w13 | 0.853 | 2.42e-5 | 1 | 0.729 | 0.0112 | 33 |
| scan: Jer 25:16 w1 to Jer 25:28 w15 | 0.491 | 2.42e-5 | 0 | - | - | 0 |
| scan: 1Chr 5:13 w1 to 1Chr 5:25 w3 | 0.703 | 2.43e-5 | 1 | 0.668 | 6.00e-4 | 41 |
| scan: 1Chr 16:34 w1 to 1Chr 16:42 w9 | 0.713 | 2.43e-5 | 1 | 0.521 | 0.0066 | 20 |
| scan: Gen 37:26 w1 to Gen 38:1 w13 | 0.543 | 2.44e-5 | 1 | 0.619 | 5.93e-5 | 16 |
| scan: Lev 21:20 w8 to Lev 22:6 w7 | 0.469 | 2.46e-5 | 1 | 0.294 | 0.0156 | 15 |
| scan: 1Chr 28:12 w13 to 1Chr 28:21 w8 | 0.555 | 2.50e-5 | 1 | 0.411 | 0.0010 | 16 |
| scan: Ezek 3:14 w1 to Ezek 3:24 w14 | 0.564 | 2.54e-5 | 1 | 0.514 | 7.00e-4 | 12 |
| scan: Num 34:28 w1 to Num 35:10 w6 | 0.350 | 2.55e-5 | 1 | 0.542 | 4.00e-6 | 22 |
| scan: Neh 7:64 w7 to Neh 8:3 w17 | 0.627 | 2.55e-5 | 1 | 0.369 | 0.0418 | 19 |
| scan: Lev 24:15 w6 to Lev 24:23 w22 | 0.776 | 2.56e-5 | 1 | 0.556 | 8.10e-4 | 8 |
| scan: Lev 4:6 w6 to Lev 4:17 w5 | 0.309 | 2.58e-5 | 1 | 0.309 | 0.0013 | 23 |
| scan: Exod 37:14 w5 to Exod 37:25 w6 | 0.527 | 2.59e-5 | 0 | - | - | 0 |
| scan: 1Chr 15:7 w1 to 1Chr 15:18 w19 | 0.431 | 2.59e-5 | 1 | 0.280 | 0.0043 | 37 |
| scan: Ezek 3:12 w8 to Ezek 3:24 w6 | 0.668 | 2.60e-5 | 1 | 0.121 | 0.2470 | 15 |
| scan: Exod 13:16 w8 to Exod 14:5 w21 | 0.552 | 2.61e-5 | 1 | 0.475 | 4.30e-4 | 21 |
| scan: Lev 21:14 w9 to Lev 21:24 w10 | 0.577 | 2.61e-5 | 1 | 0.360 | 0.0310 | 13 |
| scan: Exod 37:15 w9 to Exod 37:26 w11 | 0.585 | 2.63e-5 | 0 | - | - | 0 |
| scan: Jer 25:30 w1 to Jer 26:2 w26 | 0.606 | 2.63e-5 | 1 | 0.479 | 0.0039 | 17 |
| scan: Judg 16:28 w6 to Judg 17:8 w17 | 0.579 | 2.68e-5 | 1 | 0.471 | 0.0011 | 16 |
| scan: Ezek 20:1 w14 to Ezek 20:13 w21 | 0.483 | 2.68e-5 | 1 | 0.625 | 1.10e-4 | 12 |
| scan: Exod 28:14 w10 to Exod 28:22 w7 | 0.837 | 2.69e-5 | 1 | 0.044 | 0.4169 | 33 |
| scan: 2Kgs 14:20 w5 to 2Kgs 15:3 w4 | 0.345 | 2.70e-5 | 1 | 0.322 | 2.20e-4 | 31 |
| scan: Gen 3:24 w4 to Gen 4:11 w14 | 0.250 | 2.72e-5 | 1 | 0.165 | 0.0293 | 4 |
| scan: Judg 1:18 w11 to Judg 1:30 w9 | 0.529 | 2.73e-5 | 1 | 0.227 | 0.0065 | 38 |
| scan: Zech 4:7 w8 to Zech 5:4 w21 | 0.394 | 2.78e-5 | 1 | 0.519 | 4.10e-4 | 15 |
| scan: Num 1:2 w11 to Num 1:18 w19 | 0.484 | 2.82e-5 | 1 | 0.575 | 5.40e-6 | 29 |
| scan: Deut 6:21 w7 to Deut 7:8 w22 | 0.401 | 2.82e-5 | 1 | 0.213 | 0.0145 | 25 |
| scan: Lev 4:13 w1 to Lev 4:22 w14 | 0.435 | 2.85e-5 | 1 | 0.366 | 2.50e-4 | 16 |
| scan: Lev 24:12 w1 to Lev 24:23 w22 | 0.732 | 2.85e-5 | 1 | 0.354 | 0.0433 | 11 |
| scan: Ezek 47:20 w10 to Ezek 48:12 w7 | 0.271 | 2.85e-5 | 1 | 0.196 | 0.0060 | 14 |
| scan: 1Chr 15:7 w3 to 1Chr 15:18 w3 | 0.443 | 2.86e-5 | 1 | 0.280 | 0.0043 | 37 |
| scan: Judg 16:29 w1 to Judg 17:8 w9 | 0.571 | 2.88e-5 | 1 | 0.491 | 0.0011 | 15 |
| scan: Ezek 43:12 w4 to Ezek 43:19 w18 | 0.715 | 2.89e-5 | 1 | 0.206 | 0.0683 | 21 |
| scan: Exod 33:2 w4 to Exod 33:14 w1 | 0.382 | 2.90e-5 | 1 | 0.233 | 0.0180 | 22 |
| scan: Deut 4:12 w1 to Deut 4:21 w21 | 0.488 | 2.90e-5 | 1 | 0.229 | 0.0025 | 6 |
| scan: Exod 37:16 w1 to Exod 37:25 w6 | 0.613 | 2.91e-5 | 0 | - | - | 0 |
| scan: 1Sam 4:21 w1 to 1Sam 5:8 w24 | 0.425 | 2.94e-5 | 1 | 0.304 | 0.0046 | 33 |
| scan: Deut 2:11 w1 to Deut 2:20 w5 | 0.877 | 2.99e-5 | 1 | 0.826 | 0.0019 | 33 |
| scan: Exod 28:15 w1 to Exod 28:23 w14 | 0.876 | 3.01e-5 | 0 | - | - | 0 |
| scan: Exod 28:14 w1 to Exod 28:22 w9 | 0.747 | 3.02e-5 | 1 | 0.044 | 0.4169 | 33 |
| scan: Exod 2:7 w13 to Exod 2:16 w4 | 0.604 | 3.06e-5 | 1 | 0.411 | 0.0010 | 11 |
| scan: Deut 2:11 w6 to Deut 2:21 w5 | 0.891 | 3.07e-5 | 1 | 0.221 | 0.1791 | 37 |
| scan: 1Kgs 13:31 w1 to 1Kgs 14:9 w6 | 0.268 | 3.07e-5 | 0 | - | - | 0 |
| scan: 1Chr 6:58 w1 to 1Chr 6:69 w9 | 0.562 | 3.08e-5 | 1 | 0.027 | 0.2767 | 37 |
| scan: Num 34:26 w5 to Num 35:9 w5 | 0.397 | 3.09e-5 | 1 | 0.398 | 9.90e-4 | 24 |
| scan: 1Kgs 20:31 w1 to 1Kgs 20:41 w13 | 0.403 | 3.11e-5 | 1 | 0.286 | 0.0019 | 14 |
| scan: 2Chr 11:15 w1 to 2Chr 12:3 w16 | 0.455 | 3.11e-5 | 1 | 0.417 | 0.0015 | 22 |
| scan: Exod 28:14 w10 to Exod 28:24 w11 | 0.709 | 3.15e-5 | 0 | - | - | 0 |
| scan: Num 7:87 w16 to Num 8:8 w14 | 0.783 | 3.15e-5 | 1 | 0.712 | 1.80e-4 | 14 |
| scan: 1Kgs 2:35 w1 to 1Kgs 2:46 w14 | 0.371 | 3.18e-5 | 1 | 0.287 | 1.80e-4 | 17 |
| scan: Ezek 47:12 w25 to Ezek 48:1 w3 | 0.558 | 3.21e-5 | 1 | -0.260 | 0.9698 | 29 |
| scan: Exod 33:3 w1 to Exod 33:13 w20 | 0.380 | 3.22e-5 | 1 | 0.233 | 0.0180 | 15 |
| scan: 1Chr 15:13 w1 to 1Chr 15:24 w18 | 0.647 | 3.22e-5 | 1 | 0.608 | 0.0021 | 53 |
| scan: Ezra 3:7 w1 to Ezra 4:5 w15 | 0.520 | 3.23e-5 | 1 | 0.490 | 1.69e-5 | 27 |
| scan: Dan 2:33 w1 to Dan 2:42 w6 | 0.302 | 3.23e-5 | 1 | 0.328 | 0.0060 | 15 |
| scan: Dan 2:35 w22 to Dan 2:47 w15 | 0.289 | 3.24e-5 | 1 | 0.146 | 0.0674 | 24 |
| scan: Judg 1:20 w1 to Judg 1:29 w11 | 0.783 | 3.25e-5 | 1 | 0.465 | 0.0017 | 28 |
| scan: Ezek 47:21 w1 to Ezek 48:10 w26 | 0.282 | 3.27e-5 | 1 | 0.181 | 0.0221 | 10 |
| scan: Exod 37:14 w5 to Exod 37:25 w16 | 0.564 | 3.29e-5 | 0 | - | - | 0 |
| scan: Exod 37:15 w1 to Exod 37:25 w16 | 0.564 | 3.29e-5 | 0 | - | - | 0 |
| scan: Num 34:28 w5 to Num 35:10 w6 | 0.362 | 3.31e-5 | 1 | 0.542 | 4.00e-6 | 22 |
| scan: 2Chr 11:16 w13 to 2Chr 12:2 w14 | 0.588 | 3.32e-5 | 1 | 0.387 | 0.0196 | 16 |
| scan: 1Chr 27:23 w9 to 1Chr 28:1 w31 | 0.402 | 3.33e-5 | 1 | -0.120 | 0.8150 | 41 |
| scan: Lev 24:13 w1 to Lev 24:23 w14 | 0.777 | 3.36e-5 | 1 | 0.354 | 0.0472 | 10 |
| scan: Lev 22:8 w7 to Lev 22:16 w11 | 0.426 | 3.37e-5 | 1 | 0.305 | 0.0095 | 10 |
| scan: Josh 18:14 w1 to Josh 18:21 w6 | 0.499 | 3.38e-5 | 1 | 0.255 | 0.0094 | 28 |
| scan: Esth 6:12 w1 to Esth 7:10 w8 | 0.223 | 3.38e-5 | 0 | - | - | 0 |
| scan: 1Chr 24:17 w1 to 1Chr 25:1 w18 | 0.337 | 3.41e-5 | 1 | 0.194 | 0.0013 | 38 |
| scan: Lev 21:12 w1 to Lev 21:24 w10 | 0.465 | 3.43e-5 | 1 | 0.376 | 0.0040 | 13 |
| scan: Exod 28:15 w1 to Exod 28:24 w11 | 0.837 | 3.44e-5 | 0 | - | - | 0 |
| scan: 1Kgs 13:32 w1 to 1Kgs 14:8 w23 | 0.224 | 3.44e-5 | 0 | - | - | 0 |
| scan: 1Chr 15:2 w1 to 1Chr 15:14 w3 | 0.540 | 3.51e-5 | 1 | 0.435 | 7.60e-4 | 19 |
| scan: Exod 15:14 w4 to Exod 15:26 w27 | 0.607 | 3.52e-5 | 1 | 0.228 | 0.0723 | 23 |
| scan: 2Chr 30:2 w1 to 2Chr 30:13 w10 | 0.445 | 3.54e-5 | 1 | 0.571 | 1.47e-5 | 13 |
| scan: Isa 42:23 w1 to Isa 43:9 w12 | 0.802 | 3.54e-5 | 1 | 0.332 | 0.2042 | 12 |
| scan: Exod 30:13 w1 to Exod 30:25 w9 | 0.657 | 3.55e-5 | 1 | 0.498 | 0.0042 | 23 |
| scan: Judg 1:19 w1 to Judg 1:30 w14 | 0.525 | 3.55e-5 | 1 | 0.469 | 6.81e-5 | 34 |
| scan: Lev 21:12 w10 to Lev 21:24 w6 | 0.501 | 3.56e-5 | 1 | 0.376 | 0.0040 | 13 |
| scan: Lev 3:15 w1 to Lev 4:10 w5 | 0.470 | 3.57e-5 | 1 | 0.371 | 0.0206 | 26 |
| scan: Exod 29:39 w1 to Exod 30:4 w20 | 0.550 | 3.62e-5 | 1 | 0.283 | 0.0239 | 31 |
| scan: Ezek 2:6 w18 to Ezek 3:7 w20 | 0.340 | 3.62e-5 | 1 | 0.273 | 0.0112 | 11 |
| scan: Exod 14:7 w1 to Exod 14:17 w14 | 0.494 | 3.63e-5 | 1 | 0.250 | 0.0267 | 15 |
| scan: Deut 28:64 w10 to Deut 29:6 w7 | 0.521 | 3.64e-5 | 1 | 0.367 | 0.0181 | 10 |
| scan: 2Kgs 14:20 w1 to 2Kgs 15:2 w11 | 0.373 | 3.64e-5 | 1 | 0.333 | 7.50e-4 | 29 |
| scan: Deut 34:1 w14 to Deut 34:12 w12 | 0.457 | 3.65e-5 | 1 | 0.000 | 0.5009 | 20 |
| scan: Jer 25:15 w1 to Jer 25:28 w15 | 0.493 | 3.67e-5 | 0 | - | - | 0 |
| scan: Deut 21:3 w1 to Deut 21:14 w17 | 0.597 | 3.68e-5 | 1 | 0.751 | 0.0068 | 19 |
| scan: 2Sam 11:24 w10 to 2Sam 12:9 w18 | 0.445 | 3.71e-5 | 1 | 0.344 | 5.20e-4 | 20 |
| scan: Obad 1:8 w6 to Obad 1:19 w18 | 0.743 | 3.74e-5 | 1 | 0.473 | 0.0093 | 29 |
| scan: Lev 26:7 w1 to Lev 26:17 w13 | 0.746 | 3.75e-5 | 1 | 0.571 | 0.0129 | 18 |
| scan: 1Chr 9:38 w1 to 1Chr 10:5 w6 | 0.736 | 3.79e-5 | 1 | 0.595 | 3.27e-5 | 32 |
| scan: Lev 21:14 w1 to Lev 22:1 w5 | 0.549 | 3.81e-5 | 1 | 0.414 | 0.0106 | 13 |
| scan: 1Chr 15:13 w5 to 1Chr 15:24 w13 | 0.668 | 3.86e-5 | 1 | 0.608 | 0.0021 | 53 |
| scan: 2Kgs 4:1 w1 to 2Kgs 4:9 w11 | 0.508 | 3.90e-5 | 1 | 0.379 | 0.0038 | 7 |
| scan: Ezek 2:6 w18 to Ezek 3:8 w7 | 0.317 | 3.92e-5 | 1 | 0.263 | 0.0097 | 12 |
| scan: Gen 47:14 w1 to Gen 47:20 w19 | 0.412 | 3.93e-5 | 1 | 0.302 | 0.0070 | 13 |
| scan: 1Chr 6:26 w2 to 1Chr 6:35 w8 | 0.691 | 3.93e-5 | 1 | -0.002 | 0.5999 | 22 |
| scan: Jer 42:12 w1 to Jer 42:21 w12 | 0.358 | 3.93e-5 | 1 | 0.335 | 0.0062 | 8 |
| scan: Exod 37:2 w6 to Exod 37:14 w4 | 0.449 | 3.94e-5 | 0 | - | - | 0 |
| scan: Lev 21:15 w1 to Lev 21:24 w6 | 0.596 | 3.94e-5 | 1 | 0.360 | 0.0310 | 11 |
| scan: 2Chr 8:12 w6 to 2Chr 9:6 w15 | 0.369 | 3.94e-5 | 1 | 0.218 | 0.0037 | 17 |
| scan: Lev 21:23 w13 to Lev 22:9 w14 | 0.482 | 3.96e-5 | 1 | 0.411 | 0.0052 | 13 |
| scan: Lev 24:14 w1 to Lev 24:23 w22 | 0.738 | 3.99e-5 | 1 | 0.555 | 0.0011 | 10 |
| scan: 2Chr 11:15 w1 to 2Chr 12:3 w6 | 0.467 | 4.00e-5 | 1 | 0.407 | 0.0029 | 22 |
| scan: Exod 25:29 w9 to Exod 25:40 w2 | 0.549 | 4.05e-5 | 1 | 0.442 | 3.90e-4 | 41 |
| scan: Deut 2:11 w6 to Deut 2:21 w11 | 0.822 | 4.06e-5 | 1 | 0.199 | 0.1662 | 37 |
| scan: Num 1:3 w9 to Num 1:17 w3 | 0.516 | 4.07e-5 | 1 | 0.448 | 2.30e-4 | 23 |
| scan: Lev 21:18 w9 to Lev 22:6 w16 | 0.409 | 4.08e-5 | 1 | 0.288 | 0.0120 | 17 |
| scan: Ezek 47:18 w18 to Ezek 48:5 w10 | 0.367 | 4.09e-5 | 1 | 0.254 | 0.0032 | 18 |
| scan: 1Chr 15:8 w3 to 1Chr 15:18 w3 | 0.458 | 4.10e-5 | 1 | 0.295 | 0.0095 | 36 |
| scan: Judg 1:19 w1 to Judg 1:29 w11 | 0.587 | 4.15e-5 | 1 | 0.291 | 0.0110 | 32 |
| scan: 1Chr 15:8 w1 to 1Chr 15:18 w19 | 0.446 | 4.15e-5 | 1 | 0.295 | 0.0095 | 36 |
| scan: Ezek 47:18 w1 to Ezek 48:8 w8 | 0.110 | 4.16e-5 | 1 | 0.038 | 0.2372 | 18 |
| scan: Lev 24:14 w1 to Lev 25:2 w14 | 0.635 | 4.21e-5 | 1 | 0.502 | 7.70e-4 | 11 |
| scan: Deut 2:10 w5 to Deut 2:20 w13 | 0.790 | 4.21e-5 | 1 | 0.826 | 0.0019 | 36 |
| scan: Ezek 33:26 w11 to Ezek 34:4 w23 | 0.610 | 4.23e-5 | 0 | - | - | 0 |
| scan: Ezek 33:27 w1 to Ezek 34:4 w19 | 0.610 | 4.23e-5 | 1 | 0.562 | 0.0017 | 15 |
| scan: Ezek 47:23 w1 to Ezek 48:12 w7 | 0.211 | 4.28e-5 | 1 | 0.059 | 0.2764 | 10 |
| scan: Gen 47:14 w1 to Gen 47:21 w10 | 0.445 | 4.29e-5 | 1 | 0.261 | 0.0106 | 14 |
| scan: Exod 37:14 w1 to Exod 37:25 w16 | 0.493 | 4.29e-5 | 0 | - | - | 0 |
| scan: Lev 21:19 w8 to Lev 22:6 w16 | 0.417 | 4.29e-5 | 1 | 0.371 | 0.0020 | 16 |
| scan: Exod 25:27 w5 to Exod 25:40 w2 | 0.489 | 4.32e-5 | 1 | 0.464 | 1.36e-5 | 46 |
| scan: 1Chr 15:13 w1 to 1Chr 15:24 w13 | 0.655 | 4.36e-5 | 1 | 0.608 | 0.0021 | 53 |
| scan: Ezek 43:12 w1 to Ezek 43:19 w18 | 0.596 | 4.36e-5 | 1 | 0.216 | 0.0214 | 21 |
| scan: Ezek 43:12 w4 to Ezek 43:19 w14 | 0.596 | 4.36e-5 | 1 | 0.216 | 0.0214 | 21 |
| scan: Jer 25:15 w15 to Jer 25:29 w13 | 0.435 | 4.37e-5 | 0 | - | - | 0 |
| scan: Exod 2:8 w1 to Exod 2:16 w4 | 0.595 | 4.38e-5 | 1 | 0.530 | 2.20e-4 | 9 |
| scan: Ezek 47:18 w1 to Ezek 48:6 w10 | 0.236 | 4.38e-5 | 1 | 0.220 | 0.0049 | 18 |
| scan: 2Kgs 4:41 w1 to 2Kgs 5:6 w6 | 0.432 | 4.39e-5 | 1 | 0.167 | 0.1141 | 14 |
| scan: Gen 25:10 w8 to Gen 25:21 w14 | 0.595 | 4.41e-5 | 1 | 0.148 | 0.1432 | 26 |
| scan: Lev 24:15 w6 to Lev 24:23 w14 | 0.776 | 4.43e-5 | 1 | 0.556 | 8.10e-4 | 8 |
| scan: Jer 1:7 w8 to Jer 1:17 w17 | 0.485 | 4.47e-5 | 1 | 0.209 | 0.0585 | 12 |
| scan: Josh 15:10 w16 to Josh 15:21 w13 | 0.670 | 4.48e-5 | 1 | 0.497 | 3.00e-4 | 36 |
| scan: Josh 15:11 w1 to Josh 15:21 w10 | 0.670 | 4.48e-5 | 1 | 0.559 | 5.55e-5 | 33 |
| scan: Zech 12:7 w1 to Zech 13:5 w4 | 0.593 | 4.51e-5 | 1 | 0.326 | 0.0065 | 19 |
| scan: Gen 37:26 w5 to Gen 38:1 w13 | 0.643 | 4.52e-5 | 1 | 0.539 | 0.0014 | 16 |
| scan: Ps 145:6 w4 to Ps 145:17 w4 | 0.660 | 4.53e-5 | 1 | 0.749 | 0.0077 | 11 |
| scan: Exod 2:8 w1 to Exod 2:16 w12 | 0.567 | 4.54e-5 | 1 | 0.530 | 2.20e-4 | 9 |
| scan: Ezek 33:21 w9 to Ezek 33:33 w8 | 0.449 | 4.55e-5 | 1 | 0.590 | 8.98e-5 | 16 |
| scan: Ezek 47:22 w13 to Ezek 48:10 w26 | 0.190 | 4.57e-5 | 1 | 0.170 | 0.0270 | 9 |
| scan: Gen 4:1 w1 to Gen 4:11 w3 | 0.221 | 4.58e-5 | 1 | 0.136 | 0.0518 | 3 |
| scan: Num 28:14 w1 to Num 28:20 w11 | 0.804 | 4.58e-5 | 1 | 0.450 | 0.0096 | 19 |
| scan: 2Sam 8:13 w1 to 2Sam 9:2 w16 | 0.458 | 4.58e-5 | 1 | 0.470 | 8.80e-4 | 17 |
| scan: Exod 25:27 w5 to Exod 25:39 w9 | 0.538 | 4.60e-5 | 1 | 0.518 | 1.47e-5 | 45 |
| scan: Exod 25:28 w1 to Exod 25:39 w5 | 0.538 | 4.60e-5 | 1 | 0.518 | 1.47e-5 | 43 |
| scan: Josh 15:6 w9 to Josh 15:15 w5 | 0.280 | 4.64e-5 | 1 | -0.048 | 0.7762 | 45 |
| scan: Gen 43:24 w7 to Gen 43:31 w3 | 0.891 | 4.66e-5 | 1 | 0.460 | 0.0079 | 4 |
| scan: Gen 47:13 w1 to Gen 47:21 w10 | 0.379 | 4.67e-5 | 1 | 0.324 | 3.50e-4 | 15 |
| scan: Eccl 2:24 w11 to Eccl 3:13 w9 | 0.554 | 4.69e-5 | 1 | 0.530 | 1.69e-7 | 11 |
| scan: Ezek 3:14 w4 to Ezek 3:24 w6 | 0.583 | 4.69e-5 | 1 | 0.514 | 7.00e-4 | 12 |
| scan: Num 34:29 w5 to Num 35:10 w6 | 0.351 | 4.70e-5 | 1 | 0.402 | 3.95e-5 | 20 |
| scan: Neh 7:63 w1 to Neh 8:2 w13 | 0.481 | 4.70e-5 | 1 | 0.290 | 0.0482 | 22 |
| scan: 2Chr 11:16 w1 to 2Chr 12:2 w11 | 0.482 | 4.76e-5 | 1 | 0.479 | 5.70e-4 | 16 |
| scan: Exod 33:4 w8 to Exod 33:13 w20 | 0.391 | 4.77e-5 | 1 | 0.167 | 0.0385 | 11 |
| scan: 1Sam 4:20 w11 to 1Sam 5:9 w18 | 0.407 | 4.77e-5 | 1 | 0.220 | 0.0153 | 38 |
| scan: Exod 33:5 w1 to Exod 33:13 w15 | 0.410 | 4.81e-5 | 1 | 0.159 | 0.0521 | 9 |
| scan: Num 34:29 w5 to Num 35:9 w5 | 0.348 | 4.82e-5 | 1 | 0.361 | 1.01e-5 | 19 |
| scan: Ezek 43:11 w24 to Ezek 43:19 w14 | 0.624 | 4.84e-5 | 1 | 0.273 | 0.0194 | 26 |
| scan: 1Chr 15:12 w1 to 1Chr 15:24 w13 | 0.568 | 4.85e-5 | 1 | 0.395 | 0.0072 | 56 |
| scan: Gen 14:4 w7 to Gen 14:15 w12 | 0.679 | 4.91e-5 | 1 | 0.720 | 7.00e-4 | 40 |
| scan: Exod 34:20 w9 to Exod 34:32 w6 | 0.427 | 4.93e-5 | 1 | 0.288 | 0.1515 | 7 |
| scan: Lev 4:32 w6 to Lev 5:9 w12 | 0.424 | 4.94e-5 | 1 | 0.110 | 0.0364 | 26 |
| scan: Eccl 2:24 w11 to Eccl 3:13 w12 | 0.583 | 4.98e-5 | 1 | 0.530 | 1.69e-7 | 11 |
| scan: Jer 3:19 w1 to Jer 4:5 w16 | 0.500 | 4.98e-5 | 1 | 0.373 | 6.40e-4 | 11 |
| scan: Num 16:10 w1 to Num 16:17 w14 | 0.868 | 5.09e-5 | 1 | 0.634 | 0.0252 | 15 |
| scan: Exod 25:26 w6 to Exod 25:39 w5 | 0.497 | 5.10e-5 | 1 | 0.371 | 3.92e-5 | 46 |
| scan: 1Chr 15:1 w6 to 1Chr 15:13 w12 | 0.535 | 5.11e-5 | 1 | 0.383 | 8.10e-4 | 18 |
| scan: 1Kgs 2:35 w1 to 1Kgs 2:45 w11 | 0.308 | 5.15e-5 | 1 | 0.183 | 0.0222 | 16 |
| scan: Judg 16:29 w13 to Judg 17:7 w12 | 0.558 | 5.16e-5 | 1 | 0.557 | 7.70e-4 | 14 |
| scan: Deut 5:24 w1 to Deut 5:33 w17 | 0.337 | 5.17e-5 | 1 | 0.443 | 0.0032 | 5 |
| scan: Ezek 28:26 w1 to Ezek 29:7 w15 | 0.562 | 5.17e-5 | 1 | 0.472 | 0.0138 | 15 |
| scan: Mic 7:1 w9 to Mic 7:13 w5 | 0.716 | 5.20e-5 | 1 | 0.636 | 0.0398 | 29 |
| scan: 2Chr 12:15 w1 to 2Chr 13:7 w19 | 0.565 | 5.22e-5 | 1 | 0.839 | 1.50e-4 | 22 |
| scan: Josh 15:9 w14 to Josh 15:21 w10 | 0.715 | 5.25e-5 | 1 | 0.510 | 8.40e-4 | 42 |
| scan: Lev 21:15 w5 to Lev 21:24 w10 | 0.618 | 5.26e-5 | 1 | 0.279 | 0.0961 | 11 |
| scan: Jer 39:13 w13 to Jer 40:2 w4 | 0.568 | 5.31e-5 | 0 | - | - | 0 |
| scan: Exod 30:3 w12 to Exod 30:12 w20 | 0.698 | 5.33e-5 | 1 | 0.675 | 0.0472 | 24 |
| scan: Jer 51:16 w1 to Jer 51:27 w22 | 0.486 | 5.33e-5 | 1 | 0.139 | 0.0230 | 14 |
| scan: Lev 13:27 w5 to Lev 13:39 w8 | 0.192 | 5.36e-5 | 1 | 0.037 | 0.2792 | 49 |
| scan: Exod 2:7 w13 to Exod 2:16 w12 | 0.577 | 5.37e-5 | 1 | 0.334 | 0.0063 | 11 |
| scan: Exod 25:27 w1 to Exod 25:39 w5 | 0.535 | 5.37e-5 | 1 | 0.518 | 1.47e-5 | 45 |
| scan: 2Chr 12:14 w3 to 2Chr 13:8 w10 | 0.542 | 5.37e-5 | 1 | 0.477 | 0.0106 | 24 |
| scan: 1Sam 14:12 w15 to 1Sam 14:24 w5 | 0.329 | 5.38e-5 | 1 | 0.113 | 0.1174 | 20 |
| scan: Exod 28:15 w9 to Exod 28:24 w8 | 0.939 | 5.39e-5 | 0 | - | - | 0 |
| scan: Gen 37:2 w1 to Gen 37:12 w7 | 0.456 | 5.40e-5 | 1 | 0.184 | 0.0574 | 13 |
| scan: Exod 28:14 w10 to Exod 28:22 w9 | 0.792 | 5.44e-5 | 1 | 0.044 | 0.4169 | 33 |
| scan: 2Chr 11:16 w1 to 2Chr 12:1 w12 | 0.479 | 5.44e-5 | 1 | 0.502 | 0.0022 | 16 |
| scan: 1Kgs 3:15 w5 to 1Kgs 3:25 w7 | 0.490 | 5.45e-5 | 1 | 0.010 | 0.4756 | 7 |
| scan: 1Sam 8:9 w4 to 1Sam 8:19 w5 | 0.855 | 5.46e-5 | 1 | 0.357 | 0.0534 | 10 |
| scan: Exod 28:13 w1 to Exod 28:24 w8 | 0.527 | 5.47e-5 | 0 | - | - | 0 |
| scan: 1Chr 28:12 w13 to 1Chr 29:1 w13 | 0.487 | 5.50e-5 | 1 | -0.007 | 0.5190 | 16 |
| scan: Num 33:34 w3 to Num 33:43 w2 | 0.610 | 5.54e-5 | 1 | 0.243 | 0.2639 | 42 |
| scan: 2Kgs 10:3 w10 to 2Kgs 10:10 w14 | 0.575 | 5.57e-5 | 1 | 0.366 | 0.0020 | 8 |
| scan: 1Chr 6:19 w5 to 1Chr 6:32 w18 | 0.428 | 5.58e-5 | 1 | 0.000 | 1.0000 | 27 |
| scan: Lev 24:15 w1 to Lev 25:2 w14 | 0.611 | 5.59e-5 | 1 | 0.444 | 0.0010 | 9 |
| scan: Ezek 45:6 w14 to Ezek 45:17 w27 | 0.531 | 5.59e-5 | 1 | 0.187 | 0.0813 | 21 |
| scan: Gen 25:22 w1 to Gen 25:33 w7 | 0.462 | 5.61e-5 | 1 | 0.270 | 0.0176 | 15 |
| scan: Deut 20:1 w15 to Deut 20:11 w15 | 0.536 | 5.63e-5 | 1 | 0.293 | 0.0185 | 12 |
| scan: Judg 1:20 w1 to Judg 1:29 w7 | 0.801 | 5.65e-5 | 1 | 0.173 | 0.1032 | 28 |
| scan: Jer 6:9 w10 to Jer 6:18 w8 | 0.646 | 5.68e-5 | 1 | -0.005 | 0.5097 | 17 |
| scan: Josh 11:17 w1 to Josh 12:3 w14 | 0.502 | 5.70e-5 | 1 | 0.564 | 7.30e-6 | 33 |
| scan: Lev 10:17 w1 to Lev 11:7 w16 | 0.751 | 5.71e-5 | 1 | 0.492 | 0.0500 | 36 |
| scan: Lev 4:33 w1 to Lev 5:8 w9 | 0.481 | 5.73e-5 | 1 | 0.211 | 0.0034 | 23 |
| scan: Exod 2:7 w13 to Exod 2:17 w3 | 0.552 | 5.74e-5 | 1 | 0.272 | 0.0160 | 11 |
| scan: 1Sam 8:9 w4 to 1Sam 8:20 w5 | 0.672 | 5.75e-5 | 1 | 0.629 | 4.41e-5 | 10 |
| scan: 1Chr 5:12 w5 to 1Chr 5:25 w3 | 0.654 | 5.75e-5 | 1 | 0.552 | 0.0115 | 44 |
| scan: 1Chr 5:12 w5 to 1Chr 5:25 w12 | 0.654 | 5.75e-5 | 1 | 0.668 | 6.00e-4 | 44 |
| scan: Deut 2:12 w1 to Deut 2:21 w5 | 0.891 | 5.76e-5 | 1 | 0.190 | 0.1896 | 31 |
| scan: 2Chr 9:1 w23 to 2Chr 9:10 w14 | 0.451 | 5.76e-5 | 1 | 0.218 | 0.1003 | 12 |
| scan: 1Sam 4:20 w11 to 1Sam 5:8 w24 | 0.425 | 5.79e-5 | 1 | 0.210 | 0.0291 | 35 |
| scan: Ezek 1:23 w1 to Ezek 2:4 w15 | 0.566 | 5.85e-5 | 1 | 0.409 | 0.0117 | 7 |
| scan: Lev 4:33 w7 to Lev 5:10 w5 | 0.416 | 5.86e-5 | 1 | 0.066 | 0.1396 | 28 |
| scan: 1Sam 20:15 w9 to 1Sam 20:27 w7 | 0.424 | 5.89e-5 | 1 | -0.135 | 0.8053 | 18 |
| scan: Exod 37:16 w1 to Exod 37:25 w16 | 0.551 | 5.92e-5 | 0 | - | - | 0 |
| scan: Lev 4:6 w1 to Lev 4:16 w8 | 0.298 | 5.93e-5 | 1 | 0.192 | 0.0585 | 21 |
| scan: Lev 13:28 w1 to Lev 13:39 w8 | 0.207 | 5.94e-5 | 1 | 0.135 | 0.0466 | 45 |
| scan: Lev 14:16 w12 to Lev 14:27 w14 | 0.295 | 5.94e-5 | 1 | 0.205 | 0.0047 | 30 |
| scan: 1Kgs 6:21 w1 to 1Kgs 6:30 w7 | 0.551 | 5.94e-5 | 1 | 0.575 | 2.20e-4 | 14 |
| scan: Lev 24:14 w1 to Lev 25:2 w18 | 0.622 | 5.96e-5 | 1 | 0.502 | 7.70e-4 | 11 |
| scan: 1Kgs 20:33 w1 to 1Kgs 20:41 w6 | 0.599 | 5.98e-5 | 1 | -0.123 | 0.7659 | 12 |
| scan: Jer 51:15 w7 to Jer 51:27 w15 | 0.604 | 5.98e-5 | 1 | 0.231 | 0.0484 | 14 |
| scan: Lev 21:19 w1 to Lev 22:7 w3 | 0.390 | 6.01e-5 | 1 | 0.308 | 0.0056 | 17 |
| scan: Isa 45:4 w1 to Isa 45:15 w7 | 0.498 | 6.02e-5 | 1 | 0.299 | 0.0030 | 9 |
| scan: Lev 3:15 w1 to Lev 4:9 w10 | 0.421 | 6.06e-5 | 1 | 0.522 | 2.80e-4 | 24 |
| scan: Zech 8:16 w5 to Zech 9:2 w9 | 0.385 | 6.06e-5 | 1 | 0.491 | 9.32e-5 | 8 |
| scan: Deut 21:21 w10 to Deut 22:6 w21 | 0.565 | 6.07e-5 | 1 | 0.429 | 0.0483 | 11 |
| scan: 1Chr 28:8 w1 to 1Chr 28:20 w27 | 0.505 | 6.08e-5 | 1 | 0.114 | 0.1264 | 19 |
| scan: Judg 16:28 w6 to Judg 17:7 w12 | 0.615 | 6.09e-5 | 1 | 0.466 | 1.02e-4 | 15 |
| scan: Isa 59:2 w1 to Isa 59:12 w12 | 0.781 | 6.09e-5 | 1 | -0.021 | 0.5473 | 15 |
| scan: Exod 25:29 w9 to Exod 25:39 w9 | 0.558 | 6.12e-5 | 1 | 0.501 | 2.00e-4 | 40 |
| scan: Ezek 47:18 w18 to Ezek 48:6 w10 | 0.178 | 6.12e-5 | 1 | 0.105 | 0.0730 | 18 |
| scan: Zech 8:15 w12 to Zech 9:3 w4 | 0.457 | 6.13e-5 | 1 | 0.410 | 9.60e-4 | 10 |
| scan: Zech 8:16 w1 to Zech 9:2 w9 | 0.457 | 6.13e-5 | 1 | 0.491 | 9.32e-5 | 8 |
| scan: Zech 2:11 w1 to Zech 3:10 w8 | 0.335 | 6.17e-5 | 1 | 0.278 | 0.0032 | 14 |
| scan: 2Chr 30:2 w7 to 2Chr 30:13 w10 | 0.435 | 6.23e-5 | 1 | 0.603 | 2.52e-7 | 13 |
| scan: Exod 40:7 w9 to Exod 40:18 w16 | 0.578 | 6.24e-5 | 0 | - | - | 0 |
| scan: Exod 28:13 w1 to Exod 28:23 w6 | 0.607 | 6.27e-5 | 0 | - | - | 0 |
| scan: 1Chr 5:13 w1 to 1Chr 5:25 w12 | 0.715 | 6.30e-5 | 1 | 0.533 | 0.0152 | 41 |
| scan: 1Chr 15:7 w3 to 1Chr 15:18 w19 | 0.424 | 6.31e-5 | 1 | 0.260 | 0.0076 | 37 |
| scan: 1Kgs 20:32 w1 to 1Kgs 20:40 w15 | 0.513 | 6.32e-5 | 1 | 0.379 | 0.0018 | 13 |
| scan: 1Chr 28:12 w1 to 1Chr 29:1 w22 | 0.429 | 6.33e-5 | 1 | -0.007 | 0.5190 | 16 |
| scan: 2Chr 7:3 w1 to 2Chr 7:14 w21 | 0.271 | 6.33e-5 | 1 | 0.258 | 0.0013 | 18 |
| scan: 1Sam 28:11 w7 to 1Sam 28:23 w11 | 0.374 | 6.35e-5 | 1 | 0.288 | 0.0030 | 12 |
| scan: Deut 27:24 w5 to Deut 28:10 w11 | 0.515 | 6.39e-5 | 1 | 0.509 | 0.0014 | 2 |
| scan: Exod 31:3 w1 to Exod 31:15 w10 | 0.562 | 6.40e-5 | 1 | 0.330 | 0.1250 | 14 |
| scan: 1Sam 8:10 w1 to 1Sam 8:20 w5 | 0.731 | 6.41e-5 | 1 | 0.709 | 2.40e-4 | 10 |
| scan: 1Chr 28:8 w15 to 1Chr 28:21 w8 | 0.449 | 6.41e-5 | 1 | 0.048 | 0.3034 | 20 |
| scan: Eccl 2:23 w1 to Eccl 3:12 w11 | 0.512 | 6.43e-5 | 1 | 0.407 | 1.60e-6 | 14 |
| scan: Lev 4:32 w6 to Lev 5:8 w16 | 0.454 | 6.49e-5 | 1 | 0.110 | 0.0475 | 23 |
| scan: 1Chr 1:47 w1 to 1Chr 2:7 w2 | 0.752 | 6.50e-5 | 1 | 0.553 | 8.97e-7 | 39 |
| scan: Isa 43:16 w1 to Isa 43:26 w3 | 0.934 | 6.50e-5 | 1 | 0.681 | 0.0556 | 10 |
| scan: Gen 49:25 w14 to Gen 50:4 w19 | 0.636 | 6.54e-5 | 1 | 0.616 | 0.0020 | 20 |
| scan: Deut 22:27 w1 to Deut 23:7 w6 | 0.358 | 6.56e-5 | 1 | -0.363 | 1.0000 | 11 |
| scan: Ezek 47:19 w1 to Ezek 48:6 w10 | 0.265 | 6.57e-5 | 1 | 0.121 | 0.0584 | 15 |
| scan: 2Chr 11:15 w6 to 2Chr 12:3 w6 | 0.452 | 6.65e-5 | 1 | 0.417 | 0.0015 | 22 |
| scan: 2Chr 11:16 w1 to 2Chr 12:2 w14 | 0.452 | 6.65e-5 | 1 | 0.461 | 7.20e-4 | 16 |
| scan: Josh 15:7 w1 to Josh 15:16 w14 | 0.385 | 6.69e-5 | 1 | -0.000 | 0.5039 | 43 |
| scan: Deut 21:3 w1 to Deut 21:13 w22 | 0.677 | 6.70e-5 | 1 | 0.346 | 0.1847 | 16 |
| scan: Gen 37:35 w1 to Gen 38:10 w5 | 0.539 | 6.71e-5 | 1 | 0.306 | 0.0325 | 13 |
| scan: Ezek 3:13 w11 to Ezek 3:25 w9 | 0.510 | 6.73e-5 | 1 | 0.453 | 0.0012 | 15 |
| scan: Num 16:12 w1 to Num 16:24 w10 | 0.469 | 6.77e-5 | 1 | 0.317 | 0.0071 | 19 |
| scan: Exod 33:3 w1 to Exod 33:14 w5 | 0.371 | 6.80e-5 | 1 | 0.172 | 0.0292 | 15 |
| scan: 1Chr 24:5 w1 to 1Chr 24:23 w2 | 0.701 | 6.82e-5 | 1 | -0.021 | 0.5491 | 37 |
| scan: Ezek 42:14 w1 to Ezek 43:4 w5 | 0.610 | 6.82e-5 | 1 | 0.373 | 0.0112 | 16 |
| scan: Ezek 47:23 w1 to Ezek 48:12 w10 | 0.156 | 6.82e-5 | 1 | 0.076 | 0.2015 | 10 |
| scan: 2Sam 8:14 w1 to 2Sam 9:2 w16 | 0.553 | 6.84e-5 | 1 | 0.638 | 3.00e-4 | 14 |
| scan: 1Chr 16:35 w1 to 1Chr 16:42 w9 | 0.714 | 6.84e-5 | 1 | 0.627 | 0.0031 | 20 |
| scan: 1Sam 20:7 w7 to 1Sam 20:15 w8 | 0.496 | 6.87e-5 | 1 | 0.118 | 0.2741 | 11 |
| scan: 1Chr 24:5 w6 to 1Chr 24:22 w5 | 0.739 | 6.87e-5 | 1 | 0.440 | 0.0083 | 33 |
| scan: Num 12:16 w1 to Num 13:17 w7 | 0.350 | 6.90e-5 | 1 | 0.258 | 4.80e-4 | 31 |
| scan: Jer 25:28 w8 to Jer 26:2 w23 | 0.524 | 6.91e-5 | 0 | - | - | 0 |
| scan: Ezek 32:2 w1 to Ezek 32:12 w14 | 0.574 | 6.92e-5 | 1 | 0.609 | 0.0011 | 12 |
| scan: Lev 4:7 w1 to Lev 4:17 w13 | 0.359 | 6.93e-5 | 1 | 0.094 | 0.1726 | 21 |
| scan: Lev 23:14 w15 to Lev 23:22 w20 | 0.772 | 6.93e-5 | 1 | 0.326 | 0.0904 | 27 |
| scan: Deut 27:24 w1 to Deut 28:10 w9 | 0.521 | 6.95e-5 | 1 | 0.537 | 7.70e-4 | 2 |
| scan: Lev 23:43 w1 to Lev 24:11 w11 | 0.522 | 7.03e-5 | 1 | 0.231 | 0.0416 | 15 |
| scan: Gen 19:7 w2 to Gen 19:19 w14 | 0.433 | 7.04e-5 | 1 | 0.055 | 0.3309 | 19 |
| scan: Exod 37:15 w9 to Exod 37:26 w16 | 0.624 | 7.06e-5 | 0 | - | - | 0 |
| scan: Exod 25:28 w9 to Exod 25:40 w2 | 0.521 | 7.08e-5 | 1 | 0.551 | 9.30e-6 | 44 |
| scan: 1Sam 4:20 w1 to 1Sam 5:9 w21 | 0.385 | 7.08e-5 | 1 | 0.220 | 0.0153 | 38 |
| scan: Isa 44:26 w7 to Isa 45:9 w17 | 0.598 | 7.13e-5 | 1 | 0.545 | 0.0013 | 11 |
| scan: Deut 4:12 w6 to Deut 4:21 w21 | 0.516 | 7.14e-5 | 1 | 0.339 | 0.0087 | 6 |
| scan: Ezek 47:23 w1 to Ezek 48:11 w7 | 0.144 | 7.17e-5 | 1 | 0.031 | 0.3501 | 9 |
| scan: Exod 37:14 w5 to Exod 37:24 w8 | 0.543 | 7.24e-5 | 0 | - | - | 0 |
| scan: Num 12:16 w5 to Num 13:17 w7 | 0.380 | 7.29e-5 | 1 | 0.277 | 3.20e-4 | 31 |
| scan: Ezek 1:22 w9 to Ezek 2:4 w9 | 0.602 | 7.34e-5 | 1 | -0.118 | 0.6971 | 8 |
| scan: Ezek 47:22 w1 to Ezek 48:9 w11 | 0.154 | 7.39e-5 | 1 | 0.087 | 0.1291 | 9 |
| scan: Jer 51:17 w1 to Jer 51:26 w13 | 0.481 | 7.42e-5 | 1 | 0.066 | 0.0183 | 10 |
| scan: Deut 31:11 w12 to Deut 31:19 w20 | 0.551 | 7.43e-5 | 1 | 0.435 | 0.0020 | 13 |
| scan: Zech 2:10 w5 to Zech 3:9 w25 | 0.354 | 7.50e-5 | 1 | 0.219 | 0.0208 | 16 |
| scan: 1Kgs 9:1 w1 to 1Kgs 9:11 w13 | 0.361 | 7.51e-5 | 1 | 0.350 | 6.80e-4 | 15 |
| scan: Lev 21:14 w9 to Lev 22:2 w14 | 0.535 | 7.57e-5 | 1 | 0.445 | 0.0061 | 13 |
| scan: Jer 52:21 w13 to Jer 52:30 w20 | 0.703 | 7.59e-5 | 0 | - | - | 0 |
| scan: Ruth 1:16 w9 to Ruth 2:3 w14 | 0.573 | 7.61e-5 | 1 | -0.104 | 0.7304 | 21 |
| scan: Josh 8:24 w1 to Josh 8:34 w13 | 0.332 | 7.65e-5 | 0 | - | - | 0 |
| scan: 1Chr 15:2 w1 to 1Chr 15:13 w12 | 0.528 | 7.65e-5 | 1 | 0.307 | 0.0106 | 18 |
| scan: 2Chr 7:3 w1 to 2Chr 7:14 w12 | 0.271 | 7.66e-5 | 1 | 0.167 | 0.0199 | 18 |
| scan: Deut 5:15 w15 to Deut 5:25 w8 | 0.698 | 7.68e-5 | 1 | 0.174 | 0.0782 | 6 |
| scan: Gen 14:4 w1 to Gen 14:16 w4 | 0.640 | 7.69e-5 | 1 | 0.717 | 5.30e-4 | 41 |
| scan: Gen 14:5 w17 to Gen 14:16 w4 | 0.749 | 7.69e-5 | 1 | 0.734 | 0.0500 | 39 |
| scan: Gen 14:6 w1 to Gen 14:16 w4 | 0.749 | 7.69e-5 | 1 | 0.341 | 0.1028 | 34 |
| scan: Jer 25:14 w10 to Jer 25:28 w7 | 0.481 | 7.73e-5 | 0 | - | - | 0 |
| scan: 2Chr 7:1 w10 to 2Chr 7:13 w12 | 0.246 | 7.82e-5 | 1 | 0.162 | 0.0209 | 18 |
| scan: Judg 1:19 w1 to Judg 1:28 w11 | 0.705 | 7.87e-5 | 1 | 0.293 | 0.0211 | 29 |
| scan: Exod 40:6 w5 to Exod 40:18 w13 | 0.524 | 7.92e-5 | 1 | 0.566 | 0.0472 | 15 |
| scan: Lev 24:14 w14 to Lev 25:2 w18 | 0.583 | 7.92e-5 | 1 | 0.405 | 0.0032 | 11 |
| scan: Num 34:27 w1 to Num 35:9 w5 | 0.371 | 7.99e-5 | 1 | 0.389 | 8.10e-4 | 22 |
| scan: Num 7:86 w12 to Num 8:8 w8 | 0.695 | 8.00e-5 | 1 | 0.608 | 2.00e-4 | 17 |
| scan: Judg 16:28 w6 to Judg 17:8 w9 | 0.577 | 8.01e-5 | 1 | 0.471 | 0.0011 | 16 |
| scan: 1Kgs 20:32 w18 to 1Kgs 20:41 w6 | 0.492 | 8.03e-5 | 1 | 0.291 | 0.0030 | 14 |
| scan: Josh 8:28 w1 to Josh 9:3 w9 | 0.527 | 8.04e-5 | 0 | - | - | 19 |
| scan: Deut 28:64 w10 to Deut 29:7 w4 | 0.440 | 8.12e-5 | 1 | 0.493 | 6.80e-4 | 13 |
| scan: 1Chr 1:47 w3 to 1Chr 2:6 w9 | 0.749 | 8.17e-5 | 1 | 0.525 | 1.20e-6 | 37 |
| scan: Lev 21:15 w5 to Lev 21:23 w20 | 0.634 | 8.20e-5 | 1 | 0.285 | 0.0823 | 11 |
| scan: Exod 37:13 w6 to Exod 37:25 w6 | 0.465 | 8.28e-5 | 0 | - | - | 0 |
| scan: Judg 11:32 w1 to Judg 12:1 w5 | 0.580 | 8.28e-5 | 1 | 0.465 | 0.0039 | 21 |
| scan: 1Chr 27:27 w5 to 1Chr 28:6 w8 | 0.409 | 8.30e-5 | 1 | -0.443 | 0.9896 | 33 |
| scan: 1Chr 6:26 w2 to 1Chr 6:36 w8 | 0.559 | 8.34e-5 | 1 | -0.001 | 0.6004 | 25 |
| scan: 2Kgs 3:26 w1 to 2Kgs 4:10 w12 | 0.436 | 8.36e-5 | 1 | 0.283 | 0.0117 | 15 |
| scan: Judg 16:29 w13 to Judg 17:8 w9 | 0.629 | 8.39e-5 | 1 | 0.491 | 0.0011 | 15 |
| scan: 1Sam 8:10 w1 to 1Sam 8:18 w14 | 0.932 | 8.48e-5 | 1 | 0.796 | 0.0556 | 10 |
| scan: Judg 11:33 w1 to Judg 12:2 w17 | 0.554 | 8.54e-5 | 1 | 0.508 | 3.99e-5 | 21 |
| scan: Eccl 2:25 w1 to Eccl 3:13 w12 | 0.563 | 8.55e-5 | 1 | 0.354 | 1.60e-6 | 11 |
| scan: Lev 24:12 w1 to Lev 24:23 w14 | 0.788 | 8.58e-5 | 1 | 0.449 | 0.0068 | 11 |
| scan: Exod 25:29 w9 to Exod 25:40 w7 | 0.627 | 8.61e-5 | 1 | 0.302 | 0.0283 | 41 |
| scan: 1Chr 9:38 w5 to 1Chr 10:5 w12 | 0.648 | 8.62e-5 | 1 | 0.479 | 0.0023 | 32 |
| scan: 1Chr 9:39 w1 to 1Chr 10:5 w6 | 0.648 | 8.62e-5 | 1 | 0.479 | 0.0023 | 31 |
| scan: Gen 36:29 w4 to Gen 36:41 w6 | 0.441 | 8.65e-5 | 1 | 0.504 | 4.00e-9 | 46 |
| scan: Obad 1:9 w1 to Obad 1:19 w15 | 0.819 | 8.65e-5 | 1 | 0.884 | 0.0016 | 29 |
| scan: 1Kgs 20:32 w18 to 1Kgs 20:40 w7 | 0.546 | 8.68e-5 | 1 | 0.379 | 0.0018 | 13 |
| scan: Jer 36:19 w1 to Jer 36:27 w18 | 0.414 | 8.68e-5 | 1 | 0.285 | 0.0225 | 22 |
| scan: 1Sam 20:16 w1 to 1Sam 20:27 w23 | 0.445 | 8.71e-5 | 1 | 0.358 | 0.0200 | 17 |
| scan: Lev 21:18 w1 to Lev 22:5 w16 | 0.335 | 8.76e-5 | 1 | 0.374 | 0.0053 | 16 |
| scan: 1Kgs 13:31 w1 to 1Kgs 14:8 w23 | 0.234 | 8.78e-5 | 0 | - | - | 0 |
| scan: Ezek 42:13 w1 to Ezek 43:4 w11 | 0.542 | 8.80e-5 | 1 | 0.353 | 0.0071 | 20 |
| scan: Eccl 9:11 w1 to Eccl 10:5 w5 | 0.490 | 8.93e-5 | 1 | 0.378 | 0.0116 | 17 |
| scan: Lev 4:4 w1 to Lev 4:15 w15 | 0.261 | 8.95e-5 | 1 | 0.127 | 0.0621 | 22 |
| scan: 2Sam 3:14 w1 to 2Sam 3:24 w16 | 0.183 | 8.95e-5 | 1 | 0.099 | 0.1110 | 25 |
| scan: Lev 21:19 w1 to Lev 22:4 w25 | 0.450 | 9.09e-5 | 1 | 0.257 | 0.0760 | 13 |
| scan: Deut 4:12 w1 to Deut 4:22 w16 | 0.459 | 9.11e-5 | 1 | 0.311 | 0.0177 | 7 |
| scan: 2Kgs 14:21 w1 to 2Kgs 15:3 w9 | 0.313 | 9.11e-5 | 1 | 0.298 | 4.70e-4 | 31 |
| scan: Deut 21:19 w1 to Deut 22:7 w13 | 0.478 | 9.14e-5 | 1 | 0.613 | 1.20e-4 | 16 |
| scan: 1Kgs 2:11 w1 to 1Kgs 2:19 w24 | 0.497 | 9.19e-5 | 1 | 0.640 | 5.70e-4 | 12 |
| scan: 1Chr 24:5 w1 to 1Chr 24:20 w9 | 0.869 | 9.19e-5 | 1 | 0.392 | 0.0554 | 32 |
| scan: Jer 3:13 w1 to Jer 3:21 w8 | 0.593 | 9.23e-5 | 1 | 0.178 | 0.1582 | 13 |
| scan: Jer 51:16 w10 to Jer 51:26 w7 | 0.561 | 9.24e-5 | 1 | 0.360 | 0.0012 | 10 |
| scan: Exod 30:3 w1 to Exod 30:13 w10 | 0.610 | 9.25e-5 | 1 | 0.675 | 0.0472 | 26 |
| scan: Neh 7:65 w9 to Neh 8:4 w27 | 0.743 | 9.25e-5 | 1 | 0.446 | 0.0281 | 28 |
| scan: Dan 2:36 w1 to Dan 2:46 w8 | 0.285 | 9.28e-5 | 1 | 0.144 | 0.1048 | 19 |
| scan: Deut 13:15 w1 to Deut 14:6 w13 | 0.619 | 9.36e-5 | 1 | 0.211 | 0.2000 | 22 |
| scan: Deut 13:15 w9 to Deut 14:6 w11 | 0.619 | 9.36e-5 | 1 | 0.211 | 0.2000 | 22 |
| scan: Judg 11:19 w1 to Judg 11:28 w11 | 0.412 | 9.36e-5 | 1 | 0.441 | 0.0012 | 26 |
| scan: 1Chr 27:24 w13 to 1Chr 28:1 w31 | 0.490 | 9.49e-5 | 1 | -0.028 | 0.5635 | 40 |
| scan: Ezek 23:15 w1 to Ezek 23:25 w12 | 0.816 | 9.50e-5 | 1 | 0.903 | 3.60e-5 | 23 |
| scan: 1Chr 5:13 w1 to 1Chr 5:24 w19 | 0.687 | 9.58e-5 | 1 | 0.552 | 0.0115 | 39 |
| scan: 2Kgs 16:7 w1 to 2Kgs 16:18 w16 | 0.253 | 9.59e-5 | 1 | 0.173 | 0.0050 | 20 |
| scan: Eccl 9:11 w24 to Eccl 10:5 w5 | 0.557 | 9.64e-5 | 1 | 0.471 | 0.0033 | 17 |
| scan: Exod 39:41 w6 to Exod 40:9 w18 | 0.801 | 9.67e-5 | 1 | 0.737 | 1.98e-4 | 11 |
| scan: Judg 16:28 w1 to Judg 17:9 w5 | 0.501 | 9.72e-5 | 1 | 0.341 | 0.0039 | 17 |
| scan: Ezek 37:21 w1 to Ezek 38:2 w12 | 0.482 | 9.77e-5 | 1 | 0.034 | 0.4312 | 12 |
| scan: Jer 6:10 w1 to Jer 6:18 w8 | 0.556 | 9.82e-5 | 1 | 0.858 | 0.0222 | 14 |
| scan: 1Sam 31:1 w1 to 1Sam 31:8 w7 | 0.421 | 9.87e-5 | 1 | 0.085 | 0.2530 | 11 |
| scan: Lev 4:32 w6 to Lev 5:8 w9 | 0.429 | 9.88e-5 | 1 | 0.185 | 0.0044 | 23 |
| scan: Gen 14:4 w1 to Gen 14:15 w12 | 0.661 | 9.92e-5 | 1 | 0.833 | 1.50e-4 | 40 |
| scan: Ezek 47:23 w7 to Ezek 48:12 w7 | 0.126 | 9.95e-5 | 1 | 0.076 | 0.2015 | 10 |
| scan: Zech 8:15 w12 to Zech 9:4 w6 | 0.375 | 9.99e-5 | 1 | 0.372 | 0.0016 | 12 |
| scan: Zech 8:16 w1 to Zech 9:3 w10 | 0.375 | 9.99e-5 | 1 | 0.491 | 9.32e-5 | 8 |
| scan: Lev 24:15 w1 to Lev 25:2 w18 | 0.604 | 1.01e-4 | 1 | 0.284 | 0.0480 | 9 |
| scan: Lev 24:15 w1 to Lev 25:3 w8 | 0.604 | 1.01e-4 | 1 | 0.284 | 0.0480 | 11 |
| scan: Exod 28:15 w1 to Exod 28:22 w9 | 0.804 | 1.01e-4 | 1 | 0.309 | 0.2267 | 25 |
| scan: Gen 47:14 w1 to Gen 47:22 w5 | 0.529 | 1.01e-4 | 1 | 0.266 | 0.0063 | 14 |
| scan: 2Chr 8:12 w6 to 2Chr 9:5 w12 | 0.412 | 1.02e-4 | 1 | 0.167 | 0.0632 | 17 |
| scan: 1Chr 27:23 w9 to 1Chr 27:34 w10 | 0.365 | 1.02e-4 | 1 | -0.468 | 0.9889 | 37 |
| scan: 2Chr 6:7 w6 to 2Chr 6:18 w20 | 0.363 | 1.03e-4 | 1 | 0.051 | 0.2789 | 8 |
| scan: Exod 25:27 w1 to Exod 25:39 w9 | 0.453 | 1.03e-4 | 1 | 0.518 | 1.47e-5 | 45 |
| scan: Ezek 43:9 w1 to Ezek 43:19 w18 | 0.604 | 1.03e-4 | 1 | 0.364 | 0.0149 | 29 |
| scan: 1Chr 27:27 w1 to 1Chr 28:5 w18 | 0.434 | 1.04e-4 | 1 | -0.202 | 0.8684 | 33 |
| scan: Exod 37:15 w9 to Exod 37:25 w16 | 0.557 | 1.05e-4 | 0 | - | - | 0 |
| scan: Lev 13:29 w1 to Lev 13:40 w4 | 0.210 | 1.05e-4 | 1 | 0.098 | 0.1506 | 42 |
| scan: Exod 25:27 w5 to Exod 25:39 w5 | 0.454 | 1.05e-4 | 1 | 0.518 | 1.47e-5 | 45 |
| scan: 1Chr 1:48 w1 to 1Chr 2:5 w4 | 0.747 | 1.05e-4 | 1 | 0.491 | 3.00e-6 | 29 |
| scan: Exod 37:3 w1 to Exod 37:14 w4 | 0.485 | 1.05e-4 | 0 | - | - | 0 |
| scan: Job 23:10 w5 to Job 24:5 w7 | 0.852 | 1.06e-4 | 1 | 0.028 | 0.4799 | 5 |
| scan: 2Chr 4:3 w15 to 2Chr 4:13 w20 | 0.681 | 1.06e-4 | 1 | 0.485 | 0.0244 | 22 |
| scan: Num 34:28 w1 to Num 35:9 w5 | 0.406 | 1.08e-4 | 1 | 0.366 | 1.30e-4 | 21 |
| scan: Exod 39:41 w1 to Exod 40:9 w18 | 0.809 | 1.08e-4 | 1 | 0.737 | 1.98e-4 | 11 |
| scan: Ezek 11:21 w7 to Ezek 12:7 w20 | 0.472 | 1.09e-4 | 1 | 0.359 | 0.0625 | 7 |
| scan: Isa 42:23 w1 to Isa 43:9 w18 | 0.645 | 1.09e-4 | 1 | 0.146 | 0.3482 | 12 |
| scan: Dan 2:34 w1 to Dan 2:41 w19 | 0.331 | 1.10e-4 | 1 | 0.502 | 0.0325 | 11 |
| scan: Gen 38:7 w8 to Gen 38:18 w18 | 0.537 | 1.10e-4 | 1 | -0.005 | 0.5179 | 20 |
| scan: Exod 18:7 w1 to Exod 18:13 w15 | 0.573 | 1.10e-4 | 1 | 0.335 | 0.0611 | 10 |
| scan: Exod 20:23 w4 to Exod 21:9 w7 | 0.398 | 1.10e-4 | 1 | 0.700 | 6.71e-5 | 14 |
| scan: Exod 28:14 w10 to Exod 28:23 w6 | 0.742 | 1.10e-4 | 0 | - | - | 0 |
| scan: Exod 30:3 w1 to Exod 30:12 w14 | 0.578 | 1.10e-4 | 1 | 0.000 | 1.0000 | 24 |
| scan: Exod 33:3 w1 to Exod 33:13 w15 | 0.346 | 1.10e-4 | 1 | 0.233 | 0.0180 | 15 |
| scan: Exod 33:3 w6 to Exod 33:14 w1 | 0.380 | 1.10e-4 | 1 | 0.172 | 0.0292 | 15 |
| scan: Exod 37:15 w1 to Exod 37:24 w8 | 0.477 | 1.10e-4 | 0 | - | - | 0 |
| scan: Lev 4:33 w1 to Lev 5:9 w12 | 0.418 | 1.10e-4 | 1 | 0.212 | 0.0022 | 26 |
| scan: Lev 24:11 w1 to Lev 24:23 w14 | 0.773 | 1.10e-4 | 1 | 0.159 | 0.2432 | 13 |
| scan: Num 7:9 w5 to Num 7:18 w8 | 0.593 | 1.10e-4 | 1 | 0.169 | 0.2636 | 15 |
| scan: Num 7:10 w1 to Num 7:18 w8 | 0.593 | 1.10e-4 | 1 | 0.227 | 0.2085 | 13 |
| scan: Deut 4:12 w6 to Deut 4:23 w11 | 0.431 | 1.10e-4 | 1 | 0.127 | 0.0507 | 9 |
| scan: Deut 34:1 w14 to Deut 34:12 w6 | 0.490 | 1.10e-4 | 1 | 0.000 | 0.5009 | 20 |
| scan: Josh 24:5 w12 to Josh 24:17 w12 | 0.472 | 1.10e-4 | 1 | 0.094 | 0.2053 | 21 |
| scan: 2Sam 5:5 w1 to 2Sam 5:13 w9 | 0.284 | 1.10e-4 | 1 | 0.095 | 0.0188 | 9 |
| scan: 1Kgs 2:34 w8 to 1Kgs 2:45 w3 | 0.328 | 1.10e-4 | 1 | 0.265 | 2.60e-4 | 17 |
| scan: 1Kgs 6:20 w15 to 1Kgs 6:30 w7 | 0.528 | 1.10e-4 | 1 | 0.491 | 0.0022 | 18 |
| scan: 1Kgs 6:20 w15 to 1Kgs 6:31 w10 | 0.466 | 1.10e-4 | 1 | 0.442 | 6.50e-4 | 21 |
| scan: 1Kgs 17:23 w1 to 1Kgs 18:9 w3 | 0.442 | 1.10e-4 | 1 | 0.132 | 0.0756 | 18 |
| scan: 1Chr 1:46 w3 to 1Chr 2:6 w9 | 0.734 | 1.10e-4 | 1 | 0.383 | 1.18e-7 | 43 |
| scan: 1Chr 15:13 w5 to 1Chr 15:22 w9 | 0.770 | 1.10e-4 | 1 | 1.000 | 0.1667 | 46 |
| scan: 1Chr 27:23 w9 to 1Chr 28:2 w9 | 0.335 | 1.10e-4 | 1 | 0.200 | 0.0644 | 43 |
| scan: 1Chr 28:9 w22 to 1Chr 28:20 w27 | 0.531 | 1.10e-4 | 1 | 0.145 | 0.0863 | 18 |
| scan: 1Chr 28:10 w1 to 1Chr 28:20 w27 | 0.498 | 1.10e-4 | 1 | 0.204 | 0.0379 | 16 |
| scan: 1Chr 28:10 w1 to 1Chr 29:1 w22 | 0.371 | 1.10e-4 | 1 | 0.244 | 0.0071 | 17 |
| scan: 2Chr 6:2 w6 to 2Chr 6:14 w9 | 0.379 | 1.10e-4 | 1 | 0.078 | 0.1677 | 5 |
| scan: 2Chr 6:8 w1 to 2Chr 6:18 w20 | 0.388 | 1.10e-4 | 1 | 0.113 | 0.1453 | 8 |
| scan: 2Chr 17:3 w5 to 2Chr 17:12 w6 | 0.684 | 1.10e-4 | 1 | 0.479 | 0.0013 | 16 |
| scan: Ezra 3:8 w1 to Ezra 4:3 w14 | 0.682 | 1.10e-4 | 1 | 0.407 | 0.0062 | 18 |
| scan: Eccl 1:14 w1 to Eccl 2:7 w7 | 0.521 | 1.10e-4 | 1 | 0.203 | 0.1849 | 16 |
| scan: Eccl 2:25 w1 to Eccl 3:14 w19 | 0.570 | 1.10e-4 | 1 | 0.423 | 2.50e-6 | 11 |
| scan: Eccl 3:14 w16 to Eccl 4:2 w6 | 0.434 | 1.10e-4 | 1 | 0.538 | 0.0019 | 4 |
| scan: Jer 36:18 w1 to Jer 36:27 w18 | 0.385 | 1.10e-4 | 1 | 0.404 | 5.20e-4 | 22 |
| scan: Lam 2:7 w1 to Lam 2:17 w19 | 0.499 | 1.10e-4 | 1 | 0.287 | 0.0170 | 26 |
| scan: Ezek 31:18 w9 to Ezek 32:12 w7 | 0.450 | 1.10e-4 | 1 | 0.447 | 0.0019 | 16 |
| scan: Ezek 33:26 w11 to Ezek 34:5 w9 | 0.562 | 1.10e-4 | 0 | - | - | 0 |
| scan: Ezek 42:13 w1 to Ezek 43:4 w5 | 0.537 | 1.10e-4 | 1 | 0.282 | 0.0317 | 20 |
| scan: Ezek 43:8 w1 to Ezek 43:19 w18 | 0.663 | 1.10e-4 | 1 | 0.399 | 0.0031 | 35 |
| scan: Ezek 47:18 w18 to Ezek 48:8 w8 | 0.121 | 1.10e-4 | 1 | 0.038 | 0.2372 | 18 |
| scan: Mic 5:15 w7 to Mic 6:12 w7 | 0.567 | 1.10e-4 | 1 | 0.110 | 0.2574 | 18 |
| scan: Exod 28:14 w1 to Exod 28:23 w6 | 0.642 | 1.11e-4 | 0 | - | - | 0 |
| scan: 2Chr 5:8 w1 to 2Chr 6:5 w27 | 0.429 | 1.11e-4 | 1 | 0.275 | 0.0490 | 20 |
| scan: Gen 37:26 w5 to Gen 38:2 w8 | 0.559 | 1.12e-4 | 1 | 0.487 | 0.0017 | 17 |
| scan: Exod 28:15 w1 to Exod 28:24 w8 | 0.815 | 1.12e-4 | 0 | - | - | 0 |
| scan: 1Chr 18:13 w1 to 1Chr 19:5 w12 | 0.338 | 1.12e-4 | 1 | 0.237 | 0.0512 | 26 |
| scan: 1Kgs 2:34 w1 to 1Kgs 2:45 w11 | 0.321 | 1.13e-4 | 1 | 0.265 | 2.60e-4 | 17 |
| scan: Gen 14:5 w1 to Gen 14:15 w6 | 0.682 | 1.13e-4 | 1 | 0.720 | 7.00e-4 | 38 |
| scan: 2Chr 4:15 w1 to 2Chr 5:4 w4 | 0.580 | 1.14e-4 | 1 | 0.326 | 0.0065 | 21 |
| scan: Lev 21:13 w1 to Lev 21:23 w20 | 0.507 | 1.14e-4 | 1 | 0.267 | 0.0820 | 13 |
| scan: Dan 8:6 w1 to Dan 8:17 w17 | 0.518 | 1.15e-4 | 1 | 0.402 | 0.0019 | 25 |
| scan: 1Sam 17:5 w1 to 1Sam 17:15 w11 | 0.620 | 1.15e-4 | 0 | - | - | 0 |
| scan: 1Chr 27:25 w1 to 1Chr 27:33 w7 | 0.386 | 1.15e-4 | 1 | 0.000 | 1.0000 | 28 |
| scan: Lev 4:12 w19 to Lev 4:22 w14 | 0.410 | 1.16e-4 | 1 | 0.259 | 0.0089 | 17 |
| scan: 1Chr 1:47 w1 to 1Chr 2:5 w4 | 0.758 | 1.16e-4 | 1 | 0.276 | 9.46e-7 | 33 |
| scan: Ezek 42:13 w23 to Ezek 43:4 w11 | 0.600 | 1.17e-4 | 1 | 0.300 | 0.0209 | 20 |
| scan: Exod 30:4 w1 to Exod 30:12 w14 | 0.689 | 1.19e-4 | 1 | 0.521 | 0.1778 | 20 |
| scan: Deut 20:1 w1 to Deut 20:12 w9 | 0.443 | 1.20e-4 | 1 | 0.310 | 0.0053 | 12 |
| scan: 1Kgs 20:32 w1 to 1Kgs 20:41 w13 | 0.432 | 1.20e-4 | 1 | 0.291 | 0.0030 | 14 |
| scan: Gen 36:30 w1 to Gen 36:42 w6 | 0.422 | 1.20e-4 | 1 | 0.565 | 1.09e-7 | 45 |
| scan: Gen 49:26 w1 to Gen 50:4 w9 | 0.652 | 1.20e-4 | 1 | 0.616 | 0.0020 | 19 |
| scan: Exod 15:15 w1 to Exod 15:26 w15 | 0.613 | 1.20e-4 | 1 | 0.174 | 0.1422 | 21 |
| scan: Exod 25:29 w1 to Exod 25:39 w9 | 0.504 | 1.20e-4 | 1 | 0.501 | 2.00e-4 | 40 |
| scan: Exod 26:23 w6 to Exod 26:34 w8 | 0.803 | 1.20e-4 | 1 | -0.124 | 0.8415 | 25 |
| scan: Exod 26:24 w1 to Exod 26:34 w6 | 0.803 | 1.20e-4 | 1 | -0.041 | 0.6224 | 25 |
| scan: Exod 29:38 w6 to Exod 30:4 w14 | 0.540 | 1.20e-4 | 1 | 0.069 | 0.2681 | 35 |
| scan: Exod 37:16 w1 to Exod 37:26 w11 | 0.625 | 1.20e-4 | 0 | - | - | 0 |
| scan: Exod 39:41 w6 to Exod 40:10 w7 | 0.780 | 1.20e-4 | 1 | 0.787 | 5.07e-5 | 14 |
| scan: Lev 4:33 w1 to Lev 5:8 w16 | 0.419 | 1.20e-4 | 1 | 0.211 | 0.0034 | 23 |
| scan: Lev 4:34 w1 to Lev 5:9 w12 | 0.501 | 1.20e-4 | 1 | 0.245 | 0.0032 | 25 |
| scan: Lev 14:16 w12 to Lev 14:27 w10 | 0.261 | 1.20e-4 | 1 | 0.247 | 7.00e-4 | 30 |
| scan: Lev 21:19 w1 to Lev 22:6 w16 | 0.410 | 1.20e-4 | 1 | 0.255 | 0.0329 | 16 |
| scan: Lev 25:17 w8 to Lev 25:25 w13 | 0.601 | 1.20e-4 | 1 | 0.670 | 0.0053 | 12 |
| scan: Num 7:87 w1 to Num 8:7 w16 | 0.653 | 1.20e-4 | 1 | 0.454 | 0.0420 | 12 |
| scan: Num 34:2 w1 to Num 34:13 w20 | 0.293 | 1.20e-4 | 1 | 0.060 | 0.1082 | 25 |
| scan: Num 34:27 w5 to Num 35:9 w5 | 0.367 | 1.20e-4 | 1 | 0.328 | 1.40e-4 | 22 |
| scan: Deut 2:11 w6 to Deut 2:20 w13 | 0.799 | 1.20e-4 | 1 | 0.729 | 0.0112 | 33 |
| scan: Deut 5:24 w15 to Deut 5:33 w8 | 0.297 | 1.20e-4 | 1 | 0.443 | 0.0032 | 5 |
| scan: Deut 21:3 w6 to Deut 21:14 w11 | 0.631 | 1.20e-4 | 1 | 0.751 | 0.0068 | 19 |
| scan: Deut 21:22 w1 to Deut 22:6 w21 | 0.610 | 1.20e-4 | 1 | 0.393 | 0.0926 | 9 |
| scan: Deut 22:27 w1 to Deut 23:7 w13 | 0.374 | 1.20e-4 | 1 | -0.363 | 1.0000 | 11 |
| scan: Judg 1:18 w11 to Judg 1:29 w7 | 0.565 | 1.20e-4 | 1 | 0.279 | 0.0139 | 36 |
| scan: 1Sam 23:21 w6 to 1Sam 23:28 w15 | 0.522 | 1.20e-4 | 1 | 0.119 | 0.1651 | 10 |
| scan: 1Kgs 6:19 w1 to 1Kgs 6:31 w7 | 0.418 | 1.20e-4 | 1 | 0.486 | 6.50e-4 | 21 |
| scan: 1Kgs 6:19 w6 to 1Kgs 6:31 w10 | 0.418 | 1.20e-4 | 1 | 0.479 | 0.0020 | 21 |
| scan: 1Kgs 7:5 w1 to 1Kgs 7:17 w11 | 0.534 | 1.20e-4 | 1 | 0.553 | 7.00e-4 | 43 |
| scan: 2Kgs 3:26 w8 to 2Kgs 4:9 w14 | 0.433 | 1.20e-4 | 1 | 0.304 | 0.0080 | 14 |
| scan: 2Kgs 14:21 w12 to 2Kgs 15:2 w11 | 0.331 | 1.20e-4 | 1 | 0.319 | 7.60e-4 | 29 |
| scan: 2Kgs 16:19 w1 to 2Kgs 17:10 w12 | 0.307 | 1.20e-4 | 1 | 0.272 | 0.0018 | 28 |
| scan: 1Chr 2:32 w7 to 1Chr 2:43 w2 | 0.761 | 1.20e-4 | 1 | 0.473 | 3.10e-4 | 39 |
| scan: 1Chr 5:13 w1 to 1Chr 5:24 w4 | 0.747 | 1.20e-4 | 1 | 0.552 | 0.0115 | 39 |
| scan: 1Chr 15:13 w5 to 1Chr 15:22 w4 | 0.697 | 1.20e-4 | 1 | 0.625 | 0.0819 | 46 |
| scan: 1Chr 27:22 w5 to 1Chr 27:34 w10 | 0.366 | 1.20e-4 | 1 | -0.468 | 0.9889 | 40 |
| scan: 1Chr 28:12 w1 to 1Chr 28:19 w9 | 0.496 | 1.20e-4 | 1 | 0.829 | 0.0014 | 14 |
| scan: 1Chr 28:12 w1 to 1Chr 28:20 w11 | 0.584 | 1.20e-4 | 1 | 0.320 | 0.0204 | 15 |
| scan: 1Chr 28:12 w13 to 1Chr 28:20 w27 | 0.525 | 1.20e-4 | 1 | 0.320 | 0.0204 | 15 |
| scan: 1Chr 28:13 w1 to 1Chr 28:21 w8 | 0.554 | 1.20e-4 | 1 | 0.509 | 0.0187 | 14 |
| scan: 2Chr 7:3 w11 to 2Chr 7:15 w6 | 0.272 | 1.20e-4 | 1 | 0.053 | 0.2315 | 19 |
| scan: Neh 7:63 w1 to Neh 8:1 w11 | 0.424 | 1.20e-4 | 1 | 0.169 | 0.1955 | 20 |
| scan: Ps 67:4 w4 to Ps 68:7 w7 | 0.395 | 1.20e-4 | 1 | -0.155 | 0.8830 | 23 |
| scan: Isa 45:4 w6 to Isa 45:15 w4 | 0.504 | 1.20e-4 | 1 | 0.299 | 0.0030 | 9 |
| scan: Isa 59:2 w1 to Isa 59:13 w6 | 0.782 | 1.20e-4 | 1 | 0.144 | 0.2400 | 18 |
| scan: Jer 52:26 w1 to Jer 52:34 w17 | 0.704 | 1.20e-4 | 0 | - | - | 14 |
| scan: Jer 52:26 w6 to Jer 52:34 w14 | 0.704 | 1.20e-4 | 0 | - | - | 14 |
| scan: Ezek 3:14 w1 to Ezek 3:23 w18 | 0.605 | 1.20e-4 | 1 | 0.408 | 0.0128 | 11 |
| scan: Ezek 4:14 w1 to Ezek 5:7 w18 | 0.746 | 1.20e-4 | 1 | -0.359 | 0.8062 | 24 |
| scan: Ezek 20:2 w1 to Ezek 20:12 w14 | 0.458 | 1.20e-4 | 1 | 0.531 | 0.0033 | 7 |
| scan: Ezek 33:21 w1 to Ezek 33:33 w1 | 0.421 | 1.20e-4 | 1 | 0.590 | 8.98e-5 | 16 |
| scan: Ezek 41:2 w13 to Ezek 41:13 w6 | 0.209 | 1.20e-4 | 1 | 0.100 | 0.0014 | 33 |
| scan: Ezek 47:19 w1 to Ezek 48:4 w10 | 0.500 | 1.20e-4 | 1 | 0.386 | 8.90e-4 | 15 |
| scan: Dan 2:35 w22 to Dan 2:47 w20 | 0.267 | 1.20e-4 | 1 | 0.305 | 3.90e-4 | 24 |
| scan: Zech 12:7 w7 to Zech 13:4 w14 | 0.586 | 1.20e-4 | 1 | 0.356 | 0.0033 | 19 |
| scan: Isa 50:1 w18 to Isa 50:11 w6 | 0.621 | 1.20e-4 | 1 | 0.257 | 0.0835 | 7 |
| scan: Deut 15:2 w1 to Deut 15:9 w21 | 0.435 | 1.21e-4 | 1 | 0.284 | 0.0607 | 12 |
| scan: Ezek 32:1 w10 to Ezek 32:13 w7 | 0.485 | 1.21e-4 | 1 | 0.355 | 0.0136 | 16 |
| scan: Gen 2:8 w7 to Gen 2:19 w19 | 0.526 | 1.22e-4 | 1 | -0.017 | 0.5566 | 10 |
| scan: Exod 14:4 w16 to Exod 14:13 w27 | 0.422 | 1.22e-4 | 1 | 0.115 | 0.1413 | 14 |
| scan: Ezek 41:2 w13 to Ezek 41:13 w12 | 0.202 | 1.23e-4 | 1 | 0.124 | 3.00e-4 | 33 |
| scan: Jer 51:17 w9 to Jer 51:26 w13 | 0.551 | 1.24e-4 | 1 | 0.123 | 0.0400 | 10 |
| scan: Deut 27:24 w1 to Deut 28:9 w8 | 0.630 | 1.25e-4 | 1 | 0.084 | 0.3307 | 2 |
| scan: Gen 36:30 w1 to Gen 36:41 w6 | 0.471 | 1.26e-4 | 1 | 0.609 | 3.75e-7 | 43 |
| scan: Ezek 5:14 w1 to Ezek 6:6 w6 | 0.891 | 1.26e-4 | 1 | 0.734 | 0.0098 | 17 |
| scan: 1Chr 15:1 w6 to 1Chr 15:13 w4 | 0.576 | 1.26e-4 | 1 | 0.503 | 2.70e-4 | 18 |
| scan: 1Kgs 7:6 w1 to 1Kgs 7:16 w9 | 0.616 | 1.27e-4 | 1 | 0.641 | 3.10e-4 | 36 |
| scan: Gen 2:16 w7 to Gen 3:3 w13 | 0.408 | 1.30e-4 | 1 | 0.446 | 1.30e-4 | 6 |
| scan: Gen 37:25 w12 to Gen 38:1 w7 | 0.466 | 1.30e-4 | 1 | 0.305 | 0.0567 | 20 |
| scan: Exod 2:9 w15 to Exod 2:17 w3 | 0.784 | 1.30e-4 | 1 | 0.297 | 0.0415 | 9 |
| scan: Exod 2:10 w1 to Exod 2:17 w3 | 0.832 | 1.30e-4 | 1 | 0.356 | 0.0363 | 9 |
| scan: Exod 2:23 w1 to Exod 3:8 w17 | 0.559 | 1.30e-4 | 1 | 0.553 | 1.70e-4 | 13 |
| scan: Exod 15:8 w9 to Exod 15:21 w3 | 0.794 | 1.30e-4 | 1 | 0.255 | 0.0627 | 21 |
| scan: Exod 25:28 w1 to Exod 25:39 w9 | 0.469 | 1.30e-4 | 1 | 0.439 | 6.34e-5 | 43 |
| scan: Exod 28:15 w9 to Exod 28:23 w6 | 0.930 | 1.30e-4 | 0 | - | - | 0 |
| scan: Exod 28:15 w9 to Exod 28:23 w14 | 0.930 | 1.30e-4 | 0 | - | - | 0 |
| scan: Exod 40:7 w9 to Exod 40:18 w13 | 0.558 | 1.30e-4 | 0 | - | - | 0 |
| scan: Lev 25:17 w8 to Lev 25:26 w6 | 0.537 | 1.30e-4 | 1 | 0.643 | 0.0016 | 15 |
| scan: Num 7:87 w1 to Num 8:8 w14 | 0.695 | 1.30e-4 | 1 | 0.712 | 1.80e-4 | 14 |
| scan: Num 23:11 w8 to Num 23:21 w8 | 0.449 | 1.30e-4 | 1 | 0.091 | 0.2520 | 16 |
| scan: Num 28:13 w1 to Num 28:20 w4 | 0.841 | 1.30e-4 | 1 | 0.223 | 0.0727 | 22 |
| scan: Num 33:33 w4 to Num 33:44 w2 | 0.492 | 1.30e-4 | 1 | 0.335 | 0.1250 | 51 |
| scan: Deut 20:1 w1 to Deut 20:12 w7 | 0.449 | 1.30e-4 | 1 | 0.300 | 0.0118 | 12 |
| scan: Deut 20:2 w1 to Deut 20:11 w15 | 0.531 | 1.30e-4 | 1 | 0.321 | 0.0115 | 12 |
| scan: Judg 11:18 w18 to Judg 11:29 w10 | 0.355 | 1.30e-4 | 1 | 0.351 | 0.0017 | 38 |
| scan: Judg 11:32 w1 to Judg 12:3 w21 | 0.415 | 1.30e-4 | 1 | 0.470 | 3.10e-6 | 25 |
| scan: 1Sam 4:20 w1 to 1Sam 5:9 w18 | 0.385 | 1.30e-4 | 1 | 0.212 | 0.0261 | 38 |
| scan: 1Sam 28:12 w1 to 1Sam 28:23 w11 | 0.355 | 1.30e-4 | 1 | 0.285 | 0.0045 | 12 |
| scan: 1Sam 28:12 w8 to 1Sam 28:23 w16 | 0.416 | 1.30e-4 | 1 | 0.332 | 7.20e-4 | 12 |
| scan: 2Sam 3:15 w1 to 2Sam 3:21 w27 | 0.203 | 1.30e-4 | 1 | 0.049 | 0.3825 | 13 |
| scan: 1Kgs 9:1 w11 to 1Kgs 9:11 w13 | 0.340 | 1.30e-4 | 1 | 0.350 | 6.80e-4 | 15 |
| scan: 1Kgs 9:24 w1 to 1Kgs 10:5 w18 | 0.483 | 1.30e-4 | 0 | - | - | 0 |
| scan: 1Kgs 17:23 w1 to 1Kgs 18:10 w23 | 0.391 | 1.30e-4 | 1 | 0.136 | 0.0573 | 18 |
| scan: 1Kgs 20:31 w15 to 1Kgs 20:41 w6 | 0.442 | 1.30e-4 | 1 | 0.286 | 0.0019 | 14 |
| scan: 2Kgs 14:20 w1 to 2Kgs 15:1 w13 | 0.334 | 1.30e-4 | 1 | 0.278 | 0.0097 | 27 |
| scan: 1Chr 28:7 w6 to 1Chr 28:20 w11 | 0.576 | 1.30e-4 | 1 | -0.226 | 0.9860 | 21 |
| scan: 1Chr 28:13 w1 to 1Chr 28:20 w27 | 0.512 | 1.30e-4 | 1 | 0.662 | 4.80e-4 | 13 |
| scan: 2Chr 7:2 w8 to 2Chr 7:14 w12 | 0.255 | 1.30e-4 | 1 | 0.176 | 0.0105 | 18 |
| scan: 2Chr 29:16 w18 to 2Chr 29:28 w11 | 0.379 | 1.30e-4 | 1 | 0.080 | 0.1884 | 23 |
| scan: Isa 11:13 w1 to Isa 13:2 w13 | 0.654 | 1.30e-4 | 1 | 0.666 | 0.0021 | 8 |
| scan: Isa 11:13 w7 to Isa 13:2 w13 | 0.654 | 1.30e-4 | 1 | 0.530 | 0.0217 | 8 |
| scan: Isa 11:13 w7 to Isa 13:3 w3 | 0.654 | 1.30e-4 | 1 | 0.353 | 0.0801 | 10 |
| scan: Isa 11:14 w1 to Isa 13:2 w13 | 0.654 | 1.30e-4 | 1 | 0.530 | 0.0217 | 8 |
| scan: Jer 25:16 w1 to Jer 25:29 w26 | 0.382 | 1.30e-4 | 0 | - | - | 0 |
| scan: Jer 51:15 w7 to Jer 51:26 w7 | 0.831 | 1.30e-4 | 1 | 0.426 | 1.80e-4 | 10 |
| scan: Jer 51:16 w10 to Jer 51:27 w15 | 0.487 | 1.30e-4 | 1 | 0.139 | 0.0230 | 14 |
| scan: Ezek 3:14 w4 to Ezek 3:24 w14 | 0.544 | 1.30e-4 | 1 | 0.514 | 7.00e-4 | 12 |
| scan: Ezek 5:1 w17 to Ezek 5:12 w10 | 0.455 | 1.30e-4 | 1 | 0.459 | 1.15e-5 | 20 |
| scan: Ezek 20:3 w1 to Ezek 20:12 w9 | 0.465 | 1.30e-4 | 1 | 0.508 | 0.0061 | 7 |
| scan: Ezek 43:10 w12 to Ezek 43:19 w14 | 0.589 | 1.30e-4 | 1 | 0.290 | 0.0019 | 27 |
| scan: Ezek 47:20 w10 to Ezek 48:10 w26 | 0.188 | 1.30e-4 | 1 | 0.152 | 0.0153 | 12 |
| scan: Dan 4:8 w1 to Dan 4:19 w26 | 0.444 | 1.30e-4 | 1 | 0.400 | 0.0019 | 23 |
| scan: Amos 5:11 w1 to Amos 5:22 w12 | 0.503 | 1.30e-4 | 1 | 0.517 | 0.0084 | 12 |
| scan: Jer 25:15 w1 to Jer 25:28 w7 | 0.468 | 1.34e-4 | 0 | - | - | 0 |
| scan: Exod 29:39 w6 to Exod 30:5 w5 | 0.644 | 1.35e-4 | 1 | 0.163 | 0.0917 | 34 |
| scan: Deut 2:13 w1 to Deut 2:24 w18 | 0.703 | 1.36e-4 | 1 | 0.359 | 0.0594 | 39 |
| scan: Jonah 1:11 w9 to Jonah 2:6 w7 | 0.573 | 1.36e-4 | 1 | -0.089 | 0.6916 | 9 |
| scan: Lev 21:15 w5 to Lev 21:24 w6 | 0.609 | 1.36e-4 | 1 | 0.279 | 0.0961 | 11 |
| scan: Lev 4:6 w1 to Lev 4:15 w15 | 0.310 | 1.37e-4 | 1 | 0.196 | 0.0845 | 21 |
| scan: 2Sam 7:20 w7 to 2Sam 7:28 w15 | 0.403 | 1.38e-4 | 1 | 0.035 | 0.3759 | 2 |
| scan: Gen 2:17 w1 to Gen 3:3 w15 | 0.356 | 1.40e-4 | 1 | 0.399 | 1.20e-4 | 6 |
| scan: Gen 25:10 w8 to Gen 25:21 w8 | 0.572 | 1.40e-4 | 1 | 0.148 | 0.1432 | 26 |
| scan: Gen 37:1 w1 to Gen 37:12 w7 | 0.419 | 1.40e-4 | 1 | 0.202 | 0.0358 | 14 |
| scan: Gen 37:35 w1 to Gen 38:9 w19 | 0.483 | 1.40e-4 | 1 | 0.306 | 0.0325 | 13 |
| scan: Exod 2:9 w1 to Exod 2:16 w12 | 0.570 | 1.40e-4 | 1 | 0.544 | 3.20e-4 | 9 |
| scan: Exod 37:15 w9 to Exod 37:24 w8 | 0.538 | 1.40e-4 | 0 | - | - | 0 |
| scan: Exod 37:16 w1 to Exod 37:24 w8 | 0.538 | 1.40e-4 | 0 | - | - | 0 |
| scan: Lev 3:14 w6 to Lev 4:8 w18 | 0.384 | 1.40e-4 | 1 | 0.457 | 0.0020 | 25 |
| scan: Lev 21:2 w6 to Lev 21:11 w10 | 0.554 | 1.40e-4 | 1 | 0.634 | 0.0016 | 17 |
| scan: Lev 21:14 w1 to Lev 22:2 w20 | 0.477 | 1.40e-4 | 1 | 0.445 | 0.0061 | 13 |
| scan: Lev 21:19 w8 to Lev 22:4 w25 | 0.457 | 1.40e-4 | 1 | 0.240 | 0.0562 | 13 |
| scan: Lev 24:11 w12 to Lev 24:23 w14 | 0.810 | 1.40e-4 | 1 | 0.159 | 0.2432 | 13 |
| scan: Num 7:10 w9 to Num 7:18 w8 | 0.576 | 1.40e-4 | 1 | 0.610 | 2.30e-4 | 13 |
| scan: Num 31:7 w9 to Num 31:17 w12 | 0.609 | 1.40e-4 | 1 | -0.168 | 0.7704 | 18 |
| scan: Deut 4:12 w6 to Deut 4:22 w9 | 0.458 | 1.40e-4 | 1 | 0.311 | 0.0177 | 7 |
| scan: Deut 4:14 w1 to Deut 4:22 w16 | 0.531 | 1.40e-4 | 1 | 0.418 | 0.0199 | 7 |
| scan: Josh 11:16 w19 to Josh 12:3 w18 | 0.446 | 1.40e-4 | 1 | 0.243 | 0.0077 | 36 |
| scan: 1Sam 28:12 w8 to 1Sam 28:23 w11 | 0.417 | 1.40e-4 | 1 | 0.358 | 1.40e-4 | 12 |
| scan: 1Kgs 18:43 w14 to 1Kgs 19:6 w11 | 0.699 | 1.40e-4 | 1 | 0.007 | 0.4800 | 17 |
| scan: 2Kgs 14:21 w12 to 2Kgs 15:1 w13 | 0.329 | 1.40e-4 | 1 | 0.292 | 0.0021 | 27 |
| scan: 1Chr 6:19 w5 to 1Chr 6:31 w11 | 0.409 | 1.40e-4 | 1 | 0.000 | 1.0000 | 26 |
| scan: 1Chr 12:15 w14 to 1Chr 12:22 w13 | 0.372 | 1.40e-4 | 1 | -0.088 | 0.6949 | 15 |
| scan: 1Chr 27:24 w13 to 1Chr 27:33 w7 | 0.459 | 1.40e-4 | 1 | -0.310 | 0.9500 | 32 |
| scan: 1Chr 28:9 w22 to 1Chr 29:1 w13 | 0.377 | 1.40e-4 | 1 | 0.081 | 0.2003 | 19 |
| scan: 2Chr 8:13 w1 to 2Chr 9:5 w12 | 0.380 | 1.40e-4 | 1 | 0.297 | 0.0014 | 17 |
| scan: Song 4:9 w1 to Song 5:2 w19 | 0.509 | 1.40e-4 | 1 | 0.490 | 0.0013 | 20 |
| scan: Isa 44:21 w1 to Isa 45:3 w15 | 0.714 | 1.40e-4 | 1 | 0.642 | 0.0018 | 17 |
| scan: Jer 25:19 w1 to Jer 25:32 w15 | 0.381 | 1.40e-4 | 0 | - | - | 0 |
| scan: Jer 25:29 w1 to Jer 26:2 w26 | 0.528 | 1.40e-4 | 1 | 0.595 | 0.0011 | 18 |
| scan: Ezek 31:12 w6 to Ezek 32:6 w6 | 0.376 | 1.40e-4 | 1 | 0.223 | 0.0598 | 19 |
| scan: Jonah 1:12 w1 to Jonah 2:5 w9 | 0.580 | 1.40e-4 | 1 | -0.109 | 0.6788 | 5 |
| scan: Zech 12:7 w7 to Zech 13:5 w12 | 0.566 | 1.40e-4 | 1 | 0.451 | 7.72e-5 | 19 |
| scan: Zech 12:8 w1 to Zech 13:4 w8 | 0.600 | 1.40e-4 | 1 | 0.414 | 0.0012 | 18 |
| scan: 1Chr 27:28 w9 to 1Chr 28:5 w18 | 0.426 | 1.40e-4 | 1 | -0.367 | 0.9715 | 30 |
| scan: Hos 10:7 w1 to Hos 10:15 w13 | 0.810 | 1.41e-4 | 1 | 0.182 | 0.3111 | 16 |
| scan: Lev 13:28 w1 to Lev 13:38 w10 | 0.205 | 1.45e-4 | 1 | 0.180 | 0.0319 | 41 |
| scan: Gen 4:1 w6 to Gen 4:10 w10 | 0.199 | 1.50e-4 | 1 | 0.125 | 0.0652 | 2 |
| scan: Gen 4:5 w7 to Gen 4:16 w9 | 0.346 | 1.50e-4 | 1 | 0.129 | 0.0225 | 8 |
| scan: Gen 36:43 w5 to Gen 37:12 w2 | 0.437 | 1.50e-4 | 1 | 0.179 | 0.0576 | 19 |
| scan: Gen 43:11 w17 to Gen 43:23 w15 | 0.389 | 1.50e-4 | 1 | 0.234 | 0.0176 | 22 |
| scan: Exod 25:27 w1 to Exod 25:38 w4 | 0.438 | 1.50e-4 | 1 | 0.440 | 1.24e-5 | 44 |
| scan: Exod 25:30 w1 to Exod 26:1 w16 | 0.811 | 1.50e-4 | 1 | 0.288 | 0.0726 | 39 |
| scan: Exod 28:14 w1 to Exod 28:23 w14 | 0.600 | 1.50e-4 | 0 | - | - | 0 |
| scan: Exod 33:4 w1 to Exod 33:13 w15 | 0.305 | 1.50e-4 | 1 | 0.203 | 0.0049 | 11 |
| scan: Exod 35:34 w1 to Exod 36:9 w11 | 0.318 | 1.50e-4 | 0 | - | - | 0 |
| scan: Exod 37:2 w6 to Exod 37:13 w5 | 0.422 | 1.50e-4 | 1 | 0.145 | 0.1341 | 29 |
| scan: Exod 37:13 w1 to Exod 37:24 w8 | 0.498 | 1.50e-4 | 0 | - | - | 0 |
| scan: Exod 37:15 w9 to Exod 37:25 w6 | 0.547 | 1.50e-4 | 0 | - | - | 0 |
| scan: Lev 3:14 w6 to Lev 4:9 w17 | 0.410 | 1.50e-4 | 1 | 0.447 | 9.00e-4 | 28 |
| scan: Lev 4:13 w10 to Lev 4:23 w7 | 0.462 | 1.50e-4 | 1 | 0.367 | 1.90e-4 | 18 |
| scan: Lev 21:14 w9 to Lev 21:24 w6 | 0.552 | 1.50e-4 | 1 | 0.320 | 0.0535 | 13 |
| scan: Lev 21:15 w1 to Lev 22:1 w5 | 0.549 | 1.50e-4 | 1 | 0.347 | 0.0401 | 11 |
| scan: Lev 21:18 w1 to Lev 22:5 w9 | 0.332 | 1.50e-4 | 1 | 0.374 | 0.0053 | 16 |
| scan: Lev 24:12 w3 to Lev 24:23 w14 | 0.767 | 1.50e-4 | 1 | 0.354 | 0.0433 | 11 |
| scan: Num 5:12 w7 to Num 5:20 w7 | 0.516 | 1.50e-4 | 1 | 0.328 | 0.0170 | 14 |
| scan: Num 28:12 w9 to Num 28:20 w4 | 0.739 | 1.50e-4 | 1 | 0.145 | 0.0624 | 25 |
| scan: Deut 21:20 w1 to Deut 22:7 w13 | 0.476 | 1.50e-4 | 1 | 0.462 | 0.0188 | 15 |
| scan: Deut 27:25 w1 to Deut 28:10 w9 | 0.506 | 1.50e-4 | 1 | 0.523 | 0.0016 | 2 |
| scan: Deut 27:25 w1 to Deut 28:10 w11 | 0.506 | 1.50e-4 | 1 | 0.523 | 0.0016 | 2 |
| scan: Deut 27:25 w8 to Deut 28:10 w9 | 0.506 | 1.50e-4 | 1 | 0.523 | 0.0016 | 2 |
| scan: Deut 27:25 w8 to Deut 28:10 w11 | 0.506 | 1.50e-4 | 1 | 0.500 | 0.0014 | 2 |
| scan: Judg 1:19 w1 to Judg 1:30 w9 | 0.471 | 1.50e-4 | 1 | 0.227 | 0.0065 | 34 |
| scan: Judg 1:19 w8 to Judg 1:29 w11 | 0.604 | 1.50e-4 | 1 | 0.291 | 0.0110 | 32 |
| scan: Judg 11:31 w12 to Judg 12:1 w21 | 0.544 | 1.50e-4 | 1 | 0.371 | 0.0122 | 23 |
| scan: Judg 16:30 w1 to Judg 17:7 w12 | 0.637 | 1.50e-4 | 1 | 0.548 | 0.0024 | 13 |
| scan: 1Sam 4:21 w1 to 1Sam 5:8 w19 | 0.434 | 1.50e-4 | 1 | 0.210 | 0.0291 | 33 |
| scan: 1Sam 8:9 w4 to 1Sam 8:19 w12 | 0.713 | 1.50e-4 | 1 | 0.357 | 0.0534 | 10 |
| scan: 1Sam 15:32 w1 to 1Sam 16:4 w16 | 0.278 | 1.50e-4 | 1 | 0.112 | 0.1006 | 8 |
| scan: 2Sam 7:16 w1 to 2Sam 7:24 w14 | 0.625 | 1.50e-4 | 1 | 0.434 | 0.0927 | 6 |
| scan: 2Sam 15:12 w13 to 2Sam 15:19 w10 | 0.385 | 1.50e-4 | 1 | 0.102 | 0.2572 | 25 |
| scan: 1Kgs 7:5 w1 to 1Kgs 7:16 w19 | 0.535 | 1.50e-4 | 1 | 0.641 | 3.10e-4 | 40 |
| scan: 1Kgs 7:5 w6 to 1Kgs 7:16 w19 | 0.584 | 1.50e-4 | 1 | 0.641 | 3.10e-4 | 40 |
| scan: 1Kgs 17:23 w11 to 1Kgs 18:10 w15 | 0.392 | 1.50e-4 | 1 | 0.136 | 0.0573 | 18 |
| scan: 1Kgs 17:24 w1 to 1Kgs 18:8 w8 | 0.441 | 1.50e-4 | 1 | 0.113 | 0.1551 | 16 |
| scan: 1Kgs 20:27 w1 to 1Kgs 20:36 w18 | 0.461 | 1.50e-4 | 1 | 0.201 | 0.0304 | 19 |
| scan: 1Kgs 20:32 w18 to 1Kgs 20:41 w13 | 0.506 | 1.50e-4 | 1 | -0.061 | 0.6819 | 14 |
| scan: 2Kgs 3:26 w1 to 2Kgs 4:10 w17 | 0.403 | 1.50e-4 | 1 | 0.397 | 5.10e-4 | 15 |
| scan: 2Kgs 16:8 w13 to 2Kgs 16:19 w5 | 0.270 | 1.50e-4 | 1 | 0.141 | 0.0143 | 17 |
| scan: 1Chr 24:18 w1 to 1Chr 25:1 w13 | 0.289 | 1.50e-4 | 1 | 0.194 | 0.0013 | 36 |
| scan: 1Chr 28:8 w15 to 1Chr 28:20 w27 | 0.488 | 1.50e-4 | 1 | 0.114 | 0.1264 | 19 |
| scan: 1Chr 28:11 w1 to 1Chr 28:21 w8 | 0.436 | 1.50e-4 | 1 | 0.008 | 0.4759 | 17 |
| scan: 2Chr 6:2 w6 to 2Chr 6:12 w10 | 0.422 | 1.50e-4 | 1 | 0.035 | 0.3535 | 1 |
| scan: Eccl 2:24 w1 to Eccl 3:12 w11 | 0.493 | 1.50e-4 | 1 | 0.353 | 3.80e-6 | 11 |
| scan: Eccl 2:25 w1 to Eccl 3:13 w9 | 0.594 | 1.50e-4 | 1 | 0.415 | 2.10e-6 | 11 |
| scan: Isa 34:15 w8 to Isa 35:9 w11 | 0.783 | 1.50e-4 | 1 | 0.570 | 8.80e-4 | 18 |
| scan: Isa 45:4 w6 to Isa 45:16 w4 | 0.465 | 1.50e-4 | 1 | 0.299 | 0.0030 | 10 |
| scan: Jer 48:18 w1 to Jer 48:28 w12 | 0.378 | 1.50e-4 | 1 | 0.000 | 1.0000 | 36 |
| scan: Ezek 1:22 w9 to Ezek 2:5 w9 | 0.506 | 1.50e-4 | 1 | 0.201 | 0.1084 | 8 |
| scan: Ezek 41:2 w1 to Ezek 41:13 w6 | 0.190 | 1.50e-4 | 1 | 0.100 | 0.0014 | 33 |
| scan: Ezek 45:7 w1 to Ezek 45:18 w15 | 0.499 | 1.50e-4 | 1 | 0.415 | 0.0016 | 23 |
| scan: Ezek 47:17 w13 to Ezek 48:7 w10 | 0.177 | 1.50e-4 | 1 | 0.097 | 0.0568 | 19 |
| scan: Ezek 47:18 w18 to Ezek 48:4 w10 | 0.324 | 1.50e-4 | 1 | 0.155 | 0.0488 | 18 |
| scan: Dan 11:33 w5 to Dan 11:42 w3 | 0.750 | 1.50e-4 | 1 | 0.655 | 8.10e-4 | 20 |
| scan: Jonah 1:12 w10 to Jonah 2:5 w6 | 0.614 | 1.50e-4 | 1 | -0.109 | 0.6788 | 5 |
| scan: Exod 25:18 w1 to Exod 25:24 w9 | 0.686 | 1.52e-4 | 1 | 0.394 | 0.0958 | 16 |
| scan: Exod 37:3 w9 to Exod 37:15 w8 | 0.431 | 1.53e-4 | 0 | - | - | 0 |
| scan: Ezek 42:13 w23 to Ezek 43:4 w5 | 0.526 | 1.57e-4 | 1 | 0.353 | 0.0071 | 20 |
| scan: Lev 4:33 w1 to Lev 5:6 w20 | 0.534 | 1.59e-4 | 1 | 0.100 | 0.1454 | 18 |
| scan: Gen 25:22 w1 to Gen 25:32 w6 | 0.444 | 1.60e-4 | 1 | 0.409 | 0.0034 | 14 |
| scan: Exod 2:8 w6 to Exod 2:16 w4 | 0.645 | 1.60e-4 | 1 | 0.530 | 2.20e-4 | 9 |
| scan: Exod 14:8 w1 to Exod 14:16 w16 | 0.446 | 1.60e-4 | 1 | 0.318 | 0.0284 | 13 |
| scan: Exod 29:36 w12 to Exod 29:45 w4 | 0.704 | 1.60e-4 | 1 | 0.556 | 0.0119 | 26 |
| scan: Exod 29:37 w1 to Exod 29:44 w13 | 0.747 | 1.60e-4 | 1 | 0.828 | 3.97e-4 | 23 |
| scan: Exod 38:23 w1 to Exod 39:3 w18 | 0.530 | 1.60e-4 | 1 | 0.505 | 1.50e-4 | 41 |
| scan: Lev 19:19 w1 to Lev 19:28 w10 | 0.581 | 1.60e-4 | 1 | 0.000 | 1.0000 | 30 |
| scan: Lev 21:16 w1 to Lev 21:24 w6 | 0.631 | 1.60e-4 | 1 | 0.257 | 0.1484 | 11 |
| scan: Num 28:12 w1 to Num 28:20 w11 | 0.561 | 1.60e-4 | 1 | 0.145 | 0.0624 | 25 |
| scan: Deut 5:15 w1 to Deut 5:24 w23 | 0.579 | 1.60e-4 | 1 | 0.697 | 9.20e-4 | 3 |
| scan: Deut 28:64 w1 to Deut 29:6 w13 | 0.433 | 1.60e-4 | 1 | 0.367 | 0.0181 | 10 |
| scan: Deut 31:11 w1 to Deut 31:19 w20 | 0.496 | 1.60e-4 | 1 | 0.435 | 0.0020 | 13 |
| scan: Josh 17:3 w1 to Josh 17:14 w23 | 0.225 | 1.60e-4 | 1 | 0.380 | 4.10e-6 | 35 |
| scan: Ruth 3:13 w17 to Ruth 4:5 w18 | 0.287 | 1.60e-4 | 1 | -0.113 | 0.8627 | 24 |
| scan: 1Kgs 6:21 w1 to 1Kgs 6:31 w7 | 0.465 | 1.60e-4 | 1 | 0.458 | 3.60e-4 | 17 |
| scan: 1Kgs 17:23 w1 to 1Kgs 18:8 w8 | 0.421 | 1.60e-4 | 1 | 0.078 | 0.1840 | 16 |
| scan: 1Chr 24:5 w6 to 1Chr 24:23 w2 | 0.758 | 1.60e-4 | 1 | -0.021 | 0.5491 | 37 |
| scan: 1Chr 27:28 w9 to 1Chr 28:5 w8 | 0.402 | 1.60e-4 | 1 | -0.367 | 0.9715 | 30 |
| scan: 2Chr 6:3 w1 to 2Chr 6:12 w8 | 0.428 | 1.60e-4 | 1 | 0.265 | 0.0190 | 0 |
| scan: 2Chr 7:3 w1 to 2Chr 7:13 w16 | 0.272 | 1.60e-4 | 1 | 0.106 | 0.0950 | 17 |
| scan: 2Chr 8:12 w6 to 2Chr 9:6 w20 | 0.325 | 1.60e-4 | 1 | 0.098 | 0.1673 | 17 |
| scan: Neh 7:18 w1 to Neh 7:39 w9 | 0.161 | 1.60e-4 | 1 | 0.048 | 0.2846 | 48 |
| scan: Isa 42:23 w5 to Isa 43:9 w12 | 0.703 | 1.60e-4 | 1 | 0.146 | 0.3482 | 12 |
| scan: Isa 45:5 w1 to Isa 45:14 w29 | 0.504 | 1.60e-4 | 1 | 0.244 | 0.0283 | 8 |
| scan: Jer 36:19 w1 to Jer 36:27 w5 | 0.515 | 1.60e-4 | 1 | 0.285 | 0.0225 | 22 |
| scan: Ezek 17:4 w5 to Ezek 17:13 w13 | 0.573 | 1.60e-4 | 1 | 0.608 | 0.0012 | 28 |
| scan: Ezek 32:2 w1 to Ezek 32:13 w16 | 0.491 | 1.60e-4 | 1 | 0.630 | 4.62e-5 | 13 |
| scan: Ezek 33:22 w1 to Ezek 33:33 w8 | 0.441 | 1.60e-4 | 1 | 0.540 | 0.0018 | 12 |
| scan: Ezek 42:13 w1 to Ezek 43:3 w18 | 0.474 | 1.60e-4 | 1 | 0.284 | 0.0405 | 20 |
| scan: Ezek 42:13 w1 to Ezek 43:3 w21 | 0.451 | 1.60e-4 | 1 | 0.284 | 0.0405 | 20 |
| scan: Ezek 47:18 w1 to Ezek 48:7 w10 | 0.100 | 1.60e-4 | 1 | 0.091 | 0.0829 | 18 |
| scan: Ezek 47:22 w13 to Ezek 48:12 w10 | 0.237 | 1.60e-4 | 1 | 0.232 | 0.0118 | 11 |
| scan: Ezek 48:19 w3 to Ezek 48:32 w9 | 0.259 | 1.60e-4 | 1 | -0.035 | 0.7203 | 13 |
| scan: Exod 14:7 w9 to Exod 14:17 w8 | 0.422 | 1.64e-4 | 1 | 0.250 | 0.0267 | 15 |
| scan: Exod 2:9 w15 to Exod 2:16 w12 | 0.767 | 1.70e-4 | 1 | 0.404 | 0.0145 | 9 |
| scan: Exod 2:10 w1 to Exod 2:16 w12 | 0.767 | 1.70e-4 | 1 | 0.455 | 0.0167 | 9 |
| scan: Exod 28:13 w1 to Exod 28:23 w14 | 0.549 | 1.70e-4 | 0 | - | - | 0 |
| scan: Exod 28:14 w10 to Exod 28:23 w14 | 0.711 | 1.70e-4 | 0 | - | - | 0 |
| scan: Exod 29:39 w6 to Exod 30:4 w14 | 0.600 | 1.70e-4 | 1 | 0.283 | 0.0239 | 31 |
| scan: Exod 30:2 w9 to Exod 30:12 w20 | 0.571 | 1.70e-4 | 1 | 0.000 | 1.0000 | 27 |
| scan: Exod 30:2 w9 to Exod 30:13 w17 | 0.579 | 1.70e-4 | 1 | 0.754 | 0.0111 | 29 |
| scan: Exod 33:3 w6 to Exod 33:12 w27 | 0.322 | 1.70e-4 | 1 | 0.145 | 0.0906 | 14 |
| scan: Exod 37:12 w6 to Exod 37:24 w5 | 0.542 | 1.70e-4 | 0 | - | - | 0 |
| scan: Lev 4:12 w19 to Lev 4:23 w7 | 0.391 | 1.70e-4 | 1 | 0.262 | 0.0027 | 19 |
| scan: Lev 24:14 w1 to Lev 24:23 w14 | 0.766 | 1.70e-4 | 1 | 0.342 | 0.0728 | 10 |
| scan: Lev 24:14 w14 to Lev 25:3 w8 | 0.579 | 1.70e-4 | 1 | 0.214 | 0.1201 | 13 |
| scan: Lev 24:14 w14 to Lev 25:3 w11 | 0.579 | 1.70e-4 | 1 | 0.214 | 0.1201 | 13 |
| scan: Lev 25:17 w1 to Lev 25:25 w13 | 0.522 | 1.70e-4 | 1 | 0.670 | 0.0053 | 12 |
| scan: Num 1:3 w9 to Num 1:17 w9 | 0.501 | 1.70e-4 | 1 | 0.448 | 2.30e-4 | 23 |
| scan: Num 1:4 w1 to Num 1:18 w12 | 0.532 | 1.70e-4 | 1 | 0.366 | 0.0013 | 26 |
| scan: Num 33:35 w3 to Num 33:42 w2 | 0.650 | 1.70e-4 | 1 | 0.243 | 0.2639 | 34 |
| scan: Num 34:28 w5 to Num 35:11 w7 | 0.304 | 1.70e-4 | 1 | 0.308 | 7.10e-4 | 24 |
| scan: Num 34:28 w5 to Num 35:11 w13 | 0.276 | 1.70e-4 | 1 | 0.308 | 7.10e-4 | 24 |
| scan: Deut 27:25 w1 to Deut 28:9 w8 | 0.592 | 1.70e-4 | 1 | 0.579 | 7.40e-4 | 2 |
| scan: Deut 28:12 w1 to Deut 28:24 w7 | 0.551 | 1.70e-4 | 1 | 0.635 | 2.00e-4 | 20 |
| scan: Deut 28:64 w10 to Deut 29:6 w13 | 0.437 | 1.70e-4 | 1 | 0.367 | 0.0181 | 10 |
| scan: Judg 1:20 w1 to Judg 1:28 w11 | 0.803 | 1.70e-4 | 1 | 0.175 | 0.1240 | 25 |
| scan: Judg 11:19 w1 to Judg 11:29 w19 | 0.362 | 1.70e-4 | 1 | 0.111 | 0.2105 | 30 |
| scan: Judg 16:29 w1 to Judg 17:8 w17 | 0.587 | 1.70e-4 | 1 | 0.491 | 0.0011 | 15 |
| scan: Judg 16:30 w18 to Judg 17:7 w7 | 0.658 | 1.70e-4 | 1 | 0.548 | 0.0024 | 13 |
| scan: 1Sam 13:17 w7 to 1Sam 14:6 w16 | 0.501 | 1.70e-4 | 1 | 0.364 | 0.0046 | 33 |
| scan: 1Sam 20:16 w6 to 1Sam 20:27 w7 | 0.507 | 1.70e-4 | 1 | 0.358 | 0.0200 | 17 |
| scan: 2Sam 14:25 w10 to 2Sam 15:2 w31 | 0.337 | 1.70e-4 | 1 | 0.593 | 2.52e-5 | 42 |
| scan: 1Kgs 6:20 w15 to 1Kgs 6:31 w7 | 0.490 | 1.70e-4 | 1 | 0.479 | 0.0020 | 21 |
| scan: 1Kgs 17:23 w11 to 1Kgs 18:8 w8 | 0.465 | 1.70e-4 | 1 | 0.071 | 0.2056 | 16 |
| scan: 2Kgs 2:22 w1 to 2Kgs 3:8 w9 | 0.577 | 1.70e-4 | 1 | 0.635 | 3.18e-5 | 25 |
| scan: 2Kgs 3:27 w17 to 2Kgs 4:9 w14 | 0.477 | 1.70e-4 | 1 | 0.371 | 0.0021 | 9 |
| scan: 1Chr 5:12 w5 to 1Chr 5:24 w19 | 0.644 | 1.70e-4 | 1 | 0.552 | 0.0115 | 42 |
| scan: 1Chr 15:1 w1 to 1Chr 15:13 w4 | 0.560 | 1.70e-4 | 1 | 0.503 | 2.70e-4 | 18 |
| scan: 1Chr 15:2 w12 to 1Chr 15:14 w9 | 0.499 | 1.70e-4 | 1 | 0.435 | 2.70e-4 | 19 |
| scan: 1Chr 27:24 w13 to 1Chr 27:33 w3 | 0.406 | 1.70e-4 | 1 | -0.310 | 0.9500 | 32 |
| scan: 1Chr 28:12 w13 to 1Chr 28:20 w11 | 0.406 | 1.70e-4 | 1 | 0.320 | 0.0204 | 15 |
| scan: 1Chr 28:13 w1 to 1Chr 28:19 w9 | 0.406 | 1.70e-4 | 1 | 0.890 | 0.0444 | 12 |
| scan: 2Chr 4:15 w4 to 2Chr 5:3 w10 | 0.595 | 1.70e-4 | 1 | 0.326 | 0.0065 | 21 |
| scan: 2Chr 4:16 w1 to 2Chr 5:3 w7 | 0.595 | 1.70e-4 | 1 | 0.326 | 0.0065 | 21 |
| scan: 2Chr 7:4 w4 to 2Chr 7:14 w12 | 0.293 | 1.70e-4 | 1 | 0.014 | 0.4301 | 15 |
| scan: Ezra 2:61 w1 to Ezra 3:2 w23 | 0.455 | 1.70e-4 | 1 | 0.200 | 0.2548 | 21 |
| scan: Ps 98:8 w4 to Ps 99:9 w6 | 0.600 | 1.70e-4 | 1 | 0.050 | 0.4259 | 10 |
| scan: Jer 36:18 w11 to Jer 36:27 w5 | 0.475 | 1.70e-4 | 1 | 0.404 | 5.20e-4 | 22 |
| scan: Ezek 3:15 w1 to Ezek 3:24 w14 | 0.518 | 1.70e-4 | 1 | 0.468 | 0.0015 | 11 |
| scan: Zech 8:15 w12 to Zech 9:2 w9 | 0.363 | 1.70e-4 | 1 | 0.320 | 0.0012 | 10 |
| scan: Gen 2:9 w1 to Gen 2:17 w13 | 0.618 | 1.80e-4 | 1 | 0.171 | 0.2241 | 9 |
| scan: Gen 14:4 w7 to Gen 14:15 w6 | 0.674 | 1.80e-4 | 1 | 0.833 | 1.50e-4 | 40 |
| scan: Gen 37:27 w1 to Gen 38:1 w7 | 0.631 | 1.80e-4 | 1 | 0.523 | 0.0025 | 16 |
| scan: Gen 43:11 w17 to Gen 43:22 w12 | 0.415 | 1.80e-4 | 1 | 0.222 | 0.0364 | 21 |
| scan: Gen 49:26 w11 to Gen 50:4 w19 | 0.678 | 1.80e-4 | 1 | 0.616 | 0.0020 | 19 |
| scan: Exod 15:14 w4 to Exod 15:26 w15 | 0.609 | 1.80e-4 | 1 | 0.228 | 0.0723 | 23 |
| scan: Exod 29:34 w9 to Exod 29:46 w12 | 0.545 | 1.80e-4 | 1 | 0.405 | 0.0185 | 30 |
| scan: Exod 37:16 w18 to Exod 37:25 w6 | 0.563 | 1.80e-4 | 0 | - | - | 0 |
| scan: Lev 19:19 w1 to Lev 19:30 w5 | 0.473 | 1.80e-4 | 1 | 0.696 | 0.0076 | 31 |
| scan: Num 33:34 w1 to Num 33:43 w4 | 0.522 | 1.80e-4 | 1 | 0.243 | 0.2639 | 42 |
| scan: Deut 20:2 w1 to Deut 20:11 w6 | 0.523 | 1.80e-4 | 1 | 0.308 | 0.0242 | 12 |
| scan: Josh 15:8 w1 to Josh 15:15 w10 | 0.300 | 1.80e-4 | 1 | 0.057 | 0.2789 | 35 |
| scan: Judg 11:32 w8 to Judg 12:4 w9 | 0.420 | 1.80e-4 | 1 | 0.245 | 0.0058 | 31 |
| scan: Judg 15:10 w7 to Judg 16:2 w12 | 0.442 | 1.80e-4 | 1 | 0.398 | 0.0013 | 16 |
| scan: 1Sam 10:7 w7 to 1Sam 10:16 w10 | 0.602 | 1.80e-4 | 1 | 0.643 | 0.0239 | 7 |
| scan: 2Sam 11:24 w1 to 2Sam 12:9 w18 | 0.384 | 1.80e-4 | 1 | 0.344 | 5.20e-4 | 20 |
| scan: 1Kgs 6:20 w15 to 1Kgs 6:30 w5 | 0.550 | 1.80e-4 | 1 | 0.491 | 0.0022 | 18 |
| scan: 1Kgs 20:33 w1 to 1Kgs 20:39 w34 | 0.530 | 1.80e-4 | 1 | 0.438 | 0.0059 | 11 |
| scan: 1Kgs 22:15 w1 to 1Kgs 22:26 w15 | 0.241 | 1.80e-4 | 1 | 0.167 | 0.0093 | 12 |
| scan: 1Kgs 22:16 w1 to 1Kgs 22:28 w10 | 0.280 | 1.80e-4 | 1 | 0.084 | 0.1468 | 9 |
| scan: 1Chr 10:1 w4 to 1Chr 10:8 w7 | 0.371 | 1.80e-4 | 1 | 0.111 | 0.1815 | 8 |
| scan: 1Chr 12:12 w1 to 1Chr 12:25 w9 | 0.356 | 1.80e-4 | 1 | 0.230 | 0.0529 | 23 |
| scan: 1Chr 15:8 w3 to 1Chr 15:19 w7 | 0.460 | 1.80e-4 | 1 | 0.232 | 0.0234 | 40 |
| scan: 1Chr 28:11 w1 to 1Chr 28:19 w9 | 0.567 | 1.80e-4 | 1 | 0.675 | 0.0034 | 15 |
| scan: 1Chr 28:13 w1 to 1Chr 28:21 w21 | 0.488 | 1.80e-4 | 1 | 0.509 | 0.0187 | 14 |
| scan: Isa 2:9 w5 to Isa 2:21 w13 | 0.643 | 1.80e-4 | 1 | 0.106 | 0.2759 | 19 |
| scan: Isa 45:5 w1 to Isa 45:15 w7 | 0.477 | 1.80e-4 | 1 | 0.321 | 0.0018 | 9 |
| scan: Jer 25:29 w1 to Jer 26:2 w23 | 0.522 | 1.80e-4 | 1 | 0.602 | 0.0031 | 18 |
| scan: Jer 36:19 w1 to Jer 36:26 w23 | 0.447 | 1.80e-4 | 1 | 0.417 | 0.0102 | 22 |
| scan: Jer 51:16 w10 to Jer 51:28 w11 | 0.475 | 1.80e-4 | 1 | 0.201 | 0.0420 | 15 |
| scan: Ezek 1:23 w1 to Ezek 2:3 w24 | 0.600 | 1.80e-4 | 1 | 0.300 | 0.1330 | 7 |
| scan: Ezek 4:14 w1 to Ezek 5:7 w24 | 0.638 | 1.80e-4 | 1 | -0.359 | 0.8062 | 24 |
| scan: Ezek 7:9 w6 to Ezek 7:21 w7 | 0.550 | 1.80e-4 | 1 | 0.568 | 0.1944 | 16 |
| scan: Ezek 43:11 w1 to Ezek 43:18 w19 | 0.583 | 1.80e-4 | 1 | 0.200 | 0.0231 | 25 |
| scan: Ezek 43:11 w24 to Ezek 43:18 w19 | 0.690 | 1.80e-4 | 1 | 0.273 | 0.0194 | 25 |
| scan: Ezek 45:8 w1 to Ezek 45:17 w27 | 0.577 | 1.80e-4 | 1 | 0.642 | 1.20e-4 | 21 |
| scan: Ezek 47:22 w1 to Ezek 48:10 w22 | 0.206 | 1.80e-4 | 1 | 0.181 | 0.0221 | 9 |
| scan: Zech 4:7 w1 to Zech 5:4 w21 | 0.362 | 1.80e-4 | 1 | 0.519 | 4.10e-4 | 15 |
| scan: Zech 12:9 w1 to Zech 13:4 w8 | 0.633 | 1.80e-4 | 1 | 0.516 | 1.20e-4 | 17 |
| scan: Exod 2:22 w7 to Exod 3:8 w17 | 0.453 | 1.90e-4 | 1 | 0.504 | 1.80e-4 | 15 |
| scan: Exod 18:6 w9 to Exod 18:14 w9 | 0.453 | 1.90e-4 | 1 | -0.072 | 0.6858 | 15 |
| scan: Exod 25:29 w9 to Exod 26:1 w16 | 0.718 | 1.90e-4 | 1 | 0.307 | 0.0123 | 44 |
| scan: Exod 33:3 w6 to Exod 33:13 w15 | 0.358 | 1.90e-4 | 1 | 0.233 | 0.0180 | 15 |
| scan: Exod 33:5 w18 to Exod 33:12 w27 | 0.336 | 1.90e-4 | 1 | 0.157 | 0.0592 | 8 |
| scan: Lev 3:15 w11 to Lev 4:9 w17 | 0.423 | 1.90e-4 | 1 | 0.498 | 0.0055 | 24 |
| scan: Lev 4:19 w1 to Lev 4:26 w8 | 0.696 | 1.90e-4 | 1 | 0.111 | 0.2339 | 15 |
| scan: Lev 21:20 w1 to Lev 22:7 w3 | 0.367 | 1.90e-4 | 1 | 0.235 | 0.0286 | 16 |
| scan: Num 5:12 w7 to Num 5:20 w14 | 0.468 | 1.90e-4 | 1 | 0.328 | 0.0170 | 14 |
| scan: Num 34:29 w1 to Num 35:11 w7 | 0.270 | 1.90e-4 | 1 | 0.302 | 7.80e-4 | 22 |
| scan: Deut 5:25 w1 to Deut 5:33 w8 | 0.277 | 1.90e-4 | 1 | 0.429 | 0.0117 | 5 |
| scan: Deut 22:26 w1 to Deut 23:8 w6 | 0.340 | 1.90e-4 | 1 | -0.074 | 0.8000 | 12 |
| scan: Deut 22:26 w9 to Deut 23:7 w13 | 0.373 | 1.90e-4 | 1 | -0.363 | 1.0000 | 12 |
| scan: Deut 28:11 w10 to Deut 28:23 w10 | 0.477 | 1.90e-4 | 1 | 0.055 | 0.3368 | 18 |
| scan: Josh 10:19 w1 to Josh 10:26 w15 | 0.524 | 1.90e-4 | 1 | 0.559 | 0.0030 | 15 |
| scan: Judg 16:28 w1 to Judg 17:8 w9 | 0.533 | 1.90e-4 | 1 | 0.457 | 1.30e-4 | 16 |
| scan: Judg 16:30 w1 to Judg 17:7 w7 | 0.526 | 1.90e-4 | 1 | 0.548 | 0.0024 | 13 |
| scan: 1Sam 8:10 w1 to 1Sam 8:19 w12 | 0.702 | 1.90e-4 | 1 | 0.664 | 2.90e-4 | 10 |
| scan: 1Sam 8:10 w1 to 1Sam 8:21 w9 | 0.591 | 1.90e-4 | 1 | 0.613 | 2.70e-4 | 10 |
| scan: 1Sam 8:10 w7 to 1Sam 8:19 w12 | 0.781 | 1.90e-4 | 1 | 0.746 | 2.20e-4 | 10 |
| scan: 1Sam 20:16 w1 to 1Sam 20:27 w7 | 0.414 | 1.90e-4 | 1 | 0.037 | 0.4160 | 17 |
| scan: 1Sam 20:18 w1 to 1Sam 20:25 w18 | 0.610 | 1.90e-4 | 1 | 0.348 | 0.1246 | 11 |
| scan: 2Sam 7:15 w5 to 2Sam 7:24 w14 | 0.606 | 1.90e-4 | 1 | 0.303 | 0.1485 | 6 |
| scan: 2Sam 14:16 w1 to 2Sam 14:27 w8 | 0.219 | 1.90e-4 | 1 | 0.163 | 0.0175 | 24 |
| scan: 1Kgs 2:35 w1 to 1Kgs 2:46 w10 | 0.349 | 1.90e-4 | 1 | 0.253 | 0.0021 | 17 |
| scan: 1Kgs 6:20 w1 to 1Kgs 6:31 w7 | 0.428 | 1.90e-4 | 1 | 0.479 | 0.0020 | 21 |
| scan: 1Kgs 9:24 w12 to 1Kgs 10:5 w13 | 0.474 | 1.90e-4 | 0 | - | - | 0 |
| scan: 1Kgs 17:23 w11 to 1Kgs 18:11 w3 | 0.365 | 1.90e-4 | 1 | 0.047 | 0.2545 | 18 |
| scan: 2Kgs 4:41 w1 to 2Kgs 5:5 w22 | 0.427 | 1.90e-4 | 1 | 0.249 | 0.0645 | 14 |
| scan: 2Kgs 16:8 w1 to 2Kgs 16:19 w14 | 0.254 | 1.90e-4 | 1 | 0.141 | 0.0143 | 17 |
| scan: 1Chr 6:19 w5 to 1Chr 6:33 w3 | 0.393 | 1.90e-4 | 1 | 0.000 | 1.0000 | 30 |
| scan: 1Chr 18:13 w1 to 1Chr 19:4 w13 | 0.291 | 1.90e-4 | 1 | 0.335 | 0.0245 | 24 |
| scan: 2Chr 5:8 w8 to 2Chr 6:5 w27 | 0.500 | 1.90e-4 | 1 | 0.162 | 0.2114 | 20 |
| scan: 2Chr 7:4 w1 to 2Chr 7:14 w21 | 0.280 | 1.90e-4 | 1 | 0.014 | 0.4301 | 15 |
| scan: 2Chr 11:14 w1 to 2Chr 12:2 w14 | 0.346 | 1.90e-4 | 1 | 0.453 | 2.60e-4 | 21 |
| scan: Isa 2:1 w7 to Isa 2:13 w6 | 0.664 | 1.90e-4 | 1 | 0.575 | 0.0032 | 15 |
| scan: Jer 51:17 w1 to Jer 51:28 w15 | 0.559 | 1.90e-4 | 1 | 0.178 | 0.0225 | 15 |
| scan: Ezek 1:24 w1 to Ezek 2:2 w13 | 0.643 | 1.90e-4 | 1 | 0.480 | 0.0456 | 3 |
| scan: Ezek 41:3 w1 to Ezek 41:15 w18 | 0.181 | 1.90e-4 | 1 | 0.122 | 0.0024 | 38 |
| scan: Ezek 47:13 w1 to Ezek 47:23 w12 | 0.529 | 1.90e-4 | 1 | 0.619 | 4.80e-4 | 22 |
| scan: Amos 7:2 w16 to Amos 7:13 w6 | 0.363 | 1.90e-4 | 1 | 0.141 | 0.1499 | 18 |
| scan: Zech 2:11 w1 to Zech 3:9 w25 | 0.308 | 1.90e-4 | 1 | 0.200 | 0.0495 | 14 |
| scan: Deut 13:14 w5 to Deut 14:6 w13 | 0.544 | 1.90e-4 | 1 | 0.665 | 0.0111 | 25 |
| scan: Gen 40:20 w12 to Gen 41:9 w11 | 0.605 | 2.00e-4 | 1 | 0.548 | 2.30e-4 | 19 |
| scan: Exod 2:8 w1 to Exod 2:15 w19 | 0.582 | 2.00e-4 | 1 | 0.566 | 1.29e-4 | 7 |
| scan: Exod 2:22 w7 to Exod 3:8 w25 | 0.468 | 2.00e-4 | 1 | 0.423 | 9.90e-4 | 15 |
| scan: Exod 19:2 w1 to Exod 19:13 w21 | 0.281 | 2.00e-4 | 1 | 0.365 | 2.80e-4 | 9 |
| scan: Exod 25:28 w9 to Exod 25:39 w9 | 0.515 | 2.00e-4 | 1 | 0.546 | 3.03e-5 | 43 |
| scan: Exod 25:29 w1 to Exod 25:39 w5 | 0.515 | 2.00e-4 | 1 | 0.501 | 2.00e-4 | 40 |
| scan: Exod 29:39 w1 to Exod 30:4 w14 | 0.509 | 2.00e-4 | 1 | 0.176 | 0.1099 | 31 |
| scan: Exod 37:14 w1 to Exod 37:24 w8 | 0.446 | 2.00e-4 | 0 | - | - | 0 |
| scan: Exod 37:16 w1 to Exod 37:26 w16 | 0.596 | 2.00e-4 | 0 | - | - | 0 |
| scan: Lev 21:21 w1 to Lev 22:5 w9 | 0.401 | 2.00e-4 | 1 | 0.334 | 0.0140 | 8 |
| scan: Lev 27:5 w1 to Lev 27:16 w16 | 0.334 | 2.00e-4 | 1 | 0.552 | 1.23e-5 | 8 |
| scan: Num 1:3 w9 to Num 1:18 w12 | 0.560 | 2.00e-4 | 1 | 0.531 | 1.42e-5 | 28 |
| scan: Num 13:1 w1 to Num 13:18 w5 | 0.312 | 2.00e-4 | 1 | 0.257 | 3.50e-4 | 29 |
| scan: Num 35:1 w1 to Num 35:10 w13 | 0.306 | 2.00e-4 | 1 | 0.310 | 1.32e-4 | 19 |
| scan: Deut 4:12 w6 to Deut 4:22 w16 | 0.471 | 2.00e-4 | 1 | 0.311 | 0.0177 | 7 |
| scan: Deut 19:12 w7 to Deut 19:21 w13 | 0.707 | 2.00e-4 | 1 | 0.770 | 0.0351 | 9 |
| scan: Deut 20:1 w15 to Deut 20:13 w4 | 0.457 | 2.00e-4 | 1 | 0.162 | 0.1382 | 13 |
| scan: Deut 33:9 w14 to Deut 33:20 w11 | 0.682 | 2.00e-4 | 1 | 0.737 | 0.0040 | 20 |
| scan: Judg 16:28 w6 to Judg 17:6 w9 | 0.729 | 2.00e-4 | 1 | 0.022 | 0.4499 | 14 |
| scan: Judg 16:28 w6 to Judg 17:7 w7 | 0.727 | 2.00e-4 | 1 | -0.030 | 0.5717 | 15 |
| scan: 2Sam 14:25 w1 to 2Sam 15:3 w7 | 0.282 | 2.00e-4 | 1 | 0.530 | 1.30e-4 | 43 |
| scan: 2Sam 14:25 w10 to 2Sam 15:2 w7 | 0.374 | 2.00e-4 | 1 | 0.593 | 2.52e-5 | 42 |
| scan: 2Sam 17:6 w1 to 2Sam 17:15 w20 | 0.375 | 2.00e-4 | 1 | 0.393 | 0.0374 | 34 |
| scan: 2Sam 23:10 w1 to 2Sam 23:21 w20 | 0.570 | 2.00e-4 | 1 | 0.355 | 0.0018 | 28 |
| scan: 1Kgs 1:47 w21 to 1Kgs 2:6 w2 | 0.368 | 2.00e-4 | 1 | 0.025 | 0.4255 | 16 |
| scan: 1Kgs 6:19 w6 to 1Kgs 6:30 w7 | 0.464 | 2.00e-4 | 1 | 0.494 | 7.70e-4 | 18 |
| scan: 1Kgs 7:3 w11 to 1Kgs 7:12 w9 | 0.820 | 2.00e-4 | 1 | -1.000 | 1.0000 | 28 |
| scan: 1Chr 1:47 w3 to 1Chr 2:4 w12 | 0.742 | 2.00e-4 | 1 | 0.245 | 2.50e-6 | 32 |
| scan: 1Chr 2:47 w3 to 1Chr 3:4 w15 | 0.662 | 2.00e-4 | 1 | 0.259 | 0.0665 | 65 |
| scan: 1Chr 2:48 w1 to 1Chr 3:4 w10 | 0.662 | 2.00e-4 | 1 | 0.251 | 0.0906 | 60 |
| scan: 1Chr 28:12 w13 to 1Chr 28:21 w21 | 0.477 | 2.00e-4 | 1 | -0.002 | 0.5060 | 16 |
| scan: 2Chr 8:12 w6 to 2Chr 9:5 w8 | 0.380 | 2.00e-4 | 1 | 0.167 | 0.0632 | 17 |
| scan: 2Chr 9:8 w1 to 2Chr 9:19 w10 | 0.316 | 2.00e-4 | 1 | 0.342 | 5.06e-5 | 21 |
| scan: Neh 7:64 w7 to Neh 8:3 w23 | 0.473 | 2.00e-4 | 1 | 0.380 | 0.0378 | 19 |
| scan: Job 1:2 w1 to Job 1:11 w8 | 0.511 | 2.00e-4 | 1 | 0.547 | 0.0017 | 14 |
| scan: Song 4:8 w7 to Song 5:3 w5 | 0.472 | 2.00e-4 | 1 | 0.185 | 0.0943 | 24 |
| scan: Jer 17:16 w1 to Jer 17:23 w14 | 0.550 | 2.00e-4 | 1 | 0.415 | 0.0181 | 6 |
| scan: Jer 25:16 w4 to Jer 25:28 w15 | 0.490 | 2.00e-4 | 0 | - | - | 0 |
| scan: Jer 36:18 w11 to Jer 36:27 w18 | 0.392 | 2.00e-4 | 1 | 0.339 | 0.0037 | 22 |
| scan: Jer 48:18 w1 to Jer 48:28 w6 | 0.339 | 2.00e-4 | 1 | 0.000 | 1.0000 | 36 |
| scan: Jer 51:17 w9 to Jer 51:26 w7 | 0.378 | 2.00e-4 | 1 | 0.066 | 0.0183 | 10 |
| scan: Ezek 2:6 w1 to Ezek 3:7 w20 | 0.278 | 2.00e-4 | 1 | 0.326 | 0.0030 | 11 |
| scan: Ezek 40:49 w13 to Ezek 41:12 w21 | 0.196 | 2.00e-4 | 1 | 0.054 | 0.0130 | 34 |
| scan: Ezek 48:19 w3 to Ezek 48:31 w9 | 0.333 | 2.00e-4 | 1 | 0.090 | 0.0947 | 12 |
| scan: Mic 7:1 w9 to Mic 7:12 w16 | 0.805 | 2.00e-4 | 1 | 0.527 | 0.1167 | 28 |
| scan: Mic 7:2 w1 to Mic 7:13 w5 | 0.691 | 2.00e-4 | 1 | 0.636 | 0.0398 | 25 |
| scan: 1Chr 24:5 w1 to 1Chr 24:21 w1 | 0.844 | 2.04e-4 | 1 | 0.455 | 0.0114 | 32 |
| scan: Gen 5:32 w7 to Gen 6:10 w10 | 0.581 | 2.10e-4 | 1 | 0.297 | 0.0056 | 14 |
| scan: Gen 47:4 w1 to Gen 47:13 w15 | 0.411 | 2.10e-4 | 1 | 0.309 | 4.30e-4 | 9 |
| scan: Exod 14:4 w16 to Exod 14:13 w15 | 0.401 | 2.10e-4 | 1 | 0.039 | 0.3343 | 14 |
| scan: Exod 28:13 w1 to Exod 28:22 w9 | 0.649 | 2.10e-4 | 1 | -0.067 | 0.6688 | 35 |
| scan: Exod 30:13 w1 to Exod 30:24 w8 | 0.620 | 2.10e-4 | 1 | 0.432 | 0.0112 | 21 |
| scan: Lev 3:14 w6 to Lev 4:9 w10 | 0.420 | 2.10e-4 | 1 | 0.568 | 4.70e-4 | 28 |
| scan: Lev 3:15 w1 to Lev 4:9 w17 | 0.453 | 2.10e-4 | 1 | 0.498 | 0.0055 | 24 |
| scan: Lev 4:33 w7 to Lev 5:9 w14 | 0.404 | 2.10e-4 | 1 | 0.151 | 0.0171 | 26 |
| scan: Lev 21:14 w1 to Lev 21:24 w10 | 0.501 | 2.10e-4 | 1 | 0.320 | 0.0535 | 13 |
| scan: Lev 26:7 w1 to Lev 26:18 w12 | 0.684 | 2.10e-4 | 1 | 0.603 | 0.0059 | 18 |
| scan: Deut 5:24 w1 to Deut 6:1 w10 | 0.238 | 2.10e-4 | 1 | 0.180 | 0.0395 | 5 |
| scan: Deut 13:14 w1 to Deut 14:6 w11 | 0.502 | 2.10e-4 | 1 | 0.517 | 0.0056 | 25 |
| scan: Deut 21:3 w1 to Deut 21:14 w11 | 0.626 | 2.10e-4 | 1 | 0.346 | 0.1847 | 19 |
| scan: Deut 22:27 w1 to Deut 23:6 w4 | 0.327 | 2.10e-4 | 1 | -0.222 | 1.0000 | 9 |
| scan: Josh 4:20 w10 to Josh 5:3 w12 | 0.567 | 2.10e-4 | 1 | 0.157 | 0.1759 | 14 |
| scan: Josh 11:17 w1 to Josh 12:3 w18 | 0.516 | 2.10e-4 | 1 | 0.595 | 4.40e-6 | 33 |
| scan: Josh 17:4 w1 to Josh 17:14 w6 | 0.259 | 2.10e-4 | 1 | 0.442 | 1.66e-5 | 27 |
| scan: Josh 18:14 w1 to Josh 18:20 w12 | 0.451 | 2.10e-4 | 1 | 0.239 | 0.0141 | 25 |
| scan: Judg 11:39 w1 to Judg 12:11 w11 | 0.427 | 2.10e-4 | 1 | 0.416 | 2.80e-4 | 27 |
| scan: 1Sam 15:32 w1 to 1Sam 16:3 w14 | 0.313 | 2.10e-4 | 1 | 0.051 | 0.3317 | 8 |
| scan: 1Sam 17:9 w1 to 1Sam 17:19 w10 | 0.488 | 2.10e-4 | 0 | - | - | 0 |
| scan: 1Kgs 6:18 w9 to 1Kgs 6:30 w7 | 0.421 | 2.10e-4 | 0 | - | - | 0 |
| scan: 1Kgs 9:1 w1 to 1Kgs 9:10 w16 | 0.335 | 2.10e-4 | 1 | 0.429 | 3.00e-4 | 11 |
| scan: 1Kgs 9:1 w11 to 1Kgs 9:11 w22 | 0.352 | 2.10e-4 | 1 | 0.350 | 6.80e-4 | 15 |
| scan: 1Chr 10:1 w1 to 1Chr 10:8 w7 | 0.415 | 2.10e-4 | 1 | 0.111 | 0.1815 | 8 |
| scan: 1Chr 28:12 w13 to 1Chr 29:1 w22 | 0.425 | 2.10e-4 | 1 | -0.007 | 0.5190 | 16 |
| scan: 2Chr 6:7 w6 to 2Chr 6:19 w8 | 0.327 | 2.10e-4 | 1 | 0.032 | 0.3508 | 8 |
| scan: Neh 7:19 w1 to Neh 7:39 w1 | 0.190 | 2.10e-4 | 1 | 0.109 | 0.1019 | 46 |
| scan: Ezek 20:48 w8 to Ezek 21:7 w32 | 0.764 | 2.10e-4 | 1 | -0.064 | 0.6084 | 24 |
| scan: Ezek 43:12 w1 to Ezek 43:18 w19 | 0.576 | 2.10e-4 | 1 | 0.214 | 0.0549 | 20 |
| scan: Ezek 45:7 w22 to Ezek 45:16 w9 | 0.576 | 2.10e-4 | 1 | 0.261 | 0.1076 | 17 |
| scan: Ezek 48:18 w16 to Ezek 48:32 w9 | 0.305 | 2.10e-4 | 1 | -0.035 | 0.7320 | 13 |
| scan: Dan 4:8 w1 to Dan 4:19 w10 | 0.504 | 2.10e-4 | 1 | 0.473 | 5.30e-4 | 23 |
| scan: Obad 1:9 w1 to Obad 1:19 w18 | 0.757 | 2.10e-4 | 1 | 0.884 | 0.0016 | 29 |
| scan: Obad 1:9 w4 to Obad 1:19 w15 | 0.757 | 2.10e-4 | 1 | 0.884 | 0.0016 | 29 |
| scan: Zech 12:8 w1 to Zech 13:5 w4 | 0.580 | 2.10e-4 | 1 | 0.489 | 3.98e-5 | 18 |
| scan: Zech 12:9 w1 to Zech 13:5 w4 | 0.652 | 2.10e-4 | 1 | 0.089 | 0.3457 | 17 |
| scan: Gen 37:27 w1 to Gen 38:1 w13 | 0.537 | 2.20e-4 | 1 | 0.523 | 0.0025 | 16 |
| scan: Gen 47:4 w1 to Gen 47:14 w14 | 0.416 | 2.20e-4 | 1 | 0.137 | 0.0362 | 10 |
| scan: Exod 25:31 w1 to Exod 26:1 w5 | 0.856 | 2.20e-4 | 1 | 0.436 | 0.0295 | 39 |
| scan: Exod 29:32 w11 to Exod 29:43 w4 | 0.658 | 2.20e-4 | 1 | 0.617 | 3.10e-4 | 32 |
| scan: Exod 37:15 w1 to Exod 37:24 w5 | 0.530 | 2.20e-4 | 0 | - | - | 0 |
| scan: Exod 40:8 w1 to Exod 40:18 w13 | 0.549 | 2.20e-4 | 1 | -0.058 | 0.6528 | 14 |
| scan: Lev 21:19 w8 to Lev 22:7 w3 | 0.362 | 2.20e-4 | 1 | 0.255 | 0.0181 | 17 |
| scan: Lev 22:8 w1 to Lev 22:17 w5 | 0.342 | 2.20e-4 | 1 | 0.330 | 0.0054 | 10 |
| scan: Lev 24:14 w1 to Lev 25:3 w8 | 0.549 | 2.20e-4 | 1 | 0.405 | 0.0032 | 13 |
| scan: Lev 25:17 w8 to Lev 25:25 w5 | 0.521 | 2.20e-4 | 1 | 0.670 | 0.0053 | 12 |
| scan: Num 33:35 w1 to Num 33:42 w4 | 0.614 | 2.20e-4 | 1 | 0.243 | 0.2639 | 34 |
| scan: Deut 28:13 w1 to Deut 28:24 w7 | 0.578 | 2.20e-4 | 1 | 0.417 | 0.0108 | 20 |
| scan: Ruth 3:12 w1 to Ruth 4:1 w19 | 0.619 | 2.20e-4 | 1 | 0.284 | 0.0699 | 13 |
| scan: 1Kgs 17:22 w5 to 1Kgs 18:9 w3 | 0.393 | 2.20e-4 | 1 | 0.085 | 0.1651 | 18 |
| scan: 1Chr 15:8 w1 to 1Chr 15:17 w18 | 0.462 | 2.20e-4 | 1 | 0.356 | 0.0051 | 26 |
| scan: 1Chr 27:29 w1 to 1Chr 28:4 w29 | 0.400 | 2.20e-4 | 1 | -0.203 | 0.8417 | 28 |
| scan: 1Chr 28:12 w1 to 1Chr 28:21 w8 | 0.465 | 2.20e-4 | 1 | 0.206 | 0.0864 | 16 |
| scan: 2Chr 17:4 w7 to 2Chr 17:12 w6 | 0.588 | 2.20e-4 | 1 | 0.406 | 0.0214 | 16 |
| scan: Ps 118:14 w4 to Ps 118:22 w6 | 0.937 | 2.20e-4 | 1 | 0.606 | 0.0223 | 1 |
| scan: Isa 44:27 w1 to Isa 45:9 w17 | 0.543 | 2.20e-4 | 1 | 0.354 | 0.0109 | 8 |
| scan: Jer 25:16 w4 to Jer 25:29 w13 | 0.428 | 2.20e-4 | 0 | - | - | 0 |
| scan: Jer 51:17 w9 to Jer 51:27 w15 | 0.490 | 2.20e-4 | 1 | 0.051 | 0.3245 | 14 |
| scan: Ezek 1:21 w5 to Ezek 2:5 w9 | 0.500 | 2.20e-4 | 1 | 0.153 | 0.2150 | 9 |
| scan: Ezek 41:3 w1 to Ezek 41:15 w14 | 0.194 | 2.20e-4 | 1 | 0.127 | 0.0028 | 38 |
| scan: Dan 2:34 w1 to Dan 2:42 w6 | 0.385 | 2.20e-4 | 1 | 0.609 | 0.0055 | 13 |
| scan: Dan 2:36 w1 to Dan 2:46 w13 | 0.299 | 2.20e-4 | 1 | 0.144 | 0.1048 | 19 |
| scan: Gen 36:43 w1 to Gen 37:11 w7 | 0.472 | 2.30e-4 | 1 | 0.229 | 0.0463 | 19 |
| scan: Gen 43:12 w1 to Gen 43:22 w12 | 0.408 | 2.30e-4 | 1 | 0.318 | 0.0094 | 17 |
| scan: Exod 2:8 w6 to Exod 2:17 w3 | 0.566 | 2.30e-4 | 1 | 0.475 | 2.70e-4 | 9 |
| scan: Exod 12:6 w1 to Exod 12:14 w13 | 0.533 | 2.30e-4 | 1 | 0.460 | 0.0780 | 14 |
| scan: Exod 13:16 w1 to Exod 14:6 w3 | 0.493 | 2.30e-4 | 1 | 0.502 | 1.12e-4 | 22 |
| scan: Exod 18:6 w9 to Exod 18:13 w15 | 0.558 | 2.30e-4 | 1 | 0.252 | 0.0663 | 12 |
| scan: Exod 25:30 w1 to Exod 26:1 w5 | 0.810 | 2.30e-4 | 1 | 0.288 | 0.0726 | 39 |
| scan: Exod 34:13 w1 to Exod 34:25 w6 | 0.549 | 2.30e-4 | 1 | 0.069 | 0.3520 | 20 |
| scan: Exod 37:3 w9 to Exod 37:14 w4 | 0.457 | 2.30e-4 | 0 | - | - | 0 |
| scan: Lev 4:31 w17 to Lev 5:8 w9 | 0.361 | 2.30e-4 | 1 | 0.166 | 0.0056 | 27 |
| scan: Deut 27:24 w5 to Deut 28:9 w8 | 0.577 | 2.30e-4 | 1 | 0.084 | 0.3307 | 2 |
| scan: Josh 6:24 w7 to Josh 7:9 w12 | 0.379 | 2.30e-4 | 1 | 0.023 | 0.4104 | 31 |
| scan: Josh 15:11 w1 to Josh 15:23 w3 | 0.636 | 2.30e-4 | 1 | 0.588 | 1.20e-4 | 37 |
| scan: Judg 16:29 w1 to Judg 17:7 w12 | 0.585 | 2.30e-4 | 1 | 0.557 | 7.70e-4 | 14 |
| scan: Judg 16:29 w13 to Judg 17:7 w7 | 0.617 | 2.30e-4 | 1 | 0.557 | 7.70e-4 | 14 |
| scan: 1Sam 4:21 w1 to 1Sam 5:9 w18 | 0.427 | 2.30e-4 | 1 | 0.296 | 0.0080 | 36 |
| scan: 1Sam 16:11 w14 to 1Sam 16:20 w9 | 0.417 | 2.30e-4 | 1 | 0.229 | 0.0118 | 14 |
| scan: 1Sam 17:4 w9 to 1Sam 17:15 w11 | 0.656 | 2.30e-4 | 0 | - | - | 0 |
| scan: 1Sam 17:5 w1 to 1Sam 17:15 w5 | 0.656 | 2.30e-4 | 0 | - | - | 0 |
| scan: 1Sam 22:21 w1 to 1Sam 23:8 w6 | 0.304 | 2.30e-4 | 1 | 0.258 | 0.0060 | 19 |
| scan: 1Sam 23:21 w6 to 1Sam 23:29 w3 | 0.372 | 2.30e-4 | 1 | 0.043 | 0.3543 | 12 |
| scan: 2Sam 14:27 w1 to 2Sam 15:2 w7 | 0.416 | 2.30e-4 | 1 | 0.141 | 0.1629 | 32 |
| scan: 2Sam 18:2 w19 to 2Sam 18:13 w10 | 0.358 | 2.30e-4 | 1 | 0.138 | 0.0924 | 45 |
| scan: 1Chr 15:8 w1 to 1Chr 15:19 w7 | 0.415 | 2.30e-4 | 1 | 0.336 | 0.0038 | 40 |
| scan: 2Chr 30:1 w17 to 2Chr 30:13 w10 | 0.369 | 2.30e-4 | 1 | 0.124 | 0.1187 | 14 |
| scan: Neh 7:19 w1 to Neh 7:38 w7 | 0.185 | 2.30e-4 | 1 | 0.148 | 0.0488 | 44 |
| scan: Ps 49:9 w1 to Ps 49:19 w9 | 0.705 | 2.30e-4 | 1 | 0.024 | 0.4752 | 15 |
| scan: Eccl 2:25 w1 to Eccl 3:12 w11 | 0.499 | 2.30e-4 | 1 | 0.314 | 6.81e-5 | 11 |
| scan: Eccl 2:25 w1 to Eccl 3:14 w15 | 0.575 | 2.30e-4 | 1 | 0.464 | 4.00e-6 | 11 |
| scan: Jer 51:18 w1 to Jer 51:26 w13 | 0.406 | 2.30e-4 | 1 | 0.123 | 0.0400 | 6 |
| scan: Ezek 2:6 w18 to Ezek 3:7 w11 | 0.312 | 2.30e-4 | 1 | 0.326 | 0.0030 | 11 |
| scan: Ezek 42:10 w1 to Ezek 43:2 w7 | 0.388 | 2.30e-4 | 1 | -0.549 | 1.0000 | 28 |
| scan: Ezek 47:19 w1 to Ezek 48:5 w10 | 0.264 | 2.30e-4 | 1 | 0.142 | 0.0540 | 15 |
| scan: Ezek 47:21 w1 to Ezek 48:9 w4 | 0.231 | 2.30e-4 | 1 | 0.076 | 0.2015 | 10 |
| scan: Dan 2:34 w1 to Dan 2:41 w27 | 0.361 | 2.30e-4 | 1 | 0.711 | 0.0058 | 11 |
| scan: Dan 4:8 w16 to Dan 4:19 w26 | 0.504 | 2.30e-4 | 1 | 0.420 | 0.0049 | 23 |
| scan: Zech 8:16 w5 to Zech 9:3 w4 | 0.355 | 2.30e-4 | 1 | 0.491 | 9.32e-5 | 8 |
| scan: Zech 12:9 w1 to Zech 13:3 w17 | 0.596 | 2.30e-4 | 1 | 0.469 | 0.0044 | 14 |
| scan: Gen 4:5 w1 to Gen 4:16 w9 | 0.297 | 2.40e-4 | 1 | 0.248 | 7.70e-4 | 8 |
| scan: Gen 28:18 w13 to Gen 29:3 w13 | 0.925 | 2.40e-4 | 1 | 0.257 | 0.0971 | 8 |
| scan: Exod 9:33 w11 to Exod 10:5 w25 | 0.695 | 2.40e-4 | 1 | 0.342 | 0.0761 | 8 |
| scan: Exod 18:6 w9 to Exod 18:13 w7 | 0.564 | 2.40e-4 | 1 | 0.708 | 3.50e-4 | 12 |
| scan: Exod 24:12 w10 to Exod 25:3 w5 | 0.382 | 2.40e-4 | 1 | 0.174 | 0.0987 | 5 |
| scan: Exod 28:14 w1 to Exod 28:25 w9 | 0.481 | 2.40e-4 | 0 | - | - | 0 |
| scan: Lev 8:30 w1 to Lev 9:4 w9 | 0.288 | 2.40e-4 | 1 | 0.063 | 0.3172 | 17 |
| scan: Lev 20:19 w1 to Lev 21:3 w10 | 0.445 | 2.40e-4 | 1 | 0.531 | 0.0025 | 18 |
| scan: Num 26:2 w1 to Num 26:11 w4 | 0.686 | 2.40e-4 | 1 | 0.466 | 0.0237 | 20 |
| scan: Num 28:25 w1 to Num 29:1 w17 | 0.699 | 2.40e-4 | 1 | 0.606 | 5.90e-4 | 14 |
| scan: Deut 2:12 w1 to Deut 2:20 w13 | 0.876 | 2.40e-4 | 1 | 0.729 | 0.0112 | 27 |
| scan: Deut 21:20 w1 to Deut 22:8 w7 | 0.494 | 2.40e-4 | 1 | 0.462 | 0.0188 | 17 |
| scan: Deut 27:24 w5 to Deut 28:10 w9 | 0.485 | 2.40e-4 | 1 | 0.509 | 0.0014 | 2 |
| scan: Deut 28:13 w1 to Deut 28:21 w5 | 0.677 | 2.40e-4 | 1 | 0.449 | 0.0133 | 14 |
| scan: Deut 28:13 w1 to Deut 28:22 w9 | 0.585 | 2.40e-4 | 1 | 0.473 | 0.0052 | 18 |
| scan: Josh 10:41 w1 to Josh 11:9 w7 | 0.374 | 2.40e-4 | 1 | -0.001 | 0.5018 | 33 |
| scan: Josh 24:6 w7 to Josh 24:15 w34 | 0.529 | 2.40e-4 | 1 | 0.014 | 0.4574 | 20 |
| scan: 1Sam 4:21 w9 to 1Sam 5:8 w24 | 0.431 | 2.40e-4 | 1 | 0.410 | 0.0022 | 33 |
| scan: 1Kgs 1:47 w21 to 1Kgs 2:5 w36 | 0.366 | 2.40e-4 | 1 | 0.025 | 0.4255 | 15 |
| scan: 2Kgs 14:20 w5 to 2Kgs 15:1 w13 | 0.339 | 2.40e-4 | 1 | 0.278 | 0.0097 | 27 |
| scan: 1Chr 15:9 w1 to 1Chr 15:17 w18 | 0.474 | 2.40e-4 | 1 | 0.344 | 0.0194 | 25 |
| scan: 1Chr 22:9 w14 to 1Chr 23:1 w10 | 0.415 | 2.40e-4 | 1 | 0.332 | 5.30e-4 | 8 |
| scan: 1Chr 27:29 w1 to 1Chr 28:5 w18 | 0.387 | 2.40e-4 | 1 | -0.105 | 0.8105 | 28 |
| scan: 1Chr 28:13 w1 to 1Chr 29:1 w22 | 0.476 | 2.40e-4 | 1 | 0.568 | 0.0045 | 14 |
| scan: 2Chr 6:3 w1 to 2Chr 6:14 w17 | 0.369 | 2.40e-4 | 1 | 0.245 | 0.0036 | 4 |
| scan: 2Chr 12:14 w1 to 2Chr 13:8 w21 | 0.465 | 2.40e-4 | 1 | 0.477 | 0.0106 | 24 |
| scan: 2Chr 20:4 w1 to 2Chr 20:14 w13 | 0.599 | 2.40e-4 | 1 | 0.484 | 0.0053 | 11 |
| scan: Ezra 3:7 w5 to Ezra 4:5 w5 | 0.475 | 2.40e-4 | 1 | 0.490 | 1.69e-5 | 27 |
| scan: Ps 29:1 w7 to Ps 29:11 w9 | 0.286 | 2.40e-4 | 1 | 0.121 | 0.0248 | 11 |
| scan: Jer 51:17 w1 to Jer 51:25 w20 | 0.497 | 2.40e-4 | 1 | 0.095 | 0.1111 | 10 |
| scan: Ezek 3:14 w4 to Ezek 3:23 w15 | 0.597 | 2.40e-4 | 1 | 0.408 | 0.0128 | 11 |
| scan: Ezek 31:12 w1 to Ezek 32:5 w8 | 0.355 | 2.40e-4 | 1 | 0.286 | 0.0115 | 17 |
| scan: Ezek 33:26 w1 to Ezek 34:5 w3 | 0.540 | 2.40e-4 | 0 | - | - | 0 |
| scan: Ezek 45:7 w22 to Ezek 45:18 w12 | 0.515 | 2.40e-4 | 1 | 0.415 | 0.0016 | 23 |
| scan: Ezek 47:18 w18 to Ezek 48:3 w10 | 0.544 | 2.40e-4 | 1 | 0.204 | 0.0349 | 18 |
| scan: Obad 1:7 w12 to Obad 1:19 w15 | 0.547 | 2.40e-4 | 1 | 0.490 | 0.0053 | 30 |
| scan: Jonah 1:11 w1 to Jonah 2:4 w11 | 0.420 | 2.40e-4 | 1 | 0.183 | 0.1954 | 7 |
| scan: Jonah 1:11 w1 to Jonah 2:5 w9 | 0.398 | 2.40e-4 | 1 | 0.224 | 0.1078 | 7 |
| scan: Zech 11:5 w1 to Zech 11:13 w11 | 0.884 | 2.40e-4 | 1 | 0.872 | 0.0833 | 21 |
| scan: Gen 4:5 w7 to Gen 4:17 w8 | 0.289 | 2.50e-4 | 1 | 0.113 | 0.0187 | 9 |
| scan: Gen 30:11 w4 to Gen 30:18 w12 | 0.418 | 2.50e-4 | 1 | 0.000 | 0.5027 | 11 |
| scan: Gen 36:43 w5 to Gen 37:11 w7 | 0.495 | 2.50e-4 | 1 | 0.143 | 0.1299 | 19 |
| scan: Gen 48:5 w14 to Gen 48:14 w21 | 0.594 | 2.50e-4 | 1 | 0.502 | 0.0037 | 9 |
| scan: Gen 49:26 w11 to Gen 50:4 w9 | 0.694 | 2.50e-4 | 1 | 0.616 | 0.0020 | 19 |
| scan: Exod 28:12 w12 to Exod 28:24 w8 | 0.421 | 2.50e-4 | 0 | - | - | 0 |
| scan: Exod 29:34 w9 to Exod 29:45 w7 | 0.565 | 2.50e-4 | 1 | 0.405 | 0.0185 | 30 |
| scan: Exod 33:20 w7 to Exod 34:9 w11 | 0.553 | 2.50e-4 | 1 | 0.474 | 0.0061 | 9 |
| scan: Num 26:2 w1 to Num 26:10 w10 | 0.776 | 2.50e-4 | 1 | 0.837 | 1.16e-5 | 20 |
| scan: Num 28:21 w6 to Num 28:29 w6 | 0.744 | 2.50e-4 | 1 | 0.477 | 0.0155 | 15 |
| scan: Deut 28:65 w1 to Deut 29:6 w7 | 0.515 | 2.50e-4 | 1 | 0.492 | 0.0115 | 9 |
| scan: Josh 15:6 w9 to Josh 15:17 w6 | 0.322 | 2.50e-4 | 1 | 0.018 | 0.4124 | 50 |
| scan: Josh 15:11 w15 to Josh 15:24 w3 | 0.688 | 2.50e-4 | 1 | 0.568 | 1.20e-4 | 38 |
| scan: Judg 6:15 w9 to Judg 6:25 w27 | 0.471 | 2.50e-4 | 1 | 0.227 | 0.0254 | 16 |
| scan: 2Sam 7:16 w1 to 2Sam 7:24 w9 | 0.625 | 2.50e-4 | 1 | 0.434 | 0.0927 | 6 |
| scan: 1Kgs 17:23 w1 to 1Kgs 18:9 w11 | 0.377 | 2.50e-4 | 1 | 0.132 | 0.0756 | 18 |
| scan: 2Kgs 3:26 w8 to 2Kgs 4:10 w12 | 0.419 | 2.50e-4 | 1 | 0.397 | 5.10e-4 | 15 |
| scan: 2Kgs 3:27 w1 to 2Kgs 4:10 w17 | 0.360 | 2.50e-4 | 1 | 0.353 | 0.0029 | 10 |
| scan: 2Kgs 9:11 w14 to 2Kgs 9:19 w19 | 0.363 | 2.50e-4 | 1 | 0.253 | 0.0014 | 28 |
| scan: 1Chr 10:1 w1 to 1Chr 10:7 w19 | 0.426 | 2.50e-4 | 1 | 0.447 | 0.0033 | 6 |
| scan: 1Chr 15:1 w6 to 1Chr 15:12 w18 | 0.565 | 2.50e-4 | 1 | 0.482 | 7.30e-4 | 17 |
| scan: 1Chr 27:23 w1 to 1Chr 27:34 w10 | 0.324 | 2.50e-4 | 1 | -0.468 | 0.9889 | 37 |
| scan: 2Chr 4:14 w4 to 2Chr 5:4 w8 | 0.554 | 2.50e-4 | 1 | 0.279 | 0.0132 | 23 |
| scan: 2Chr 6:3 w1 to 2Chr 6:14 w9 | 0.367 | 2.50e-4 | 1 | 0.250 | 0.0059 | 4 |
| scan: 2Chr 12:13 w6 to 2Chr 13:9 w9 | 0.413 | 2.50e-4 | 1 | 0.253 | 0.0392 | 29 |
| scan: Esth 6:11 w1 to Esth 7:9 w25 | 0.197 | 2.50e-4 | 0 | - | - | 0 |
| scan: Eccl 3:4 w1 to Eccl 3:17 w17 | 0.451 | 2.50e-4 | 1 | 0.474 | 0.0027 | 8 |
| scan: Jer 17:16 w1 to Jer 17:23 w6 | 0.668 | 2.50e-4 | 1 | -0.055 | 0.6250 | 6 |
| scan: Ezek 3:14 w1 to Ezek 3:25 w9 | 0.495 | 2.50e-4 | 1 | 0.449 | 0.0015 | 13 |
| scan: Ezek 5:1 w1 to Ezek 5:12 w10 | 0.478 | 2.50e-4 | 1 | 0.341 | 0.0025 | 20 |
| scan: Ezek 41:1 w4 to Ezek 41:13 w12 | 0.155 | 2.50e-4 | 1 | 0.095 | 0.0015 | 35 |
| scan: Ezek 47:19 w1 to Ezek 48:8 w8 | 0.154 | 2.50e-4 | 1 | 0.006 | 0.4583 | 15 |
| scan: Ezek 47:22 w1 to Ezek 48:13 w19 | 0.209 | 2.50e-4 | 1 | 0.164 | 0.0287 | 11 |
| scan: Zech 12:8 w14 to Zech 13:3 w22 | 0.605 | 2.50e-4 | 1 | 0.456 | 0.0013 | 15 |
| scan: Gen 49:25 w1 to Gen 50:4 w9 | 0.561 | 2.60e-4 | 1 | 0.662 | 4.00e-4 | 20 |
| scan: Exod 19:1 w8 to Exod 19:12 w16 | 0.344 | 2.60e-4 | 1 | 0.247 | 0.0394 | 8 |
| scan: Exod 28:12 w12 to Exod 28:21 w19 | 0.780 | 2.60e-4 | 1 | 0.743 | 0.0181 | 37 |
| scan: Exod 28:13 w1 to Exod 28:25 w9 | 0.428 | 2.60e-4 | 0 | - | - | 0 |
| scan: Exod 30:2 w1 to Exod 30:14 w8 | 0.534 | 2.60e-4 | 1 | 0.754 | 0.0111 | 30 |
| scan: Lev 14:21 w1 to Lev 14:32 w11 | 0.345 | 2.60e-4 | 1 | 0.235 | 0.0025 | 26 |
| scan: Num 8:11 w11 to Num 8:24 w3 | 0.250 | 2.60e-4 | 1 | 0.120 | 0.0376 | 16 |
| scan: Deut 4:13 w1 to Deut 4:21 w5 | 0.519 | 2.60e-4 | 1 | 0.562 | 0.0014 | 6 |
| scan: Deut 9:25 w12 to Deut 10:7 w9 | 0.529 | 2.60e-4 | 1 | 0.368 | 0.0243 | 21 |
| scan: Deut 21:19 w5 to Deut 22:8 w7 | 0.449 | 2.60e-4 | 1 | 0.623 | 5.00e-4 | 18 |
| scan: Judg 11:39 w14 to Judg 12:12 w3 | 0.412 | 2.60e-4 | 1 | 0.383 | 0.0040 | 29 |
| scan: 1Sam 4:20 w1 to 1Sam 5:8 w24 | 0.348 | 2.60e-4 | 1 | 0.210 | 0.0291 | 35 |
| scan: 1Sam 4:21 w1 to 1Sam 5:10 w22 | 0.325 | 2.60e-4 | 1 | 0.170 | 0.0158 | 41 |
| scan: 1Sam 10:9 w12 to 1Sam 10:19 w24 | 0.484 | 2.60e-4 | 1 | 0.233 | 0.0722 | 9 |
| scan: 2Sam 11:24 w10 to 2Sam 12:9 w23 | 0.380 | 2.60e-4 | 1 | 0.244 | 0.0068 | 20 |
| scan: 1Kgs 20:33 w1 to 1Kgs 20:41 w13 | 0.478 | 2.60e-4 | 1 | -0.123 | 0.7659 | 12 |
| scan: 1Chr 15:8 w3 to 1Chr 15:19 w4 | 0.426 | 2.60e-4 | 1 | 0.336 | 0.0038 | 40 |
| scan: 1Chr 28:9 w22 to 1Chr 28:21 w8 | 0.398 | 2.60e-4 | 1 | 0.067 | 0.2545 | 19 |
| scan: 2Chr 6:2 w6 to 2Chr 6:13 w29 | 0.425 | 2.60e-4 | 1 | 0.143 | 0.0684 | 5 |
| scan: Ezra 3:7 w5 to Ezra 4:6 w4 | 0.452 | 2.60e-4 | 1 | 0.217 | 0.0340 | 29 |
| scan: Isa 8:18 w11 to Isa 9:8 w4 | 0.676 | 2.60e-4 | 1 | -0.321 | 0.7940 | 17 |
| scan: Isa 45:1 w1 to Isa 45:9 w8 | 0.666 | 2.60e-4 | 1 | 0.164 | 0.0556 | 7 |
| scan: Ezek 3:15 w1 to Ezek 3:23 w18 | 0.554 | 2.60e-4 | 1 | 0.523 | 0.0053 | 10 |
| scan: Ezek 14:21 w1 to Ezek 16:3 w10 | 0.377 | 2.60e-4 | 1 | 0.351 | 0.0076 | 18 |
| scan: Gen 1:28 w13 to Gen 2:7 w16 | 0.372 | 2.70e-4 | 1 | 0.211 | 0.0032 | 5 |
| scan: Exod 9:12 w1 to Exod 9:21 w7 | 0.469 | 2.70e-4 | 1 | 0.640 | 0.0035 | 7 |
| scan: Exod 15:9 w1 to Exod 15:20 w14 | 0.806 | 2.70e-4 | 1 | 0.527 | 0.0080 | 18 |
| scan: Exod 15:9 w7 to Exod 15:20 w8 | 0.806 | 2.70e-4 | 1 | 0.527 | 0.0080 | 18 |
| scan: Exod 25:29 w9 to Exod 26:1 w5 | 0.584 | 2.70e-4 | 1 | 0.307 | 0.0123 | 44 |
| scan: Exod 29:34 w9 to Exod 29:45 w4 | 0.576 | 2.70e-4 | 1 | 0.427 | 0.0097 | 30 |
| scan: Exod 29:35 w1 to Exod 29:45 w4 | 0.576 | 2.70e-4 | 1 | 0.553 | 0.0032 | 27 |
| scan: Exod 37:13 w6 to Exod 37:24 w5 | 0.489 | 2.70e-4 | 0 | - | - | 0 |
| scan: Lev 13:27 w5 to Lev 13:38 w8 | 0.185 | 2.70e-4 | 1 | 0.054 | 0.2334 | 45 |
| scan: Num 35:1 w1 to Num 35:10 w6 | 0.275 | 2.70e-4 | 1 | 0.310 | 1.32e-4 | 19 |
| scan: Deut 5:23 w10 to Deut 6:1 w10 | 0.257 | 2.70e-4 | 1 | 0.180 | 0.0395 | 6 |
| scan: Deut 28:66 w6 to Deut 29:6 w7 | 0.477 | 2.70e-4 | 1 | -0.054 | 0.5669 | 6 |
| scan: 1Sam 9:20 w1 to 1Sam 10:4 w9 | 0.320 | 2.70e-4 | 1 | 0.370 | 4.81e-5 | 20 |
| scan: 1Sam 20:8 w1 to 1Sam 20:14 w11 | 0.492 | 2.70e-4 | 1 | 0.424 | 0.0595 | 9 |
| scan: 2Sam 3:13 w7 to 2Sam 3:23 w18 | 0.195 | 2.70e-4 | 1 | 0.052 | 0.2972 | 26 |
| scan: 1Kgs 9:23 w11 to 1Kgs 10:5 w18 | 0.416 | 2.70e-4 | 0 | - | - | 0 |
| scan: 1Kgs 9:24 w1 to 1Kgs 10:5 w13 | 0.416 | 2.70e-4 | 0 | - | - | 0 |
| scan: 1Chr 27:27 w1 to 1Chr 28:5 w8 | 0.518 | 2.70e-4 | 1 | 0.000 | 1.0000 | 33 |
| scan: 2Chr 26:8 w5 to 2Chr 26:16 w16 | 0.671 | 2.70e-4 | 1 | 0.539 | 0.0033 | 20 |
| scan: Neh 7:19 w1 to Neh 7:40 w5 | 0.159 | 2.70e-4 | 1 | 0.197 | 0.0234 | 47 |
| scan: Neh 7:65 w1 to Neh 8:2 w17 | 0.586 | 2.70e-4 | 1 | 0.316 | 0.0736 | 16 |
| scan: Isa 2:10 w1 to Isa 2:21 w5 | 0.641 | 2.70e-4 | 1 | 0.297 | 0.0595 | 17 |
| scan: Jer 25:30 w1 to Jer 26:3 w17 | 0.523 | 2.70e-4 | 1 | 0.397 | 0.0076 | 19 |
| scan: Ezek 22:15 w1 to Ezek 22:26 w20 | 0.450 | 2.70e-4 | 1 | 0.181 | 0.0629 | 25 |
| scan: Ezek 47:19 w1 to Ezek 48:7 w10 | 0.175 | 2.70e-4 | 1 | 0.105 | 0.0604 | 15 |
| scan: Dan 8:5 w1 to Dan 8:16 w12 | 0.466 | 2.70e-4 | 1 | 0.215 | 0.0934 | 27 |
| scan: Amos 8:11 w1 to Amos 9:9 w10 | 0.431 | 2.70e-4 | 1 | 0.250 | 0.0393 | 27 |
| scan: Gen 10:31 w1 to Gen 11:10 w10 | 0.527 | 2.80e-4 | 1 | 0.475 | 0.0036 | 11 |
| scan: Gen 25:10 w1 to Gen 25:21 w14 | 0.501 | 2.80e-4 | 1 | 0.148 | 0.1432 | 26 |
| scan: Gen 36:24 w1 to Gen 36:36 w2 | 0.424 | 2.80e-4 | 1 | 0.000 | 1.0000 | 40 |
| scan: Exod 2:8 w1 to Exod 2:17 w3 | 0.475 | 2.80e-4 | 1 | 0.453 | 8.70e-4 | 9 |
| scan: Exod 2:8 w6 to Exod 2:16 w12 | 0.568 | 2.80e-4 | 1 | 0.530 | 2.20e-4 | 9 |
| scan: Exod 29:35 w1 to Exod 29:44 w13 | 0.586 | 2.80e-4 | 1 | 0.534 | 0.0034 | 26 |
| scan: Exod 37:13 w6 to Exod 37:24 w8 | 0.502 | 2.80e-4 | 0 | - | - | 0 |
| scan: Exod 37:16 w18 to Exod 37:24 w8 | 0.580 | 2.80e-4 | 0 | - | - | 0 |
| scan: Num 15:15 w1 to Num 15:26 w8 | 0.551 | 2.80e-4 | 1 | 0.559 | 4.90e-4 | 9 |
| scan: Deut 4:13 w1 to Deut 4:22 w16 | 0.457 | 2.80e-4 | 1 | 0.231 | 0.0282 | 7 |
| scan: Deut 19:13 w1 to Deut 19:21 w13 | 0.686 | 2.80e-4 | 1 | 0.721 | 0.0838 | 7 |
| scan: Josh 6:25 w1 to Josh 7:9 w12 | 0.388 | 2.80e-4 | 1 | 0.010 | 0.4578 | 29 |
| scan: Judg 11:39 w14 to Judg 12:11 w6 | 0.439 | 2.80e-4 | 1 | 0.416 | 2.80e-4 | 27 |
| scan: 1Sam 28:12 w1 to 1Sam 28:22 w18 | 0.396 | 2.80e-4 | 1 | 0.236 | 0.0238 | 9 |
| scan: 2Chr 9:7 w6 to 2Chr 9:19 w10 | 0.302 | 2.80e-4 | 1 | 0.302 | 2.30e-4 | 22 |
| scan: 2Chr 12:12 w9 to 2Chr 13:8 w10 | 0.389 | 2.80e-4 | 1 | 0.305 | 0.0225 | 28 |
| scan: Eccl 2:23 w12 to Eccl 3:12 w11 | 0.502 | 2.80e-4 | 1 | 0.429 | 7.10e-6 | 14 |
| scan: Isa 44:21 w1 to Isa 45:4 w11 | 0.619 | 2.80e-4 | 1 | 0.568 | 1.20e-4 | 17 |
| scan: Isa 45:4 w6 to Isa 45:15 w7 | 0.486 | 2.80e-4 | 1 | 0.299 | 0.0030 | 9 |
| scan: Jer 25:30 w1 to Jer 26:3 w6 | 0.504 | 2.80e-4 | 1 | 0.479 | 0.0039 | 19 |
| scan: Jer 25:31 w14 to Jer 26:2 w23 | 0.762 | 2.80e-4 | 1 | 0.470 | 0.0038 | 14 |
| scan: Jer 31:9 w14 to Jer 31:17 w5 | 0.562 | 2.80e-4 | 1 | 0.494 | 0.0330 | 16 |
| scan: Ezek 3:15 w1 to Ezek 3:24 w6 | 0.580 | 2.80e-4 | 1 | 0.540 | 0.0014 | 11 |
| scan: Ezek 19:11 w1 to Ezek 20:9 w10 | 0.522 | 2.80e-4 | 1 | 0.566 | 8.70e-4 | 11 |
| scan: Ezek 45:7 w1 to Ezek 45:17 w13 | 0.521 | 2.80e-4 | 1 | 0.185 | 0.1203 | 21 |
| scan: Ezek 47:13 w15 to Ezek 47:23 w12 | 0.402 | 2.80e-4 | 1 | 0.619 | 4.80e-4 | 22 |
| scan: Ezek 47:20 w10 to Ezek 48:11 w7 | 0.217 | 2.80e-4 | 1 | 0.199 | 0.0057 | 13 |
| scan: Ezek 47:22 w13 to Ezek 48:13 w11 | 0.169 | 2.80e-4 | 1 | 0.164 | 0.0287 | 11 |
| scan: Ezek 48:19 w1 to Ezek 48:31 w18 | 0.320 | 2.80e-4 | 1 | 0.090 | 0.0947 | 12 |
| scan: Dan 11:33 w5 to Dan 11:41 w13 | 0.781 | 2.80e-4 | 1 | 0.465 | 0.0523 | 19 |
| scan: Amos 7:2 w1 to Amos 7:12 w16 | 0.366 | 2.80e-4 | 1 | 0.131 | 0.1652 | 16 |
| scan: Mic 7:2 w1 to Mic 7:12 w16 | 0.701 | 2.80e-4 | 1 | 0.527 | 0.1167 | 24 |
| scan: Zech 4:9 w1 to Zech 5:4 w21 | 0.365 | 2.80e-4 | 1 | 0.498 | 5.60e-4 | 14 |
| scan: Zech 8:16 w1 to Zech 9:2 w4 | 0.347 | 2.80e-4 | 1 | 0.337 | 5.50e-4 | 8 |
| scan: Gen 49:26 w1 to Gen 50:4 w19 | 0.622 | 2.90e-4 | 1 | 0.616 | 0.0020 | 19 |
| scan: Exod 13:17 w1 to Exod 14:5 w6 | 0.552 | 2.90e-4 | 1 | 0.491 | 3.90e-4 | 21 |
| scan: Exod 28:15 w1 to Exod 28:23 w6 | 0.829 | 2.90e-4 | 0 | - | - | 0 |
| scan: Exod 29:36 w12 to Exod 29:44 w13 | 0.711 | 2.90e-4 | 1 | 0.556 | 0.0119 | 25 |
| scan: Exod 34:14 w1 to Exod 34:25 w6 | 0.576 | 2.90e-4 | 1 | 0.570 | 0.0019 | 16 |
| scan: Lev 6:16 w6 to Lev 6:26 w10 | 0.616 | 2.90e-4 | 1 | 0.375 | 0.0166 | 25 |
| scan: Lev 8:29 w1 to Lev 9:4 w9 | 0.389 | 2.90e-4 | 1 | 0.529 | 1.90e-4 | 19 |
| scan: Deut 4:13 w1 to Deut 4:21 w21 | 0.451 | 2.90e-4 | 1 | 0.562 | 0.0014 | 6 |
| scan: Josh 4:9 w1 to Josh 4:18 w15 | 0.375 | 2.90e-4 | 1 | 0.181 | 0.0757 | 10 |
| scan: Josh 10:41 w1 to Josh 11:8 w22 | 0.416 | 2.90e-4 | 1 | 0.037 | 0.4205 | 32 |
| scan: Judg 16:28 w6 to Judg 17:9 w5 | 0.506 | 2.90e-4 | 1 | 0.341 | 0.0039 | 17 |
| scan: Judg 16:29 w1 to Judg 17:7 w7 | 0.578 | 2.90e-4 | 1 | 0.485 | 1.80e-4 | 14 |
| scan: 1Sam 4:20 w11 to 1Sam 5:9 w21 | 0.406 | 2.90e-4 | 1 | 0.296 | 0.0080 | 38 |
| scan: 2Sam 14:16 w1 to 2Sam 14:26 w21 | 0.209 | 2.90e-4 | 1 | 0.096 | 0.0904 | 22 |
| scan: 1Kgs 6:20 w1 to 1Kgs 6:31 w10 | 0.419 | 2.90e-4 | 1 | 0.479 | 0.0020 | 21 |
| scan: 1Kgs 7:45 w18 to 1Kgs 8:2 w10 | 0.635 | 2.90e-4 | 1 | 0.190 | 0.0581 | 18 |
| scan: 1Chr 15:8 w1 to 1Chr 15:18 w3 | 0.415 | 2.90e-4 | 1 | 0.295 | 0.0095 | 36 |
| scan: 1Chr 27:28 w1 to 1Chr 28:6 w17 | 0.363 | 2.90e-4 | 1 | -0.110 | 0.8214 | 30 |
| scan: 2Chr 4:15 w1 to 2Chr 5:3 w7 | 0.502 | 2.90e-4 | 1 | 0.187 | 0.0577 | 21 |
| scan: Eccl 2:23 w12 to Eccl 3:12 w5 | 0.491 | 2.90e-4 | 1 | 0.407 | 1.60e-6 | 14 |
| scan: Isa 2:11 w8 to Isa 2:20 w17 | 0.708 | 2.90e-4 | 1 | -0.349 | 0.8411 | 12 |
| scan: Isa 34:15 w1 to Isa 35:9 w11 | 0.659 | 2.90e-4 | 1 | 0.488 | 0.0059 | 18 |
| scan: Isa 34:15 w1 to Isa 35:9 w13 | 0.659 | 2.90e-4 | 1 | 0.570 | 8.80e-4 | 18 |
| scan: Jer 1:6 w1 to Jer 1:17 w17 | 0.331 | 2.90e-4 | 1 | 0.138 | 0.0944 | 12 |
| scan: Jer 25:30 w1 to Jer 26:2 w23 | 0.565 | 2.90e-4 | 1 | 0.479 | 0.0039 | 17 |
| scan: Jer 36:18 w11 to Jer 36:28 w5 | 0.362 | 2.90e-4 | 1 | 0.037 | 0.3401 | 23 |
| scan: Lam 2:6 w6 to Lam 2:18 w4 | 0.466 | 2.90e-4 | 1 | 0.058 | 0.2747 | 30 |
| scan: Lam 2:7 w1 to Lam 2:17 w13 | 0.523 | 2.90e-4 | 1 | 0.287 | 0.0170 | 26 |
| scan: Ezek 1:22 w1 to Ezek 2:4 w15 | 0.523 | 2.90e-4 | 1 | -0.118 | 0.6971 | 8 |
| scan: Ezek 3:14 w1 to Ezek 3:25 w12 | 0.431 | 2.90e-4 | 1 | 0.477 | 2.70e-4 | 13 |
| scan: Ezek 11:14 w1 to Ezek 12:1 w5 | 0.463 | 2.90e-4 | 1 | 0.529 | 1.10e-4 | 8 |
| scan: Ezek 19:11 w13 to Ezek 20:8 w27 | 0.537 | 2.90e-4 | 1 | 0.527 | 0.0045 | 10 |
| scan: Ezek 43:9 w8 to Ezek 43:19 w14 | 0.591 | 2.90e-4 | 1 | 0.364 | 0.0149 | 29 |
| scan: Obad 1:8 w1 to Obad 1:18 w21 | 0.517 | 2.90e-4 | 1 | 0.508 | 0.0069 | 24 |
| scan: Gen 25:10 w8 to Gen 25:22 w9 | 0.509 | 3.00e-4 | 1 | 0.179 | 0.0946 | 26 |
| scan: Gen 36:29 w4 to Gen 36:40 w13 | 0.384 | 3.00e-4 | 1 | 0.592 | 7.90e-8 | 43 |
| scan: Gen 37:34 w7 to Gen 38:10 w5 | 0.451 | 3.00e-4 | 1 | 0.253 | 0.0589 | 13 |
| scan: Gen 37:35 w16 to Gen 38:9 w19 | 0.534 | 3.00e-4 | 1 | 0.306 | 0.0325 | 13 |
| scan: Exod 2:7 w1 to Exod 2:16 w12 | 0.438 | 3.00e-4 | 1 | 0.411 | 0.0010 | 11 |
| scan: Lev 4:6 w6 to Lev 4:15 w15 | 0.332 | 3.00e-4 | 1 | 0.188 | 0.1205 | 21 |
| scan: Lev 4:34 w11 to Lev 5:9 w12 | 0.445 | 3.00e-4 | 1 | 0.245 | 0.0032 | 25 |
| scan: Lev 21:14 w1 to Lev 22:2 w14 | 0.481 | 3.00e-4 | 1 | 0.445 | 0.0061 | 13 |
| scan: Num 26:6 w1 to Num 26:13 w6 | 0.675 | 3.00e-4 | 1 | 0.682 | 1.30e-6 | 18 |
| scan: Num 34:27 w1 to Num 35:8 w20 | 0.323 | 3.00e-4 | 1 | 0.256 | 0.0151 | 22 |
| scan: Josh 11:17 w1 to Josh 12:2 w22 | 0.466 | 3.00e-4 | 1 | 0.491 | 5.30e-4 | 26 |
| scan: Josh 18:14 w26 to Josh 18:21 w6 | 0.450 | 3.00e-4 | 1 | 0.260 | 0.0068 | 28 |
| scan: Josh 24:5 w1 to Josh 24:14 w20 | 0.535 | 3.00e-4 | 1 | 0.407 | 0.0167 | 19 |
| scan: Judg 11:19 w1 to Judg 11:29 w10 | 0.373 | 3.00e-4 | 1 | 0.111 | 0.2105 | 30 |
| scan: Judg 11:33 w14 to Judg 12:2 w11 | 0.542 | 3.00e-4 | 1 | 0.508 | 3.99e-5 | 21 |
| scan: 1Sam 28:12 w8 to 1Sam 28:22 w12 | 0.446 | 3.00e-4 | 1 | 0.236 | 0.0238 | 9 |
| scan: 2Sam 18:2 w19 to 2Sam 18:12 w17 | 0.390 | 3.00e-4 | 1 | -0.067 | 0.7088 | 42 |
| scan: 1Kgs 2:33 w8 to 1Kgs 2:45 w3 | 0.324 | 3.00e-4 | 1 | 0.342 | 4.20e-4 | 18 |
| scan: 1Kgs 2:35 w10 to 1Kgs 2:45 w3 | 0.285 | 3.00e-4 | 1 | 0.183 | 0.0222 | 16 |
| scan: 1Kgs 9:1 w1 to 1Kgs 9:12 w10 | 0.315 | 3.00e-4 | 1 | 0.248 | 0.0086 | 16 |
| scan: 2Kgs 9:11 w1 to 2Kgs 9:20 w8 | 0.290 | 3.00e-4 | 1 | 0.211 | 0.0037 | 29 |
| scan: 2Kgs 16:7 w13 to 2Kgs 16:19 w5 | 0.243 | 3.00e-4 | 1 | 0.133 | 0.0085 | 20 |
| scan: 1Chr 1:48 w3 to 1Chr 2:4 w12 | 0.718 | 3.00e-4 | 1 | 0.451 | 8.30e-6 | 28 |
| scan: 1Chr 2:32 w1 to 1Chr 2:43 w6 | 0.744 | 3.00e-4 | 1 | 0.473 | 3.10e-4 | 39 |
| scan: 1Chr 22:11 w6 to 1Chr 22:19 w25 | 0.566 | 3.00e-4 | 1 | 0.344 | 0.0023 | 7 |
| scan: 1Chr 27:25 w1 to 1Chr 27:34 w10 | 0.486 | 3.00e-4 | 1 | 0.000 | 1.0000 | 32 |
| scan: 1Chr 27:28 w9 to 1Chr 28:6 w8 | 0.366 | 3.00e-4 | 1 | -0.110 | 0.8214 | 30 |
| scan: 1Chr 28:11 w1 to 1Chr 29:1 w13 | 0.368 | 3.00e-4 | 1 | 0.224 | 0.0188 | 17 |
| scan: 2Chr 7:2 w1 to 2Chr 7:13 w16 | 0.214 | 3.00e-4 | 1 | 0.131 | 0.0318 | 17 |
| scan: Neh 7:63 w7 to Neh 8:2 w13 | 0.482 | 3.00e-4 | 1 | 0.290 | 0.0482 | 22 |
| scan: Esth 5:13 w1 to Esth 6:10 w24 | 0.127 | 3.00e-4 | 0 | - | - | 0 |
| scan: Jer 3:13 w1 to Jer 3:21 w16 | 0.471 | 3.00e-4 | 1 | 0.178 | 0.1582 | 13 |
| scan: Jer 25:16 w1 to Jer 25:28 w7 | 0.489 | 3.00e-4 | 0 | - | - | 0 |
| scan: Ezek 3:15 w14 to Ezek 3:22 w14 | 0.590 | 3.00e-4 | 1 | 0.308 | 0.1200 | 9 |
| scan: Obad 1:8 w6 to Obad 1:19 w15 | 0.607 | 3.00e-4 | 1 | 0.646 | 1.10e-4 | 29 |
| scan: Mic 7:2 w8 to Mic 7:14 w10 | 0.759 | 3.00e-4 | 1 | 0.680 | 0.0070 | 30 |
| scan: Mic 7:3 w1 to Mic 7:13 w7 | 0.759 | 3.00e-4 | 1 | 0.582 | 0.0401 | 20 |
| scan: Gen 5:32 w1 to Gen 6:9 w9 | 0.521 | 3.10e-4 | 1 | 0.361 | 0.0060 | 12 |
| scan: Gen 37:2 w1 to Gen 37:13 w11 | 0.403 | 3.10e-4 | 1 | 0.226 | 0.0208 | 13 |
| scan: Exod 29:35 w9 to Exod 29:44 w13 | 0.639 | 3.10e-4 | 1 | 0.528 | 0.0056 | 26 |
| scan: Lev 4:33 w1 to Lev 5:7 w22 | 0.421 | 3.10e-4 | 1 | 0.285 | 0.0012 | 19 |
| scan: Lev 4:34 w1 to Lev 5:9 w14 | 0.412 | 3.10e-4 | 1 | 0.245 | 0.0032 | 25 |
| scan: Lev 21:20 w8 to Lev 22:6 w16 | 0.346 | 3.10e-4 | 1 | 0.277 | 0.0178 | 15 |
| scan: Lev 26:7 w1 to Lev 26:18 w6 | 0.665 | 3.10e-4 | 1 | 0.571 | 0.0129 | 18 |
| scan: Num 26:48 w1 to Num 26:58 w17 | 0.558 | 3.10e-4 | 1 | 0.109 | 0.0166 | 31 |
| scan: Deut 5:15 w1 to Deut 5:25 w18 | 0.512 | 3.10e-4 | 1 | 0.174 | 0.0782 | 6 |
| scan: Deut 7:9 w7 to Deut 7:21 w10 | 0.351 | 3.10e-4 | 1 | 0.114 | 0.0615 | 9 |
| scan: Deut 21:20 w12 to Deut 22:6 w21 | 0.523 | 3.10e-4 | 1 | 0.461 | 0.0074 | 13 |
| scan: Deut 28:12 w1 to Deut 28:23 w6 | 0.548 | 3.10e-4 | 1 | 0.570 | 3.60e-4 | 18 |
| scan: Josh 15:12 w1 to Josh 15:23 w3 | 0.712 | 3.10e-4 | 1 | 0.416 | 0.0066 | 31 |
| scan: Josh 24:5 w12 to Josh 24:16 w11 | 0.496 | 3.10e-4 | 1 | -0.074 | 0.7097 | 20 |
| scan: Josh 24:6 w1 to Josh 24:16 w8 | 0.496 | 3.10e-4 | 1 | -0.050 | 0.6444 | 20 |
| scan: 1Sam 4:21 w9 to 1Sam 5:8 w19 | 0.376 | 3.10e-4 | 1 | 0.304 | 0.0046 | 33 |
| scan: 2Sam 20:9 w1 to 2Sam 20:18 w11 | 0.312 | 3.10e-4 | 1 | 0.303 | 0.0539 | 42 |
| scan: 1Kgs 6:21 w1 to 1Kgs 6:30 w5 | 0.488 | 3.10e-4 | 1 | 0.575 | 2.20e-4 | 14 |
| scan: 1Chr 27:24 w1 to 1Chr 27:34 w10 | 0.368 | 3.10e-4 | 1 | -0.289 | 0.9667 | 36 |
| scan: 1Chr 27:27 w5 to 1Chr 28:4 w29 | 0.547 | 3.10e-4 | 1 | 0.000 | 1.0000 | 33 |
| scan: 2Chr 11:16 w13 to 2Chr 12:2 w11 | 0.447 | 3.10e-4 | 1 | 0.461 | 7.20e-4 | 16 |
| scan: Esth 6:7 w5 to Esth 7:5 w17 | 0.240 | 3.10e-4 | 0 | - | - | 0 |
| scan: Jer 25:14 w10 to Jer 25:27 w14 | 0.367 | 3.10e-4 | 0 | - | - | 0 |
| scan: Ezek 41:2 w13 to Ezek 41:15 w14 | 0.169 | 3.10e-4 | 1 | 0.073 | 0.0071 | 41 |
| scan: Ezek 42:14 w1 to Ezek 43:3 w21 | 0.499 | 3.10e-4 | 1 | 0.485 | 0.0014 | 16 |
| scan: Ezek 47:18 w1 to Ezek 48:5 w10 | 0.186 | 3.10e-4 | 1 | 0.125 | 0.0613 | 18 |
| scan: Mic 5:5 w4 to Mic 6:2 w8 | 0.417 | 3.10e-4 | 1 | 0.345 | 0.0165 | 22 |
| scan: Gen 5:31 w11 to Gen 6:9 w13 | 0.527 | 3.20e-4 | 1 | 0.305 | 0.0147 | 13 |
| scan: Gen 15:1 w11 to Gen 15:12 w7 | 0.471 | 3.20e-4 | 1 | 0.353 | 0.0106 | 14 |
| scan: Gen 37:26 w1 to Gen 38:1 w7 | 0.482 | 3.20e-4 | 1 | 0.366 | 0.0378 | 16 |
| scan: Exod 28:29 w1 to Exod 28:36 w10 | 0.525 | 3.20e-4 | 1 | 0.003 | 0.4980 | 29 |
| scan: Exod 37:2 w1 to Exod 37:13 w14 | 0.382 | 3.20e-4 | 1 | 0.145 | 0.1341 | 29 |
| scan: Exod 37:14 w1 to Exod 37:24 w5 | 0.531 | 3.20e-4 | 0 | - | - | 0 |
| scan: Lev 22:9 w1 to Lev 22:16 w7 | 0.357 | 3.20e-4 | 1 | 0.426 | 0.0020 | 8 |
| scan: Num 7:86 w1 to Num 8:8 w14 | 0.640 | 3.20e-4 | 1 | 0.608 | 2.00e-4 | 17 |
| scan: Deut 13:15 w1 to Deut 14:6 w11 | 0.549 | 3.20e-4 | 1 | 0.211 | 0.2000 | 22 |
| scan: Deut 21:20 w12 to Deut 22:7 w8 | 0.482 | 3.20e-4 | 1 | 0.462 | 0.0188 | 15 |
| scan: Deut 21:21 w1 to Deut 22:6 w26 | 0.482 | 3.20e-4 | 1 | 0.429 | 0.0483 | 11 |
| scan: Josh 10:40 w1 to Josh 11:8 w22 | 0.365 | 3.20e-4 | 1 | 0.087 | 0.2698 | 35 |
| scan: Judg 11:39 w14 to Judg 12:11 w11 | 0.442 | 3.20e-4 | 1 | 0.383 | 0.0040 | 27 |
| scan: Judg 16:30 w18 to Judg 17:6 w9 | 0.529 | 3.20e-4 | 1 | 0.549 | 0.0034 | 12 |
| scan: 1Kgs 6:20 w1 to 1Kgs 6:32 w13 | 0.333 | 3.20e-4 | 0 | - | - | 0 |
| scan: 1Kgs 9:1 w1 to 1Kgs 9:10 w10 | 0.351 | 3.20e-4 | 1 | 0.452 | 2.90e-4 | 11 |
| scan: 1Kgs 12:33 w1 to 1Kgs 13:11 w28 | 0.221 | 3.20e-4 | 1 | 0.090 | 0.0890 | 19 |
| scan: 1Kgs 18:13 w1 to 1Kgs 18:19 w23 | 0.627 | 3.20e-4 | 1 | 0.770 | 1.30e-4 | 9 |
| scan: 1Kgs 20:31 w1 to 1Kgs 20:40 w15 | 0.326 | 3.20e-4 | 1 | 0.300 | 0.0011 | 13 |
| scan: 2Kgs 4:1 w21 to 2Kgs 4:8 w13 | 0.674 | 3.20e-4 | 1 | 0.396 | 0.0043 | 7 |
| scan: 2Chr 29:6 w1 to 2Chr 29:17 w17 | 0.570 | 3.20e-4 | 1 | 0.292 | 0.0226 | 32 |
| scan: Esth 6:8 w1 to Esth 7:5 w6 | 0.277 | 3.20e-4 | 0 | - | - | 0 |
| scan: Eccl 9:11 w24 to Eccl 10:5 w9 | 0.497 | 3.20e-4 | 1 | 0.471 | 0.0033 | 17 |
| scan: Jer 6:10 w1 to Jer 6:17 w9 | 0.595 | 3.20e-4 | 1 | 0.849 | 0.0111 | 14 |
| scan: Jer 34:13 w6 to Jer 35:2 w15 | 0.544 | 3.20e-4 | 1 | 0.419 | 0.0048 | 14 |
| scan: Ezek 5:17 w1 to Ezek 6:12 w10 | 0.444 | 3.20e-4 | 1 | 0.423 | 0.0040 | 25 |
| scan: Ezek 13:8 w1 to Ezek 13:18 w20 | 0.504 | 3.20e-4 | 1 | 0.510 | 6.90e-6 | 24 |
| scan: Ezek 46:8 w3 to Ezek 46:20 w12 | 0.494 | 3.20e-4 | 1 | 0.521 | 9.90e-4 | 28 |
| scan: Exod 20:19 w1 to Exod 21:4 w17 | 0.559 | 3.30e-4 | 1 | 0.022 | 0.4776 | 6 |
| scan: Exod 28:5 w9 to Exod 28:15 w8 | 0.472 | 3.30e-4 | 1 | 0.306 | 0.0056 | 37 |
| scan: Exod 33:4 w1 to Exod 33:15 w2 | 0.362 | 3.30e-4 | 1 | 0.241 | 0.0033 | 12 |
| scan: Exod 33:4 w8 to Exod 33:12 w27 | 0.287 | 3.30e-4 | 1 | 0.183 | 0.0102 | 10 |
| scan: Exod 37:14 w5 to Exod 37:24 w5 | 0.433 | 3.30e-4 | 0 | - | - | 0 |
| scan: Exod 39:42 w1 to Exod 40:10 w7 | 0.768 | 3.30e-4 | 1 | 0.598 | 0.0035 | 14 |
| scan: Exod 40:8 w5 to Exod 40:18 w16 | 0.696 | 3.30e-4 | 1 | -0.058 | 0.6528 | 14 |
| scan: Lev 12:2 w11 to Lev 13:6 w13 | 0.374 | 3.30e-4 | 1 | 0.032 | 0.3198 | 25 |
| scan: Lev 21:13 w1 to Lev 22:1 w5 | 0.505 | 3.30e-4 | 1 | 0.381 | 0.0189 | 13 |
| scan: Lev 26:7 w4 to Lev 26:17 w13 | 0.746 | 3.30e-4 | 1 | 0.571 | 0.0129 | 18 |
| scan: Num 26:48 w7 to Num 26:58 w13 | 0.579 | 3.30e-4 | 1 | 0.109 | 0.0166 | 31 |
| scan: Deut 27:26 w1 to Deut 28:10 w9 | 0.494 | 3.30e-4 | 1 | 0.508 | 0.0014 | 2 |
| scan: Deut 34:2 w8 to Deut 34:12 w6 | 0.449 | 3.30e-4 | 1 | 0.178 | 0.0626 | 13 |
| scan: Judg 1:19 w8 to Judg 1:31 w9 | 0.422 | 3.30e-4 | 1 | 0.297 | 2.30e-4 | 41 |
| scan: 1Sam 20:17 w1 to 1Sam 20:28 w11 | 0.380 | 3.30e-4 | 1 | 0.032 | 0.4284 | 17 |
| scan: 1Kgs 2:35 w10 to 1Kgs 2:46 w10 | 0.278 | 3.30e-4 | 1 | 0.287 | 1.80e-4 | 17 |
| scan: 1Kgs 3:16 w1 to 1Kgs 3:24 w9 | 0.447 | 3.30e-4 | 1 | 0.309 | 0.0653 | 6 |
| scan: 1Kgs 13:30 w5 to 1Kgs 14:8 w23 | 0.213 | 3.30e-4 | 0 | - | - | 0 |
| scan: 2Kgs 16:7 w13 to 2Kgs 16:18 w16 | 0.230 | 3.30e-4 | 1 | 0.146 | 0.0103 | 20 |
| scan: 1Chr 16:34 w1 to 1Chr 16:42 w12 | 0.636 | 3.30e-4 | 1 | 0.521 | 0.0066 | 20 |
| scan: 1Chr 27:28 w1 to 1Chr 28:6 w8 | 0.382 | 3.30e-4 | 1 | -0.443 | 0.9896 | 30 |
| scan: Neh 7:65 w9 to Neh 8:4 w19 | 0.694 | 3.30e-4 | 1 | 0.269 | 0.0972 | 28 |
| scan: Ps 28:9 w7 to Ps 29:11 w4 | 0.278 | 3.30e-4 | 1 | 0.222 | 0.0031 | 12 |
| scan: Song 5:2 w5 to Song 5:11 w7 | 0.354 | 3.30e-4 | 1 | 1.000 | 0.5000 | 26 |
| scan: Jer 22:3 w11 to Jer 22:12 w7 | 0.431 | 3.30e-4 | 1 | 0.377 | 0.0569 | 13 |
| scan: Jer 25:20 w9 to Jer 25:31 w18 | 0.447 | 3.30e-4 | 0 | - | - | 6 |
| scan: Ezek 3:5 w1 to Ezek 3:11 w19 | 0.661 | 3.30e-4 | 1 | 0.269 | 0.2327 | 7 |
| scan: Ezek 23:14 w4 to Ezek 23:25 w19 | 0.691 | 3.30e-4 | 1 | 0.878 | 3.34e-5 | 26 |
| scan: Ezek 41:2 w1 to Ezek 41:14 w7 | 0.152 | 3.30e-4 | 1 | 0.116 | 4.00e-4 | 34 |
| scan: Amos 7:1 w11 to Amos 7:13 w6 | 0.346 | 3.30e-4 | 1 | 0.133 | 0.1401 | 21 |
| scan: Gen 2:7 w13 to Gen 2:19 w19 | 0.404 | 3.40e-4 | 1 | 0.015 | 0.4473 | 10 |
| scan: Gen 38:8 w1 to Gen 38:18 w12 | 0.514 | 3.40e-4 | 1 | 0.081 | 0.2639 | 20 |
| scan: Exod 13:16 w1 to Exod 14:5 w6 | 0.530 | 3.40e-4 | 1 | 0.130 | 0.1454 | 21 |
| scan: Exod 20:24 w15 to Exod 21:8 w15 | 0.403 | 3.40e-4 | 1 | 0.575 | 0.0098 | 13 |
| scan: Exod 23:23 w13 to Exod 24:1 w15 | 0.578 | 3.40e-4 | 1 | 0.703 | 0.0014 | 19 |
| scan: Exod 25:29 w9 to Exod 25:39 w5 | 0.492 | 3.40e-4 | 1 | 0.501 | 2.00e-4 | 40 |
| scan: Exod 27:16 w1 to Exod 28:6 w12 | 0.750 | 3.40e-4 | 1 | 0.479 | 0.0051 | 25 |
| scan: Exod 37:2 w6 to Exod 37:13 w14 | 0.405 | 3.40e-4 | 1 | 0.261 | 0.0846 | 29 |
| scan: Deut 5:24 w15 to Deut 6:1 w10 | 0.213 | 3.40e-4 | 1 | 0.180 | 0.0395 | 5 |
| scan: Deut 11:30 w1 to Deut 12:10 w10 | 0.282 | 3.40e-4 | 1 | 0.377 | 0.0013 | 26 |
| scan: Deut 27:25 w8 to Deut 28:9 w16 | 0.517 | 3.40e-4 | 1 | 0.568 | 0.0017 | 2 |
| scan: 1Sam 15:32 w13 to 1Sam 16:4 w9 | 0.324 | 3.40e-4 | 1 | 0.112 | 0.1006 | 8 |
| scan: 2Sam 15:12 w1 to 2Sam 15:20 w19 | 0.380 | 3.40e-4 | 1 | 0.033 | 0.4131 | 27 |
| scan: 2Sam 15:12 w13 to 2Sam 15:20 w12 | 0.380 | 3.40e-4 | 1 | 0.033 | 0.4131 | 27 |
| scan: 2Sam 19:27 w1 to 2Sam 19:37 w22 | 0.226 | 3.40e-4 | 1 | 0.193 | 0.0039 | 19 |
| scan: 1Kgs 18:1 w1 to 1Kgs 18:9 w3 | 0.503 | 3.40e-4 | 1 | 0.051 | 0.3606 | 18 |
| scan: 1Chr 27:28 w1 to 1Chr 28:4 w29 | 0.420 | 3.40e-4 | 1 | -0.053 | 0.6080 | 30 |
| scan: Neh 7:17 w1 to Neh 7:39 w9 | 0.124 | 3.40e-4 | 1 | 0.118 | 0.0664 | 50 |
| scan: Neh 7:19 w1 to Neh 7:41 w6 | 0.145 | 3.40e-4 | 1 | 0.187 | 0.0187 | 49 |
| scan: Isa 44:28 w1 to Isa 45:9 w17 | 0.540 | 3.40e-4 | 1 | 0.354 | 0.0109 | 7 |
| scan: Jer 23:38 w1 to Jer 24:5 w21 | 0.583 | 3.40e-4 | 1 | 0.020 | 0.4583 | 17 |
| scan: Jer 36:17 w1 to Jer 36:27 w18 | 0.332 | 3.40e-4 | 1 | 0.371 | 0.0011 | 22 |
| scan: Jer 51:17 w1 to Jer 51:27 w22 | 0.439 | 3.40e-4 | 1 | 0.051 | 0.3245 | 14 |
| scan: Jer 51:19 w1 to Jer 51:26 w13 | 0.505 | 3.40e-4 | 1 | 0.078 | 0.0287 | 5 |
| scan: Ezek 32:1 w1 to Ezek 32:11 w9 | 0.502 | 3.40e-4 | 1 | 0.488 | 0.0072 | 14 |
| scan: Dan 2:36 w1 to Dan 2:47 w15 | 0.281 | 3.40e-4 | 1 | 0.320 | 5.10e-4 | 20 |
| scan: Dan 2:36 w1 to Dan 2:48 w14 | 0.264 | 3.40e-4 | 1 | 0.322 | 0.0018 | 21 |
| scan: Zech 8:16 w5 to Zech 9:2 w4 | 0.427 | 3.40e-4 | 1 | 0.491 | 9.32e-5 | 8 |
| scan: Exod 10:4 w8 to Exod 10:15 w19 | 0.427 | 3.50e-4 | 1 | 0.310 | 1.30e-4 | 19 |
| scan: Exod 25:17 w1 to Exod 25:25 w10 | 0.558 | 3.50e-4 | 1 | 0.431 | 0.0090 | 22 |
| scan: Lev 4:31 w17 to Lev 5:6 w20 | 0.471 | 3.50e-4 | 1 | 0.078 | 0.2465 | 22 |
| scan: Lev 21:20 w1 to Lev 22:6 w16 | 0.355 | 3.50e-4 | 1 | 0.294 | 0.0156 | 15 |
| scan: Deut 4:13 w11 to Deut 4:23 w11 | 0.454 | 3.50e-4 | 1 | 0.056 | 0.3597 | 9 |
| scan: Deut 9:26 w1 to Deut 10:7 w3 | 0.538 | 3.50e-4 | 1 | 0.358 | 0.0403 | 19 |
| scan: Judg 11:31 w1 to Judg 12:2 w11 | 0.368 | 3.50e-4 | 1 | 0.251 | 0.0303 | 25 |
| scan: Judg 11:32 w1 to Judg 12:1 w21 | 0.485 | 3.50e-4 | 1 | 0.539 | 4.32e-5 | 21 |
| scan: Judg 16:28 w6 to Judg 17:9 w17 | 0.396 | 3.50e-4 | 1 | 0.392 | 4.40e-4 | 17 |
| scan: 1Sam 20:42 w1 to 1Sam 21:11 w9 | 0.239 | 3.50e-4 | 1 | 0.360 | 4.28e-5 | 33 |
| scan: 2Sam 3:13 w7 to 2Sam 3:25 w8 | 0.159 | 3.50e-4 | 1 | 0.048 | 0.2655 | 30 |
| scan: 2Sam 14:25 w1 to 2Sam 15:3 w12 | 0.237 | 3.50e-4 | 1 | 0.388 | 7.00e-4 | 43 |
| scan: 1Kgs 14:20 w1 to 1Kgs 15:1 w7 | 0.287 | 3.50e-4 | 0 | - | - | 0 |
| scan: 2Kgs 3:27 w1 to 2Kgs 4:10 w12 | 0.408 | 3.50e-4 | 1 | 0.353 | 0.0029 | 10 |
| scan: 1Chr 11:2 w1 to 1Chr 11:10 w16 | 0.333 | 3.50e-4 | 1 | 0.528 | 3.20e-4 | 10 |
| scan: 1Chr 12:16 w1 to 1Chr 12:23 w9 | 0.305 | 3.50e-4 | 1 | -0.054 | 0.6835 | 14 |
| scan: 1Chr 19:19 w12 to 1Chr 21:4 w5 | 0.365 | 3.50e-4 | 1 | 0.281 | 0.0242 | 53 |
| scan: 1Chr 22:9 w14 to 1Chr 23:3 w6 | 0.389 | 3.50e-4 | 1 | 0.099 | 0.1687 | 10 |
| scan: 1Chr 24:6 w1 to 1Chr 24:23 w2 | 0.815 | 3.50e-4 | 1 | -0.134 | 0.7363 | 36 |
| scan: 1Chr 24:19 w1 to 1Chr 24:31 w22 | 0.305 | 3.50e-4 | 1 | 0.234 | 2.10e-4 | 29 |
| scan: 2Chr 36:10 w13 to 2Chr 36:21 w17 | 0.436 | 3.50e-4 | 1 | 0.206 | 0.0769 | 15 |
| scan: Eccl 2:23 w1 to Eccl 3:12 w5 | 0.521 | 3.50e-4 | 1 | 0.510 | 8.50e-6 | 14 |
| scan: Song 5:2 w5 to Song 5:11 w3 | 0.300 | 3.50e-4 | 1 | 1.000 | 0.3333 | 26 |
| scan: Jer 25:16 w1 to Jer 25:27 w20 | 0.420 | 3.50e-4 | 0 | - | - | 0 |
| scan: Jer 51:16 w10 to Jer 51:26 w13 | 0.596 | 3.50e-4 | 1 | 0.360 | 0.0012 | 10 |
| scan: Ezek 5:2 w1 to Ezek 5:10 w17 | 0.553 | 3.50e-4 | 1 | 0.289 | 0.0859 | 12 |
| scan: Ezek 33:21 w9 to Ezek 33:33 w1 | 0.405 | 3.50e-4 | 1 | 0.590 | 8.98e-5 | 16 |
| scan: Exod 11:6 w7 to Exod 12:5 w7 | 0.706 | 3.60e-4 | 1 | 0.168 | 0.3491 | 14 |
| scan: Exod 25:31 w1 to Exod 25:40 w7 | 0.859 | 3.60e-4 | 1 | 0.444 | 0.0417 | 36 |
| scan: Exod 26:24 w12 to Exod 26:33 w20 | 0.813 | 3.60e-4 | 1 | -0.041 | 0.6224 | 25 |
| scan: Exod 26:25 w1 to Exod 26:33 w12 | 0.813 | 3.60e-4 | 1 | 0.037 | 0.3922 | 22 |
| scan: Num 2:17 w1 to Num 2:25 w5 | 0.623 | 3.60e-4 | 1 | 0.083 | 0.2960 | 19 |
| scan: Deut 15:1 w1 to Deut 15:9 w28 | 0.438 | 3.60e-4 | 1 | 0.338 | 0.0294 | 12 |
| scan: Deut 27:24 w5 to Deut 28:9 w16 | 0.533 | 3.60e-4 | 1 | 0.574 | 6.10e-4 | 2 |
| scan: Deut 28:63 w18 to Deut 29:2 w7 | 0.517 | 3.60e-4 | 1 | 0.512 | 7.30e-4 | 10 |
| scan: Josh 4:21 w1 to Josh 5:3 w12 | 0.524 | 3.60e-4 | 1 | 0.287 | 0.0710 | 13 |
| scan: Josh 15:9 w1 to Josh 15:21 w10 | 0.565 | 3.60e-4 | 1 | 0.427 | 0.0019 | 42 |
| scan: Judg 11:17 w1 to Judg 11:28 w11 | 0.318 | 3.60e-4 | 1 | 0.247 | 0.0111 | 38 |
| scan: 1Sam 20:17 w1 to 1Sam 20:26 w16 | 0.523 | 3.60e-4 | 1 | 0.380 | 0.0727 | 13 |
| scan: 2Sam 7:19 w13 to 2Sam 7:29 w19 | 0.313 | 3.60e-4 | 1 | 0.119 | 0.0599 | 4 |
| scan: 1Kgs 2:36 w13 to 1Kgs 2:43 w11 | 0.449 | 3.60e-4 | 1 | 0.321 | 0.0155 | 12 |
| scan: 1Kgs 7:4 w4 to 1Kgs 7:17 w11 | 0.467 | 3.60e-4 | 1 | 0.418 | 0.0074 | 45 |
| scan: 1Kgs 7:5 w6 to 1Kgs 7:16 w9 | 0.519 | 3.60e-4 | 1 | 0.641 | 3.10e-4 | 40 |
| scan: 1Kgs 17:17 w10 to 1Kgs 18:2 w8 | 0.393 | 3.60e-4 | 1 | 0.113 | 0.1756 | 6 |
| scan: 2Kgs 14:21 w1 to 2Kgs 15:3 w4 | 0.307 | 3.60e-4 | 1 | 0.270 | 0.0020 | 31 |
| scan: 1Chr 24:18 w1 to 1Chr 25:1 w18 | 0.305 | 3.60e-4 | 1 | 0.075 | 0.0650 | 36 |
| scan: 2Chr 8:11 w1 to 2Chr 9:1 w33 | 0.488 | 3.60e-4 | 1 | 0.587 | 0.0011 | 14 |
| scan: 2Chr 17:4 w1 to 2Chr 17:12 w6 | 0.665 | 3.60e-4 | 1 | 0.406 | 0.0214 | 16 |
| scan: Eccl 2:26 w1 to Eccl 3:13 w9 | 0.537 | 3.60e-4 | 1 | 0.317 | 7.90e-6 | 11 |
| scan: Jer 25:1 w1 to Jer 25:12 w18 | 0.430 | 3.60e-4 | 1 | 0.105 | 0.3029 | 13 |
| scan: Jer 37:2 w7 to Jer 37:14 w16 | 0.354 | 3.60e-4 | 1 | 0.276 | 0.0063 | 8 |
| scan: Ezek 2:7 w1 to Ezek 3:7 w20 | 0.280 | 3.60e-4 | 1 | 0.249 | 0.0360 | 9 |
| scan: Ezek 32:1 w1 to Ezek 32:11 w5 | 0.517 | 3.60e-4 | 1 | 0.488 | 0.0072 | 14 |
| scan: Ezek 43:10 w1 to Ezek 43:18 w19 | 0.592 | 3.60e-4 | 1 | 0.309 | 0.0342 | 26 |
| scan: Ezek 48:20 w1 to Ezek 48:30 w10 | 0.245 | 3.60e-4 | 1 | 0.082 | 0.1206 | 11 |
| scan: Amos 7:2 w1 to Amos 7:13 w13 | 0.344 | 3.60e-4 | 1 | 0.141 | 0.1499 | 18 |
| scan: Gen 3:24 w4 to Gen 4:12 w9 | 0.210 | 3.70e-4 | 1 | 0.164 | 0.0265 | 5 |
| scan: Gen 14:5 w17 to Gen 14:16 w15 | 0.697 | 3.70e-4 | 1 | 0.341 | 0.1028 | 39 |
| scan: Gen 42:27 w1 to Gen 42:35 w16 | 0.378 | 3.70e-4 | 1 | 0.335 | 0.0604 | 11 |
| scan: Exod 13:15 w17 to Exod 14:5 w21 | 0.450 | 3.70e-4 | 1 | 0.174 | 0.0572 | 23 |
| scan: Num 7:88 w1 to Num 8:8 w14 | 0.715 | 3.70e-4 | 1 | 0.400 | 0.0199 | 10 |
| scan: Deut 13:14 w5 to Deut 14:5 w7 | 0.514 | 3.70e-4 | 1 | 0.517 | 0.0056 | 19 |
| scan: Deut 21:4 w1 to Deut 21:13 w22 | 0.639 | 3.70e-4 | 1 | 0.740 | 0.0178 | 16 |
| scan: Josh 6:25 w1 to Josh 7:9 w16 | 0.372 | 3.70e-4 | 1 | 0.328 | 0.0031 | 29 |
| scan: 1Kgs 5:9 w19 to 1Kgs 5:18 w11 | 0.387 | 3.70e-4 | 1 | 0.053 | 0.2828 | 14 |
| scan: 1Kgs 14:21 w1 to 1Kgs 15:2 w4 | 0.310 | 3.70e-4 | 1 | 0.245 | 0.0012 | 24 |
| scan: 1Kgs 17:23 w11 to 1Kgs 18:10 w23 | 0.399 | 3.70e-4 | 1 | 0.120 | 0.0818 | 18 |
| scan: 2Kgs 16:8 w1 to 2Kgs 16:19 w5 | 0.254 | 3.70e-4 | 1 | 0.111 | 0.0329 | 17 |
| scan: 2Chr 11:17 w1 to 2Chr 12:2 w11 | 0.553 | 3.70e-4 | 1 | 0.455 | 0.0293 | 16 |
| scan: Ps 145:7 w5 to Ps 145:16 w3 | 0.749 | 3.70e-4 | 1 | 1.000 | 0.0250 | 10 |
| scan: Ps 145:8 w1 to Ps 145:15 w10 | 0.749 | 3.70e-4 | 1 | 1.000 | 0.0250 | 8 |
| scan: Jer 3:12 w17 to Jer 3:23 w5 | 0.409 | 3.70e-4 | 1 | 0.125 | 0.1200 | 15 |
| scan: Ezek 20:1 w14 to Ezek 20:13 w27 | 0.402 | 3.70e-4 | 1 | 0.578 | 3.01e-5 | 12 |
| scan: Ezek 47:12 w25 to Ezek 47:23 w12 | 0.393 | 3.70e-4 | 1 | 0.517 | 2.60e-4 | 24 |
| scan: Obad 1:9 w4 to Obad 1:18 w21 | 0.768 | 3.70e-4 | 1 | 0.822 | 0.0045 | 24 |
| scan: Gen 2:9 w1 to Gen 2:18 w12 | 0.555 | 3.80e-4 | 1 | 0.257 | 0.0662 | 9 |
| scan: Gen 14:8 w1 to Gen 14:18 w7 | 0.595 | 3.80e-4 | 1 | 0.404 | 7.50e-4 | 27 |
| scan: Gen 37:1 w6 to Gen 37:12 w7 | 0.389 | 3.80e-4 | 1 | 0.202 | 0.0358 | 14 |
| scan: Gen 44:26 w1 to Gen 45:3 w17 | 0.337 | 3.80e-4 | 1 | 0.402 | 1.50e-4 | 9 |
| scan: Exod 8:6 w1 to Exod 8:17 w23 | 0.352 | 3.80e-4 | 1 | 0.196 | 0.0314 | 20 |
| scan: Exod 31:10 w4 to Exod 32:3 w11 | 0.382 | 3.80e-4 | 1 | 0.262 | 0.0410 | 8 |
| scan: Lev 4:33 w7 to Lev 5:7 w22 | 0.477 | 3.80e-4 | 1 | 0.185 | 0.0184 | 19 |
| scan: Lev 21:15 w1 to Lev 21:23 w20 | 0.533 | 3.80e-4 | 1 | 0.235 | 0.1290 | 11 |
| scan: Lev 21:21 w1 to Lev 22:6 w7 | 0.374 | 3.80e-4 | 1 | 0.228 | 0.0514 | 9 |
| scan: Lev 25:25 w1 to Lev 25:36 w10 | 0.321 | 3.80e-4 | 1 | 0.439 | 4.90e-4 | 25 |
| scan: Lev 26:8 w1 to Lev 26:17 w13 | 0.762 | 3.80e-4 | 1 | 0.882 | 2.20e-4 | 18 |
| scan: Num 9:23 w9 to Num 10:10 w20 | 0.436 | 3.80e-4 | 1 | 0.515 | 0.0079 | 28 |
| scan: Num 26:5 w4 to Num 26:14 w3 | 0.474 | 3.80e-4 | 1 | 0.236 | 0.0064 | 21 |
| scan: Num 31:7 w9 to Num 31:18 w8 | 0.485 | 3.80e-4 | 1 | 0.326 | 0.0515 | 19 |
| scan: Num 33:55 w16 to Num 34:8 w5 | 0.351 | 3.80e-4 | 1 | 0.253 | 0.1070 | 18 |
| scan: Deut 23:19 w8 to Deut 24:6 w4 | 0.271 | 3.80e-4 | 1 | 0.204 | 0.1933 | 17 |
| scan: Deut 34:2 w8 to Deut 34:11 w14 | 0.452 | 3.80e-4 | 1 | 0.284 | 0.0377 | 13 |
| scan: Josh 8:25 w1 to Josh 9:1 w16 | 0.258 | 3.80e-4 | 0 | - | - | 19 |
| scan: 1Sam 4:19 w16 to 1Sam 5:9 w18 | 0.323 | 3.80e-4 | 1 | 0.195 | 0.0166 | 41 |
| scan: 1Sam 20:16 w1 to 1Sam 20:26 w16 | 0.450 | 3.80e-4 | 1 | 0.017 | 0.4754 | 14 |
| scan: 1Sam 22:19 w14 to 1Sam 23:8 w6 | 0.286 | 3.80e-4 | 1 | 0.011 | 0.4456 | 23 |
| scan: 2Sam 19:26 w1 to 2Sam 19:37 w9 | 0.195 | 3.80e-4 | 1 | 0.107 | 0.0259 | 23 |
| scan: 1Kgs 6:20 w1 to 1Kgs 6:30 w5 | 0.464 | 3.80e-4 | 1 | 0.494 | 7.70e-4 | 18 |
| scan: 1Kgs 13:31 w18 to 1Kgs 14:8 w23 | 0.192 | 3.80e-4 | 0 | - | - | 0 |
| scan: 2Kgs 3:27 w17 to 2Kgs 4:10 w12 | 0.426 | 3.80e-4 | 1 | 0.353 | 0.0029 | 10 |
| scan: 1Chr 28:10 w1 to 1Chr 29:1 w13 | 0.346 | 3.80e-4 | 1 | 0.085 | 0.2062 | 17 |
| scan: 1Chr 28:12 w1 to 1Chr 28:21 w21 | 0.406 | 3.80e-4 | 1 | 0.411 | 0.0010 | 16 |
| scan: 2Chr 4:3 w15 to 2Chr 4:13 w6 | 0.669 | 3.80e-4 | 1 | 0.485 | 0.0244 | 22 |
| scan: 2Chr 12:15 w1 to 2Chr 13:8 w10 | 0.521 | 3.80e-4 | 1 | 0.465 | 0.0244 | 24 |
| scan: 2Chr 29:7 w1 to 2Chr 29:18 w23 | 0.444 | 3.80e-4 | 1 | 0.522 | 1.30e-4 | 33 |
| scan: Ps 145:7 w1 to Ps 145:16 w7 | 0.701 | 3.80e-4 | 1 | 1.000 | 0.0250 | 10 |
| scan: Isa 10:5 w5 to Isa 10:16 w7 | 0.392 | 3.80e-4 | 1 | 0.522 | 0.0012 | 20 |
| scan: Isa 42:22 w11 to Isa 43:9 w12 | 0.659 | 3.80e-4 | 1 | 0.125 | 0.3318 | 15 |
| scan: Isa 62:7 w5 to Isa 63:7 w10 | 0.584 | 3.80e-4 | 1 | -0.183 | 0.8123 | 19 |
| scan: Jer 1:6 w9 to Jer 1:17 w17 | 0.370 | 3.80e-4 | 1 | 0.162 | 0.0863 | 12 |
| scan: Ezek 37:21 w18 to Ezek 38:1 w5 | 0.539 | 3.80e-4 | 1 | 0.322 | 0.0860 | 9 |
| scan: Dan 2:33 w4 to Dan 2:42 w14 | 0.307 | 3.80e-4 | 1 | 0.339 | 0.0053 | 15 |
| scan: Amos 2:7 w10 to Amos 3:3 w3 | 0.628 | 3.80e-4 | 1 | 0.272 | 0.1830 | 17 |
| scan: Zech 4:8 w1 to Zech 5:5 w4 | 0.331 | 3.80e-4 | 1 | 0.295 | 0.0126 | 14 |
| scan: Gen 14:5 w17 to Gen 14:13 w18 | 0.760 | 3.90e-4 | 1 | 0.803 | 0.0020 | 34 |
| scan: Exod 9:9 w7 to Exod 9:17 w3 | 0.730 | 3.90e-4 | 1 | 0.436 | 0.1250 | 9 |
| scan: Exod 19:2 w8 to Exod 19:14 w6 | 0.218 | 3.90e-4 | 1 | 0.252 | 0.0089 | 9 |
| scan: Exod 26:7 w1 to Exod 26:15 w4 | 0.237 | 3.90e-4 | 1 | -0.144 | 0.8657 | 35 |
| scan: Lev 13:57 w15 to Lev 14:9 w26 | 0.429 | 3.90e-4 | 1 | 0.288 | 0.0421 | 23 |
| scan: Lev 13:58 w1 to Lev 14:9 w26 | 0.429 | 3.90e-4 | 1 | 0.359 | 0.0241 | 20 |
| scan: Lev 21:20 w1 to Lev 22:4 w25 | 0.456 | 3.90e-4 | 1 | 0.269 | 0.0524 | 12 |
| scan: Lev 21:21 w1 to Lev 22:4 w25 | 0.431 | 3.90e-4 | 1 | 0.222 | 0.1124 | 6 |
| scan: Lev 21:23 w1 to Lev 22:10 w5 | 0.374 | 3.90e-4 | 1 | 0.294 | 0.0087 | 13 |
| scan: Deut 12:16 w1 to Deut 12:23 w14 | 0.361 | 3.90e-4 | 1 | 0.226 | 0.0468 | 12 |
| scan: Deut 27:26 w1 to Deut 28:9 w16 | 0.523 | 3.90e-4 | 1 | 0.578 | 0.0014 | 2 |
| scan: Josh 6:25 w1 to Josh 7:8 w11 | 0.388 | 3.90e-4 | 1 | 0.128 | 0.1234 | 28 |
| scan: 1Sam 21:13 w1 to 1Sam 22:9 w19 | 0.317 | 3.90e-4 | 1 | -0.044 | 0.6159 | 28 |
| scan: 2Sam 3:14 w1 to 2Sam 3:23 w6 | 0.213 | 3.90e-4 | 1 | 0.097 | 0.1894 | 23 |
| scan: 2Sam 15:17 w1 to 2Sam 15:23 w20 | 0.457 | 3.90e-4 | 1 | 0.252 | 0.0456 | 18 |
| scan: 1Kgs 1:48 w1 to 1Kgs 2:5 w36 | 0.358 | 3.90e-4 | 1 | 0.179 | 0.1314 | 14 |
| scan: 1Kgs 6:20 w1 to 1Kgs 6:30 w7 | 0.472 | 3.90e-4 | 1 | 0.491 | 0.0022 | 18 |
| scan: 1Kgs 6:25 w1 to 1Kgs 6:34 w14 | 0.523 | 3.90e-4 | 1 | -0.293 | 0.8064 | 14 |
| scan: 1Kgs 6:25 w5 to 1Kgs 6:34 w14 | 0.529 | 3.90e-4 | 1 | -0.293 | 0.8064 | 14 |
| scan: 2Kgs 18:31 w1 to 2Kgs 19:1 w12 | 0.539 | 3.90e-4 | 1 | 0.632 | 0.0013 | 16 |
| scan: 1Chr 6:19 w5 to 1Chr 6:32 w14 | 0.356 | 3.90e-4 | 1 | 0.000 | 1.0000 | 27 |
| scan: 1Chr 9:33 w1 to 1Chr 10:1 w3 | 0.698 | 3.90e-4 | 1 | 0.640 | 0.0186 | 43 |
| scan: 2Chr 9:2 w1 to 2Chr 9:10 w9 | 0.467 | 3.90e-4 | 1 | 0.728 | 1.70e-4 | 11 |
| scan: Ezra 8:34 w4 to Ezra 9:9 w28 | 0.516 | 3.90e-4 | 1 | 0.334 | 0.0369 | 24 |
| scan: Prov 12:14 w1 to Prov 12:25 w7 | 0.879 | 3.90e-4 | 1 | 0.230 | 0.1798 | 13 |
| scan: Isa 2:8 w1 to Isa 2:20 w10 | 0.552 | 3.90e-4 | 1 | 0.347 | 0.0097 | 16 |
| scan: Isa 24:4 w1 to Isa 24:14 w8 | 0.670 | 3.90e-4 | 1 | 0.144 | 0.1759 | 16 |
| scan: Isa 24:4 w7 to Isa 24:14 w4 | 0.694 | 3.90e-4 | 1 | 0.144 | 0.1759 | 16 |
| scan: Jer 12:16 w18 to Jer 13:11 w28 | 0.380 | 3.90e-4 | 1 | 0.271 | 0.0133 | 14 |
| scan: Jer 48:19 w1 to Jer 48:28 w12 | 0.459 | 3.90e-4 | 1 | 0.000 | 1.0000 | 29 |
| scan: Ezek 31:12 w6 to Ezek 32:5 w8 | 0.378 | 3.90e-4 | 1 | 0.210 | 0.0991 | 17 |
| scan: Ezek 40:47 w11 to Ezek 41:8 w5 | 0.194 | 3.90e-4 | 1 | 0.063 | 0.0361 | 34 |
| scan: Ezek 43:9 w8 to Ezek 43:19 w18 | 0.640 | 3.90e-4 | 1 | 0.364 | 0.0149 | 29 |
| scan: Gen 2:17 w1 to Gen 3:3 w13 | 0.345 | 4.00e-4 | 1 | 0.522 | 1.58e-5 | 6 |
| scan: Gen 4:5 w7 to Gen 4:16 w4 | 0.323 | 4.00e-4 | 1 | 0.248 | 7.70e-4 | 8 |
| scan: Exod 3:7 w10 to Exod 3:17 w18 | 0.423 | 4.00e-4 | 1 | 0.139 | 0.1165 | 20 |
| scan: Exod 30:1 w5 to Exod 30:13 w17 | 0.505 | 4.00e-4 | 1 | -1.000 | 1.0000 | 30 |
| scan: Exod 30:2 w1 to Exod 30:13 w10 | 0.505 | 4.00e-4 | 1 | 0.000 | 1.0000 | 29 |
| scan: Exod 33:1 w14 to Exod 33:13 w20 | 0.301 | 4.00e-4 | 1 | 0.253 | 0.0018 | 22 |
| scan: Exod 33:2 w1 to Exod 33:13 w20 | 0.353 | 4.00e-4 | 1 | 0.233 | 0.0180 | 22 |
| scan: Num 1:2 w1 to Num 1:18 w12 | 0.409 | 4.00e-4 | 1 | 0.564 | 2.30e-6 | 29 |
| scan: Num 28:12 w9 to Num 28:20 w11 | 0.609 | 4.00e-4 | 1 | 0.145 | 0.0624 | 25 |
| scan: Num 33:35 w1 to Num 33:43 w2 | 0.566 | 4.00e-4 | 1 | 0.440 | 0.5000 | 38 |
| scan: Judg 1:20 w8 to Judg 1:30 w9 | 0.648 | 4.00e-4 | 1 | 0.371 | 0.0044 | 30 |
| scan: 2Sam 7:19 w1 to 2Sam 7:28 w15 | 0.302 | 4.00e-4 | 1 | 0.150 | 0.0504 | 3 |
| scan: 1Kgs 2:11 w9 to 1Kgs 2:19 w10 | 0.527 | 4.00e-4 | 1 | 0.640 | 5.70e-4 | 12 |
| scan: 1Kgs 17:22 w5 to 1Kgs 18:10 w15 | 0.328 | 4.00e-4 | 1 | 0.134 | 0.0617 | 18 |
| scan: 1Chr 6:25 w1 to 1Chr 6:37 w8 | 0.367 | 4.00e-4 | 1 | 0.000 | 0.5556 | 29 |
| scan: 1Chr 9:33 w8 to 1Chr 10:1 w4 | 0.595 | 4.00e-4 | 1 | 0.296 | 0.0054 | 43 |
| scan: 1Chr 9:34 w1 to 1Chr 10:1 w3 | 0.595 | 4.00e-4 | 1 | 0.296 | 0.0054 | 40 |
| scan: 1Chr 12:13 w1 to 1Chr 12:26 w7 | 0.350 | 4.00e-4 | 1 | 0.200 | 0.0447 | 23 |
| scan: 1Chr 28:12 w1 to 1Chr 29:1 w13 | 0.392 | 4.00e-4 | 1 | -0.007 | 0.5190 | 16 |
| scan: Neh 7:18 w1 to Neh 7:39 w1 | 0.149 | 4.00e-4 | 1 | 0.077 | 0.1839 | 48 |
| scan: Neh 7:63 w7 to Neh 8:1 w24 | 0.416 | 4.00e-4 | 1 | 0.177 | 0.1927 | 20 |
| scan: Isa 45:20 w7 to Isa 46:7 w18 | 0.471 | 4.00e-4 | 1 | -0.215 | 0.8630 | 23 |
| scan: Ezek 3:4 w1 to Ezek 3:12 w11 | 0.544 | 4.00e-4 | 1 | 0.066 | 0.3845 | 9 |
| scan: Ezek 41:4 w1 to Ezek 41:15 w14 | 0.224 | 4.00e-4 | 1 | 0.042 | 0.2061 | 32 |
| scan: Ezek 45:7 w22 to Ezek 45:17 w27 | 0.516 | 4.00e-4 | 1 | 0.287 | 0.0282 | 21 |
| scan: Ezek 48:18 w16 to Ezek 48:31 w9 | 0.399 | 4.00e-4 | 1 | 0.061 | 0.1725 | 12 |
| scan: Zech 12:8 w14 to Zech 13:4 w14 | 0.606 | 4.00e-4 | 1 | 0.510 | 2.64e-5 | 18 |
| scan: Gen 15:1 w1 to Gen 15:12 w7 | 0.417 | 4.10e-4 | 1 | 0.528 | 8.00e-4 | 14 |
| scan: Exod 14:6 w1 to Exod 14:17 w14 | 0.418 | 4.10e-4 | 1 | 0.203 | 0.0284 | 16 |
| scan: Exod 28:13 w1 to Exod 28:22 w7 | 0.696 | 4.10e-4 | 1 | -0.067 | 0.6688 | 35 |
| scan: Exod 30:3 w1 to Exod 30:12 w20 | 0.531 | 4.10e-4 | 1 | 0.000 | 1.0000 | 24 |
| scan: Exod 34:14 w6 to Exod 34:24 w21 | 0.645 | 4.10e-4 | 1 | 0.570 | 0.0019 | 15 |
| scan: Lev 19:17 w1 to Lev 19:27 w9 | 0.425 | 4.10e-4 | 1 | 0.000 | 0.7778 | 30 |
| scan: Lev 24:14 w14 to Lev 24:23 w14 | 0.690 | 4.10e-4 | 1 | 0.555 | 0.0011 | 10 |
| scan: Num 7:88 w1 to Num 8:8 w8 | 0.731 | 4.10e-4 | 1 | 0.688 | 0.0029 | 10 |
| scan: Num 33:34 w3 to Num 33:42 w4 | 0.614 | 4.10e-4 | 1 | 0.000 | 1.0000 | 38 |
| scan: Deut 19:21 w4 to Deut 20:12 w7 | 0.407 | 4.10e-4 | 1 | 0.300 | 0.0118 | 12 |
| scan: Judg 11:18 w1 to Judg 11:28 w11 | 0.358 | 4.10e-4 | 1 | 0.057 | 0.3457 | 34 |
| scan: 1Kgs 2:35 w1 to 1Kgs 2:44 w21 | 0.305 | 4.10e-4 | 1 | 0.218 | 0.0029 | 16 |
| scan: 2Kgs 4:4 w12 to 2Kgs 4:13 w29 | 0.434 | 4.10e-4 | 1 | 0.501 | 0.0018 | 9 |
| scan: 1Chr 1:47 w3 to 1Chr 2:7 w8 | 0.818 | 4.10e-4 | 1 | 0.370 | 0.1111 | 39 |
| scan: 1Chr 1:48 w1 to 1Chr 2:7 w2 | 0.818 | 4.10e-4 | 1 | 0.370 | 0.1111 | 35 |
| scan: 1Chr 15:1 w1 to 1Chr 15:12 w18 | 0.550 | 4.10e-4 | 1 | 0.482 | 7.30e-4 | 17 |
| scan: 1Chr 15:3 w1 to 1Chr 15:14 w9 | 0.469 | 4.10e-4 | 1 | 0.366 | 0.0081 | 18 |
| scan: 1Chr 15:8 w3 to 1Chr 15:20 w8 | 0.415 | 4.10e-4 | 1 | 0.232 | 0.0234 | 48 |
| scan: 1Chr 15:9 w1 to 1Chr 15:19 w4 | 0.469 | 4.10e-4 | 1 | 0.280 | 0.0271 | 39 |
| scan: 1Chr 28:12 w13 to 1Chr 28:19 w9 | 0.478 | 4.10e-4 | 1 | 0.743 | 0.0081 | 14 |
| scan: Neh 6:5 w10 to Neh 6:16 w13 | 0.442 | 4.10e-4 | 1 | 0.271 | 0.0799 | 18 |
| scan: Esth 6:1 w6 to Esth 6:9 w30 | 0.177 | 4.10e-4 | 0 | - | - | 0 |
| scan: Esth 6:7 w5 to Esth 7:3 w13 | 0.243 | 4.10e-4 | 0 | - | - | 0 |
| scan: Jer 36:5 w1 to Jer 36:17 w4 | 0.232 | 4.10e-4 | 1 | 0.269 | 0.0026 | 20 |
| scan: Ezek 1:2 w3 to Ezek 1:14 w3 | 0.485 | 4.10e-4 | 0 | - | - | 0 |
| scan: Ezek 3:13 w1 to Ezek 3:23 w18 | 0.615 | 4.10e-4 | 1 | 0.193 | 0.2142 | 13 |
| scan: Ezek 19:11 w13 to Ezek 20:9 w10 | 0.500 | 4.10e-4 | 1 | 0.566 | 8.70e-4 | 11 |
| scan: Ezek 19:12 w1 to Ezek 20:8 w27 | 0.500 | 4.10e-4 | 1 | 0.401 | 0.0285 | 10 |
| scan: Ezek 46:22 w10 to Ezek 47:10 w12 | 0.399 | 4.10e-4 | 1 | 0.175 | 0.0970 | 30 |
| scan: Ezek 46:23 w1 to Ezek 47:9 w29 | 0.399 | 4.10e-4 | 1 | 0.118 | 0.1908 | 26 |
| scan: Dan 4:7 w7 to Dan 4:19 w10 | 0.416 | 4.10e-4 | 1 | 0.457 | 2.00e-4 | 25 |
| scan: Gen 19:14 w19 to Gen 19:26 w3 | 0.434 | 4.20e-4 | 1 | 0.001 | 0.4970 | 13 |
| scan: Exod 15:15 w1 to Exod 15:26 w27 | 0.468 | 4.20e-4 | 1 | 0.368 | 0.0100 | 21 |
| scan: Exod 20:25 w10 to Exod 21:7 w10 | 0.540 | 4.20e-4 | 1 | 0.575 | 0.0098 | 11 |
| scan: Exod 25:17 w5 to Exod 25:25 w5 | 0.628 | 4.20e-4 | 1 | 0.431 | 0.0090 | 22 |
| scan: Lev 21:12 w1 to Lev 21:23 w20 | 0.421 | 4.20e-4 | 1 | 0.299 | 0.0331 | 13 |
| scan: Num 1:4 w6 to Num 1:18 w12 | 0.591 | 4.20e-4 | 1 | 0.420 | 0.0024 | 26 |
| scan: Num 18:9 w1 to Num 18:17 w13 | 0.392 | 4.20e-4 | 1 | 0.366 | 0.0298 | 20 |
| scan: Num 33:34 w1 to Num 33:43 w2 | 0.548 | 4.20e-4 | 1 | 0.000 | 1.0000 | 42 |
| scan: Deut 7:6 w1 to Deut 7:15 w5 | 0.543 | 4.20e-4 | 1 | 0.283 | 0.0208 | 7 |
| scan: Deut 21:22 w1 to Deut 22:6 w26 | 0.485 | 4.20e-4 | 1 | 0.468 | 0.0300 | 9 |
| scan: Deut 27:26 w11 to Deut 28:9 w16 | 0.554 | 4.20e-4 | 1 | 0.593 | 9.00e-4 | 2 |
| scan: Josh 15:10 w1 to Josh 15:21 w13 | 0.644 | 4.20e-4 | 1 | 0.507 | 5.70e-4 | 36 |
| scan: 2Sam 14:3 w1 to 2Sam 14:10 w11 | 0.427 | 4.20e-4 | 1 | 0.408 | 8.60e-4 | 9 |
| scan: 1Kgs 6:16 w1 to 1Kgs 6:27 w28 | 0.392 | 4.20e-4 | 1 | 0.672 | 0.0102 | 20 |
| scan: 1Kgs 12:28 w7 to 1Kgs 13:6 w29 | 0.270 | 4.20e-4 | 1 | 0.245 | 0.0027 | 26 |
| scan: 1Kgs 22:17 w1 to 1Kgs 22:26 w15 | 0.339 | 4.20e-4 | 1 | 0.093 | 0.2125 | 9 |
| scan: 1Chr 6:1 w1 to 1Chr 6:17 w6 | 0.360 | 4.20e-4 | 1 | 0.112 | 2.56e-5 | 43 |
| scan: 1Chr 27:27 w1 to 1Chr 28:4 w29 | 0.505 | 4.20e-4 | 1 | 0.000 | 1.0000 | 33 |
| scan: Jer 3:13 w1 to Jer 3:22 w12 | 0.440 | 4.20e-4 | 1 | 0.256 | 0.0348 | 13 |
| scan: Ezek 3:5 w11 to Ezek 3:12 w7 | 0.657 | 4.20e-4 | 1 | 0.380 | 0.1223 | 8 |
| scan: Ezek 45:7 w1 to Ezek 45:19 w13 | 0.455 | 4.20e-4 | 1 | 0.371 | 0.0035 | 26 |
| scan: Zech 12:10 w1 to Zech 13:4 w8 | 0.729 | 4.20e-4 | 1 | 0.159 | 0.2907 | 16 |
| scan: Gen 47:4 w18 to Gen 47:14 w14 | 0.442 | 4.30e-4 | 1 | 0.137 | 0.0362 | 10 |
| scan: Exod 35:34 w4 to Exod 36:8 w21 | 0.310 | 4.30e-4 | 1 | 0.111 | 0.2056 | 11 |
| scan: Lev 4:32 w1 to Lev 5:8 w9 | 0.349 | 4.30e-4 | 1 | 0.086 | 0.0935 | 23 |
| scan: Num 7:2 w1 to Num 7:12 w11 | 0.480 | 4.30e-4 | 1 | 0.310 | 0.0082 | 14 |
| scan: Num 28:21 w1 to Num 28:29 w6 | 0.551 | 4.30e-4 | 1 | 0.477 | 0.0155 | 15 |
| scan: Num 33:33 w4 to Num 33:43 w2 | 0.532 | 4.30e-4 | 1 | 0.000 | 0.6667 | 46 |
| scan: Deut 9:17 w8 to Deut 9:25 w11 | 0.500 | 4.30e-4 | 1 | 0.416 | 0.0448 | 9 |
| scan: Deut 9:26 w14 to Deut 10:6 w16 | 0.558 | 4.30e-4 | 1 | 0.129 | 0.3036 | 15 |
| scan: Josh 17:5 w5 to Josh 17:14 w6 | 0.275 | 4.30e-4 | 1 | 0.353 | 6.81e-5 | 26 |
| scan: Judg 1:19 w1 to Judg 1:29 w7 | 0.540 | 4.30e-4 | 1 | 0.291 | 0.0110 | 32 |
| scan: Judg 11:18 w1 to Judg 11:29 w19 | 0.323 | 4.30e-4 | 1 | 0.351 | 0.0017 | 38 |
| scan: 1Sam 4:21 w9 to 1Sam 5:11 w19 | 0.248 | 4.30e-4 | 1 | 0.152 | 0.0128 | 44 |
| scan: 1Sam 14:13 w1 to 1Sam 14:23 w11 | 0.328 | 4.30e-4 | 1 | 0.048 | 0.3451 | 17 |
| scan: 1Sam 20:17 w8 to 1Sam 20:26 w6 | 0.572 | 4.30e-4 | 1 | 0.380 | 0.0727 | 13 |
| scan: 2Sam 17:6 w1 to 2Sam 17:15 w16 | 0.347 | 4.30e-4 | 1 | 0.507 | 0.0230 | 34 |
| scan: 2Sam 18:2 w1 to 2Sam 18:13 w13 | 0.310 | 4.30e-4 | 1 | 0.138 | 0.0924 | 45 |
| scan: 1Kgs 6:19 w1 to 1Kgs 6:30 w7 | 0.434 | 4.30e-4 | 1 | 0.452 | 0.0155 | 18 |
| scan: 1Kgs 6:33 w1 to 1Kgs 7:6 w17 | 0.593 | 4.30e-4 | 0 | - | - | 0 |
| scan: 1Kgs 17:24 w1 to 1Kgs 18:9 w11 | 0.383 | 4.30e-4 | 1 | 0.171 | 0.0659 | 18 |
| scan: 1Chr 28:10 w1 to 1Chr 28:19 w9 | 0.458 | 4.30e-4 | 1 | 0.662 | 0.0027 | 15 |
| scan: 2Chr 11:13 w1 to 2Chr 12:1 w12 | 0.342 | 4.30e-4 | 1 | 0.480 | 7.50e-4 | 21 |
| scan: 2Chr 29:17 w18 to 2Chr 29:29 w2 | 0.373 | 4.30e-4 | 1 | 0.378 | 5.08e-5 | 25 |
| scan: Isa 17:7 w7 to Isa 18:4 w8 | 0.746 | 4.30e-4 | 1 | 0.486 | 0.0037 | 20 |
| scan: Jer 43:7 w9 to Jer 44:1 w18 | 0.558 | 4.30e-4 | 1 | -0.113 | 0.5694 | 16 |
| scan: Jer 51:17 w1 to Jer 51:27 w15 | 0.535 | 4.30e-4 | 1 | 0.051 | 0.3245 | 14 |
| scan: Ezek 41:2 w1 to Ezek 41:13 w12 | 0.165 | 4.30e-4 | 1 | 0.100 | 0.0014 | 33 |
| scan: Zech 8:17 w1 to Zech 9:2 w4 | 0.350 | 4.30e-4 | 1 | 0.470 | 2.40e-4 | 8 |
| scan: Zech 12:6 w22 to Zech 13:4 w14 | 0.504 | 4.30e-4 | 1 | 0.461 | 1.34e-5 | 23 |
| scan: Gen 30:11 w1 to Gen 30:19 w7 | 0.328 | 4.40e-4 | 1 | 0.041 | 0.3480 | 11 |
| scan: Gen 37:1 w1 to Gen 37:12 w2 | 0.405 | 4.40e-4 | 1 | 0.178 | 0.0720 | 14 |
| scan: Exod 2:9 w1 to Exod 2:16 w4 | 0.576 | 4.40e-4 | 1 | 0.550 | 5.80e-4 | 9 |
| scan: Exod 25:28 w9 to Exod 25:39 w5 | 0.426 | 4.40e-4 | 1 | 0.439 | 6.34e-5 | 43 |
| scan: Exod 33:4 w1 to Exod 33:13 w20 | 0.332 | 4.40e-4 | 1 | 0.167 | 0.0385 | 11 |
| scan: Exod 40:8 w1 to Exod 40:19 w11 | 0.583 | 4.40e-4 | 1 | -0.051 | 0.6389 | 15 |
| scan: Lev 4:33 w7 to Lev 5:8 w9 | 0.414 | 4.40e-4 | 1 | 0.211 | 0.0034 | 23 |
| scan: Num 33:34 w3 to Num 33:42 w2 | 0.646 | 4.40e-4 | 1 | 0.000 | 1.0000 | 38 |
| scan: Deut 33:8 w7 to Deut 33:20 w5 | 0.673 | 4.40e-4 | 1 | 0.615 | 0.0090 | 20 |
| scan: Deut 33:9 w1 to Deut 33:20 w11 | 0.645 | 4.40e-4 | 1 | 0.737 | 0.0040 | 20 |
| scan: Judg 11:18 w18 to Judg 11:28 w5 | 0.370 | 4.40e-4 | 1 | 0.057 | 0.3457 | 34 |
| scan: 2Sam 14:15 w14 to 2Sam 14:27 w8 | 0.183 | 4.40e-4 | 1 | 0.054 | 0.1789 | 25 |
| scan: 2Sam 17:26 w1 to 2Sam 18:9 w5 | 0.298 | 4.40e-4 | 1 | 0.178 | 0.0106 | 54 |
| scan: 2Kgs 1:6 w1 to 2Kgs 1:17 w16 | 0.288 | 4.40e-4 | 1 | 0.239 | 3.70e-4 | 10 |
| scan: 2Kgs 18:31 w1 to 2Kgs 18:37 w22 | 0.511 | 4.40e-4 | 1 | 0.758 | 0.0087 | 16 |
| scan: 1Chr 27:22 w1 to 1Chr 27:33 w7 | 0.326 | 4.40e-4 | 1 | 0.504 | 0.0297 | 36 |
| scan: 1Chr 28:11 w1 to 1Chr 29:1 w22 | 0.355 | 4.40e-4 | 1 | -0.106 | 0.8258 | 17 |
| scan: 2Chr 2:14 w1 to 2Chr 3:7 w12 | 0.629 | 4.40e-4 | 1 | 0.665 | 0.0014 | 37 |
| scan: Esth 6:7 w5 to Esth 7:3 w19 | 0.224 | 4.40e-4 | 0 | - | - | 0 |
| scan: Isa 2:9 w5 to Isa 2:20 w17 | 0.609 | 4.40e-4 | 1 | 0.343 | 0.0155 | 16 |
| scan: Isa 2:10 w1 to Isa 2:20 w10 | 0.609 | 4.40e-4 | 1 | 0.422 | 0.0073 | 14 |
| scan: Isa 19:2 w1 to Isa 19:13 w11 | 0.711 | 4.40e-4 | 1 | 0.663 | 0.0073 | 30 |
| scan: Jer 25:20 w1 to Jer 25:32 w10 | 0.402 | 4.40e-4 | 0 | - | - | 7 |
| scan: Jer 42:11 w10 to Jer 42:21 w12 | 0.303 | 4.40e-4 | 1 | 0.051 | 0.3528 | 9 |
| scan: Ezek 3:14 w4 to Ezek 3:25 w9 | 0.440 | 4.40e-4 | 1 | 0.477 | 2.70e-4 | 13 |
| scan: Ezek 42:11 w11 to Ezek 43:3 w18 | 0.402 | 4.40e-4 | 1 | 0.034 | 0.3968 | 26 |
| scan: Ezek 43:11 w24 to Ezek 43:19 w18 | 0.583 | 4.40e-4 | 1 | 0.273 | 0.0194 | 26 |
| scan: Zech 4:3 w1 to Zech 4:12 w16 | 0.497 | 4.40e-4 | 1 | 0.506 | 8.90e-4 | 10 |
| scan: Gen 17:26 w6 to Gen 18:8 w9 | 0.734 | 4.50e-4 | 1 | 0.716 | 0.0108 | 16 |
| scan: Gen 30:8 w10 to Gen 30:21 w7 | 0.257 | 4.50e-4 | 1 | 0.040 | 0.2606 | 16 |
| scan: Gen 49:26 w11 to Gen 50:3 w14 | 0.684 | 4.50e-4 | 1 | 0.696 | 0.0013 | 19 |
| scan: Exod 28:14 w1 to Exod 28:24 w8 | 0.489 | 4.50e-4 | 0 | - | - | 0 |
| scan: Exod 37:16 w1 to Exod 37:24 w5 | 0.519 | 4.50e-4 | 0 | - | - | 0 |
| scan: Exod 39:16 w8 to Exod 39:26 w14 | 0.375 | 4.50e-4 | 1 | 0.035 | 0.3639 | 52 |
| scan: Lev 4:5 w6 to Lev 4:15 w15 | 0.304 | 4.50e-4 | 1 | 0.144 | 0.1476 | 21 |
| scan: Deut 19:12 w7 to Deut 20:1 w14 | 0.559 | 4.50e-4 | 1 | 0.685 | 0.0213 | 9 |
| scan: Deut 20:1 w15 to Deut 20:12 w7 | 0.456 | 4.50e-4 | 1 | 0.310 | 0.0053 | 12 |
| scan: Deut 27:26 w11 to Deut 28:10 w11 | 0.502 | 4.50e-4 | 1 | 0.508 | 0.0019 | 2 |
| scan: Deut 28:63 w18 to Deut 29:7 w4 | 0.372 | 4.50e-4 | 1 | 0.192 | 0.0942 | 16 |
| scan: Judg 16:27 w9 to Judg 17:8 w17 | 0.446 | 4.50e-4 | 1 | 0.497 | 1.11e-5 | 17 |
| scan: 2Sam 3:14 w10 to 2Sam 3:24 w7 | 0.189 | 4.50e-4 | 1 | 0.099 | 0.1110 | 25 |
| scan: 2Sam 19:27 w1 to 2Sam 19:36 w7 | 0.276 | 4.50e-4 | 1 | 0.074 | 0.1152 | 17 |
| scan: 1Chr 1:48 w1 to 1Chr 2:4 w8 | 0.738 | 4.50e-4 | 1 | 0.245 | 2.50e-6 | 28 |
| scan: Ezra 2:61 w1 to Ezra 2:70 w9 | 0.588 | 4.50e-4 | 1 | 0.793 | 0.2222 | 20 |
| scan: Esth 6:10 w19 to Esth 7:8 w30 | 0.200 | 4.50e-4 | 0 | - | - | 0 |
| scan: Eccl 2:22 w9 to Eccl 3:12 w5 | 0.474 | 4.50e-4 | 1 | 0.498 | 5.80e-6 | 15 |
| scan: Eccl 9:11 w24 to Eccl 10:4 w13 | 0.479 | 4.50e-4 | 1 | 0.205 | 0.1083 | 17 |
| scan: Isa 37:35 w1 to Isa 38:8 w13 | 0.562 | 4.50e-4 | 1 | 0.256 | 0.0937 | 16 |
| scan: Isa 45:4 w6 to Isa 45:14 w29 | 0.547 | 4.50e-4 | 1 | 0.130 | 0.1587 | 8 |
| scan: Isa 53:12 w17 to Isa 54:12 w6 | 0.367 | 4.50e-4 | 1 | 0.091 | 0.3856 | 18 |
| scan: Isa 54:1 w1 to Isa 54:11 w11 | 0.367 | 4.50e-4 | 1 | 0.091 | 0.3856 | 15 |
| scan: Ezek 3:4 w3 to Ezek 3:12 w7 | 0.568 | 4.50e-4 | 1 | 0.066 | 0.3845 | 9 |
| scan: Ezek 48:20 w1 to Ezek 48:31 w18 | 0.247 | 4.50e-4 | 1 | 0.002 | 0.4858 | 12 |
| scan: Amos 5:15 w8 to Amos 5:27 w9 | 0.635 | 4.50e-4 | 1 | 0.136 | 0.3051 | 11 |
| scan: Mic 7:2 w1 to Mic 7:13 w7 | 0.655 | 4.50e-4 | 1 | 0.584 | 0.0112 | 25 |
| scan: Mic 7:3 w1 to Mic 7:14 w10 | 0.821 | 4.50e-4 | 1 | 0.651 | 0.0192 | 25 |
| scan: Gen 47:10 w5 to Gen 47:22 w5 | 0.281 | 4.60e-4 | 1 | 0.145 | 0.0057 | 17 |
| scan: Exod 30:12 w15 to Exod 30:25 w9 | 0.520 | 4.60e-4 | 1 | 0.403 | 0.0071 | 25 |
| scan: Num 23:11 w8 to Num 23:20 w6 | 0.467 | 4.60e-4 | 1 | 0.155 | 0.1399 | 16 |
| scan: Num 26:48 w7 to Num 26:61 w3 | 0.557 | 4.60e-4 | 1 | 0.090 | 0.0854 | 36 |
| scan: Deut 21:20 w1 to Deut 22:7 w8 | 0.495 | 4.60e-4 | 1 | 0.462 | 0.0188 | 15 |
| scan: Judg 11:17 w22 to Judg 11:29 w10 | 0.338 | 4.60e-4 | 1 | 0.118 | 0.1256 | 42 |
| scan: 1Sam 4:21 w1 to 1Sam 5:9 w21 | 0.344 | 4.60e-4 | 1 | 0.296 | 0.0080 | 36 |
| scan: 1Sam 8:9 w1 to 1Sam 8:19 w5 | 0.804 | 4.60e-4 | 1 | 0.357 | 0.0534 | 10 |
| scan: 1Sam 8:9 w4 to 1Sam 8:21 w6 | 0.523 | 4.60e-4 | 1 | 0.628 | 5.14e-5 | 10 |
| scan: 1Sam 31:1 w1 to 1Sam 31:8 w16 | 0.358 | 4.60e-4 | 1 | 0.085 | 0.2530 | 11 |
| scan: 1Kgs 6:21 w8 to 1Kgs 6:31 w10 | 0.443 | 4.60e-4 | 1 | 0.484 | 0.0014 | 17 |
| scan: 1Kgs 12:33 w17 to 1Kgs 13:12 w7 | 0.219 | 4.60e-4 | 1 | 0.086 | 0.1378 | 19 |
| scan: 1Chr 1:49 w1 to 1Chr 2:4 w8 | 0.704 | 4.60e-4 | 1 | 0.451 | 8.30e-6 | 25 |
| scan: 1Chr 5:14 w1 to 1Chr 5:24 w19 | 0.657 | 4.60e-4 | 1 | 0.673 | 9.10e-4 | 34 |
| scan: 1Chr 15:3 w8 to 1Chr 15:14 w9 | 0.462 | 4.60e-4 | 1 | 0.366 | 0.0081 | 18 |
| scan: 2Chr 2:13 w1 to 2Chr 3:7 w12 | 0.642 | 4.60e-4 | 1 | 0.665 | 0.0109 | 38 |
| scan: 2Chr 8:13 w1 to 2Chr 9:6 w15 | 0.316 | 4.60e-4 | 1 | 0.132 | 0.1090 | 17 |
| scan: 2Chr 12:13 w1 to 2Chr 13:7 w19 | 0.402 | 4.60e-4 | 1 | 0.521 | 0.0026 | 25 |
| scan: 2Chr 22:2 w1 to 2Chr 22:9 w29 | 0.476 | 4.60e-4 | 1 | 0.551 | 0.0016 | 31 |
| scan: Prov 8:10 w1 to Prov 8:21 w5 | 0.879 | 4.60e-4 | 1 | -0.123 | 0.6394 | 3 |
| scan: Eccl 9:12 w1 to Eccl 10:5 w5 | 0.497 | 4.60e-4 | 1 | 0.501 | 0.0045 | 13 |
| scan: Eccl 9:12 w1 to Eccl 10:5 w9 | 0.497 | 4.60e-4 | 1 | 0.501 | 0.0045 | 13 |
| scan: Jer 25:29 w14 to Jer 26:2 w26 | 0.498 | 4.60e-4 | 1 | 0.595 | 0.0011 | 18 |
| scan: Ezek 2:7 w1 to Ezek 3:7 w11 | 0.292 | 4.60e-4 | 1 | 0.249 | 0.0360 | 9 |
| scan: Ezek 22:14 w11 to Ezek 22:27 w5 | 0.427 | 4.60e-4 | 1 | 0.128 | 0.1135 | 28 |
| scan: Ezek 22:27 w6 to Ezek 23:8 w16 | 0.787 | 4.60e-4 | 1 | 0.733 | 0.0230 | 25 |
| scan: Ezek 43:8 w11 to Ezek 43:19 w14 | 0.631 | 4.60e-4 | 1 | 0.399 | 0.0031 | 35 |
| scan: Gen 14:5 w1 to Gen 14:16 w4 | 0.594 | 4.70e-4 | 1 | 0.734 | 0.0500 | 39 |
| scan: Gen 35:19 w3 to Gen 36:3 w6 | 0.473 | 4.70e-4 | 1 | 0.254 | 0.0287 | 18 |
| scan: Exod 14:7 w1 to Exod 14:17 w8 | 0.462 | 4.70e-4 | 1 | 0.250 | 0.0267 | 15 |
| scan: Exod 25:30 w1 to Exod 25:39 w5 | 0.439 | 4.70e-4 | 1 | 0.366 | 0.0077 | 35 |
| scan: Exod 33:4 w1 to Exod 33:15 w9 | 0.351 | 4.70e-4 | 1 | 0.263 | 0.0228 | 12 |
| scan: Exod 38:23 w1 to Exod 39:3 w16 | 0.508 | 4.70e-4 | 1 | 0.573 | 3.92e-5 | 41 |
| scan: Exod 38:23 w9 to Exod 39:3 w16 | 0.508 | 4.70e-4 | 1 | 0.505 | 1.50e-4 | 41 |
| scan: Lev 19:19 w12 to Lev 19:27 w9 | 0.667 | 4.70e-4 | 1 | 0.000 | 1.0000 | 28 |
| scan: Deut 20:1 w1 to Deut 20:11 w15 | 0.418 | 4.70e-4 | 1 | 0.293 | 0.0185 | 12 |
| scan: Josh 11:17 w1 to Josh 12:4 w6 | 0.444 | 4.70e-4 | 1 | 0.577 | 5.00e-6 | 37 |
| scan: Josh 11:17 w1 to Josh 12:4 w9 | 0.425 | 4.70e-4 | 1 | 0.577 | 5.00e-6 | 37 |
| scan: 1Sam 15:8 w7 to 1Sam 15:15 w18 | 0.521 | 4.70e-4 | 1 | 0.326 | 0.0539 | 15 |
| scan: 1Sam 17:40 w1 to 1Sam 17:50 w10 | 0.226 | 4.70e-4 | 0 | - | - | 0 |
| scan: 2Sam 7:19 w1 to 2Sam 7:29 w19 | 0.260 | 4.70e-4 | 1 | 0.119 | 0.0599 | 4 |
| scan: 2Sam 11:24 w1 to 2Sam 12:8 w15 | 0.355 | 4.70e-4 | 1 | 0.327 | 0.0011 | 17 |
| scan: 1Kgs 20:30 w14 to 1Kgs 20:41 w13 | 0.297 | 4.70e-4 | 1 | 0.289 | 0.0013 | 17 |
| scan: 2Kgs 4:40 w4 to 2Kgs 5:6 w6 | 0.347 | 4.70e-4 | 1 | 0.179 | 0.1002 | 16 |
| scan: 1Chr 6:27 w1 to 1Chr 6:36 w8 | 0.604 | 4.70e-4 | 1 | 0.020 | 0.1148 | 22 |
| scan: 1Chr 17:8 w11 to 1Chr 17:19 w13 | 0.651 | 4.70e-4 | 1 | 0.607 | 0.0237 | 7 |
| scan: 1Chr 18:13 w1 to 1Chr 19:4 w12 | 0.305 | 4.70e-4 | 1 | 0.335 | 0.0245 | 24 |
| scan: 1Chr 24:19 w1 to 1Chr 25:2 w15 | 0.310 | 4.70e-4 | 1 | 0.026 | 0.2890 | 38 |
| scan: Isa 2:11 w8 to Isa 2:20 w10 | 0.721 | 4.70e-4 | 1 | -0.349 | 0.8411 | 12 |
| scan: Isa 44:7 w1 to Isa 44:18 w4 | 0.696 | 4.70e-4 | 1 | -0.309 | 0.9284 | 30 |
| scan: Jer 26:2 w24 to Jer 26:13 w15 | 0.279 | 4.70e-4 | 1 | 0.069 | 0.2118 | 9 |
| scan: Ezek 29:1 w1 to Ezek 29:7 w15 | 0.608 | 4.70e-4 | 1 | 0.773 | 0.0131 | 10 |
| scan: Ezek 47:19 w13 to Ezek 48:5 w10 | 0.388 | 4.70e-4 | 1 | 0.142 | 0.0540 | 15 |
| scan: Zech 4:9 w1 to Zech 5:5 w4 | 0.384 | 4.70e-4 | 1 | 0.270 | 0.0464 | 14 |
| scan: Gen 28:3 w1 to Gen 28:14 w9 | 0.439 | 4.80e-4 | 1 | 0.405 | 9.90e-4 | 11 |
| scan: Gen 29:26 w1 to Gen 29:35 w14 | 0.610 | 4.80e-4 | 1 | 0.488 | 0.0636 | 9 |
| scan: Gen 49:25 w1 to Gen 50:2 w13 | 0.708 | 4.80e-4 | 1 | 0.459 | 0.0302 | 19 |
| scan: Exod 2:23 w1 to Exod 3:8 w25 | 0.433 | 4.80e-4 | 1 | 0.553 | 1.70e-4 | 13 |
| scan: Exod 25:26 w1 to Exod 25:38 w4 | 0.477 | 4.80e-4 | 1 | 0.344 | 0.0022 | 45 |
| scan: Exod 31:3 w5 to Exod 31:15 w10 | 0.540 | 4.80e-4 | 1 | 0.330 | 0.1250 | 14 |
| scan: Lev 10:18 w9 to Lev 11:11 w3 | 0.440 | 4.80e-4 | 1 | 0.437 | 0.0400 | 43 |
| scan: Lev 21:14 w1 to Lev 21:23 w20 | 0.480 | 4.80e-4 | 1 | 0.235 | 0.1290 | 13 |
| scan: Num 6:15 w11 to Num 6:26 w7 | 0.549 | 4.80e-4 | 1 | 0.525 | 0.0198 | 20 |
| scan: Num 15:15 w1 to Num 15:25 w9 | 0.606 | 4.80e-4 | 1 | 0.464 | 0.0212 | 8 |
| scan: Deut 4:13 w11 to Deut 4:22 w9 | 0.417 | 4.80e-4 | 1 | 0.231 | 0.0282 | 7 |
| scan: Josh 11:16 w19 to Josh 12:4 w6 | 0.448 | 4.80e-4 | 1 | 0.221 | 0.0144 | 40 |
| scan: Judg 11:17 w1 to Judg 11:28 w5 | 0.327 | 4.80e-4 | 1 | 0.326 | 0.0032 | 38 |
| scan: Judg 16:29 w13 to Judg 17:6 w9 | 0.570 | 4.80e-4 | 1 | 0.483 | 2.00e-4 | 13 |
| scan: 1Sam 3:10 w9 to 1Sam 3:18 w9 | 0.327 | 4.80e-4 | 1 | -0.094 | 0.7941 | 7 |
| scan: 1Kgs 8:14 w1 to 1Kgs 8:23 w20 | 0.347 | 4.80e-4 | 1 | 0.212 | 0.0074 | 1 |
| scan: Ezra 3:7 w5 to Ezra 4:3 w27 | 0.532 | 4.80e-4 | 1 | 0.451 | 0.0011 | 22 |
| scan: Neh 7:18 w1 to Neh 7:40 w5 | 0.135 | 4.80e-4 | 1 | 0.057 | 0.2400 | 49 |
| scan: Esth 5:4 w7 to Esth 5:11 w8 | 0.451 | 4.80e-4 | 0 | - | - | 0 |
| scan: Eccl 2:24 w11 to Eccl 3:12 w11 | 0.523 | 4.80e-4 | 1 | 0.423 | 4.50e-6 | 11 |
| scan: Isa 2:2 w13 to Isa 2:12 w8 | 0.801 | 4.80e-4 | 1 | 0.575 | 0.0032 | 12 |
| scan: Isa 66:15 w8 to Isa 66:23 w14 | 0.552 | 4.80e-4 | 1 | -0.003 | 0.5079 | 19 |
| scan: Jer 12:16 w18 to Jer 13:12 w14 | 0.350 | 4.80e-4 | 1 | 0.379 | 7.70e-4 | 14 |
| scan: Jer 17:16 w1 to Jer 17:22 w18 | 0.678 | 4.80e-4 | 1 | -0.055 | 0.6250 | 6 |
| scan: Jer 25:17 w1 to Jer 25:28 w7 | 0.370 | 4.80e-4 | 0 | - | - | 0 |
| scan: Jer 50:32 w1 to Jer 50:42 w13 | 0.631 | 4.80e-4 | 1 | -0.236 | 0.7751 | 27 |
| scan: Ezek 23:15 w10 to Ezek 23:24 w18 | 0.805 | 4.80e-4 | 1 | 0.926 | 1.30e-4 | 21 |
| scan: Ezek 47:14 w1 to Ezek 48:1 w3 | 0.377 | 4.80e-4 | 1 | -0.139 | 0.8643 | 25 |
| scan: Dan 5:22 w1 to Dan 5:31 w8 | 0.759 | 4.80e-4 | 1 | 1.000 | 0.5000 | 16 |
| scan: Obad 1:8 w6 to Obad 1:20 w13 | 0.622 | 4.80e-4 | 1 | 0.307 | 0.0416 | 31 |
| scan: Zech 2:11 w11 to Zech 3:10 w14 | 0.278 | 4.80e-4 | 1 | 0.190 | 0.0298 | 14 |
| scan: Zech 3:4 w1 to Zech 4:3 w9 | 0.429 | 4.80e-4 | 1 | 0.269 | 0.1642 | 8 |
| scan: Zech 12:7 w7 to Zech 13:5 w4 | 0.508 | 4.80e-4 | 1 | 0.326 | 0.0065 | 19 |
| scan: Gen 2:9 w1 to Gen 2:17 w7 | 0.603 | 4.90e-4 | 1 | 0.171 | 0.2241 | 9 |
| scan: Gen 26:3 w7 to Gen 26:15 w9 | 0.435 | 4.90e-4 | 1 | 0.396 | 0.0082 | 16 |
| scan: Gen 37:1 w1 to Gen 37:11 w7 | 0.429 | 4.90e-4 | 1 | 0.123 | 0.1764 | 14 |
| scan: Exod 10:4 w8 to Exod 10:14 w10 | 0.396 | 4.90e-4 | 1 | 0.411 | 5.09e-5 | 19 |
| scan: Exod 13:16 w8 to Exod 14:5 w6 | 0.509 | 4.90e-4 | 1 | 0.130 | 0.1454 | 21 |
| scan: Exod 28:14 w1 to Exod 28:22 w7 | 0.733 | 4.90e-4 | 1 | 0.044 | 0.4169 | 33 |
| scan: Exod 28:14 w1 to Exod 28:24 w11 | 0.480 | 4.90e-4 | 0 | - | - | 0 |
| scan: Exod 29:35 w1 to Exod 29:46 w15 | 0.545 | 4.90e-4 | 1 | 0.553 | 0.0032 | 27 |
| scan: Exod 39:16 w8 to Exod 39:26 w8 | 0.378 | 4.90e-4 | 1 | 0.035 | 0.3639 | 52 |
| scan: Lev 21:14 w9 to Lev 22:1 w5 | 0.519 | 4.90e-4 | 1 | 0.347 | 0.0401 | 13 |
| scan: Lev 21:24 w7 to Lev 22:9 w14 | 0.435 | 4.90e-4 | 1 | 0.224 | 0.1201 | 12 |
| scan: Num 33:33 w1 to Num 33:44 w7 | 0.412 | 4.90e-4 | 1 | 0.335 | 0.1250 | 51 |
| scan: Num 33:34 w1 to Num 33:44 w2 | 0.462 | 4.90e-4 | 1 | 0.440 | 0.5000 | 47 |
| scan: Deut 22:26 w9 to Deut 23:8 w6 | 0.366 | 4.90e-4 | 1 | -0.074 | 0.8000 | 12 |
| scan: Josh 18:14 w1 to Josh 18:23 w3 | 0.399 | 4.90e-4 | 1 | -0.048 | 0.6523 | 34 |
| scan: Judg 13:24 w8 to Judg 14:6 w10 | 0.482 | 4.90e-4 | 1 | 0.201 | 0.1100 | 14 |
| scan: 1Sam 30:24 w1 to 1Sam 31:3 w11 | 0.720 | 4.90e-4 | 1 | 1.000 | 0.0833 | 23 |
| scan: 1Sam 30:24 w6 to 1Sam 31:3 w8 | 0.720 | 4.90e-4 | 1 | 1.000 | 0.0833 | 23 |
| scan: 1Kgs 20:27 w7 to 1Kgs 20:36 w13 | 0.450 | 4.90e-4 | 1 | 0.201 | 0.0304 | 19 |
| scan: 1Kgs 20:30 w14 to 1Kgs 20:40 w7 | 0.349 | 4.90e-4 | 1 | 0.032 | 0.3564 | 16 |
| scan: 1Chr 2:33 w1 to 1Chr 2:43 w6 | 0.690 | 4.90e-4 | 1 | 0.278 | 1.63e-5 | 34 |
| scan: 1Chr 15:2 w12 to 1Chr 15:13 w12 | 0.458 | 4.90e-4 | 1 | 0.307 | 0.0106 | 18 |
| scan: 1Chr 20:1 w1 to 1Chr 21:3 w15 | 0.398 | 4.90e-4 | 1 | 0.331 | 0.0319 | 46 |
| scan: 2Chr 4:15 w1 to 2Chr 5:5 w12 | 0.487 | 4.90e-4 | 1 | 0.195 | 0.0447 | 21 |
| scan: 2Chr 36:11 w1 to 2Chr 36:22 w10 | 0.394 | 4.90e-4 | 1 | 0.421 | 0.0018 | 15 |
| scan: Neh 2:8 w24 to Neh 2:20 w14 | 0.454 | 4.90e-4 | 1 | 0.208 | 0.0365 | 18 |
| scan: Esth 6:8 w1 to Esth 7:3 w19 | 0.242 | 4.90e-4 | 0 | - | - | 0 |
| scan: Job 1:3 w1 to Job 1:10 w17 | 0.503 | 4.90e-4 | 1 | 0.547 | 0.0017 | 13 |
| scan: Isa 11:9 w1 to Isa 12:4 w14 | 0.408 | 4.90e-4 | 1 | 0.326 | 0.0226 | 12 |
| scan: Isa 37:35 w1 to Isa 38:7 w5 | 0.613 | 4.90e-4 | 1 | 0.154 | 0.2231 | 16 |
| scan: Jer 25:20 w1 to Jer 25:32 w15 | 0.332 | 4.90e-4 | 0 | - | - | 7 |
| scan: Jer 42:12 w6 to Jer 42:21 w3 | 0.300 | 4.90e-4 | 1 | 0.335 | 0.0062 | 8 |
| scan: Jer 51:16 w1 to Jer 51:27 w15 | 0.561 | 4.90e-4 | 1 | 0.059 | 0.3238 | 14 |
| scan: Ezek 1:23 w1 to Ezek 2:2 w13 | 0.535 | 4.90e-4 | 1 | 0.399 | 0.0626 | 6 |
| scan: Ezek 19:8 w1 to Ezek 20:5 w18 | 0.691 | 4.90e-4 | 1 | 0.672 | 3.40e-4 | 8 |
| scan: Ezek 20:2 w1 to Ezek 20:13 w21 | 0.410 | 4.90e-4 | 1 | 0.563 | 1.20e-4 | 10 |
| scan: Ezek 20:3 w17 to Ezek 20:11 w14 | 0.461 | 4.90e-4 | 1 | 0.552 | 0.0101 | 7 |
| scan: Ezek 20:3 w17 to Ezek 20:12 w9 | 0.461 | 4.90e-4 | 1 | 0.543 | 6.10e-4 | 7 |
| scan: Ezek 20:4 w1 to Ezek 20:11 w14 | 0.461 | 4.90e-4 | 1 | 0.496 | 0.0107 | 7 |
| scan: Ezek 42:12 w1 to Ezek 43:3 w21 | 0.401 | 4.90e-4 | 1 | 0.215 | 0.0404 | 23 |
| scan: Ezek 42:13 w23 to Ezek 43:3 w21 | 0.497 | 4.90e-4 | 1 | 0.284 | 0.0405 | 20 |
| scan: Gen 22:19 w11 to Gen 23:8 w3 | 0.567 | 5.00e-4 | 1 | -0.051 | 0.7994 | 24 |
| scan: Exod 29:35 w1 to Exod 29:45 w7 | 0.535 | 5.00e-4 | 1 | 0.553 | 0.0032 | 27 |
| scan: Num 31:43 w6 to Num 31:52 w14 | 0.690 | 5.00e-4 | 1 | 0.630 | 0.0040 | 14 |
| scan: Deut 13:14 w1 to Deut 14:6 w13 | 0.507 | 5.00e-4 | 1 | 0.665 | 0.0111 | 25 |
| scan: Deut 13:14 w5 to Deut 14:6 w11 | 0.507 | 5.00e-4 | 1 | 0.665 | 0.0111 | 25 |
| scan: Deut 28:12 w18 to Deut 28:22 w12 | 0.515 | 5.00e-4 | 1 | 0.505 | 0.0016 | 18 |
| scan: Judg 11:40 w1 to Judg 12:12 w3 | 0.438 | 5.00e-4 | 1 | 0.424 | 0.0031 | 28 |
| scan: 1Sam 11:1 w1 to 1Sam 11:10 w6 | 0.384 | 5.00e-4 | 1 | 0.398 | 0.0068 | 24 |
| scan: 2Sam 18:21 w1 to 2Sam 18:32 w7 | 0.221 | 5.00e-4 | 1 | 0.007 | 0.4556 | 26 |
| scan: 2Kgs 14:21 w12 to 2Kgs 15:2 w15 | 0.305 | 5.00e-4 | 1 | 0.319 | 7.60e-4 | 29 |
| scan: 2Kgs 16:8 w1 to 2Kgs 16:18 w16 | 0.251 | 5.00e-4 | 1 | 0.129 | 0.0309 | 17 |
| scan: 1Chr 1:47 w3 to 1Chr 2:5 w4 | 0.774 | 5.00e-4 | 1 | 0.609 | 1.18e-5 | 33 |
| scan: 1Chr 2:4 w9 to 1Chr 2:18 w14 | 0.450 | 5.00e-4 | 1 | 0.617 | 3.83e-5 | 24 |
| scan: 2Chr 4:15 w4 to 2Chr 5:4 w8 | 0.529 | 5.00e-4 | 1 | 0.154 | 0.0978 | 21 |
| scan: 2Chr 4:16 w1 to 2Chr 5:4 w4 | 0.529 | 5.00e-4 | 1 | 0.154 | 0.0978 | 21 |
| scan: 2Chr 6:8 w14 to 2Chr 6:18 w8 | 0.431 | 5.00e-4 | 1 | 0.113 | 0.1453 | 8 |
| scan: 2Chr 7:3 w11 to 2Chr 7:14 w12 | 0.249 | 5.00e-4 | 1 | 0.258 | 0.0013 | 18 |
| scan: 2Chr 8:13 w1 to 2Chr 9:5 w8 | 0.370 | 5.00e-4 | 1 | 0.353 | 0.0119 | 17 |
| scan: 2Chr 10:14 w1 to 2Chr 11:4 w25 | 0.410 | 5.00e-4 | 1 | 0.263 | 0.0374 | 9 |
| scan: 2Chr 12:12 w9 to 2Chr 13:7 w19 | 0.386 | 5.00e-4 | 1 | 0.479 | 0.0035 | 26 |
| scan: 2Chr 30:22 w11 to 2Chr 31:3 w15 | 0.617 | 5.00e-4 | 1 | 0.436 | 0.0086 | 17 |
| scan: Ps 67:4 w8 to Ps 68:7 w7 | 0.365 | 5.00e-4 | 1 | -0.155 | 0.8830 | 23 |
| scan: Jer 12:17 w1 to Jer 13:12 w14 | 0.348 | 5.00e-4 | 1 | 0.269 | 0.0350 | 14 |
| scan: Jer 25:29 w14 to Jer 26:3 w6 | 0.490 | 5.00e-4 | 1 | 0.595 | 0.0011 | 20 |
| scan: Ezek 1:3 w15 to Ezek 1:14 w3 | 0.501 | 5.00e-4 | 0 | - | - | 0 |
| scan: Ezek 1:23 w8 to Ezek 2:3 w16 | 0.576 | 5.00e-4 | 1 | 0.300 | 0.1330 | 7 |
| scan: Ezek 48:16 w1 to Ezek 48:27 w10 | 0.402 | 5.00e-4 | 1 | 0.266 | 0.0040 | 7 |
| scan: Gen 36:24 w6 to Gen 36:35 w15 | 0.485 | 5.10e-4 | 1 | 0.000 | 1.0000 | 36 |
| scan: Exod 2:22 w1 to Exod 3:8 w25 | 0.402 | 5.10e-4 | 1 | 0.504 | 1.80e-4 | 15 |
| scan: Exod 3:7 w1 to Exod 3:18 w2 | 0.378 | 5.10e-4 | 1 | -0.022 | 0.5849 | 21 |
| scan: Exod 21:9 w4 to Exod 21:23 w3 | 0.375 | 5.10e-4 | 1 | 0.518 | 0.0065 | 13 |
| scan: Exod 29:35 w9 to Exod 29:46 w12 | 0.591 | 5.10e-4 | 1 | 0.553 | 0.0032 | 27 |
| scan: Exod 30:13 w1 to Exod 30:24 w5 | 0.602 | 5.10e-4 | 1 | 0.375 | 0.0682 | 21 |
| scan: Lev 4:13 w1 to Lev 4:23 w14 | 0.399 | 5.10e-4 | 1 | 0.367 | 1.90e-4 | 18 |
| scan: Lev 21:23 w13 to Lev 22:10 w11 | 0.370 | 5.10e-4 | 1 | 0.135 | 0.1142 | 13 |
| scan: Num 7:87 w1 to Num 8:8 w8 | 0.711 | 5.10e-4 | 1 | 0.712 | 1.80e-4 | 14 |
| scan: Josh 15:10 w16 to Josh 15:23 w3 | 0.607 | 5.10e-4 | 1 | 0.644 | 2.97e-5 | 40 |
| scan: Josh 15:11 w1 to Josh 15:22 w3 | 0.607 | 5.10e-4 | 1 | 0.588 | 1.20e-4 | 35 |
| scan: Judg 1:19 w8 to Judg 1:28 w11 | 0.718 | 5.10e-4 | 1 | 0.321 | 0.0168 | 29 |
| scan: 1Sam 28:13 w1 to 1Sam 28:22 w18 | 0.431 | 5.10e-4 | 1 | 0.320 | 0.0031 | 8 |
| scan: 2Kgs 19:34 w1 to 2Kgs 20:6 w21 | 0.503 | 5.10e-4 | 1 | 0.380 | 0.0185 | 17 |
| scan: 1Chr 5:15 w1 to 1Chr 5:25 w3 | 0.737 | 5.10e-4 | 1 | 0.537 | 0.0190 | 30 |
| scan: 1Chr 14:17 w6 to 1Chr 15:12 w18 | 0.520 | 5.10e-4 | 1 | 0.444 | 5.20e-4 | 17 |
| scan: 1Chr 15:2 w1 to 1Chr 15:13 w4 | 0.447 | 5.10e-4 | 1 | 0.298 | 0.0060 | 18 |
| scan: 2Chr 4:15 w1 to 2Chr 5:4 w8 | 0.499 | 5.10e-4 | 1 | 0.154 | 0.0978 | 21 |
| scan: 2Chr 4:15 w4 to 2Chr 5:4 w4 | 0.499 | 5.10e-4 | 1 | 0.154 | 0.0978 | 21 |
| scan: Ezra 8:21 w1 to Ezra 8:32 w6 | 0.402 | 5.10e-4 | 1 | 0.274 | 0.0097 | 14 |
| scan: Esth 6:12 w1 to Esth 7:9 w25 | 0.184 | 5.10e-4 | 0 | - | - | 0 |
| scan: Song 4:9 w1 to Song 5:3 w10 | 0.436 | 5.10e-4 | 1 | 0.457 | 0.0039 | 21 |
| scan: Isa 7:23 w1 to Isa 8:10 w3 | 0.590 | 5.10e-4 | 1 | 0.415 | 0.0415 | 29 |
| scan: Isa 54:1 w5 to Isa 54:11 w11 | 0.443 | 5.10e-4 | 1 | 0.091 | 0.3856 | 15 |
| scan: Jer 51:17 w1 to Jer 51:26 w7 | 0.555 | 5.10e-4 | 1 | 0.174 | 0.0317 | 10 |
| scan: Ezek 11:22 w1 to Ezek 12:7 w20 | 0.458 | 5.10e-4 | 1 | 0.368 | 0.0699 | 7 |
| scan: Ezek 14:22 w1 to Ezek 16:4 w11 | 0.469 | 5.10e-4 | 1 | 0.353 | 0.0128 | 19 |
| scan: Obad 1:8 w1 to Obad 1:19 w18 | 0.532 | 5.10e-4 | 1 | 0.646 | 1.10e-4 | 29 |
| scan: Gen 2:16 w7 to Gen 3:2 w4 | 0.320 | 5.20e-4 | 1 | 0.328 | 7.40e-4 | 5 |
| scan: Exod 20:24 w1 to Exod 21:9 w7 | 0.397 | 5.20e-4 | 1 | 0.529 | 0.0477 | 14 |
| scan: Exod 25:27 w5 to Exod 25:38 w4 | 0.451 | 5.20e-4 | 1 | 0.476 | 6.02e-5 | 44 |
| scan: Exod 26:7 w1 to Exod 26:15 w7 | 0.237 | 5.20e-4 | 1 | -0.144 | 0.8657 | 35 |
| scan: Lev 3:15 w11 to Lev 4:10 w10 | 0.359 | 5.20e-4 | 1 | 0.236 | 0.0222 | 26 |
| scan: Lev 4:34 w1 to Lev 5:8 w16 | 0.415 | 5.20e-4 | 1 | 0.299 | 7.50e-4 | 22 |
| scan: Lev 24:15 w6 to Lev 25:1 w7 | 0.636 | 5.20e-4 | 1 | 0.527 | 5.80e-4 | 8 |
| scan: Num 7:2 w1 to Num 7:12 w6 | 0.490 | 5.20e-4 | 1 | 0.310 | 0.0082 | 14 |
| scan: Num 7:2 w1 to Num 7:13 w14 | 0.468 | 5.20e-4 | 1 | 0.469 | 7.70e-4 | 19 |
| scan: Deut 4:13 w11 to Deut 4:21 w21 | 0.520 | 5.20e-4 | 1 | 0.562 | 0.0014 | 6 |
| scan: Deut 15:1 w1 to Deut 15:9 w21 | 0.426 | 5.20e-4 | 1 | 0.338 | 0.0294 | 12 |
| scan: Judg 10:8 w8 to Judg 11:2 w5 | 0.343 | 5.20e-4 | 1 | 0.084 | 0.0833 | 30 |
| scan: Judg 16:29 w13 to Judg 17:6 w5 | 0.802 | 5.20e-4 | 1 | 0.021 | 0.4556 | 13 |
| scan: 1Sam 17:5 w9 to 1Sam 17:15 w5 | 0.601 | 5.20e-4 | 0 | - | - | 0 |
| scan: 2Sam 5:1 w8 to 2Sam 5:12 w14 | 0.273 | 5.20e-4 | 1 | 0.288 | 1.90e-4 | 15 |
| scan: 2Sam 11:24 w1 to 2Sam 12:8 w21 | 0.372 | 5.20e-4 | 1 | 0.286 | 0.0046 | 17 |
| scan: 2Sam 14:24 w9 to 2Sam 15:3 w7 | 0.219 | 5.20e-4 | 1 | 0.121 | 0.0795 | 44 |
| scan: 2Sam 18:3 w25 to 2Sam 18:12 w17 | 0.408 | 5.20e-4 | 1 | 0.252 | 0.0368 | 37 |
| scan: 1Kgs 20:30 w1 to 1Kgs 20:41 w13 | 0.254 | 5.20e-4 | 1 | 0.319 | 2.30e-4 | 17 |
| scan: 1Kgs 20:30 w14 to 1Kgs 20:41 w6 | 0.300 | 5.20e-4 | 1 | 0.319 | 2.30e-4 | 17 |
| scan: 2Kgs 10:15 w1 to 2Kgs 10:23 w23 | 0.397 | 5.20e-4 | 1 | -0.068 | 0.7357 | 18 |
| scan: 1Chr 5:14 w1 to 1Chr 5:24 w4 | 0.713 | 5.20e-4 | 1 | 0.557 | 0.0149 | 34 |
| scan: 1Chr 15:7 w1 to 1Chr 15:18 w3 | 0.368 | 5.20e-4 | 1 | 0.136 | 0.0874 | 37 |
| scan: 2Chr 5:9 w14 to 2Chr 6:7 w5 | 0.352 | 5.20e-4 | 1 | -0.088 | 0.7370 | 18 |
| scan: 2Chr 29:7 w11 to 2Chr 29:19 w11 | 0.456 | 5.20e-4 | 1 | 0.385 | 0.0037 | 34 |
| scan: Neh 6:6 w1 to Neh 6:15 w8 | 0.457 | 5.20e-4 | 1 | 0.724 | 0.0011 | 17 |
| scan: Isa 11:13 w1 to Isa 13:2 w8 | 0.726 | 5.20e-4 | 1 | 0.627 | 0.0123 | 8 |
| scan: Isa 50:1 w18 to Isa 50:11 w17 | 0.596 | 5.20e-4 | 1 | 0.257 | 0.0835 | 7 |
| scan: Ezek 1:3 w1 to Ezek 1:13 w18 | 0.480 | 5.20e-4 | 1 | 0.544 | 2.20e-4 | 15 |
| scan: Ezek 13:7 w8 to Ezek 13:18 w26 | 0.474 | 5.20e-4 | 1 | 0.503 | 6.90e-6 | 25 |
| scan: Ezek 23:47 w1 to Ezek 24:7 w15 | 0.646 | 5.20e-4 | 1 | 1.000 | 0.1667 | 26 |
| scan: Ezek 33:22 w1 to Ezek 34:1 w5 | 0.469 | 5.20e-4 | 1 | 0.216 | 0.0967 | 12 |
| scan: Zech 2:12 w9 to Zech 4:1 w9 | 0.335 | 5.20e-4 | 1 | -0.076 | 0.7800 | 11 |
| scan: Gen 3:24 w1 to Gen 4:11 w14 | 0.206 | 5.30e-4 | 1 | 0.196 | 0.0123 | 4 |
| scan: Exod 23:23 w13 to Exod 23:33 w15 | 0.583 | 5.30e-4 | 1 | 0.682 | 0.0271 | 18 |
| scan: Exod 31:4 w3 to Exod 31:16 w11 | 0.407 | 5.30e-4 | 1 | 0.496 | 0.1667 | 13 |
| scan: Exod 35:34 w1 to Exod 36:8 w21 | 0.252 | 5.30e-4 | 1 | -0.052 | 0.7194 | 11 |
| scan: Num 10:29 w19 to Num 11:2 w10 | 0.375 | 5.30e-4 | 1 | -0.015 | 0.5535 | 8 |
| scan: Num 15:30 w1 to Num 16:1 w8 | 0.551 | 5.30e-4 | 1 | 0.456 | 0.0012 | 15 |
| scan: 2Sam 11:5 w3 to 2Sam 11:12 w10 | 0.164 | 5.30e-4 | 1 | 0.094 | 0.0556 | 9 |
| scan: 1Chr 10:1 w1 to 1Chr 10:8 w15 | 0.313 | 5.30e-4 | 1 | 0.111 | 0.1815 | 8 |
| scan: 1Chr 28:16 w1 to 1Chr 29:4 w14 | 0.479 | 5.30e-4 | 1 | 0.112 | 0.1676 | 14 |
| scan: 2Chr 20:4 w5 to 2Chr 20:13 w9 | 0.562 | 5.30e-4 | 1 | 0.591 | 0.0031 | 7 |
| scan: Esth 6:13 w1 to Esth 7:9 w25 | 0.186 | 5.30e-4 | 0 | - | - | 0 |
| scan: Isa 52:1 w6 to Isa 52:9 w5 | 0.614 | 5.30e-4 | 1 | 0.128 | 0.2225 | 10 |
| scan: Jer 25:15 w1 to Jer 25:27 w20 | 0.406 | 5.30e-4 | 0 | - | - | 0 |
| scan: Jer 25:15 w15 to Jer 25:28 w15 | 0.411 | 5.30e-4 | 0 | - | - | 0 |
| scan: Ezek 41:3 w8 to Ezek 41:15 w18 | 0.193 | 5.30e-4 | 1 | 0.044 | 0.1096 | 38 |
| scan: Dan 8:5 w17 to Dan 8:16 w12 | 0.524 | 5.30e-4 | 1 | 0.301 | 0.0569 | 27 |
| scan: Gen 30:9 w1 to Gen 30:21 w3 | 0.230 | 5.40e-4 | 1 | -0.030 | 0.6884 | 14 |
| scan: Gen 47:14 w1 to Gen 47:21 w5 | 0.381 | 5.40e-4 | 1 | 0.327 | 0.0031 | 14 |
| scan: Exod 29:35 w9 to Exod 29:44 w6 | 0.658 | 5.40e-4 | 1 | 0.534 | 0.0034 | 26 |
| scan: Exod 29:36 w1 to Exod 29:44 w6 | 0.658 | 5.40e-4 | 1 | 0.556 | 0.0119 | 25 |
| scan: Lev 7:28 w1 to Lev 8:1 w5 | 0.354 | 5.40e-4 | 1 | 0.297 | 0.0019 | 18 |
| scan: Lev 21:15 w1 to Lev 21:24 w10 | 0.502 | 5.40e-4 | 1 | 0.279 | 0.0961 | 11 |
| scan: Lev 26:2 w6 to Lev 26:13 w17 | 0.696 | 5.40e-4 | 1 | -0.562 | 0.8333 | 10 |
| scan: Num 5:9 w1 to Num 5:17 w6 | 0.694 | 5.40e-4 | 1 | 0.575 | 0.0060 | 8 |
| scan: Num 5:9 w1 to Num 5:17 w17 | 0.590 | 5.40e-4 | 1 | 0.575 | 0.0060 | 8 |
| scan: Num 7:1 w1 to Num 7:13 w14 | 0.416 | 5.40e-4 | 1 | 0.160 | 0.0615 | 20 |
| scan: Num 23:16 w1 to Num 23:27 w10 | 0.330 | 5.40e-4 | 1 | 0.077 | 0.2284 | 16 |
| scan: Deut 2:6 w1 to Deut 2:15 w10 | 0.602 | 5.40e-4 | 1 | 0.753 | 6.04e-5 | 32 |
| scan: Deut 2:6 w6 to Deut 2:15 w8 | 0.602 | 5.40e-4 | 1 | 0.753 | 6.04e-5 | 32 |
| scan: Deut 27:25 w8 to Deut 28:9 w8 | 0.567 | 5.40e-4 | 1 | 0.568 | 0.0017 | 2 |
| scan: 1Sam 15:31 w5 to 1Sam 16:5 w9 | 0.237 | 5.40e-4 | 1 | 0.105 | 0.0794 | 8 |
| scan: 1Kgs 7:6 w1 to 1Kgs 7:15 w19 | 0.533 | 5.40e-4 | 1 | 0.766 | 3.03e-5 | 30 |
| scan: 1Chr 1:47 w1 to 1Chr 2:6 w9 | 0.769 | 5.40e-4 | 1 | 0.638 | 6.40e-6 | 37 |
| scan: 1Chr 6:20 w1 to 1Chr 6:32 w14 | 0.383 | 5.40e-4 | 1 | 0.000 | 1.0000 | 25 |
| scan: 1Chr 6:20 w2 to 1Chr 6:31 w11 | 0.383 | 5.40e-4 | 1 | 0.000 | 1.0000 | 24 |
| scan: 1Chr 12:15 w1 to 1Chr 12:23 w9 | 0.267 | 5.40e-4 | 1 | 0.036 | 0.3940 | 16 |
| scan: 1Chr 28:11 w1 to 1Chr 28:20 w27 | 0.466 | 5.40e-4 | 1 | 0.125 | 0.1665 | 16 |
| scan: Song 4:8 w7 to Song 5:4 w8 | 0.409 | 5.40e-4 | 1 | 0.258 | 0.0480 | 26 |
| scan: Isa 2:11 w8 to Isa 2:19 w13 | 0.572 | 5.40e-4 | 1 | -0.597 | 0.8965 | 11 |
| scan: Ezek 3:8 w8 to Ezek 3:20 w10 | 0.463 | 5.40e-4 | 1 | 0.345 | 0.0638 | 14 |
| scan: Ezek 5:1 w1 to Ezek 5:11 w26 | 0.508 | 5.40e-4 | 1 | 0.252 | 0.1088 | 18 |
| scan: Ezek 42:14 w1 to Ezek 43:4 w11 | 0.519 | 5.40e-4 | 1 | 0.373 | 0.0112 | 16 |
| scan: Amos 7:3 w1 to Amos 7:12 w16 | 0.345 | 5.40e-4 | 1 | -0.020 | 0.5530 | 16 |
| scan: Gen 5:30 w13 to Gen 6:10 w4 | 0.532 | 5.50e-4 | 1 | 0.389 | 9.10e-4 | 16 |
| scan: Gen 37:27 w1 to Gen 37:36 w10 | 0.538 | 5.50e-4 | 1 | 0.671 | 4.70e-4 | 14 |
| scan: Exod 38:23 w9 to Exod 39:3 w18 | 0.544 | 5.50e-4 | 1 | 0.613 | 1.90e-4 | 41 |
| scan: Num 15:13 w1 to Num 15:22 w8 | 0.635 | 5.50e-4 | 1 | -0.192 | 0.8405 | 6 |
| scan: Deut 4:11 w5 to Deut 4:22 w9 | 0.367 | 5.50e-4 | 1 | 0.269 | 0.0034 | 9 |
| scan: Deut 31:10 w5 to Deut 31:20 w13 | 0.426 | 5.50e-4 | 1 | 0.194 | 0.0590 | 19 |
| scan: Josh 4:9 w1 to Josh 4:17 w8 | 0.437 | 5.50e-4 | 1 | 0.144 | 0.2082 | 9 |
| scan: 1Sam 28:13 w1 to 1Sam 28:23 w11 | 0.421 | 5.50e-4 | 1 | 0.301 | 0.0066 | 11 |
| scan: 1Kgs 22:16 w1 to 1Kgs 22:27 w17 | 0.279 | 5.50e-4 | 1 | 0.086 | 0.1748 | 9 |
| scan: 2Kgs 3:26 w8 to 2Kgs 4:10 w17 | 0.326 | 5.50e-4 | 1 | 0.378 | 0.0015 | 15 |
| scan: 2Kgs 14:22 w1 to 2Kgs 15:1 w13 | 0.305 | 5.50e-4 | 1 | 0.230 | 0.0324 | 24 |
| scan: 1Chr 15:8 w3 to 1Chr 15:18 w19 | 0.400 | 5.50e-4 | 1 | 0.295 | 0.0095 | 36 |
| scan: 1Chr 27:27 w5 to 1Chr 28:5 w8 | 0.393 | 5.50e-4 | 1 | -0.202 | 0.8684 | 33 |
| scan: 2Chr 11:15 w6 to 2Chr 12:4 w6 | 0.346 | 5.50e-4 | 1 | 0.282 | 0.0584 | 23 |
| scan: 2Chr 18:15 w1 to 2Chr 18:26 w16 | 0.224 | 5.50e-4 | 1 | 0.161 | 0.0143 | 11 |
| scan: 2Chr 32:33 w1 to 2Chr 33:9 w6 | 0.417 | 5.50e-4 | 1 | 0.288 | 0.0474 | 21 |
| scan: Isa 24:21 w1 to Isa 25:8 w10 | 0.582 | 5.50e-4 | 1 | 0.512 | 0.0121 | 14 |
| scan: Zech 4:3 w1 to Zech 4:11 w12 | 0.597 | 5.50e-4 | 1 | 0.563 | 0.0015 | 6 |
| scan: Zech 13:8 w1 to Zech 14:7 w15 | 0.473 | 5.50e-4 | 1 | 0.542 | 0.0205 | 20 |
| scan: Gen 2:8 w7 to Gen 2:18 w8 | 0.497 | 5.60e-4 | 1 | -0.140 | 0.8375 | 10 |
| scan: Gen 2:13 w1 to Gen 2:20 w15 | 0.574 | 5.60e-4 | 1 | 0.309 | 0.1127 | 5 |
| scan: Exod 28:12 w12 to Exod 28:23 w14 | 0.451 | 5.60e-4 | 0 | - | - | 0 |
| scan: Num 6:23 w1 to Num 7:8 w16 | 0.480 | 5.60e-4 | 1 | 0.549 | 1.40e-4 | 12 |
| scan: Num 26:3 w1 to Num 26:11 w4 | 0.737 | 5.60e-4 | 1 | 0.488 | 0.0587 | 17 |
| scan: Num 28:21 w6 to Num 28:30 w3 | 0.717 | 5.60e-4 | 1 | 0.246 | 0.0763 | 18 |
| scan: Num 31:8 w1 to Num 31:17 w12 | 0.556 | 5.60e-4 | 1 | 0.722 | 0.0029 | 16 |
| scan: Deut 4:12 w1 to Deut 4:23 w20 | 0.350 | 5.60e-4 | 1 | 0.127 | 0.0507 | 9 |
| scan: Deut 4:13 w1 to Deut 4:22 w9 | 0.469 | 5.60e-4 | 1 | 0.596 | 8.10e-4 | 7 |
| scan: Deut 28:65 w1 to Deut 29:6 w13 | 0.443 | 5.60e-4 | 1 | 0.565 | 0.0015 | 9 |
| scan: Deut 31:12 w1 to Deut 31:18 w16 | 0.594 | 5.60e-4 | 1 | 0.341 | 0.0518 | 11 |
| scan: Josh 1:7 w1 to Josh 1:18 w17 | 0.393 | 5.60e-4 | 1 | 0.354 | 0.0182 | 9 |
| scan: Josh 15:6 w1 to Josh 15:15 w10 | 0.237 | 5.60e-4 | 1 | -0.048 | 0.7762 | 45 |
| scan: Judg 1:20 w8 to Judg 1:28 w8 | 0.759 | 5.60e-4 | 1 | 0.175 | 0.1240 | 25 |
| scan: 2Sam 14:27 w9 to 2Sam 15:1 w12 | 0.467 | 5.60e-4 | 1 | 0.573 | 2.90e-4 | 30 |
| scan: 2Sam 23:38 w1 to 2Sam 24:7 w13 | 0.399 | 5.60e-4 | 1 | 0.457 | 0.0293 | 20 |
| scan: 1Chr 28:10 w1 to 1Chr 28:21 w21 | 0.342 | 5.60e-4 | 1 | 0.017 | 0.4376 | 17 |
| scan: 2Chr 5:8 w8 to 2Chr 6:6 w5 | 0.410 | 5.60e-4 | 1 | 0.157 | 0.1882 | 20 |
| scan: 2Chr 30:2 w7 to 2Chr 30:13 w13 | 0.371 | 5.60e-4 | 1 | 0.586 | 2.90e-6 | 13 |
| scan: Esth 6:7 w5 to Esth 7:4 w18 | 0.221 | 5.60e-4 | 0 | - | - | 0 |
| scan: Isa 42:23 w5 to Isa 43:9 w18 | 0.638 | 5.60e-4 | 1 | 0.509 | 0.1053 | 12 |
| scan: Jer 1:7 w1 to Jer 1:17 w17 | 0.345 | 5.60e-4 | 1 | 0.209 | 0.0585 | 12 |
| scan: Jer 3:19 w1 to Jer 4:5 w8 | 0.449 | 5.60e-4 | 1 | 0.204 | 0.0311 | 11 |
| scan: Jer 25:31 w1 to Jer 26:2 w26 | 0.662 | 5.60e-4 | 1 | 0.470 | 0.0038 | 14 |
| scan: Ezek 42:12 w9 to Ezek 43:3 w18 | 0.415 | 5.60e-4 | 1 | 0.215 | 0.0404 | 23 |
| scan: Ezek 47:22 w1 to Ezek 48:13 w11 | 0.223 | 5.60e-4 | 1 | 0.163 | 0.0404 | 11 |
| scan: Zech 8:17 w1 to Zech 9:2 w9 | 0.340 | 5.60e-4 | 1 | 0.470 | 2.40e-4 | 8 |
| scan: Gen 38:7 w1 to Gen 38:18 w18 | 0.451 | 5.70e-4 | 1 | 0.182 | 0.0767 | 20 |
| scan: Gen 49:31 w1 to Gen 50:6 w2 | 0.729 | 5.70e-4 | 1 | -0.167 | 0.6750 | 12 |
| scan: Exod 14:9 w1 to Exod 14:17 w14 | 0.548 | 5.70e-4 | 1 | 0.291 | 0.0482 | 13 |
| scan: Exod 28:9 w1 to Exod 28:20 w5 | 0.692 | 5.70e-4 | 1 | 0.169 | 0.1891 | 42 |
| scan: Lev 4:6 w6 to Lev 4:16 w8 | 0.255 | 5.70e-4 | 1 | 0.192 | 0.0585 | 21 |
| scan: Num 1:4 w1 to Num 1:17 w3 | 0.388 | 5.70e-4 | 1 | 0.356 | 0.0032 | 21 |
| scan: Deut 12:16 w1 to Deut 12:24 w2 | 0.373 | 5.70e-4 | 1 | 0.381 | 0.0067 | 12 |
| scan: Deut 28:13 w1 to Deut 28:23 w10 | 0.545 | 5.70e-4 | 1 | 0.702 | 0.0011 | 18 |
| scan: 1Sam 14:3 w15 to 1Sam 14:15 w11 | 0.248 | 5.70e-4 | 1 | 0.024 | 0.4007 | 27 |
| scan: 1Sam 31:1 w4 to 1Sam 31:8 w16 | 0.324 | 5.70e-4 | 1 | 0.322 | 0.0029 | 11 |
| scan: 1Kgs 2:34 w8 to 1Kgs 2:45 w11 | 0.288 | 5.70e-4 | 1 | 0.183 | 0.0222 | 17 |
| scan: 1Kgs 2:35 w1 to 1Kgs 2:45 w3 | 0.298 | 5.70e-4 | 1 | 0.183 | 0.0222 | 16 |
| scan: 1Kgs 20:31 w15 to 1Kgs 20:40 w15 | 0.394 | 5.70e-4 | 1 | 0.277 | 0.0036 | 13 |
| scan: 1Chr 3:1 w9 to 1Chr 3:15 w6 | 0.786 | 5.70e-4 | 1 | 0.012 | 0.4502 | 40 |
| scan: 1Chr 6:17 w1 to 1Chr 6:32 w14 | 0.368 | 5.70e-4 | 1 | 0.010 | 0.1552 | 33 |
| scan: 1Chr 6:57 w13 to 1Chr 6:70 w11 | 0.390 | 5.70e-4 | 1 | 0.073 | 0.0886 | 50 |
| scan: 1Chr 15:8 w1 to 1Chr 15:19 w4 | 0.387 | 5.70e-4 | 1 | 0.295 | 0.0095 | 40 |
| scan: 1Chr 15:8 w3 to 1Chr 15:17 w18 | 0.448 | 5.70e-4 | 1 | 0.332 | 0.0088 | 26 |
| scan: Esth 6:12 w6 to Esth 7:10 w8 | 0.198 | 5.70e-4 | 0 | - | - | 0 |
| scan: Jer 25:16 w4 to Jer 25:28 w7 | 0.423 | 5.70e-4 | 0 | - | - | 0 |
| scan: Jer 32:15 w8 to Jer 32:25 w11 | 0.406 | 5.70e-4 | 1 | 0.290 | 0.0294 | 10 |
| scan: Jer 51:15 w1 to Jer 51:26 w13 | 0.698 | 5.70e-4 | 1 | 0.426 | 1.80e-4 | 10 |
| scan: Jer 51:15 w7 to Jer 51:26 w13 | 0.729 | 5.70e-4 | 1 | 0.518 | 5.20e-4 | 10 |
| scan: Jer 51:17 w9 to Jer 51:28 w11 | 0.523 | 5.70e-4 | 1 | 0.178 | 0.0225 | 15 |
| scan: Ezek 33:18 w1 to Ezek 33:26 w10 | 0.667 | 5.70e-4 | 0 | - | - | 0 |
| scan: Ezek 46:9 w1 to Ezek 46:20 w12 | 0.503 | 5.70e-4 | 1 | 0.533 | 8.40e-4 | 26 |
| scan: Gen 14:5 w1 to Gen 14:16 w15 | 0.630 | 5.80e-4 | 1 | 0.734 | 0.0500 | 39 |
| scan: Gen 25:21 w9 to Gen 25:33 w7 | 0.374 | 5.80e-4 | 1 | -0.001 | 0.5038 | 16 |
| scan: Lev 4:12 w19 to Lev 4:19 w5 | 0.529 | 5.80e-4 | 1 | 0.128 | 0.2569 | 13 |
| scan: Num 7:87 w1 to Num 8:9 w12 | 0.597 | 5.80e-4 | 1 | 0.501 | 6.60e-4 | 15 |
| scan: Num 33:34 w3 to Num 33:44 w2 | 0.497 | 5.80e-4 | 1 | 0.440 | 0.5000 | 47 |
| scan: Deut 18:14 w1 to Deut 19:3 w11 | 0.246 | 5.80e-4 | 1 | 0.316 | 0.0012 | 13 |
| scan: Deut 28:13 w1 to Deut 28:25 w13 | 0.541 | 5.80e-4 | 1 | -0.164 | 0.7949 | 20 |
| scan: Deut 33:8 w1 to Deut 33:19 w14 | 0.799 | 5.80e-4 | 1 | 0.802 | 0.0039 | 18 |
| scan: Josh 4:19 w1 to Josh 5:5 w6 | 0.443 | 5.80e-4 | 1 | 0.194 | 0.0706 | 19 |
| scan: 1Sam 4:20 w11 to 1Sam 5:10 w5 | 0.305 | 5.80e-4 | 1 | 0.301 | 0.0025 | 43 |
| scan: 1Sam 14:12 w15 to 1Sam 14:22 w15 | 0.305 | 5.80e-4 | 1 | -0.003 | 0.5108 | 18 |
| scan: 1Sam 30:29 w1 to 1Sam 31:8 w7 | 0.355 | 5.80e-4 | 1 | 0.135 | 0.1510 | 15 |
| scan: 2Sam 14:26 w1 to 2Sam 15:2 w7 | 0.369 | 5.80e-4 | 1 | 0.562 | 1.50e-4 | 38 |
| scan: 1Kgs 13:8 w15 to 1Kgs 13:17 w12 | 0.548 | 5.80e-4 | 1 | 0.021 | 0.4420 | 10 |
| scan: 2Kgs 4:5 w1 to 2Kgs 4:13 w24 | 0.415 | 5.80e-4 | 1 | 0.565 | 9.30e-4 | 8 |
| scan: 1Chr 5:14 w1 to 1Chr 5:25 w3 | 0.691 | 5.80e-4 | 1 | 0.537 | 0.0190 | 36 |
| scan: 1Chr 5:14 w1 to 1Chr 5:25 w12 | 0.691 | 5.80e-4 | 1 | 0.537 | 0.0190 | 36 |
| scan: 1Chr 7:8 w12 to 1Chr 7:21 w6 | 0.376 | 5.80e-4 | 1 | 0.010 | 0.3379 | 57 |
| scan: 1Chr 15:9 w3 to 1Chr 15:18 w19 | 0.494 | 5.80e-4 | 1 | 0.280 | 0.0271 | 35 |
| scan: 1Chr 20:1 w1 to 1Chr 21:4 w12 | 0.369 | 5.80e-4 | 1 | 0.263 | 0.0373 | 49 |
| scan: 1Chr 28:9 w1 to 1Chr 28:19 w9 | 0.535 | 5.80e-4 | 1 | 0.650 | 0.0018 | 17 |
| scan: 2Chr 8:10 w1 to 2Chr 9:1 w33 | 0.381 | 5.80e-4 | 1 | 0.258 | 0.0084 | 15 |
| scan: Neh 7:63 w7 to Neh 8:2 w17 | 0.417 | 5.80e-4 | 1 | 0.300 | 0.0293 | 22 |
| scan: Ezek 1:3 w15 to Ezek 1:13 w18 | 0.561 | 5.80e-4 | 1 | 0.544 | 2.20e-4 | 15 |
| scan: Ezek 23:16 w1 to Ezek 23:24 w13 | 0.811 | 5.80e-4 | 1 | 0.939 | 4.80e-4 | 18 |
| scan: Ezek 45:7 w22 to Ezek 45:19 w18 | 0.461 | 5.80e-4 | 1 | 0.348 | 0.0047 | 26 |
| scan: Dan 2:21 w9 to Dan 2:30 w13 | 0.276 | 5.80e-4 | 1 | 0.249 | 0.0019 | 7 |
| scan: Zech 12:7 w1 to Zech 13:4 w14 | 0.516 | 5.80e-4 | 1 | 0.356 | 0.0033 | 19 |
| scan: Gen 30:8 w10 to Gen 30:20 w19 | 0.245 | 5.90e-4 | 1 | 0.034 | 0.2712 | 16 |
| scan: Exod 8:5 w18 to Exod 8:17 w15 | 0.334 | 5.90e-4 | 1 | 0.183 | 0.0308 | 22 |
| scan: Exod 25:30 w1 to Exod 25:39 w9 | 0.421 | 5.90e-4 | 1 | 0.255 | 0.0324 | 35 |
| scan: Exod 28:12 w12 to Exod 28:24 w11 | 0.381 | 5.90e-4 | 0 | - | - | 0 |
| scan: Exod 29:36 w1 to Exod 29:45 w7 | 0.607 | 5.90e-4 | 1 | 0.556 | 0.0119 | 26 |
| scan: Exod 30:8 w1 to Exod 30:20 w8 | 0.389 | 5.90e-4 | 1 | 0.665 | 1.30e-6 | 22 |
| scan: Exod 40:8 w1 to Exod 40:19 w16 | 0.597 | 5.90e-4 | 1 | 0.226 | 0.1406 | 15 |
| scan: Lev 14:10 w1 to Lev 14:21 w21 | 0.286 | 5.90e-4 | 1 | 0.223 | 7.20e-4 | 35 |
| scan: Lev 26:7 w4 to Lev 26:18 w6 | 0.699 | 5.90e-4 | 1 | 0.603 | 0.0059 | 18 |
| scan: Num 5:12 w1 to Num 5:20 w14 | 0.432 | 5.90e-4 | 1 | 0.328 | 0.0170 | 14 |
| scan: Num 21:24 w5 to Num 21:33 w4 | 0.416 | 5.90e-4 | 1 | 0.034 | 0.4478 | 35 |
| scan: Deut 18:12 w7 to Deut 19:2 w12 | 0.224 | 5.90e-4 | 1 | 0.270 | 0.0012 | 10 |
| scan: Deut 19:12 w1 to Deut 19:21 w13 | 0.585 | 5.90e-4 | 1 | 0.418 | 0.0628 | 9 |
| scan: Deut 27:26 w1 to Deut 28:9 w8 | 0.530 | 5.90e-4 | 1 | 0.578 | 0.0014 | 2 |
| scan: Deut 34:1 w14 to Deut 34:11 w14 | 0.447 | 5.90e-4 | 1 | -0.000 | 0.5026 | 20 |
| scan: 1Sam 28:13 w1 to 1Sam 28:21 w23 | 0.461 | 5.90e-4 | 1 | 0.349 | 0.0084 | 7 |
| scan: 1Chr 1:9 w1 to 1Chr 1:23 w10 | 0.544 | 5.90e-4 | 0 | - | - | 0 |
| scan: 1Chr 10:1 w5 to 1Chr 10:8 w15 | 0.321 | 5.90e-4 | 1 | 0.305 | 0.0045 | 8 |
| scan: 2Chr 4:1 w1 to 2Chr 4:9 w10 | 0.438 | 5.90e-4 | 1 | 0.107 | 0.2122 | 21 |
| scan: 2Chr 11:4 w1 to 2Chr 11:16 w18 | 0.630 | 5.90e-4 | 1 | 0.695 | 0.0039 | 21 |
| scan: Ps 29:3 w5 to Ps 29:9 w10 | 0.477 | 5.90e-4 | 1 | 0.088 | 0.1403 | 9 |
| scan: Eccl 1:7 w9 to Eccl 1:15 w8 | 0.568 | 5.90e-4 | 1 | 0.481 | 0.0600 | 12 |
| scan: Ezek 3:13 w11 to Ezek 3:23 w18 | 0.647 | 5.90e-4 | 1 | 0.193 | 0.2142 | 13 |
| scan: Ezek 32:3 w1 to Ezek 32:11 w9 | 0.638 | 5.90e-4 | 1 | 0.479 | 0.0493 | 10 |
| scan: Gen 43:11 w17 to Gen 43:22 w6 | 0.365 | 6.00e-4 | 1 | 0.272 | 0.0073 | 21 |
| scan: Exod 24:12 w1 to Exod 25:3 w5 | 0.217 | 6.00e-4 | 1 | 0.174 | 0.0987 | 5 |
| scan: Exod 27:19 w1 to Exod 28:10 w5 | 0.536 | 6.00e-4 | 1 | 0.501 | 0.0065 | 26 |
| scan: Lev 14:16 w12 to Lev 14:28 w20 | 0.234 | 6.00e-4 | 1 | 0.172 | 0.0063 | 36 |
| scan: Lev 26:1 w17 to Lev 26:13 w11 | 0.676 | 6.00e-4 | 1 | -0.359 | 0.9033 | 12 |
| scan: Lev 27:6 w14 to Lev 27:13 w7 | 0.549 | 6.00e-4 | 1 | 0.795 | 6.23e-5 | 5 |
| scan: Num 33:35 w1 to Num 33:42 w2 | 0.667 | 6.00e-4 | 1 | 0.000 | 1.0000 | 34 |
| scan: Deut 21:3 w6 to Deut 21:13 w14 | 0.621 | 6.00e-4 | 1 | 0.346 | 0.1847 | 16 |
| scan: Deut 23:9 w6 to Deut 23:16 w12 | 0.516 | 6.00e-4 | 1 | -0.229 | 1.0000 | 8 |
| scan: 1Sam 3:11 w1 to 1Sam 3:19 w2 | 0.394 | 6.00e-4 | 1 | 0.074 | 0.3230 | 7 |
| scan: 2Sam 7:15 w1 to 2Sam 7:25 w13 | 0.499 | 6.00e-4 | 1 | 0.054 | 0.3589 | 6 |
| scan: 1Kgs 8:14 w1 to 1Kgs 8:22 w12 | 0.385 | 6.00e-4 | 1 | 0.283 | 0.0059 | 1 |
| scan: 1Chr 12:13 w1 to 1Chr 12:24 w11 | 0.293 | 6.00e-4 | 1 | 0.165 | 0.1299 | 22 |
| scan: 1Chr 27:21 w7 to 1Chr 27:33 w3 | 0.325 | 6.00e-4 | 1 | 0.361 | 0.0738 | 40 |
| scan: 2Chr 4:15 w1 to 2Chr 5:3 w10 | 0.431 | 6.00e-4 | 1 | 0.187 | 0.0577 | 21 |
| scan: 2Chr 4:15 w4 to 2Chr 5:3 w7 | 0.431 | 6.00e-4 | 1 | 0.187 | 0.0577 | 21 |
| scan: 2Chr 4:16 w1 to 2Chr 5:3 w10 | 0.516 | 6.00e-4 | 1 | 0.154 | 0.0978 | 21 |
| scan: 2Chr 6:3 w10 to 2Chr 6:13 w29 | 0.357 | 6.00e-4 | 1 | 0.344 | 0.0017 | 4 |
| scan: Esth 2:23 w8 to Esth 3:10 w6 | 0.279 | 6.00e-4 | 0 | - | - | 0 |
| scan: Esth 6:8 w1 to Esth 7:4 w7 | 0.242 | 6.00e-4 | 0 | - | - | 0 |
| scan: Song 4:10 w1 to Song 5:5 w4 | 0.433 | 6.00e-4 | 1 | -0.047 | 0.6053 | 24 |
| scan: Jer 25:29 w14 to Jer 26:2 w23 | 0.521 | 6.00e-4 | 1 | 0.595 | 0.0011 | 18 |
| scan: Ezek 45:7 w22 to Ezek 45:17 w13 | 0.556 | 6.00e-4 | 1 | 0.185 | 0.1203 | 21 |
| scan: Ezek 47:20 w1 to Ezek 48:12 w7 | 0.151 | 6.00e-4 | 1 | 0.183 | 0.0049 | 14 |
| scan: Gen 36:29 w4 to Gen 36:40 w7 | 0.322 | 6.10e-4 | 1 | 0.590 | 9.00e-8 | 43 |
| scan: Gen 47:4 w1 to Gen 47:14 w20 | 0.347 | 6.10e-4 | 1 | 0.137 | 0.0362 | 10 |
| scan: Exod 15:14 w4 to Exod 15:27 w9 | 0.433 | 6.10e-4 | 1 | 0.316 | 0.0185 | 25 |
| scan: Exod 29:40 w1 to Exod 30:5 w5 | 0.731 | 6.10e-4 | 1 | 0.196 | 0.1885 | 33 |
| scan: Lev 4:3 w7 to Lev 4:15 w10 | 0.225 | 6.10e-4 | 1 | 0.047 | 0.2671 | 25 |
| scan: Lev 14:3 w6 to Lev 14:13 w20 | 0.553 | 6.10e-4 | 1 | 0.381 | 0.0110 | 19 |
| scan: Num 8:12 w1 to Num 8:23 w5 | 0.253 | 6.10e-4 | 1 | 0.237 | 0.0026 | 13 |
| scan: Num 26:49 w1 to Num 26:60 w10 | 0.576 | 6.10e-4 | 1 | 0.258 | 0.0493 | 30 |
| scan: Num 33:34 w3 to Num 33:43 w4 | 0.517 | 6.10e-4 | 1 | 0.440 | 0.5000 | 42 |
| scan: Deut 23:7 w1 to Deut 23:18 w17 | 0.276 | 6.10e-4 | 1 | 0.472 | 0.0026 | 13 |
| scan: Deut 33:9 w1 to Deut 33:19 w14 | 0.670 | 6.10e-4 | 1 | 0.639 | 0.0519 | 18 |
| scan: Josh 8:25 w1 to Josh 8:35 w20 | 0.269 | 6.10e-4 | 0 | - | - | 0 |
| scan: Josh 18:14 w26 to Josh 18:22 w5 | 0.452 | 6.10e-4 | 1 | -0.048 | 0.6523 | 31 |
| scan: 1Sam 8:10 w1 to 1Sam 8:21 w6 | 0.566 | 6.10e-4 | 1 | 0.770 | 3.40e-5 | 10 |
| scan: 1Sam 14:13 w1 to 1Sam 14:24 w5 | 0.339 | 6.10e-4 | 1 | 0.046 | 0.3346 | 17 |
| scan: 1Sam 15:30 w1 to 1Sam 16:6 w10 | 0.246 | 6.10e-4 | 1 | 0.155 | 0.0152 | 8 |
| scan: 1Sam 17:55 w1 to 1Sam 18:7 w4 | 0.362 | 6.10e-4 | 0 | - | - | 0 |
| scan: 1Sam 20:17 w1 to 1Sam 20:28 w4 | 0.355 | 6.10e-4 | 1 | 0.234 | 0.1243 | 17 |
| scan: 1Chr 25:21 w1 to 1Chr 26:4 w13 | 0.041 | 6.10e-4 | 1 | 0.028 | 0.3141 | 35 |
| scan: 2Chr 9:7 w6 to 2Chr 9:18 w18 | 0.326 | 6.10e-4 | 1 | 0.285 | 6.00e-4 | 22 |
| scan: Ps 29:1 w3 to Ps 30:0 w5 | 0.250 | 6.10e-4 | 1 | 0.224 | 0.0016 | 13 |
| scan: Eccl 4:7 w1 to Eccl 4:15 w7 | 0.533 | 6.10e-4 | 1 | 0.356 | 0.2889 | 9 |
| scan: Jer 25:16 w4 to Jer 25:29 w26 | 0.377 | 6.10e-4 | 0 | - | - | 0 |
| scan: Jer 36:6 w1 to Jer 36:16 w9 | 0.248 | 6.10e-4 | 1 | 0.275 | 0.0064 | 20 |
| scan: Ezek 11:15 w1 to Ezek 12:2 w7 | 0.474 | 6.10e-4 | 1 | 0.510 | 5.86e-5 | 8 |
| scan: Ezek 36:17 w12 to Ezek 36:26 w8 | 0.430 | 6.10e-4 | 1 | 0.229 | 0.0616 | 18 |
| scan: Ezek 41:3 w1 to Ezek 41:13 w6 | 0.189 | 6.10e-4 | 1 | 0.192 | 1.80e-4 | 30 |
| scan: Gen 14:8 w14 to Gen 14:17 w19 | 0.680 | 6.20e-4 | 1 | 0.438 | 0.0013 | 27 |
| scan: Gen 46:19 w1 to Gen 46:31 w10 | 0.394 | 6.20e-4 | 1 | 0.159 | 0.0845 | 31 |
| scan: Exod 9:8 w13 to Exod 9:18 w7 | 0.626 | 6.20e-4 | 1 | 0.118 | 0.2483 | 12 |
| scan: Exod 9:9 w1 to Exod 9:17 w5 | 0.626 | 6.20e-4 | 1 | 0.436 | 0.1250 | 9 |
| scan: Exod 30:13 w11 to Exod 30:24 w8 | 0.616 | 6.20e-4 | 1 | 0.453 | 0.0133 | 21 |
| scan: Lev 7:5 w7 to Lev 7:16 w15 | 0.390 | 6.20e-4 | 1 | 0.187 | 0.2070 | 28 |
| scan: Deut 20:1 w15 to Deut 20:11 w6 | 0.466 | 6.20e-4 | 1 | 0.293 | 0.0185 | 12 |
| scan: Deut 20:15 w1 to Deut 21:4 w20 | 0.252 | 6.20e-4 | 1 | 0.373 | 0.0215 | 17 |
| scan: Deut 23:10 w1 to Deut 23:16 w12 | 0.525 | 6.20e-4 | 1 | 0.000 | 1.0000 | 8 |
| scan: 1Sam 17:56 w1 to 1Sam 18:6 w17 | 0.467 | 6.20e-4 | 0 | - | - | 0 |
| scan: 2Sam 8:13 w1 to 2Sam 9:3 w11 | 0.348 | 6.20e-4 | 1 | 0.200 | 0.0692 | 21 |
| scan: 1Kgs 14:20 w8 to 1Kgs 15:1 w11 | 0.290 | 6.20e-4 | 0 | - | - | 0 |
| scan: 1Kgs 17:24 w1 to 1Kgs 18:11 w3 | 0.368 | 6.20e-4 | 1 | 0.052 | 0.2655 | 18 |
| scan: 1Kgs 20:31 w15 to 1Kgs 20:41 w13 | 0.327 | 6.20e-4 | 1 | 0.286 | 0.0019 | 14 |
| scan: 1Kgs 20:33 w1 to 1Kgs 20:40 w15 | 0.435 | 6.20e-4 | 1 | 0.215 | 0.0294 | 11 |
| scan: 1Chr 2:31 w1 to 1Chr 2:43 w6 | 0.746 | 6.20e-4 | 1 | 0.000 | 1.0000 | 43 |
| scan: 2Chr 4:14 w4 to 2Chr 5:3 w10 | 0.464 | 6.20e-4 | 1 | 0.132 | 0.1250 | 23 |
| scan: Ps 134:3 w4 to Ps 135:7 w7 | 0.847 | 6.20e-4 | 1 | 0.444 | 0.0458 | 5 |
| scan: Ps 134:3 w4 to Ps 135:7 w10 | 0.847 | 6.20e-4 | 1 | 0.444 | 0.0458 | 5 |
| scan: Ps 134:3 w4 to Ps 135:8 w3 | 0.847 | 6.20e-4 | 1 | 0.441 | 0.0361 | 5 |
| scan: Jer 44:13 w1 to Jer 44:24 w16 | 0.376 | 6.20e-4 | 1 | 0.158 | 0.1103 | 16 |
| scan: Ezek 1:4 w1 to Ezek 1:13 w18 | 0.506 | 6.20e-4 | 1 | 0.504 | 1.30e-4 | 12 |
| scan: Ezek 41:2 w13 to Ezek 41:12 w21 | 0.181 | 6.20e-4 | 1 | 0.141 | 4.10e-4 | 30 |
| scan: Amos 2:12 w1 to Amos 3:7 w13 | 0.469 | 6.20e-4 | 1 | 0.703 | 0.0233 | 17 |
| scan: Gen 30:9 w1 to Gen 30:20 w15 | 0.236 | 6.30e-4 | 1 | 0.021 | 0.3496 | 14 |
| scan: Exod 14:6 w4 to Exod 14:17 w14 | 0.451 | 6.30e-4 | 1 | 0.238 | 0.0273 | 16 |
| scan: Exod 19:2 w1 to Exod 19:12 w11 | 0.324 | 6.30e-4 | 1 | 0.309 | 0.0138 | 7 |
| scan: Exod 29:39 w1 to Exod 30:2 w10 | 0.694 | 6.30e-4 | 1 | 0.598 | 0.0125 | 21 |
| scan: Exod 33:5 w1 to Exod 33:14 w1 | 0.379 | 6.30e-4 | 1 | 0.237 | 0.0046 | 9 |
| scan: Lev 3:15 w11 to Lev 4:10 w5 | 0.401 | 6.30e-4 | 1 | 0.371 | 0.0206 | 26 |
| scan: Num 20:22 w1 to Num 21:4 w10 | 0.378 | 6.30e-4 | 1 | 0.278 | 0.0039 | 21 |
| scan: Num 33:33 w4 to Num 33:43 w4 | 0.479 | 6.30e-4 | 1 | 0.000 | 0.6667 | 46 |
| scan: Deut 27:26 w11 to Deut 28:10 w9 | 0.499 | 6.30e-4 | 1 | 0.442 | 0.0052 | 2 |
| scan: Deut 28:64 w10 to Deut 29:7 w14 | 0.388 | 6.30e-4 | 1 | 0.363 | 0.0375 | 13 |
| scan: Josh 10:39 w19 to Josh 11:8 w22 | 0.328 | 6.30e-4 | 1 | -0.034 | 0.6039 | 40 |
| scan: 1Sam 28:11 w1 to 1Sam 28:22 w18 | 0.368 | 6.30e-4 | 1 | 0.362 | 5.60e-4 | 9 |
| scan: 2Sam 7:14 w9 to 2Sam 7:25 w16 | 0.455 | 6.30e-4 | 1 | 0.054 | 0.3589 | 7 |
| scan: 1Kgs 22:18 w1 to 1Kgs 22:26 w15 | 0.443 | 6.30e-4 | 1 | 0.196 | 0.0881 | 8 |
| scan: 2Kgs 2:22 w6 to 2Kgs 3:8 w5 | 0.555 | 6.30e-4 | 1 | 0.635 | 3.18e-5 | 25 |
| scan: 2Kgs 16:8 w13 to 2Kgs 16:19 w14 | 0.249 | 6.30e-4 | 1 | 0.175 | 0.0058 | 17 |
| scan: 1Chr 15:7 w3 to 1Chr 15:17 w18 | 0.388 | 6.30e-4 | 1 | 0.155 | 0.0826 | 27 |
| scan: 2Chr 4:3 w1 to 2Chr 4:13 w20 | 0.619 | 6.30e-4 | 1 | 0.485 | 0.0244 | 22 |
| scan: 2Chr 20:31 w5 to 2Chr 21:5 w10 | 0.546 | 6.30e-4 | 1 | 0.126 | 0.1788 | 21 |
| scan: Ezra 2:61 w1 to Ezra 3:2 w15 | 0.469 | 6.30e-4 | 1 | 0.200 | 0.2548 | 21 |
| scan: Neh 7:65 w1 to Neh 8:3 w17 | 0.441 | 6.30e-4 | 1 | 0.380 | 0.0378 | 18 |
| scan: Ps 148:4 w1 to Ps 148:13 w12 | 0.794 | 6.30e-4 | 1 | 0.782 | 0.0250 | 6 |
| scan: Eccl 2:23 w1 to Eccl 3:11 w23 | 0.522 | 6.30e-4 | 1 | 0.392 | 5.58e-5 | 14 |
| scan: Jer 12:17 w1 to Jer 13:11 w28 | 0.345 | 6.30e-4 | 1 | 0.289 | 0.0096 | 14 |
| scan: Jer 28:15 w10 to Jer 29:9 w6 | 0.497 | 6.30e-4 | 1 | 0.088 | 0.3845 | 18 |
| scan: Jer 51:18 w5 to Jer 51:26 w7 | 0.349 | 6.30e-4 | 1 | 0.123 | 0.0400 | 6 |
| scan: Ezek 43:11 w24 to Ezek 43:18 w13 | 0.524 | 6.30e-4 | 1 | 0.200 | 0.0231 | 25 |
| scan: Gen 40:21 w1 to Gen 41:9 w6 | 0.565 | 6.40e-4 | 1 | 0.538 | 8.20e-4 | 17 |
| scan: Gen 43:12 w1 to Gen 43:22 w6 | 0.371 | 6.40e-4 | 1 | 0.318 | 0.0094 | 17 |
| scan: Exod 2:22 w7 to Exod 3:9 w7 | 0.355 | 6.40e-4 | 1 | 0.312 | 0.0067 | 16 |
| scan: Exod 28:14 w10 to Exod 28:25 w16 | 0.586 | 6.40e-4 | 0 | - | - | 0 |
| scan: Lev 4:34 w1 to Lev 5:10 w13 | 0.352 | 6.40e-4 | 1 | 0.147 | 0.0261 | 27 |
| scan: Deut 20:2 w5 to Deut 20:11 w15 | 0.613 | 6.40e-4 | 1 | 0.140 | 0.2400 | 12 |
| scan: Judg 7:6 w10 to Judg 7:14 w13 | 0.437 | 6.40e-4 | 1 | 0.098 | 0.2071 | 7 |
| scan: Judg 11:32 w8 to Judg 12:3 w21 | 0.406 | 6.40e-4 | 1 | 0.281 | 0.0036 | 25 |
| scan: 1Sam 24:5 w8 to 1Sam 24:12 w7 | 0.524 | 6.40e-4 | 1 | 0.368 | 0.0055 | 4 |
| scan: 1Chr 1:48 w3 to 1Chr 2:6 w9 | 0.837 | 6.40e-4 | 1 | 0.413 | 0.1333 | 33 |
| scan: 2Chr 30:3 w7 to 2Chr 30:15 w6 | 0.381 | 6.40e-4 | 1 | 0.294 | 0.0191 | 16 |
| scan: 2Chr 33:4 w1 to 2Chr 33:16 w9 | 0.286 | 6.40e-4 | 1 | 0.157 | 0.0318 | 23 |
| scan: Ezra 3:7 w5 to Ezra 4:4 w7 | 0.447 | 6.40e-4 | 1 | 0.331 | 0.0090 | 23 |
| scan: Isa 45:24 w1 to Isa 46:11 w7 | 0.759 | 6.40e-4 | 1 | -0.174 | 0.7165 | 23 |
| scan: Lam 2:6 w1 to Lam 2:17 w19 | 0.450 | 6.40e-4 | 1 | 0.414 | 0.0011 | 29 |
| scan: Lam 2:6 w6 to Lam 2:17 w19 | 0.450 | 6.40e-4 | 1 | 0.261 | 0.0215 | 29 |
| scan: Ezek 47:18 w1 to Ezek 48:4 w10 | 0.332 | 6.40e-4 | 1 | 0.155 | 0.0488 | 18 |
| scan: Exod 2:9 w1 to Exod 2:17 w3 | 0.578 | 6.50e-4 | 1 | 0.297 | 0.0415 | 9 |
| scan: Exod 10:24 w14 to Exod 11:4 w11 | 0.479 | 6.50e-4 | 1 | 0.078 | 0.2864 | 8 |
| scan: Num 1:3 w9 to Num 1:16 w10 | 0.397 | 6.50e-4 | 1 | 0.269 | 0.0015 | 22 |
| scan: Num 6:27 w7 to Num 7:12 w11 | 0.403 | 6.50e-4 | 1 | 0.251 | 0.0077 | 15 |
| scan: Deut 13:14 w1 to Deut 14:7 w10 | 0.491 | 6.50e-4 | 1 | 0.665 | 0.0111 | 34 |
| scan: Josh 1:18 w1 to Josh 2:11 w19 | 0.350 | 6.50e-4 | 1 | 0.409 | 0.0030 | 19 |
| scan: Judg 7:5 w6 to Judg 7:15 w9 | 0.299 | 6.50e-4 | 1 | 0.003 | 0.4844 | 9 |
| scan: 1Kgs 17:24 w1 to 1Kgs 18:10 w15 | 0.406 | 6.50e-4 | 1 | 0.085 | 0.1957 | 18 |
| scan: 2Kgs 8:27 w11 to 2Kgs 9:10 w8 | 0.444 | 6.50e-4 | 1 | 0.107 | 0.1666 | 47 |
| scan: 2Kgs 8:29 w1 to 2Kgs 9:10 w8 | 0.548 | 6.50e-4 | 1 | -0.163 | 0.8277 | 40 |
| scan: 1Chr 27:29 w1 to 1Chr 28:5 w8 | 0.364 | 6.50e-4 | 1 | -0.367 | 0.9715 | 28 |
| scan: 1Chr 28:9 w1 to 1Chr 28:21 w8 | 0.387 | 6.50e-4 | 1 | 0.067 | 0.2545 | 19 |
| scan: 2Chr 28:17 w1 to 2Chr 28:25 w9 | 0.622 | 6.50e-4 | 1 | 0.438 | 0.0039 | 16 |
| scan: Song 5:2 w5 to Song 5:12 w10 | 0.394 | 6.50e-4 | 1 | 1.000 | 0.1667 | 26 |
| scan: Ezek 2:5 w10 to Ezek 3:7 w11 | 0.238 | 6.50e-4 | 1 | 0.431 | 3.20e-4 | 11 |
| scan: Ezek 19:11 w13 to Ezek 20:9 w17 | 0.436 | 6.50e-4 | 1 | 0.477 | 8.90e-4 | 11 |
| scan: Ezek 36:17 w12 to Ezek 36:29 w4 | 0.435 | 6.50e-4 | 1 | 0.346 | 0.0654 | 19 |
| scan: Ezek 45:6 w14 to Ezek 45:18 w15 | 0.424 | 6.50e-4 | 1 | 0.170 | 0.0706 | 23 |
| scan: Amos 2:9 w13 to Amos 3:5 w8 | 0.673 | 6.50e-4 | 1 | 0.557 | 0.0162 | 20 |
| scan: Obad 1:8 w6 to Obad 1:18 w13 | 0.520 | 6.50e-4 | 1 | 0.508 | 0.0069 | 24 |
| scan: Gen 14:24 w11 to Gen 15:12 w7 | 0.397 | 6.60e-4 | 1 | 0.528 | 8.00e-4 | 19 |
| scan: Exod 29:36 w1 to Exod 29:44 w13 | 0.590 | 6.60e-4 | 1 | 0.556 | 0.0119 | 25 |
| scan: Lev 4:3 w7 to Lev 4:10 w5 | 0.412 | 6.60e-4 | 1 | 0.181 | 0.0732 | 18 |
| scan: Lev 21:12 w10 to Lev 21:24 w10 | 0.437 | 6.60e-4 | 1 | 0.341 | 0.0104 | 13 |
| scan: Lev 21:22 w5 to Lev 22:10 w11 | 0.312 | 6.60e-4 | 1 | 0.276 | 0.0037 | 13 |
| scan: Lev 24:16 w1 to Lev 24:23 w14 | 0.734 | 6.60e-4 | 1 | 0.690 | 3.10e-4 | 7 |
| scan: Num 28:21 w1 to Num 28:29 w4 | 0.601 | 6.60e-4 | 1 | 0.477 | 0.0155 | 15 |
| scan: Deut 19:11 w1 to Deut 19:21 w13 | 0.565 | 6.60e-4 | 1 | 0.362 | 0.0902 | 9 |
| scan: Deut 21:21 w1 to Deut 22:6 w21 | 0.544 | 6.60e-4 | 1 | 0.429 | 0.0483 | 11 |
| scan: Josh 15:7 w1 to Josh 15:17 w12 | 0.455 | 6.60e-4 | 1 | -0.125 | 0.8750 | 46 |
| scan: Judg 1:20 w1 to Judg 1:31 w19 | 0.568 | 6.60e-4 | 1 | 0.449 | 5.10e-4 | 37 |
| scan: Judg 1:20 w8 to Judg 1:31 w9 | 0.568 | 6.60e-4 | 1 | 0.449 | 5.10e-4 | 37 |
| scan: Judg 1:21 w1 to Judg 1:29 w11 | 0.792 | 6.60e-4 | 1 | 0.563 | 4.60e-4 | 25 |
| scan: 1Sam 3:10 w9 to 1Sam 3:19 w2 | 0.271 | 6.60e-4 | 1 | 0.054 | 0.2791 | 7 |
| scan: 1Sam 15:32 w13 to 1Sam 16:4 w16 | 0.369 | 6.60e-4 | 1 | 0.072 | 0.2356 | 8 |
| scan: 1Sam 28:13 w9 to 1Sam 28:21 w8 | 0.579 | 6.60e-4 | 1 | 0.349 | 0.0084 | 7 |
| scan: 1Sam 30:30 w1 to 1Sam 31:7 w25 | 0.352 | 6.60e-4 | 1 | 0.329 | 0.0385 | 12 |
| scan: 1Kgs 6:21 w1 to 1Kgs 6:31 w10 | 0.437 | 6.60e-4 | 1 | 0.484 | 0.0014 | 17 |
| scan: 1Kgs 17:23 w11 to 1Kgs 18:8 w3 | 0.409 | 6.60e-4 | 1 | 0.078 | 0.1840 | 16 |
| scan: 2Kgs 4:9 w12 to 2Kgs 4:21 w6 | 0.348 | 6.60e-4 | 1 | 0.298 | 0.0122 | 10 |
| scan: 2Kgs 9:32 w9 to 2Kgs 10:4 w10 | 0.672 | 6.60e-4 | 1 | 0.460 | 0.0214 | 12 |
| scan: 1Chr 5:5 w1 to 1Chr 5:15 w8 | 0.723 | 6.60e-4 | 1 | 0.110 | 0.0818 | 31 |
| scan: 2Chr 11:16 w13 to 2Chr 12:1 w9 | 0.439 | 6.60e-4 | 1 | 0.502 | 0.0022 | 16 |
| scan: Neh 6:6 w16 to Neh 6:15 w5 | 0.472 | 6.60e-4 | 1 | 0.724 | 0.0011 | 17 |
| scan: Isa 50:1 w18 to Isa 50:10 w18 | 0.567 | 6.60e-4 | 1 | 0.189 | 0.1699 | 7 |
| scan: Jer 37:1 w6 to Jer 37:13 w13 | 0.533 | 6.60e-4 | 1 | 0.216 | 0.0528 | 12 |
| scan: Jer 51:18 w5 to Jer 51:26 w13 | 0.564 | 6.60e-4 | 1 | 0.123 | 0.0400 | 6 |
| scan: Ezek 4:13 w10 to Ezek 5:7 w24 | 0.538 | 6.60e-4 | 1 | -0.356 | 0.9411 | 24 |
| scan: Ezek 36:16 w1 to Ezek 36:27 w12 | 0.409 | 6.60e-4 | 1 | 0.496 | 0.0116 | 18 |
| scan: Zech 5:7 w5 to Zech 6:8 w5 | 0.437 | 6.60e-4 | 1 | 0.182 | 0.0581 | 14 |
| scan: Gen 44:27 w1 to Gen 45:4 w8 | 0.286 | 6.70e-4 | 1 | 0.235 | 0.0536 | 8 |
| scan: Exod 37:16 w18 to Exod 37:26 w11 | 0.578 | 6.70e-4 | 0 | - | - | 0 |
| scan: Deut 19:11 w13 to Deut 19:21 w13 | 0.600 | 6.70e-4 | 1 | 0.362 | 0.0902 | 9 |
| scan: Deut 22:26 w9 to Deut 23:6 w7 | 0.381 | 6.70e-4 | 1 | -0.222 | 1.0000 | 10 |
| scan: Josh 11:16 w19 to Josh 12:3 w14 | 0.410 | 6.70e-4 | 1 | 0.153 | 0.0749 | 36 |
| scan: Josh 11:17 w1 to Josh 12:5 w10 | 0.433 | 6.70e-4 | 1 | 0.503 | 1.88e-5 | 44 |
| scan: Judg 1:20 w1 to Judg 1:30 w9 | 0.634 | 6.70e-4 | 1 | 0.371 | 0.0044 | 30 |
| scan: 1Kgs 7:46 w1 to 1Kgs 8:2 w13 | 0.585 | 6.70e-4 | 1 | 0.680 | 0.0046 | 13 |
| scan: 1Kgs 14:20 w8 to 1Kgs 14:31 w17 | 0.320 | 6.70e-4 | 0 | - | - | 0 |
| scan: 1Chr 12:13 w1 to 1Chr 12:25 w9 | 0.345 | 6.70e-4 | 1 | 0.230 | 0.0529 | 23 |
| scan: 1Chr 18:14 w6 to 1Chr 19:8 w9 | 0.287 | 6.70e-4 | 1 | 0.105 | 0.1380 | 35 |
| scan: Isa 2:8 w4 to Isa 2:20 w17 | 0.550 | 6.70e-4 | 1 | 0.295 | 0.0333 | 16 |
| scan: Isa 2:12 w9 to Isa 3:2 w7 | 0.834 | 6.70e-4 | 1 | 0.106 | 0.3417 | 19 |
| scan: Ezek 9:6 w18 to Ezek 10:5 w11 | 0.430 | 6.70e-4 | 1 | -0.097 | 0.7909 | 12 |
| scan: Ezek 20:1 w1 to Ezek 20:13 w21 | 0.383 | 6.70e-4 | 1 | 0.625 | 1.10e-4 | 12 |
| scan: Amos 2:13 w5 to Amos 3:8 w5 | 0.435 | 6.70e-4 | 1 | 0.711 | 0.0333 | 16 |
| scan: Amos 2:14 w1 to Amos 3:8 w5 | 0.435 | 6.70e-4 | 1 | 0.711 | 0.0333 | 14 |
| scan: Mic 7:2 w8 to Mic 7:13 w7 | 0.763 | 6.70e-4 | 1 | 0.668 | 0.0102 | 25 |
| scan: Mic 7:3 w1 to Mic 7:13 w5 | 0.763 | 6.70e-4 | 1 | 0.582 | 0.0401 | 20 |
| scan: Zech 12:9 w1 to Zech 13:4 w14 | 0.620 | 6.70e-4 | 1 | 0.154 | 0.2508 | 17 |
| scan: Mal 2:11 w7 to Mal 3:3 w17 | 0.497 | 6.70e-4 | 1 | 0.269 | 0.0537 | 12 |
| scan: Gen 1:29 w1 to Gen 2:7 w12 | 0.395 | 6.80e-4 | 1 | 0.333 | 3.00e-4 | 3 |
| scan: Gen 22:17 w1 to Gen 23:4 w12 | 0.633 | 6.80e-4 | 1 | 0.364 | 0.0083 | 19 |
| scan: Exod 3:16 w18 to Exod 4:3 w7 | 0.486 | 6.80e-4 | 1 | 0.094 | 0.2812 | 15 |
| scan: Exod 10:16 w6 to Exod 10:26 w14 | 0.524 | 6.80e-4 | 1 | -0.042 | 0.6054 | 8 |
| scan: Exod 29:34 w1 to Exod 29:45 w7 | 0.519 | 6.80e-4 | 1 | 0.427 | 0.0097 | 30 |
| scan: Exod 37:16 w18 to Exod 37:24 w5 | 0.505 | 6.80e-4 | 0 | - | - | 0 |
| scan: Exod 40:8 w1 to Exod 40:18 w16 | 0.497 | 6.80e-4 | 1 | -0.058 | 0.6528 | 14 |
| scan: Num 26:49 w1 to Num 26:61 w3 | 0.595 | 6.80e-4 | 1 | 0.226 | 0.0643 | 31 |
| scan: Num 33:34 w1 to Num 33:42 w4 | 0.555 | 6.80e-4 | 1 | 0.000 | 1.0000 | 38 |
| scan: Deut 21:11 w1 to Deut 21:21 w9 | 0.512 | 6.80e-4 | 1 | 0.684 | 0.1597 | 19 |
| scan: Deut 21:11 w6 to Deut 21:20 w13 | 0.512 | 6.80e-4 | 1 | 0.684 | 0.1597 | 17 |
| scan: Deut 21:12 w1 to Deut 21:20 w11 | 0.512 | 6.80e-4 | 1 | 0.684 | 0.1597 | 16 |
| scan: Josh 24:6 w1 to Josh 24:17 w12 | 0.434 | 6.80e-4 | 1 | 0.072 | 0.2723 | 21 |
| scan: Judg 1:21 w1 to Judg 1:30 w14 | 0.728 | 6.80e-4 | 1 | 0.598 | 7.90e-6 | 27 |
| scan: 1Sam 14:12 w1 to 1Sam 14:23 w6 | 0.281 | 6.80e-4 | 1 | -0.014 | 0.5465 | 20 |
| scan: 1Kgs 6:21 w8 to 1Kgs 6:30 w5 | 0.496 | 6.80e-4 | 1 | 0.575 | 2.20e-4 | 14 |
| scan: 1Kgs 8:14 w1 to 1Kgs 8:24 w15 | 0.317 | 6.80e-4 | 1 | 0.100 | 0.1397 | 1 |
| scan: 2Kgs 7:7 w1 to 2Kgs 7:14 w4 | 0.491 | 6.80e-4 | 1 | 0.302 | 0.0768 | 7 |
| scan: 2Kgs 18:1 w1 to 2Kgs 18:10 w15 | 0.390 | 6.80e-4 | 1 | 0.268 | 0.0176 | 18 |
| scan: 2Kgs 22:17 w12 to 2Kgs 23:9 w9 | 0.220 | 6.80e-4 | 1 | -0.161 | 0.9488 | 21 |
| scan: 1Chr 5:4 w3 to 1Chr 5:15 w8 | 0.678 | 6.80e-4 | 1 | 0.066 | 0.1341 | 33 |
| scan: Neh 7:20 w1 to Neh 7:40 w5 | 0.137 | 6.80e-4 | 1 | 0.185 | 0.0207 | 45 |
| scan: Jer 12:7 w1 to Jer 12:15 w11 | 0.553 | 6.80e-4 | 1 | 0.604 | 0.0667 | 15 |
| scan: Jer 25:15 w15 to Jer 25:28 w7 | 0.389 | 6.80e-4 | 0 | - | - | 0 |
| scan: Zech 8:15 w12 to Zech 9:2 w4 | 0.287 | 6.80e-4 | 1 | 0.259 | 0.0133 | 10 |
| scan: Zech 8:16 w1 to Zech 9:1 w14 | 0.287 | 6.80e-4 | 1 | 0.228 | 0.0222 | 7 |
| scan: Gen 34:27 w1 to Gen 35:5 w13 | 0.332 | 6.90e-4 | 1 | 0.324 | 0.0385 | 16 |
| scan: Exod 29:39 w6 to Exod 30:3 w11 | 0.691 | 6.90e-4 | 1 | 0.630 | 1.70e-4 | 25 |
| scan: Lev 25:17 w1 to Lev 25:25 w5 | 0.523 | 6.90e-4 | 1 | 0.670 | 0.0053 | 12 |
| scan: Num 8:2 w6 to Num 8:11 w15 | 0.559 | 6.90e-4 | 1 | 0.209 | 0.1697 | 11 |
| scan: Num 12:16 w5 to Num 13:16 w15 | 0.245 | 6.90e-4 | 1 | 0.174 | 0.0052 | 30 |
| scan: Josh 11:21 w22 to Josh 12:7 w26 | 0.565 | 6.90e-4 | 1 | 0.410 | 7.10e-4 | 40 |
| scan: 1Sam 12:1 w13 to 1Sam 12:13 w7 | 0.356 | 6.90e-4 | 1 | 0.445 | 3.80e-6 | 18 |
| scan: 1Sam 28:11 w7 to 1Sam 28:22 w12 | 0.389 | 6.90e-4 | 1 | 0.362 | 5.60e-4 | 9 |
| scan: 2Sam 3:35 w1 to 2Sam 4:7 w21 | 0.316 | 6.90e-4 | 1 | 0.244 | 0.0212 | 37 |
| scan: 1Kgs 2:36 w13 to 1Kgs 2:43 w6 | 0.380 | 6.90e-4 | 1 | 0.227 | 0.0115 | 12 |
| scan: 1Kgs 3:15 w1 to 1Kgs 3:25 w14 | 0.392 | 6.90e-4 | 1 | 0.010 | 0.4756 | 7 |
| scan: 1Chr 18:13 w9 to 1Chr 19:4 w13 | 0.308 | 6.90e-4 | 1 | 0.335 | 0.0245 | 24 |
| scan: 1Chr 20:1 w1 to 1Chr 21:4 w5 | 0.356 | 6.90e-4 | 1 | 0.343 | 0.0163 | 49 |
| scan: 2Chr 1:10 w11 to 2Chr 2:5 w10 | 0.342 | 6.90e-4 | 1 | 0.312 | 0.0119 | 12 |
| scan: 2Chr 30:4 w1 to 2Chr 30:14 w13 | 0.384 | 6.90e-4 | 1 | 0.300 | 0.0422 | 11 |
| scan: Isa 49:4 w1 to Isa 49:15 w12 | 0.604 | 6.90e-4 | 1 | 0.330 | 0.0139 | 11 |
| scan: Isa 49:5 w1 to Isa 49:15 w6 | 0.647 | 6.90e-4 | 1 | 0.355 | 0.0175 | 9 |
| scan: Isa 66:11 w1 to Isa 66:19 w30 | 0.590 | 6.90e-4 | 1 | 0.328 | 0.0565 | 20 |
| scan: Jer 1:6 w9 to Jer 1:17 w11 | 0.322 | 6.90e-4 | 1 | 0.138 | 0.0944 | 12 |
| scan: Ezek 2:7 w1 to Ezek 3:8 w12 | 0.268 | 6.90e-4 | 1 | 0.271 | 0.0183 | 10 |
| scan: Ezek 14:22 w1 to Ezek 16:3 w14 | 0.487 | 6.90e-4 | 1 | 0.353 | 0.0128 | 17 |
| scan: Ezek 48:19 w1 to Ezek 48:30 w10 | 0.316 | 6.90e-4 | 1 | 0.138 | 0.0411 | 11 |
| scan: Zech 2:12 w9 to Zech 3:8 w13 | 0.355 | 6.90e-4 | 1 | 0.160 | 0.1653 | 10 |
| scan: Mal 2:11 w1 to Mal 3:4 w5 | 0.420 | 6.90e-4 | 1 | 0.371 | 0.0024 | 13 |
| scan: Gen 25:22 w10 to Gen 25:32 w6 | 0.414 | 7.00e-4 | 1 | 0.409 | 0.0034 | 14 |
| scan: Gen 30:9 w6 to Gen 30:19 w7 | 0.280 | 7.00e-4 | 1 | 0.084 | 0.1042 | 13 |
| scan: Gen 38:8 w1 to Gen 38:17 w7 | 0.447 | 7.00e-4 | 1 | 0.208 | 0.1146 | 19 |
| scan: Gen 43:12 w1 to Gen 43:23 w19 | 0.331 | 7.00e-4 | 1 | 0.348 | 0.0038 | 18 |
| scan: Gen 43:16 w1 to Gen 43:27 w9 | 0.388 | 7.00e-4 | 1 | 0.181 | 0.0926 | 15 |
| scan: Exod 2:6 w1 to Exod 2:13 w8 | 0.550 | 7.00e-4 | 1 | 0.255 | 0.1355 | 8 |
| scan: Exod 26:7 w1 to Exod 26:14 w10 | 0.229 | 7.00e-4 | 1 | 0.441 | 0.0154 | 34 |
| scan: Exod 29:32 w11 to Exod 29:42 w15 | 0.649 | 7.00e-4 | 1 | 0.434 | 0.0316 | 30 |
| scan: Num 13:1 w1 to Num 13:16 w15 | 0.272 | 7.00e-4 | 1 | 0.195 | 0.0046 | 27 |
| scan: Num 34:1 w1 to Num 34:13 w6 | 0.203 | 7.00e-4 | 1 | 0.085 | 0.0619 | 25 |
| scan: Josh 4:23 w11 to Josh 5:6 w38 | 0.380 | 7.00e-4 | 1 | 0.550 | 7.80e-4 | 18 |
| scan: Judg 1:19 w8 to Judg 1:28 w8 | 0.794 | 7.00e-4 | 1 | 0.293 | 0.0211 | 29 |
| scan: Judg 5:2 w6 to Judg 5:10 w10 | 0.715 | 7.00e-4 | 1 | 0.155 | 0.1683 | 20 |
| scan: 1Sam 17:8 w1 to 1Sam 17:19 w10 | 0.400 | 7.00e-4 | 0 | - | - | 0 |
| scan: 1Sam 23:22 w1 to 1Sam 23:28 w15 | 0.374 | 7.00e-4 | 1 | 0.190 | 0.1209 | 9 |
| scan: 1Kgs 20:30 w14 to 1Kgs 20:40 w15 | 0.271 | 7.00e-4 | 1 | 0.032 | 0.3564 | 16 |
| scan: 2Kgs 14:19 w7 to 2Kgs 15:1 w13 | 0.305 | 7.00e-4 | 1 | 0.278 | 0.0097 | 30 |
| scan: 2Kgs 17:26 w1 to 2Kgs 17:34 w27 | 0.321 | 7.00e-4 | 1 | 0.103 | 0.2108 | 25 |
| scan: 1Chr 22:10 w1 to 1Chr 23:1 w4 | 0.464 | 7.00e-4 | 1 | 0.412 | 8.87e-5 | 7 |
| scan: Neh 2:8 w24 to Neh 2:19 w23 | 0.492 | 7.00e-4 | 1 | 0.264 | 0.0180 | 17 |
| scan: Eccl 2:24 w1 to Eccl 3:12 w5 | 0.486 | 7.00e-4 | 1 | 0.421 | 9.80e-6 | 11 |
| scan: Isa 59:2 w1 to Isa 59:12 w7 | 0.727 | 7.00e-4 | 1 | -0.021 | 0.5473 | 15 |
| scan: Jer 14:14 w15 to Jer 15:3 w12 | 0.359 | 7.00e-4 | 1 | -0.117 | 0.8544 | 20 |
| scan: Ezek 22:15 w1 to Ezek 22:27 w5 | 0.418 | 7.00e-4 | 1 | -0.028 | 0.5978 | 26 |
| scan: Ezek 43:8 w1 to Ezek 43:19 w14 | 0.818 | 7.00e-4 | 1 | 0.537 | 0.0435 | 35 |
| scan: Ezek 45:6 w14 to Ezek 45:17 w13 | 0.475 | 7.00e-4 | 1 | 0.187 | 0.0813 | 21 |
| scan: Zech 12:8 w14 to Zech 13:5 w12 | 0.583 | 7.00e-4 | 1 | 0.023 | 0.4443 | 18 |
| scan: Gen 24:46 w1 to Gen 24:54 w7 | 0.741 | 7.10e-4 | 1 | 0.384 | 0.0249 | 4 |
| scan: Gen 37:27 w1 to Gen 38:2 w8 | 0.554 | 7.10e-4 | 1 | 0.448 | 0.0067 | 17 |
| scan: Exod 14:8 w1 to Exod 14:17 w8 | 0.414 | 7.10e-4 | 1 | 0.251 | 0.0333 | 15 |
| scan: Exod 19:2 w8 to Exod 19:13 w21 | 0.266 | 7.10e-4 | 1 | 0.361 | 0.0021 | 9 |
| scan: Exod 24:12 w10 to Exod 25:2 w16 | 0.259 | 7.10e-4 | 1 | 0.174 | 0.0987 | 5 |
| scan: Exod 28:12 w12 to Exod 28:22 w9 | 0.548 | 7.10e-4 | 1 | -0.087 | 0.6977 | 41 |
| scan: Lev 19:17 w1 to Lev 19:26 w8 | 0.534 | 7.10e-4 | 1 | -0.545 | 0.9611 | 28 |
| scan: Lev 25:18 w1 to Lev 25:25 w13 | 0.523 | 7.10e-4 | 1 | 0.643 | 0.0016 | 12 |
| scan: Lev 25:18 w9 to Lev 25:25 w5 | 0.523 | 7.10e-4 | 1 | 0.643 | 0.0016 | 12 |
| scan: Num 1:2 w11 to Num 1:18 w12 | 0.426 | 7.10e-4 | 1 | 0.575 | 5.40e-6 | 29 |
| scan: Num 8:12 w8 to Num 8:24 w3 | 0.254 | 7.10e-4 | 1 | 0.253 | 8.50e-4 | 15 |
| scan: Num 12:16 w5 to Num 13:17 w15 | 0.284 | 7.10e-4 | 1 | 0.255 | 3.00e-4 | 31 |
| scan: Num 33:32 w4 to Num 33:44 w2 | 0.405 | 7.10e-4 | 1 | 0.000 | 0.7778 | 55 |
| scan: Deut 5:15 w1 to Deut 5:25 w8 | 0.492 | 7.10e-4 | 1 | 0.174 | 0.0782 | 6 |
| scan: Deut 13:15 w9 to Deut 14:6 w13 | 0.557 | 7.10e-4 | 1 | 0.160 | 0.1667 | 22 |
| scan: Deut 22:27 w4 to Deut 23:6 w7 | 0.314 | 7.10e-4 | 1 | -0.363 | 1.0000 | 9 |
| scan: Deut 31:9 w16 to Deut 31:21 w17 | 0.345 | 7.10e-4 | 1 | 0.154 | 0.0862 | 20 |
| scan: Josh 2:6 w4 to Josh 2:16 w18 | 0.618 | 7.10e-4 | 1 | 0.595 | 0.0051 | 14 |
| scan: 1Kgs 6:24 w11 to 1Kgs 6:34 w14 | 0.453 | 7.10e-4 | 1 | 0.469 | 0.0162 | 17 |
| scan: 1Kgs 7:45 w18 to 1Kgs 8:3 w4 | 0.581 | 7.10e-4 | 1 | 0.376 | 0.0034 | 18 |
| scan: 1Kgs 18:23 w1 to 1Kgs 18:33 w10 | 0.407 | 7.10e-4 | 1 | 0.079 | 0.2487 | 25 |
| scan: 1Chr 6:59 w1 to 1Chr 6:68 w9 | 0.421 | 7.10e-4 | 1 | 0.027 | 0.2767 | 29 |
| scan: 1Chr 24:5 w1 to 1Chr 24:22 w5 | 0.652 | 7.10e-4 | 1 | 0.440 | 0.0083 | 33 |
| scan: 1Chr 25:4 w2 to 1Chr 25:13 w6 | 0.469 | 7.10e-4 | 1 | 0.048 | 0.2500 | 30 |
| scan: 1Chr 27:27 w5 to 1Chr 28:5 w18 | 0.396 | 7.10e-4 | 1 | -0.367 | 0.9715 | 33 |
| scan: Esth 6:8 w1 to Esth 7:2 w20 | 0.246 | 7.10e-4 | 0 | - | - | 0 |
| scan: Esth 6:13 w1 to Esth 7:10 w8 | 0.178 | 7.10e-4 | 0 | - | - | 0 |
| scan: Ezek 9:7 w1 to Ezek 10:5 w11 | 0.486 | 7.10e-4 | 1 | 0.271 | 0.0364 | 12 |
| scan: Ezek 14:22 w16 to Ezek 16:3 w14 | 0.496 | 7.10e-4 | 1 | 0.353 | 0.0128 | 17 |
| scan: Exod 2:9 w1 to Exod 2:15 w19 | 0.617 | 7.20e-4 | 1 | 0.497 | 0.0029 | 7 |
| scan: Lev 13:27 w1 to Lev 13:38 w10 | 0.162 | 7.20e-4 | 1 | 0.054 | 0.2334 | 45 |
| scan: Deut 4:12 w1 to Deut 4:23 w11 | 0.386 | 7.20e-4 | 1 | 0.121 | 0.1102 | 9 |
| scan: Deut 27:1 w1 to Deut 27:11 w7 | 0.423 | 7.20e-4 | 1 | 0.339 | 0.0048 | 9 |
| scan: Josh 11:21 w1 to Josh 12:7 w26 | 0.478 | 7.20e-4 | 1 | 0.439 | 1.80e-4 | 40 |
| scan: 1Sam 4:20 w11 to 1Sam 5:8 w19 | 0.342 | 7.20e-4 | 1 | 0.210 | 0.0291 | 35 |
| scan: 1Sam 22:21 w4 to 1Sam 23:8 w6 | 0.257 | 7.20e-4 | 1 | 0.258 | 0.0060 | 19 |
| scan: 2Sam 18:3 w1 to 2Sam 18:12 w31 | 0.386 | 7.20e-4 | 1 | 0.252 | 0.0368 | 37 |
| scan: 2Sam 19:27 w1 to 2Sam 19:38 w17 | 0.204 | 7.20e-4 | 1 | 0.154 | 0.0137 | 19 |
| scan: 1Chr 25:2 w1 to 1Chr 25:9 w5 | 0.552 | 7.20e-4 | 1 | 0.091 | 0.3611 | 36 |
| scan: 1Chr 27:15 w1 to 1Chr 27:26 w6 | 0.252 | 7.20e-4 | 1 | 0.446 | 0.1149 | 32 |
| scan: 2Chr 29:17 w1 to 2Chr 29:28 w7 | 0.357 | 7.20e-4 | 1 | 0.165 | 0.0496 | 23 |
| scan: Esth 6:12 w6 to Esth 7:9 w25 | 0.184 | 7.20e-4 | 0 | - | - | 0 |
| scan: Eccl 11:3 w14 to Eccl 12:3 w7 | 0.476 | 7.20e-4 | 1 | 0.021 | 0.4748 | 16 |
| scan: Isa 2:9 w5 to Isa 2:21 w5 | 0.627 | 7.20e-4 | 1 | 0.106 | 0.2759 | 19 |
| scan: Isa 10:5 w1 to Isa 10:16 w13 | 0.380 | 7.20e-4 | 1 | 0.522 | 0.0012 | 20 |
| scan: Isa 30:13 w11 to Isa 30:20 w16 | 0.607 | 7.20e-4 | 1 | 0.720 | 0.1111 | 14 |
| scan: Isa 30:14 w1 to Isa 30:20 w16 | 0.607 | 7.20e-4 | 1 | 0.720 | 0.1111 | 12 |
| scan: Jer 28:15 w1 to Jer 29:9 w10 | 0.443 | 7.20e-4 | 1 | 0.088 | 0.3845 | 18 |
| scan: Ezek 2:7 w1 to Ezek 3:6 w19 | 0.303 | 7.20e-4 | 1 | 0.326 | 0.0141 | 8 |
| scan: Ezek 43:2 w8 to Ezek 43:14 w10 | 0.531 | 7.20e-4 | 1 | 0.533 | 2.80e-4 | 31 |
| scan: Ezek 43:10 w1 to Ezek 43:21 w9 | 0.380 | 7.20e-4 | 1 | 0.230 | 0.0061 | 32 |
| scan: Zech 12:9 w4 to Zech 13:3 w22 | 0.608 | 7.20e-4 | 1 | 0.496 | 4.80e-4 | 14 |
| scan: Gen 2:9 w1 to Gen 2:18 w8 | 0.550 | 7.30e-4 | 1 | 0.082 | 0.3206 | 9 |
| scan: Exod 15:10 w1 to Exod 15:19 w19 | 0.864 | 7.30e-4 | 1 | 0.891 | 2.92e-5 | 14 |
| scan: Exod 25:30 w1 to Exod 25:40 w2 | 0.534 | 7.30e-4 | 1 | 0.298 | 0.0911 | 36 |
| scan: Exod 30:7 w1 to Exod 30:19 w8 | 0.340 | 7.30e-4 | 1 | 0.430 | 0.0103 | 19 |
| scan: Lev 13:27 w5 to Lev 13:38 w10 | 0.175 | 7.30e-4 | 1 | 0.044 | 0.2815 | 45 |
| scan: Deut 22:27 w1 to Deut 23:6 w7 | 0.367 | 7.30e-4 | 1 | -0.363 | 1.0000 | 9 |
| scan: Josh 4:12 w1 to Josh 4:23 w21 | 0.418 | 7.30e-4 | 1 | 0.197 | 0.0404 | 14 |
| scan: Judg 1:18 w1 to Judg 1:29 w11 | 0.484 | 7.30e-4 | 1 | 0.279 | 0.0139 | 36 |
| scan: 1Kgs 1:48 w1 to 1Kgs 2:6 w2 | 0.367 | 7.30e-4 | 1 | 0.179 | 0.1314 | 15 |
| scan: 1Kgs 8:13 w6 to 1Kgs 8:23 w12 | 0.341 | 7.30e-4 | 0 | - | - | 0 |
| scan: 1Kgs 9:23 w11 to 1Kgs 10:6 w9 | 0.385 | 7.30e-4 | 0 | - | - | 0 |
| scan: 2Kgs 2:23 w5 to 2Kgs 3:8 w9 | 0.612 | 7.30e-4 | 1 | 0.619 | 2.10e-4 | 25 |
| scan: 1Chr 5:26 w21 to 1Chr 6:16 w5 | 0.338 | 7.30e-4 | 1 | 0.097 | 1.90e-4 | 47 |
| scan: 1Chr 6:26 w1 to 1Chr 6:37 w8 | 0.423 | 7.30e-4 | 1 | -0.001 | 0.6090 | 27 |
| scan: Neh 1:8 w1 to Neh 2:5 w19 | 0.339 | 7.30e-4 | 1 | 0.226 | 0.2725 | 13 |
| scan: Isa 7:22 w1 to Isa 8:9 w7 | 0.531 | 7.30e-4 | 1 | 0.197 | 0.2438 | 29 |
| scan: Jer 51:16 w1 to Jer 51:26 w7 | 0.784 | 7.30e-4 | 1 | 0.360 | 0.0012 | 10 |
| scan: Ezek 3:4 w1 to Ezek 3:11 w19 | 0.540 | 7.30e-4 | 1 | 0.150 | 0.2585 | 8 |
| scan: Ezek 5:1 w17 to Ezek 5:11 w16 | 0.512 | 7.30e-4 | 1 | 0.252 | 0.1088 | 18 |
| scan: Ezek 32:2 w1 to Ezek 32:13 w7 | 0.436 | 7.30e-4 | 1 | 0.477 | 0.0024 | 13 |
| scan: Gen 19:16 w1 to Gen 19:23 w4 | 0.507 | 7.40e-4 | 1 | -0.686 | 0.9340 | 7 |
| scan: Gen 40:20 w12 to Gen 41:9 w6 | 0.586 | 7.40e-4 | 1 | 0.556 | 0.0017 | 19 |
| scan: Exod 29:33 w1 to Exod 29:42 w15 | 0.541 | 7.40e-4 | 1 | 0.491 | 0.0035 | 27 |
| scan: Josh 18:14 w1 to Josh 18:21 w11 | 0.375 | 7.40e-4 | 1 | 0.260 | 0.0068 | 28 |
| scan: 2Sam 18:2 w1 to 2Sam 18:12 w17 | 0.343 | 7.40e-4 | 1 | -0.067 | 0.7088 | 42 |
| scan: 1Kgs 7:25 w21 to 1Kgs 7:34 w10 | 0.478 | 7.40e-4 | 1 | 0.095 | 0.4222 | 27 |
| scan: 1Chr 13:12 w1 to 1Chr 14:11 w15 | 0.289 | 7.40e-4 | 1 | 0.267 | 4.90e-4 | 24 |
| scan: 1Chr 27:22 w5 to 1Chr 27:33 w3 | 0.325 | 7.40e-4 | 1 | 0.504 | 0.0297 | 36 |
| scan: 1Chr 28:13 w9 to 1Chr 28:20 w27 | 0.424 | 7.40e-4 | 1 | 0.339 | 0.1051 | 13 |
| scan: 2Chr 34:8 w8 to 2Chr 34:16 w12 | 0.439 | 7.40e-4 | 1 | -0.043 | 0.6405 | 31 |
| scan: Esth 6:3 w10 to Esth 7:1 w7 | 0.192 | 7.40e-4 | 0 | - | - | 0 |
| scan: Esth 6:12 w6 to Esth 7:9 w29 | 0.177 | 7.40e-4 | 0 | - | - | 0 |
| scan: Isa 11:9 w1 to Isa 12:3 w5 | 0.394 | 7.40e-4 | 1 | 0.183 | 0.1814 | 10 |
| scan: Isa 24:3 w6 to Isa 24:15 w5 | 0.571 | 7.40e-4 | 1 | 0.214 | 0.0499 | 19 |
| scan: Jer 32:25 w1 to Jer 32:37 w11 | 0.467 | 7.40e-4 | 1 | 0.061 | 0.2519 | 27 |
| scan: Ezek 33:27 w1 to Ezek 34:3 w8 | 0.535 | 7.40e-4 | 1 | 0.171 | 0.2389 | 13 |
| scan: Ezek 45:7 w1 to Ezek 45:17 w27 | 0.493 | 7.40e-4 | 1 | 0.185 | 0.1203 | 21 |
| scan: Ezek 46:22 w1 to Ezek 47:9 w29 | 0.393 | 7.40e-4 | 1 | 0.271 | 0.0072 | 27 |
| scan: Ezek 47:11 w1 to Ezek 47:23 w12 | 0.373 | 7.40e-4 | 1 | 0.577 | 1.90e-4 | 28 |
| scan: Dan 4:7 w7 to Dan 4:18 w27 | 0.432 | 7.40e-4 | 1 | 0.422 | 0.0019 | 22 |
| scan: Gen 13:12 w5 to Gen 14:2 w10 | 0.786 | 7.50e-4 | 1 | 0.289 | 0.2171 | 17 |
| scan: Gen 32:17 w1 to Gen 32:27 w6 | 0.396 | 7.50e-4 | 1 | -0.148 | 0.7630 | 9 |
| scan: Exod 3:7 w10 to Exod 3:18 w2 | 0.377 | 7.50e-4 | 1 | 0.060 | 0.2235 | 21 |
| scan: Num 7:1 w20 to Num 7:12 w11 | 0.447 | 7.50e-4 | 1 | 0.171 | 0.0554 | 15 |
| scan: Num 19:17 w6 to Num 20:5 w9 | 0.469 | 7.50e-4 | 1 | -0.116 | 0.7571 | 22 |
| scan: Num 26:8 w1 to Num 26:20 w10 | 0.177 | 7.50e-4 | 1 | -0.011 | 0.6563 | 32 |
| scan: Num 34:25 w5 to Num 35:8 w12 | 0.734 | 7.50e-4 | 1 | 0.000 | 1.0000 | 26 |
| scan: Deut 21:20 w12 to Deut 22:6 w26 | 0.507 | 7.50e-4 | 1 | 0.446 | 0.0286 | 13 |
| scan: Deut 26:9 w1 to Deut 26:16 w18 | 0.518 | 7.50e-4 | 1 | 0.341 | 0.0237 | 9 |
| scan: Josh 16:10 w1 to Josh 17:11 w25 | 0.143 | 7.50e-4 | 1 | 0.452 | 5.80e-8 | 46 |
| scan: Josh 19:8 w12 to Josh 19:16 w5 | 0.785 | 7.50e-4 | 1 | 0.531 | 0.0864 | 27 |
| scan: 1Sam 10:8 w13 to 1Sam 10:20 w9 | 0.423 | 7.50e-4 | 1 | 0.345 | 0.0185 | 15 |
| scan: 2Sam 14:25 w10 to 2Sam 15:3 w12 | 0.269 | 7.50e-4 | 1 | 0.180 | 0.0711 | 43 |
| scan: 1Kgs 18:43 w1 to 1Kgs 19:6 w7 | 0.498 | 7.50e-4 | 1 | 0.075 | 0.2817 | 17 |
| scan: 2Kgs 3:26 w1 to 2Kgs 4:9 w14 | 0.382 | 7.50e-4 | 1 | 0.304 | 0.0080 | 14 |
| scan: 1Chr 27:23 w1 to 1Chr 27:33 w7 | 0.296 | 7.50e-4 | 1 | -0.458 | 0.9833 | 33 |
| scan: 2Chr 36:11 w1 to 2Chr 36:21 w10 | 0.427 | 7.50e-4 | 1 | 0.582 | 1.10e-4 | 12 |
| scan: Eccl 4:15 w1 to Eccl 5:5 w7 | 0.475 | 7.50e-4 | 1 | 1.000 | 0.5000 | 7 |
| scan: Isa 22:4 w8 to Isa 22:15 w5 | 0.792 | 7.50e-4 | 1 | 0.665 | 0.0146 | 17 |
| scan: Isa 44:27 w4 to Isa 45:9 w17 | 0.518 | 7.50e-4 | 1 | 0.354 | 0.0109 | 8 |
| scan: Jer 48:18 w8 to Jer 48:28 w6 | 0.329 | 7.50e-4 | 1 | 0.000 | 1.0000 | 36 |
| scan: Jer 51:18 w5 to Jer 51:27 w15 | 0.542 | 7.50e-4 | 1 | 0.147 | 0.0332 | 10 |
| scan: Ezek 2:6 w1 to Ezek 3:7 w11 | 0.258 | 7.50e-4 | 1 | 0.386 | 0.0022 | 11 |
| scan: Ezek 19:12 w1 to Ezek 20:9 w10 | 0.458 | 7.50e-4 | 1 | 0.381 | 0.0082 | 11 |
| scan: Ezek 47:17 w13 to Ezek 48:5 w10 | 0.241 | 7.50e-4 | 1 | 0.019 | 0.3857 | 19 |
| scan: Zech 4:7 w8 to Zech 5:4 w13 | 0.345 | 7.50e-4 | 1 | 0.519 | 4.10e-4 | 15 |
| scan: Zech 8:15 w1 to Zech 9:4 w6 | 0.323 | 7.50e-4 | 1 | 0.372 | 0.0016 | 12 |
| scan: Gen 14:3 w7 to Gen 14:15 w12 | 0.501 | 7.60e-4 | 1 | 0.422 | 0.0583 | 40 |
| scan: Gen 25:11 w1 to Gen 25:21 w8 | 0.581 | 7.60e-4 | 1 | 0.108 | 0.2728 | 25 |
| scan: Gen 25:11 w1 to Gen 25:21 w14 | 0.581 | 7.60e-4 | 1 | 0.128 | 0.2310 | 25 |
| scan: Gen 32:17 w1 to Gen 32:28 w16 | 0.352 | 7.60e-4 | 1 | 0.272 | 0.0829 | 9 |
| scan: Gen 36:23 w7 to Gen 36:35 w15 | 0.284 | 7.60e-4 | 1 | 0.642 | 1.79e-5 | 42 |
| scan: Deut 11:30 w13 to Deut 12:10 w10 | 0.283 | 7.60e-4 | 1 | 0.508 | 1.50e-4 | 26 |
| scan: Deut 21:21 w10 to Deut 22:7 w8 | 0.450 | 7.60e-4 | 1 | 0.534 | 0.0049 | 13 |
| scan: Josh 24:6 w7 to Josh 24:17 w12 | 0.430 | 7.60e-4 | 1 | 0.027 | 0.4049 | 21 |
| scan: Judg 6:9 w1 to Judg 6:20 w16 | 0.303 | 7.60e-4 | 1 | 0.112 | 0.1575 | 17 |
| scan: Judg 6:9 w1 to Judg 6:20 w18 | 0.303 | 7.60e-4 | 1 | 0.101 | 0.1565 | 17 |
| scan: Judg 6:9 w8 to Judg 6:20 w16 | 0.303 | 7.60e-4 | 1 | 0.101 | 0.1565 | 17 |
| scan: 1Sam 12:1 w13 to 1Sam 12:12 w18 | 0.410 | 7.60e-4 | 1 | 0.402 | 1.80e-4 | 18 |
| scan: 2Sam 17:6 w1 to 2Sam 17:14 w25 | 0.438 | 7.60e-4 | 1 | 0.618 | 0.0179 | 30 |
| scan: 1Kgs 3:26 w24 to 1Kgs 4:7 w18 | 0.641 | 7.60e-4 | 1 | 0.071 | 0.3254 | 13 |
| scan: 1Kgs 7:4 w4 to 1Kgs 7:16 w9 | 0.469 | 7.60e-4 | 1 | 0.581 | 3.00e-4 | 42 |
| scan: 1Kgs 8:13 w6 to 1Kgs 8:23 w20 | 0.347 | 7.60e-4 | 0 | - | - | 0 |
| scan: 2Chr 11:4 w18 to 2Chr 11:16 w18 | 0.710 | 7.60e-4 | 1 | 0.695 | 0.0039 | 21 |
| scan: 2Chr 18:15 w9 to 2Chr 18:27 w10 | 0.246 | 7.60e-4 | 1 | 0.054 | 0.1853 | 11 |
| scan: Ps 135:3 w6 to Ps 135:14 w4 | 0.595 | 7.60e-4 | 1 | 0.437 | 0.0326 | 9 |
| scan: Jer 24:9 w7 to Jer 25:11 w6 | 0.400 | 7.60e-4 | 1 | 0.072 | 0.3685 | 13 |
| scan: Dan 4:34 w17 to Dan 5:8 w12 | 0.338 | 7.60e-4 | 1 | 0.256 | 0.0411 | 24 |
| scan: Amos 2:12 w5 to Amos 3:8 w5 | 0.381 | 7.60e-4 | 1 | 0.460 | 0.0932 | 17 |
| scan: Gen 29:3 w14 to Gen 29:12 w14 | 0.514 | 7.70e-4 | 1 | 0.206 | 0.1423 | 9 |
| scan: Gen 36:7 w1 to Gen 36:15 w4 | 0.189 | 7.70e-4 | 1 | 0.058 | 0.0297 | 30 |
| scan: Exod 2:5 w12 to Exod 2:12 w7 | 0.288 | 7.70e-4 | 1 | 0.147 | 0.1334 | 8 |
| scan: Exod 4:17 w6 to Exod 4:29 w3 | 0.267 | 7.70e-4 | 1 | 0.065 | 0.2354 | 8 |
| scan: Exod 37:17 w1 to Exod 37:24 w8 | 0.456 | 7.70e-4 | 0 | - | - | 0 |
| scan: Lev 4:32 w1 to Lev 5:7 w22 | 0.367 | 7.70e-4 | 1 | 0.092 | 0.1072 | 19 |
| scan: Lev 20:19 w8 to Lev 20:27 w16 | 0.554 | 7.70e-4 | 1 | 1.000 | 0.0556 | 14 |
| scan: Lev 27:6 w1 to Lev 27:13 w7 | 0.466 | 7.70e-4 | 1 | 0.820 | 6.70e-6 | 5 |
| scan: Num 33:35 w3 to Num 33:43 w2 | 0.577 | 7.70e-4 | 1 | 0.440 | 0.5000 | 38 |
| scan: Num 34:29 w5 to Num 35:11 w7 | 0.263 | 7.70e-4 | 1 | 0.302 | 7.80e-4 | 22 |
| scan: Deut 7:10 w1 to Deut 7:21 w3 | 0.327 | 7.70e-4 | 1 | 0.191 | 0.0642 | 9 |
| scan: Deut 32:37 w1 to Deut 32:49 w24 | 0.603 | 7.70e-4 | 1 | 0.000 | 0.4959 | 15 |
| scan: Judg 16:28 w1 to Judg 17:7 w12 | 0.601 | 7.70e-4 | 1 | -0.030 | 0.5717 | 15 |
| scan: 1Sam 4:1 w1 to 1Sam 4:10 w16 | 0.339 | 7.70e-4 | 1 | 0.017 | 0.4135 | 17 |
| scan: 1Sam 4:19 w1 to 1Sam 5:8 w24 | 0.258 | 7.70e-4 | 1 | 0.195 | 0.0189 | 38 |
| scan: 1Sam 28:12 w8 to 1Sam 28:22 w18 | 0.387 | 7.70e-4 | 1 | 0.236 | 0.0238 | 9 |
| scan: 1Kgs 3:2 w1 to 1Kgs 3:9 w11 | 0.698 | 7.70e-4 | 1 | 0.747 | 7.00e-4 | 9 |
| scan: 1Kgs 9:25 w1 to 1Kgs 10:4 w10 | 0.417 | 7.70e-4 | 0 | - | - | 0 |
| scan: 1Kgs 17:5 w1 to 1Kgs 17:16 w14 | 0.440 | 7.70e-4 | 1 | 0.309 | 0.0373 | 18 |
| scan: 2Kgs 4:3 w11 to 2Kgs 4:14 w12 | 0.403 | 7.70e-4 | 1 | 0.556 | 1.10e-4 | 12 |
| scan: 2Chr 7:3 w11 to 2Chr 7:13 w16 | 0.247 | 7.70e-4 | 1 | 0.106 | 0.0950 | 17 |
| scan: Neh 7:65 w9 to Neh 8:2 w13 | 0.576 | 7.70e-4 | 1 | 0.316 | 0.0736 | 16 |
| scan: Isa 10:6 w1 to Isa 10:14 w12 | 0.648 | 7.70e-4 | 1 | 0.166 | 0.2606 | 14 |
| scan: Isa 24:20 w7 to Isa 25:8 w19 | 0.452 | 7.70e-4 | 1 | 0.552 | 0.0050 | 17 |
| scan: Isa 48:21 w1 to Isa 49:11 w4 | 0.445 | 7.70e-4 | 1 | 0.336 | 0.0087 | 14 |
| scan: Jer 1:7 w1 to Jer 1:18 w13 | 0.339 | 7.70e-4 | 1 | 0.105 | 0.2101 | 12 |
| scan: Ezek 2:6 w18 to Ezek 3:6 w19 | 0.324 | 7.70e-4 | 1 | 0.421 | 0.0037 | 10 |
| scan: Ezek 36:17 w1 to Ezek 36:27 w4 | 0.436 | 7.70e-4 | 1 | 0.533 | 0.0085 | 18 |
| scan: Ezek 40:40 w10 to Ezek 41:2 w12 | 0.370 | 7.70e-4 | 1 | 0.242 | 0.0107 | 35 |
| scan: Ezek 41:19 w1 to Ezek 41:26 w11 | 0.584 | 7.70e-4 | 1 | 0.805 | 0.0024 | 19 |
| scan: Zeph 1:18 w1 to Zeph 2:11 w16 | 0.475 | 7.70e-4 | 1 | 0.148 | 0.1568 | 24 |
| scan: Gen 2:7 w13 to Gen 2:16 w6 | 0.519 | 7.80e-4 | 1 | 0.139 | 0.1645 | 10 |
| scan: Gen 37:36 w1 to Gen 38:9 w7 | 0.515 | 7.80e-4 | 1 | 0.424 | 0.0069 | 12 |
| scan: Exod 27:2 w9 to Exod 27:10 w9 | 0.538 | 7.80e-4 | 1 | 0.356 | 0.0356 | 25 |
| scan: Exod 34:20 w9 to Exod 34:31 w12 | 0.354 | 7.80e-4 | 1 | 0.320 | 0.1769 | 7 |
| scan: Lev 20:20 w1 to Lev 21:3 w10 | 0.438 | 7.80e-4 | 1 | 0.384 | 0.0771 | 17 |
| scan: Num 7:1 w1 to Num 7:12 w6 | 0.401 | 7.80e-4 | 1 | 0.315 | 0.0026 | 15 |
| scan: 2Sam 3:9 w8 to 2Sam 3:19 w22 | 0.328 | 7.80e-4 | 1 | 0.050 | 0.3102 | 21 |
| scan: 1Chr 6:19 w5 to 1Chr 6:33 w11 | 0.289 | 7.80e-4 | 1 | 0.000 | 1.0000 | 30 |
| scan: 1Chr 27:22 w1 to 1Chr 27:32 w14 | 0.319 | 7.80e-4 | 1 | 0.620 | 0.0486 | 34 |
| scan: Isa 18:4 w9 to Isa 19:8 w7 | 0.673 | 7.80e-4 | 1 | 0.333 | 0.0571 | 29 |
| scan: Isa 33:17 w5 to Isa 34:1 w11 | 0.866 | 7.80e-4 | 1 | 0.046 | 0.4322 | 16 |
| scan: Ezek 3:5 w1 to Ezek 3:12 w11 | 0.583 | 7.80e-4 | 1 | 0.380 | 0.1223 | 8 |
| scan: Ezek 19:12 w1 to Ezek 20:10 w3 | 0.431 | 7.80e-4 | 1 | 0.423 | 0.0055 | 11 |
| scan: Ezek 33:26 w11 to Ezek 34:5 w3 | 0.515 | 7.80e-4 | 0 | - | - | 0 |
| scan: Ezek 33:27 w1 to Ezek 34:4 w23 | 0.515 | 7.80e-4 | 1 | 0.482 | 0.0236 | 15 |
| scan: Ezek 33:27 w1 to Ezek 34:5 w3 | 0.515 | 7.80e-4 | 1 | 0.771 | 2.80e-4 | 15 |
| scan: Ezek 46:23 w6 to Ezek 47:9 w17 | 0.433 | 7.80e-4 | 1 | 0.118 | 0.1908 | 26 |
| scan: Dan 4:34 w17 to Dan 5:7 w31 | 0.399 | 7.80e-4 | 1 | 0.373 | 0.0325 | 24 |
| scan: Zech 2:11 w11 to Zech 3:9 w25 | 0.257 | 7.80e-4 | 1 | 0.218 | 0.0200 | 14 |
| scan: Zech 12:8 w14 to Zech 13:4 w8 | 0.562 | 7.80e-4 | 1 | 0.414 | 0.0012 | 18 |
| scan: Gen 4:13 w1 to Gen 4:23 w17 | 0.589 | 7.90e-4 | 1 | 0.656 | 0.0055 | 23 |
| scan: Gen 4:16 w1 to Gen 4:25 w22 | 0.468 | 7.90e-4 | 1 | 0.296 | 0.0359 | 23 |
| scan: Gen 38:7 w8 to Gen 38:17 w7 | 0.404 | 7.90e-4 | 1 | 0.144 | 0.1894 | 19 |
| scan: Num 18:31 w1 to Num 19:10 w18 | 0.470 | 7.90e-4 | 1 | 0.217 | 0.1946 | 6 |
| scan: Deut 27:25 w1 to Deut 28:9 w16 | 0.506 | 7.90e-4 | 1 | 0.568 | 0.0017 | 2 |
| scan: Josh 8:25 w1 to Josh 8:35 w7 | 0.334 | 7.90e-4 | 0 | - | - | 0 |
| scan: Josh 11:16 w19 to Josh 12:5 w10 | 0.403 | 7.90e-4 | 1 | 0.204 | 0.0173 | 47 |
| scan: Josh 11:17 w1 to Josh 12:2 w5 | 0.423 | 7.90e-4 | 1 | 0.491 | 5.30e-4 | 26 |
| scan: Ruth 3:12 w8 to Ruth 4:1 w19 | 0.642 | 7.90e-4 | 1 | 0.220 | 0.1696 | 13 |
| scan: 1Sam 10:7 w1 to 1Sam 10:16 w10 | 0.401 | 7.90e-4 | 1 | 0.643 | 0.0239 | 7 |
| scan: 1Sam 18:5 w1 to 1Sam 18:14 w7 | 0.119 | 7.90e-4 | 0 | - | - | 0 |
| scan: 2Sam 13:13 w11 to 2Sam 13:22 w20 | 0.546 | 7.90e-4 | 1 | 0.203 | 0.1953 | 27 |
| scan: 1Kgs 13:32 w1 to 1Kgs 14:9 w6 | 0.205 | 7.90e-4 | 0 | - | - | 0 |
| scan: 2Kgs 9:4 w1 to 2Kgs 9:12 w5 | 0.593 | 7.90e-4 | 1 | -0.012 | 0.5351 | 26 |
| scan: 2Chr 7:4 w4 to 2Chr 7:12 w16 | 0.285 | 7.90e-4 | 1 | 0.066 | 0.2352 | 14 |
| scan: 2Chr 32:8 w10 to 2Chr 32:20 w9 | 0.266 | 7.90e-4 | 1 | 0.062 | 0.2084 | 14 |
| scan: 2Chr 32:32 w5 to 2Chr 33:9 w6 | 0.348 | 7.90e-4 | 1 | 0.285 | 0.0357 | 21 |
| scan: Ezra 3:7 w1 to Ezra 4:4 w10 | 0.433 | 7.90e-4 | 1 | 0.331 | 0.0090 | 23 |
| scan: Jer 25:1 w17 to Jer 25:12 w18 | 0.489 | 7.90e-4 | 1 | 0.105 | 0.3029 | 13 |
| scan: Jer 36:16 w10 to Jer 36:27 w18 | 0.295 | 7.90e-4 | 1 | 0.197 | 0.0260 | 22 |
| scan: Ezek 5:1 w17 to Ezek 5:12 w17 | 0.530 | 7.90e-4 | 1 | 0.228 | 0.0359 | 20 |
| scan: Ezek 45:2 w11 to Ezek 45:14 w15 | 0.375 | 7.90e-4 | 1 | -0.142 | 0.8092 | 18 |
| scan: Ezek 45:8 w6 to Ezek 45:19 w18 | 0.527 | 7.90e-4 | 1 | -0.068 | 0.6725 | 26 |
| scan: Gen 12:19 w9 to Gen 13:10 w12 | 0.505 | 8.00e-4 | 1 | 0.067 | 0.3594 | 9 |
| scan: Gen 47:12 w11 to Gen 47:22 w23 | 0.305 | 8.00e-4 | 1 | 0.169 | 0.0163 | 16 |
| scan: Lev 23:15 w1 to Lev 23:22 w13 | 0.680 | 8.00e-4 | 1 | 0.302 | 0.0756 | 24 |
| scan: Num 13:2 w1 to Num 13:18 w16 | 0.293 | 8.00e-4 | 1 | 0.185 | 0.0036 | 29 |
| scan: Num 23:15 w8 to Num 23:27 w10 | 0.304 | 8.00e-4 | 1 | 0.042 | 0.3129 | 16 |
| scan: Num 28:22 w1 to Num 28:30 w3 | 0.859 | 8.00e-4 | 1 | 0.113 | 0.3498 | 17 |
| scan: Num 33:33 w4 to Num 33:44 w7 | 0.408 | 8.00e-4 | 1 | 0.716 | 0.1667 | 51 |
| scan: Num 34:29 w1 to Num 35:9 w5 | 0.281 | 8.00e-4 | 1 | 0.363 | 8.84e-5 | 19 |
| scan: Josh 11:16 w19 to Josh 12:5 w16 | 0.397 | 8.00e-4 | 1 | 0.169 | 0.0364 | 47 |
| scan: Judg 10:7 w5 to Judg 11:1 w9 | 0.304 | 8.00e-4 | 1 | 0.140 | 0.0384 | 32 |
| scan: Judg 11:18 w18 to Judg 11:28 w11 | 0.351 | 8.00e-4 | 1 | 0.057 | 0.3457 | 34 |
| scan: Ruth 3:12 w8 to Ruth 4:1 w17 | 0.605 | 8.00e-4 | 1 | 0.284 | 0.0699 | 13 |
| scan: 1Sam 10:27 w12 to 1Sam 11:10 w11 | 0.340 | 8.00e-4 | 1 | 0.401 | 0.0055 | 24 |
| scan: 1Sam 24:5 w8 to 1Sam 24:12 w11 | 0.539 | 8.00e-4 | 1 | 0.284 | 0.0952 | 4 |
| scan: 1Sam 28:12 w1 to 1Sam 28:22 w12 | 0.383 | 8.00e-4 | 1 | 0.236 | 0.0238 | 9 |
| scan: 2Sam 17:18 w1 to 2Sam 17:25 w24 | 0.414 | 8.00e-4 | 1 | 0.343 | 0.0967 | 24 |
| scan: 1Kgs 2:35 w10 to 1Kgs 2:46 w14 | 0.269 | 8.00e-4 | 1 | 0.247 | 0.0060 | 17 |
| scan: 2Kgs 3:26 w8 to 2Kgs 4:11 w4 | 0.296 | 8.00e-4 | 1 | 0.326 | 0.0037 | 15 |
| scan: 2Kgs 5:24 w8 to 2Kgs 6:4 w6 | 0.313 | 8.00e-4 | 1 | 0.124 | 0.2336 | 6 |
| scan: 1Chr 28:13 w1 to 1Chr 28:20 w11 | 0.382 | 8.00e-4 | 1 | 0.635 | 0.0128 | 13 |
| scan: 2Chr 5:9 w1 to 2Chr 6:6 w11 | 0.353 | 8.00e-4 | 1 | 0.183 | 0.1149 | 18 |
| scan: Eccl 4:15 w1 to Eccl 5:10 w13 | 0.398 | 8.00e-4 | 1 | 0.262 | 0.0502 | 9 |
| scan: Isa 45:5 w1 to Isa 45:15 w4 | 0.467 | 8.00e-4 | 1 | 0.321 | 0.0018 | 9 |
| scan: Isa 55:5 w1 to Isa 56:3 w20 | 0.347 | 8.00e-4 | 1 | 0.442 | 0.0050 | 16 |
| scan: Ezek 43:10 w1 to Ezek 43:19 w14 | 0.625 | 8.00e-4 | 1 | 0.364 | 0.0149 | 27 |
| scan: Zech 3:8 w14 to Zech 4:10 w20 | 0.422 | 8.00e-4 | 1 | 0.215 | 0.0444 | 9 |
| scan: Gen 15:1 w11 to Gen 15:11 w7 | 0.443 | 8.10e-4 | 1 | 0.425 | 0.0087 | 14 |
| scan: Exod 37:15 w9 to Exod 37:27 w13 | 0.451 | 8.10e-4 | 0 | - | - | 0 |
| scan: Lev 13:28 w1 to Lev 13:38 w8 | 0.189 | 8.10e-4 | 1 | 0.180 | 0.0319 | 41 |
| scan: Lev 14:17 w1 to Lev 14:27 w10 | 0.231 | 8.10e-4 | 1 | 0.096 | 0.0950 | 28 |
| scan: Lev 21:13 w1 to Lev 21:24 w6 | 0.479 | 8.10e-4 | 1 | 0.320 | 0.0535 | 13 |
| scan: Lev 27:4 w4 to Lev 27:16 w10 | 0.282 | 8.10e-4 | 1 | 0.612 | 7.00e-6 | 9 |
| scan: Num 33:33 w1 to Num 33:43 w4 | 0.435 | 8.10e-4 | 1 | 0.000 | 0.6667 | 46 |
| scan: 2Sam 7:19 w13 to 2Sam 7:28 w15 | 0.334 | 8.10e-4 | 1 | -0.004 | 0.5166 | 3 |
| scan: 1Kgs 6:21 w8 to 1Kgs 6:31 w7 | 0.463 | 8.10e-4 | 1 | 0.484 | 0.0014 | 17 |
| scan: 1Kgs 6:23 w7 to 1Kgs 6:34 w14 | 0.430 | 8.10e-4 | 1 | 0.332 | 0.0654 | 20 |
| scan: 1Kgs 6:24 w1 to 1Kgs 6:34 w14 | 0.430 | 8.10e-4 | 1 | 0.368 | 0.0668 | 17 |
| scan: 2Kgs 18:31 w1 to 2Kgs 19:1 w7 | 0.524 | 8.10e-4 | 1 | 0.472 | 0.0235 | 16 |
| scan: 2Chr 7:3 w11 to 2Chr 7:14 w21 | 0.237 | 8.10e-4 | 1 | 0.053 | 0.2315 | 18 |
| scan: Esth 6:7 w5 to Esth 7:4 w7 | 0.219 | 8.10e-4 | 0 | - | - | 0 |
| scan: Isa 2:9 w1 to Isa 2:21 w5 | 0.565 | 8.10e-4 | 1 | 0.383 | 0.0038 | 19 |
| scan: Isa 50:2 w1 to Isa 50:11 w17 | 0.588 | 8.10e-4 | 1 | 0.368 | 0.0537 | 7 |
| scan: Ezek 11:6 w5 to Ezek 11:17 w17 | 0.468 | 8.10e-4 | 0 | - | - | 13 |
| scan: Ezek 23:15 w1 to Ezek 23:25 w19 | 0.673 | 8.10e-4 | 1 | 0.903 | 3.60e-5 | 23 |
| scan: Ezek 45:6 w14 to Ezek 45:18 w12 | 0.440 | 8.10e-4 | 1 | 0.070 | 0.2677 | 23 |
| scan: Zech 7:12 w17 to Zech 8:10 w11 | 0.198 | 8.10e-4 | 1 | 0.119 | 0.0224 | 16 |
| scan: Gen 34:27 w1 to Gen 35:6 w9 | 0.281 | 8.20e-4 | 1 | 0.240 | 0.0993 | 18 |
| scan: Exod 28:4 w12 to Exod 28:15 w8 | 0.381 | 8.20e-4 | 1 | 0.334 | 6.60e-4 | 41 |
| scan: Exod 38:22 w8 to Exod 39:3 w16 | 0.457 | 8.20e-4 | 1 | 0.541 | 4.65e-5 | 43 |
| scan: Lev 4:13 w10 to Lev 4:22 w14 | 0.471 | 8.20e-4 | 1 | 0.336 | 4.00e-4 | 16 |
| scan: Deut 34:2 w1 to Deut 34:12 w12 | 0.365 | 8.20e-4 | 1 | 0.178 | 0.0626 | 13 |
| scan: Judg 11:40 w1 to Judg 12:11 w11 | 0.419 | 8.20e-4 | 1 | 0.424 | 0.0031 | 26 |
| scan: 2Kgs 22:18 w12 to 2Kgs 23:8 w17 | 0.267 | 8.20e-4 | 1 | -0.177 | 0.9427 | 18 |
| scan: 1Chr 1:48 w3 to 1Chr 2:3 w19 | 0.701 | 8.20e-4 | 1 | 0.210 | 1.29e-5 | 28 |
| scan: 1Chr 25:21 w1 to 1Chr 26:3 w6 | 0.030 | 8.20e-4 | 1 | 0.095 | 0.0834 | 30 |
| scan: Isa 24:3 w6 to Isa 24:13 w7 | 0.712 | 8.20e-4 | 1 | 0.461 | 0.0295 | 15 |
| scan: Isa 37:35 w1 to Isa 38:6 w11 | 0.709 | 8.20e-4 | 1 | 0.552 | 0.0447 | 16 |
| scan: Ezek 37:23 w1 to Ezek 38:6 w10 | 0.487 | 8.20e-4 | 1 | -0.183 | 0.7500 | 17 |
| scan: Ezek 48:16 w16 to Ezek 48:27 w10 | 0.457 | 8.20e-4 | 1 | 0.229 | 0.0345 | 7 |
| scan: Gen 8:22 w1 to Gen 9:9 w9 | 0.712 | 8.30e-4 | 1 | 0.605 | 0.0012 | 1 |
| scan: Gen 25:10 w1 to Gen 25:22 w9 | 0.437 | 8.30e-4 | 1 | 0.164 | 0.1160 | 26 |
| scan: Gen 25:10 w1 to Gen 25:22 w13 | 0.437 | 8.30e-4 | 1 | 0.179 | 0.0946 | 26 |
| scan: Lev 26:2 w6 to Lev 26:14 w4 | 0.651 | 8.30e-4 | 1 | -0.048 | 0.5412 | 11 |
| scan: Num 16:10 w1 to Num 16:17 w18 | 0.715 | 8.30e-4 | 1 | 0.847 | 0.0023 | 15 |
| scan: Num 21:6 w10 to Num 21:18 w8 | 0.557 | 8.30e-4 | 1 | 0.491 | 0.0125 | 35 |
| scan: Num 34:27 w5 to Num 35:8 w12 | 0.315 | 8.30e-4 | 1 | 0.256 | 0.0151 | 22 |
| scan: Deut 28:65 w10 to Deut 29:6 w7 | 0.415 | 8.30e-4 | 1 | 0.565 | 0.0015 | 9 |
| scan: 1Sam 4:21 w9 to 1Sam 5:10 w5 | 0.323 | 8.30e-4 | 1 | 0.170 | 0.0158 | 41 |
| scan: 1Sam 20:42 w1 to 1Sam 21:10 w12 | 0.248 | 8.30e-4 | 1 | 0.368 | 1.50e-4 | 30 |
| scan: 2Sam 17:6 w16 to 2Sam 17:15 w16 | 0.379 | 8.30e-4 | 1 | 0.393 | 0.0374 | 34 |
| scan: 2Sam 17:7 w1 to 2Sam 17:15 w16 | 0.410 | 8.30e-4 | 1 | 0.349 | 0.0734 | 30 |
| scan: 1Chr 6:19 w1 to 1Chr 6:33 w3 | 0.343 | 8.30e-4 | 1 | 0.000 | 1.0000 | 30 |
| scan: 1Chr 23:13 w5 to 1Chr 23:26 w2 | 0.290 | 8.30e-4 | 1 | 0.254 | 0.0376 | 37 |
| scan: 2Chr 21:5 w1 to 2Chr 21:13 w21 | 0.576 | 8.30e-4 | 1 | 0.336 | 0.0440 | 12 |
| scan: Ezra 3:7 w5 to Ezra 4:5 w15 | 0.421 | 8.30e-4 | 1 | 0.207 | 0.0477 | 27 |
| scan: Eccl 3:15 w1 to Eccl 4:3 w17 | 0.355 | 8.30e-4 | 1 | 0.563 | 2.80e-4 | 4 |
| scan: Mic 5:6 w1 to Mic 6:2 w16 | 0.386 | 8.30e-4 | 1 | 0.178 | 0.1222 | 19 |
| scan: Gen 14:5 w1 to Gen 14:14 w17 | 0.684 | 8.40e-4 | 1 | 0.820 | 3.70e-4 | 36 |
| scan: Gen 19:27 w1 to Gen 20:1 w10 | 0.387 | 8.40e-4 | 1 | 0.227 | 0.0154 | 12 |
| scan: Exod 15:16 w1 to Exod 15:24 w7 | 0.683 | 8.40e-4 | 1 | -0.193 | 0.7642 | 15 |
| scan: Exod 28:14 w1 to Exod 28:25 w16 | 0.426 | 8.40e-4 | 0 | - | - | 0 |
| scan: Exod 34:13 w8 to Exod 34:25 w12 | 0.497 | 8.40e-4 | 1 | 0.570 | 0.0019 | 20 |
| scan: Exod 37:3 w1 to Exod 37:13 w5 | 0.416 | 8.40e-4 | 1 | 0.227 | 0.1491 | 23 |
| scan: Lev 13:56 w10 to Lev 14:9 w26 | 0.328 | 8.40e-4 | 1 | 0.244 | 0.0338 | 28 |
| scan: Num 7:88 w1 to Num 8:9 w12 | 0.638 | 8.40e-4 | 1 | 0.315 | 0.1102 | 11 |
| scan: Deut 4:12 w6 to Deut 4:21 w5 | 0.435 | 8.40e-4 | 1 | 0.229 | 0.0025 | 6 |
| scan: 1Kgs 14:21 w6 to 1Kgs 15:2 w9 | 0.339 | 8.40e-4 | 1 | 0.160 | 0.0299 | 24 |
| scan: 1Kgs 18:22 w10 to 1Kgs 18:33 w10 | 0.416 | 8.40e-4 | 1 | -0.138 | 0.9021 | 28 |
| scan: 1Chr 22:13 w17 to 1Chr 23:5 w3 | 0.566 | 8.40e-4 | 1 | 0.232 | 0.0396 | 12 |
| scan: 2Chr 6:3 w1 to 2Chr 6:12 w10 | 0.321 | 8.40e-4 | 1 | 0.262 | 0.0077 | 0 |
| scan: 2Chr 6:8 w14 to 2Chr 6:17 w10 | 0.442 | 8.40e-4 | 1 | 0.021 | 0.4189 | 7 |
| scan: 2Chr 6:9 w1 to 2Chr 6:17 w10 | 0.442 | 8.40e-4 | 1 | 0.146 | 0.1121 | 7 |
| scan: Isa 22:5 w1 to Isa 22:15 w5 | 0.815 | 8.40e-4 | 1 | 0.750 | 0.0678 | 17 |
| scan: Isa 36:16 w1 to Isa 37:1 w12 | 0.543 | 8.40e-4 | 1 | 0.451 | 0.0154 | 15 |
| scan: Ezek 5:14 w7 to Ezek 6:6 w6 | 0.921 | 8.40e-4 | 1 | 0.734 | 0.0098 | 17 |
| scan: Ezek 47:12 w1 to Ezek 48:1 w3 | 0.349 | 8.40e-4 | 1 | -0.087 | 0.7813 | 29 |
| scan: Dan 5:14 w7 to Dan 5:26 w3 | 0.229 | 8.40e-4 | 1 | 0.216 | 0.0591 | 26 |
| scan: Gen 4:12 w1 to Gen 4:23 w17 | 0.540 | 8.50e-4 | 1 | 0.694 | 0.0012 | 24 |
| scan: Gen 43:16 w1 to Gen 43:27 w11 | 0.375 | 8.50e-4 | 1 | 0.362 | 0.0036 | 15 |
| scan: Exod 9:11 w9 to Exod 9:21 w7 | 0.390 | 8.50e-4 | 1 | 0.398 | 0.0341 | 7 |
| scan: Exod 37:3 w9 to Exod 37:14 w9 | 0.421 | 8.50e-4 | 0 | - | - | 0 |
| scan: Lev 4:7 w1 to Lev 4:18 w12 | 0.287 | 8.50e-4 | 1 | 0.174 | 0.0607 | 24 |
| scan: Lev 13:28 w13 to Lev 13:40 w4 | 0.173 | 8.50e-4 | 1 | 0.076 | 0.1806 | 47 |
| scan: Judg 6:32 w7 to Judg 7:1 w20 | 0.605 | 8.50e-4 | 1 | 0.657 | 0.0369 | 27 |
| scan: 2Sam 5:4 w6 to 2Sam 5:14 w5 | 0.224 | 8.50e-4 | 1 | 0.140 | 0.0043 | 11 |
| scan: 2Sam 5:5 w9 to 2Sam 5:13 w9 | 0.184 | 8.50e-4 | 1 | 0.095 | 0.0188 | 9 |
| scan: 1Kgs 17:23 w1 to 1Kgs 18:10 w15 | 0.337 | 8.50e-4 | 1 | 0.134 | 0.0617 | 18 |
| scan: 1Kgs 18:43 w1 to 1Kgs 19:6 w11 | 0.481 | 8.50e-4 | 1 | 0.269 | 0.0170 | 17 |
| scan: 2Kgs 4:39 w1 to 2Kgs 5:6 w6 | 0.298 | 8.50e-4 | 1 | 0.142 | 0.1068 | 21 |
| scan: 1Chr 2:3 w12 to 1Chr 2:13 w6 | 0.671 | 8.50e-4 | 1 | 0.496 | 0.0357 | 15 |
| scan: 1Chr 2:26 w1 to 1Chr 2:34 w12 | 0.495 | 8.50e-4 | 1 | 0.000 | 0.5971 | 35 |
| scan: 1Chr 15:2 w12 to 1Chr 15:14 w3 | 0.481 | 8.50e-4 | 1 | 0.435 | 7.60e-4 | 19 |
| scan: 2Chr 8:14 w1 to 2Chr 9:4 w19 | 0.303 | 8.50e-4 | 1 | 0.179 | 0.0328 | 14 |
| scan: Isa 34:15 w8 to Isa 35:9 w13 | 0.726 | 8.50e-4 | 1 | 0.583 | 0.0027 | 18 |
| scan: Jer 34:13 w1 to Jer 35:2 w15 | 0.480 | 8.50e-4 | 1 | 0.419 | 0.0048 | 14 |
| scan: Ezek 48:20 w9 to Ezek 48:31 w9 | 0.233 | 8.50e-4 | 1 | 0.002 | 0.4858 | 12 |
| scan: Dan 2:20 w13 to Dan 2:30 w13 | 0.241 | 8.50e-4 | 1 | 0.216 | 0.0132 | 7 |
| scan: Jonah 1:11 w1 to Jonah 2:5 w6 | 0.388 | 8.50e-4 | 1 | 0.110 | 0.2914 | 7 |
| scan: Mic 3:4 w1 to Mic 4:1 w16 | 0.518 | 8.50e-4 | 1 | 0.575 | 0.0048 | 22 |
| scan: Gen 4:1 w1 to Gen 4:11 w14 | 0.175 | 8.60e-4 | 1 | 0.136 | 0.0518 | 3 |
| scan: Gen 49:25 w14 to Gen 50:3 w14 | 0.595 | 8.60e-4 | 1 | 0.738 | 2.70e-4 | 20 |
| scan: Gen 49:26 w1 to Gen 50:3 w9 | 0.595 | 8.60e-4 | 1 | 0.738 | 2.70e-4 | 19 |
| scan: Exod 27:19 w6 to Exod 28:9 w10 | 0.527 | 8.60e-4 | 1 | 0.501 | 0.0065 | 26 |
| scan: Num 18:8 w12 to Num 18:17 w13 | 0.344 | 8.60e-4 | 1 | 0.153 | 0.2254 | 20 |
| scan: Deut 13:6 w19 to Deut 13:13 w17 | 0.604 | 8.60e-4 | 1 | -0.144 | 0.6225 | 6 |
| scan: Deut 22:25 w13 to Deut 23:7 w13 | 0.295 | 8.60e-4 | 1 | -0.222 | 1.0000 | 14 |
| scan: Deut 24:6 w5 to Deut 24:17 w9 | 0.508 | 8.60e-4 | 1 | -0.100 | 0.5986 | 19 |
| scan: Deut 27:23 w5 to Deut 28:9 w16 | 0.492 | 8.60e-4 | 1 | 0.104 | 0.2932 | 2 |
| scan: Josh 11:16 w19 to Josh 12:2 w22 | 0.370 | 8.60e-4 | 1 | 0.158 | 0.0733 | 29 |
| scan: Josh 15:10 w16 to Josh 15:21 w10 | 0.602 | 8.60e-4 | 1 | 0.507 | 5.70e-4 | 36 |
| scan: Judg 11:18 w18 to Judg 11:29 w19 | 0.327 | 8.60e-4 | 1 | 0.046 | 0.3527 | 38 |
| scan: Judg 16:28 w1 to Judg 17:8 w17 | 0.455 | 8.60e-4 | 1 | 0.471 | 0.0011 | 16 |
| scan: Judg 16:29 w1 to Judg 17:6 w5 | 0.709 | 8.60e-4 | 1 | 0.021 | 0.4556 | 13 |
| scan: 1Sam 8:9 w1 to 1Sam 8:19 w12 | 0.640 | 8.60e-4 | 1 | 0.357 | 0.0534 | 10 |
| scan: 1Sam 23:21 w6 to 1Sam 23:28 w8 | 0.450 | 8.60e-4 | 1 | 0.133 | 0.1093 | 10 |
| scan: 1Sam 30:15 w8 to 1Sam 30:25 w11 | 0.329 | 8.60e-4 | 1 | 0.070 | 0.2509 | 25 |
| scan: 2Sam 20:8 w10 to 2Sam 20:19 w4 | 0.258 | 8.60e-4 | 1 | 0.086 | 0.3078 | 49 |
| scan: 1Kgs 3:15 w5 to 1Kgs 3:24 w5 | 0.420 | 8.60e-4 | 1 | 0.002 | 0.4966 | 6 |
| scan: 1Kgs 3:15 w5 to 1Kgs 3:24 w9 | 0.452 | 8.60e-4 | 1 | -0.113 | 0.7469 | 6 |
| scan: 2Kgs 4:38 w10 to 2Kgs 5:5 w22 | 0.316 | 8.60e-4 | 1 | 0.160 | 0.0760 | 26 |
| scan: Ezra 8:12 w1 to Ezra 8:20 w13 | 0.550 | 8.60e-4 | 1 | 0.143 | 0.1090 | 29 |
| scan: Isa 2:10 w5 to Isa 2:19 w13 | 0.658 | 8.60e-4 | 1 | 0.545 | 0.0016 | 13 |
| scan: Isa 11:13 w7 to Isa 13:1 w7 | 0.714 | 8.60e-4 | 1 | 0.509 | 0.0705 | 8 |
| scan: Jer 14:15 w1 to Jer 15:3 w12 | 0.365 | 8.60e-4 | 1 | 0.025 | 0.4182 | 17 |
| scan: Amos 4:13 w1 to Amos 5:10 w3 | 0.532 | 8.60e-4 | 1 | 0.487 | 0.0029 | 19 |
| scan: Zech 4:4 w1 to Zech 4:12 w16 | 0.466 | 8.60e-4 | 1 | 0.557 | 0.0030 | 10 |
| scan: Zech 8:16 w5 to Zech 9:1 w14 | 0.315 | 8.60e-4 | 1 | 0.296 | 0.0022 | 7 |
| scan: Gen 47:9 w11 to Gen 47:19 w25 | 0.385 | 8.70e-4 | 1 | 0.032 | 0.3746 | 16 |
| scan: Exod 9:12 w1 to Exod 9:21 w13 | 0.406 | 8.70e-4 | 1 | 0.640 | 0.0035 | 7 |
| scan: Exod 10:6 w22 to Exod 10:18 w3 | 0.402 | 8.70e-4 | 1 | -0.249 | 0.9817 | 16 |
| scan: Num 7:87 w16 to Num 8:9 w6 | 0.578 | 8.70e-4 | 1 | 0.501 | 6.60e-4 | 15 |
| scan: Num 13:1 w1 to Num 13:17 w15 | 0.309 | 8.70e-4 | 1 | 0.271 | 4.30e-4 | 28 |
| scan: Num 15:13 w7 to Num 15:25 w23 | 0.373 | 8.70e-4 | 1 | 0.415 | 4.20e-4 | 11 |
| scan: Num 23:14 w7 to Num 23:26 w5 | 0.376 | 8.70e-4 | 1 | -0.131 | 0.8725 | 19 |
| scan: Num 33:33 w1 to Num 33:44 w2 | 0.417 | 8.70e-4 | 1 | 0.000 | 0.6667 | 51 |
| scan: 1Sam 1:20 w1 to 1Sam 2:1 w16 | 0.423 | 8.70e-4 | 1 | 0.045 | 0.3451 | 17 |
| scan: 1Sam 24:6 w1 to 1Sam 24:12 w11 | 0.538 | 8.70e-4 | 1 | 0.115 | 0.2768 | 4 |
| scan: 1Chr 18:13 w1 to 1Chr 19:3 w23 | 0.266 | 8.70e-4 | 1 | 0.307 | 0.0135 | 21 |
| scan: 1Chr 28:2 w10 to 1Chr 28:14 w15 | 0.194 | 8.70e-4 | 1 | 0.202 | 0.0071 | 15 |
| scan: 2Chr 6:2 w6 to 2Chr 6:13 w17 | 0.320 | 8.70e-4 | 1 | 0.163 | 0.0326 | 5 |
| scan: Neh 10:30 w1 to Neh 11:2 w7 | 0.287 | 8.70e-4 | 1 | 0.259 | 0.0019 | 20 |
| scan: Isa 2:10 w1 to Isa 2:19 w13 | 0.662 | 8.70e-4 | 1 | 0.395 | 0.0364 | 13 |
| scan: Isa 53:8 w1 to Isa 54:4 w19 | 0.736 | 8.70e-4 | 1 | 0.695 | 0.1944 | 11 |
| scan: Jer 50:33 w1 to Jer 50:41 w11 | 0.649 | 8.70e-4 | 1 | 0.000 | 0.5667 | 21 |
| scan: Lev 14:26 w1 to Lev 14:37 w15 | 0.358 | 8.80e-4 | 1 | 0.132 | 0.0802 | 21 |
| scan: Num 5:9 w1 to Num 5:16 w6 | 0.706 | 8.80e-4 | 1 | 0.712 | 0.0178 | 8 |
| scan: Num 20:24 w1 to Num 21:3 w15 | 0.525 | 8.80e-4 | 1 | 0.340 | 0.0401 | 11 |
| scan: Num 26:49 w4 to Num 26:60 w10 | 0.620 | 8.80e-4 | 1 | 0.258 | 0.0493 | 30 |
| scan: Num 31:5 w1 to Num 31:14 w12 | 0.501 | 8.80e-4 | 1 | 0.122 | 0.2934 | 22 |
| scan: Deut 20:2 w5 to Deut 20:10 w9 | 0.511 | 8.80e-4 | 1 | 0.292 | 0.0341 | 11 |
| scan: Deut 23:6 w1 to Deut 23:16 w12 | 0.353 | 8.80e-4 | 1 | 0.117 | 0.3313 | 10 |
| scan: Josh 15:11 w15 to Josh 15:22 w3 | 0.591 | 8.80e-4 | 1 | 0.588 | 1.20e-4 | 35 |
| scan: Josh 24:6 w7 to Josh 24:16 w8 | 0.442 | 8.80e-4 | 1 | -0.050 | 0.6444 | 20 |
| scan: 1Sam 20:17 w1 to 1Sam 20:25 w18 | 0.489 | 8.80e-4 | 1 | 0.189 | 0.3366 | 12 |
| scan: 1Chr 2:31 w4 to 1Chr 2:45 w3 | 0.474 | 8.80e-4 | 1 | 0.331 | 8.16e-5 | 51 |
| scan: 2Chr 2:14 w1 to 2Chr 3:7 w8 | 0.617 | 8.80e-4 | 1 | 0.665 | 0.0109 | 37 |
| scan: Neh 7:66 w1 to Neh 8:4 w19 | 0.697 | 8.80e-4 | 1 | 0.234 | 0.2336 | 26 |
| scan: Eccl 10:6 w5 to Eccl 10:18 w3 | 0.805 | 8.80e-4 | 1 | -1.000 | 1.0000 | 15 |
| scan: Eccl 10:7 w1 to Eccl 10:17 w11 | 0.805 | 8.80e-4 | 1 | -1.000 | 1.0000 | 10 |
| scan: Eccl 10:7 w1 to Eccl 10:18 w3 | 0.805 | 8.80e-4 | 1 | -1.000 | 1.0000 | 12 |
| scan: Eccl 10:7 w5 to Eccl 10:17 w11 | 0.805 | 8.80e-4 | 1 | -1.000 | 1.0000 | 10 |
| scan: Isa 24:2 w8 to Isa 24:14 w4 | 0.676 | 8.80e-4 | 1 | 0.394 | 0.0011 | 22 |
| scan: Isa 24:3 w1 to Isa 24:13 w13 | 0.676 | 8.80e-4 | 1 | 0.461 | 0.0295 | 15 |
| scan: Isa 36:11 w1 to Isa 36:22 w23 | 0.348 | 8.80e-4 | 1 | 0.187 | 0.0615 | 22 |
| scan: Isa 44:28 w1 to Isa 45:11 w14 | 0.431 | 8.80e-4 | 1 | 0.349 | 0.0020 | 8 |
| scan: Ezek 45:8 w1 to Ezek 45:19 w13 | 0.472 | 8.80e-4 | 1 | 0.301 | 0.0209 | 26 |
| scan: Ezek 45:8 w1 to Ezek 45:20 w7 | 0.481 | 8.80e-4 | 1 | -0.098 | 0.7530 | 31 |
| scan: Zech 12:9 w4 to Zech 13:4 w14 | 0.680 | 8.80e-4 | 1 | 0.154 | 0.2508 | 17 |
| scan: Gen 45:9 w16 to Gen 45:19 w4 | 0.502 | 8.90e-4 | 1 | -0.090 | 0.7254 | 8 |
| scan: Exod 20:25 w1 to Exod 21:8 w15 | 0.414 | 8.90e-4 | 1 | 0.079 | 0.4228 | 12 |
| scan: Exod 29:35 w9 to Exod 29:45 w4 | 0.572 | 8.90e-4 | 1 | 0.553 | 0.0032 | 27 |
| scan: Exod 30:8 w1 to Exod 30:20 w16 | 0.338 | 8.90e-4 | 1 | 0.665 | 1.30e-6 | 22 |
| scan: Exod 38:23 w9 to Exod 39:4 w4 | 0.505 | 8.90e-4 | 1 | 0.657 | 9.90e-6 | 45 |
| scan: Lev 13:29 w1 to Lev 13:40 w8 | 0.179 | 8.90e-4 | 1 | 0.024 | 0.3676 | 42 |
| scan: Lev 21:24 w1 to Lev 22:10 w5 | 0.385 | 8.90e-4 | 1 | 0.156 | 0.1149 | 12 |
| scan: Lev 23:44 w1 to Lev 24:11 w11 | 0.459 | 8.90e-4 | 1 | 0.416 | 0.0016 | 15 |
| scan: Num 1:3 w1 to Num 1:19 w5 | 0.367 | 8.90e-4 | 1 | 0.500 | 8.60e-6 | 29 |
| scan: Num 6:27 w7 to Num 7:11 w15 | 0.442 | 8.90e-4 | 1 | 0.186 | 0.0524 | 15 |
| scan: Deut 11:28 w1 to Deut 12:6 w9 | 0.274 | 8.90e-4 | 1 | 0.367 | 0.0029 | 23 |
| scan: Deut 28:13 w1 to Deut 28:23 w6 | 0.537 | 8.90e-4 | 1 | 0.702 | 0.0011 | 18 |
| scan: Josh 8:25 w12 to Josh 8:35 w7 | 0.308 | 8.90e-4 | 0 | - | - | 0 |
| scan: Judg 11:19 w1 to Judg 11:27 w20 | 0.371 | 8.90e-4 | 1 | -0.096 | 0.7037 | 25 |
| scan: Judg 11:33 w1 to Judg 12:3 w14 | 0.428 | 8.90e-4 | 1 | 0.251 | 0.0215 | 23 |
| scan: Ruth 2:10 w6 to Ruth 2:21 w3 | 0.329 | 8.90e-4 | 1 | 0.410 | 1.40e-4 | 14 |
| scan: 2Sam 6:4 w1 to 2Sam 6:11 w9 | 0.451 | 8.90e-4 | 1 | 0.044 | 0.4122 | 23 |
| scan: 2Sam 11:23 w12 to 2Sam 12:8 w21 | 0.340 | 8.90e-4 | 1 | 0.240 | 0.0070 | 17 |
| scan: 2Kgs 22:18 w1 to 2Kgs 23:8 w33 | 0.237 | 8.90e-4 | 1 | -0.177 | 0.9427 | 18 |
| scan: 1Chr 5:12 w1 to 1Chr 5:24 w4 | 0.677 | 8.90e-4 | 1 | 0.565 | 0.0077 | 42 |
| scan: 1Chr 8:28 w1 to 1Chr 8:39 w3 | 0.522 | 8.90e-4 | 1 | 0.386 | 0.0015 | 40 |
| scan: 2Chr 11:14 w10 to 2Chr 12:2 w14 | 0.340 | 8.90e-4 | 1 | 0.351 | 0.0049 | 21 |
| scan: Isa 51:18 w7 to Isa 52:7 w12 | 0.652 | 8.90e-4 | 1 | 0.032 | 0.4407 | 17 |
| scan: Lam 2:7 w11 to Lam 2:17 w13 | 0.478 | 8.90e-4 | 1 | 0.287 | 0.0170 | 26 |
| scan: Gen 19:15 w1 to Gen 19:25 w13 | 0.400 | 9.00e-4 | 1 | 0.144 | 0.2685 | 7 |
| scan: Exod 25:17 w5 to Exod 25:24 w4 | 0.597 | 9.00e-4 | 1 | 0.328 | 0.0139 | 20 |
| scan: Lev 26:2 w1 to Lev 26:13 w17 | 0.653 | 9.00e-4 | 1 | 0.474 | 0.0735 | 10 |
| scan: Num 6:14 w17 to Num 6:27 w8 | 0.480 | 9.00e-4 | 1 | 0.072 | 0.3371 | 23 |
| scan: Num 6:15 w1 to Num 6:27 w6 | 0.480 | 9.00e-4 | 1 | 0.200 | 0.1563 | 20 |
| scan: Num 26:9 w1 to Num 26:19 w9 | 0.189 | 9.00e-4 | 1 | 0.112 | 0.0050 | 28 |
| scan: Deut 2:10 w1 to Deut 2:21 w11 | 0.620 | 9.00e-4 | 1 | 0.174 | 0.2298 | 40 |
| scan: 2Sam 14:26 w1 to 2Sam 15:1 w12 | 0.366 | 9.00e-4 | 1 | 0.676 | 1.50e-4 | 36 |
| scan: 2Chr 18:15 w1 to 2Chr 18:26 w8 | 0.225 | 9.00e-4 | 1 | 0.057 | 0.2018 | 11 |
| scan: 2Chr 21:18 w1 to 2Chr 22:4 w16 | 0.596 | 9.00e-4 | 1 | 0.475 | 0.0567 | 12 |
| scan: 2Chr 33:5 w1 to 2Chr 33:16 w9 | 0.317 | 9.00e-4 | 1 | 0.236 | 0.0105 | 23 |
| scan: Ezek 46:9 w1 to Ezek 46:19 w18 | 0.465 | 9.00e-4 | 1 | 0.505 | 0.0020 | 22 |
| scan: Zech 7:12 w1 to Zech 8:10 w11 | 0.190 | 9.00e-4 | 1 | 0.119 | 0.0224 | 16 |
| scan: Gen 37:35 w1 to Gen 38:9 w7 | 0.434 | 9.10e-4 | 1 | 0.306 | 0.0325 | 13 |
| scan: Exod 4:1 w11 to Exod 4:13 w3 | 0.379 | 9.10e-4 | 1 | -0.205 | 0.9207 | 15 |
| scan: Exod 11:5 w17 to Exod 12:6 w9 | 0.533 | 9.10e-4 | 1 | 0.110 | 0.3311 | 18 |
| scan: Exod 28:6 w4 to Exod 28:14 w9 | 0.438 | 9.10e-4 | 1 | 0.173 | 0.1139 | 32 |
| scan: Num 6:21 w14 to Num 7:8 w16 | 0.383 | 9.10e-4 | 1 | -0.059 | 0.6506 | 15 |
| scan: Num 8:3 w1 to Num 8:11 w10 | 0.655 | 9.10e-4 | 1 | 0.248 | 0.1606 | 10 |
| scan: Num 28:21 w6 to Num 28:29 w4 | 0.659 | 9.10e-4 | 1 | 0.477 | 0.0155 | 15 |
| scan: Deut 22:27 w1 to Deut 23:5 w18 | 0.254 | 9.10e-4 | 1 | 0.000 | 1.0000 | 9 |
| scan: Ruth 3:12 w1 to Ruth 4:4 w29 | 0.355 | 9.10e-4 | 1 | -0.301 | 0.9899 | 24 |
| scan: 1Sam 29:8 w18 to 1Sam 30:8 w17 | 0.395 | 9.10e-4 | 1 | 0.238 | 0.0039 | 30 |
| scan: 2Sam 8:13 w10 to 2Sam 9:3 w11 | 0.471 | 9.10e-4 | 1 | 0.200 | 0.0692 | 21 |
| scan: 2Sam 8:14 w1 to 2Sam 9:3 w11 | 0.471 | 9.10e-4 | 1 | 0.364 | 0.0196 | 18 |
| scan: 1Kgs 6:21 w8 to 1Kgs 6:30 w7 | 0.416 | 9.10e-4 | 1 | 0.462 | 2.60e-4 | 14 |
| scan: 1Kgs 7:26 w1 to 1Kgs 7:34 w7 | 0.516 | 9.10e-4 | 1 | 0.095 | 0.4222 | 23 |
| scan: 1Kgs 8:66 w1 to 1Kgs 9:11 w22 | 0.254 | 9.10e-4 | 1 | 0.354 | 4.10e-4 | 15 |
| scan: 1Kgs 13:31 w18 to 1Kgs 14:9 w17 | 0.206 | 9.10e-4 | 0 | - | - | 0 |
| scan: 1Kgs 18:22 w10 to 1Kgs 18:34 w16 | 0.388 | 9.10e-4 | 1 | -0.132 | 0.9315 | 32 |
| scan: 1Chr 12:14 w1 to 1Chr 12:25 w9 | 0.316 | 9.10e-4 | 1 | 0.176 | 0.0730 | 22 |
| scan: 1Chr 24:5 w1 to 1Chr 24:21 w5 | 0.642 | 9.10e-4 | 1 | 0.455 | 0.0114 | 32 |
| scan: 2Chr 8:10 w9 to 2Chr 9:1 w33 | 0.445 | 9.10e-4 | 1 | 0.258 | 0.0084 | 15 |
| scan: Jer 26:3 w1 to Jer 26:14 w8 | 0.241 | 9.10e-4 | 1 | 0.241 | 0.0066 | 8 |
| scan: Ezek 41:1 w1 to Ezek 41:12 w18 | 0.180 | 9.10e-4 | 1 | 0.065 | 0.0069 | 32 |
| scan: Lev 13:29 w1 to Lev 13:39 w8 | 0.193 | 9.20e-4 | 1 | 0.054 | 0.2776 | 40 |
| scan: Deut 4:12 w6 to Deut 4:24 w6 | 0.327 | 9.20e-4 | 1 | 0.138 | 0.1518 | 9 |
| scan: Deut 4:13 w11 to Deut 4:21 w5 | 0.465 | 9.20e-4 | 1 | 0.562 | 0.0014 | 6 |
| scan: Deut 33:9 w14 to Deut 33:21 w8 | 0.600 | 9.20e-4 | 1 | 0.579 | 0.0049 | 20 |
| scan: Deut 34:2 w1 to Deut 34:11 w14 | 0.418 | 9.20e-4 | 1 | 0.284 | 0.0377 | 13 |
| scan: Judg 6:15 w1 to Judg 6:26 w9 | 0.422 | 9.20e-4 | 1 | 0.232 | 0.0226 | 23 |
| scan: Judg 15:10 w7 to Judg 16:2 w20 | 0.336 | 9.20e-4 | 1 | 0.398 | 0.0013 | 16 |
| scan: 1Sam 4:21 w9 to 1Sam 5:9 w18 | 0.329 | 9.20e-4 | 1 | 0.296 | 0.0080 | 36 |
| scan: 2Sam 3:14 w1 to 2Sam 3:23 w18 | 0.156 | 9.20e-4 | 1 | 0.096 | 0.0936 | 23 |
| scan: 1Kgs 9:2 w1 to 1Kgs 9:11 w13 | 0.302 | 9.20e-4 | 1 | 0.514 | 0.0030 | 14 |
| scan: 1Chr 2:2 w1 to 1Chr 2:13 w10 | 0.486 | 9.20e-4 | 1 | 0.484 | 0.0141 | 16 |
| scan: 1Chr 2:3 w1 to 1Chr 2:13 w6 | 0.486 | 9.20e-4 | 1 | 0.484 | 0.0141 | 15 |
| scan: Isa 30:18 w1 to Isa 30:28 w15 | 0.700 | 9.20e-4 | 1 | 0.000 | 0.5667 | 19 |
| scan: Isa 34:15 w8 to Isa 35:8 w18 | 0.739 | 9.20e-4 | 1 | 0.468 | 0.0146 | 17 |
| scan: Jer 42:13 w1 to Jer 42:20 w25 | 0.291 | 9.20e-4 | 1 | 0.264 | 0.0173 | 8 |
| scan: Ezek 1:18 w6 to Ezek 2:2 w9 | 0.336 | 9.20e-4 | 1 | 0.362 | 0.0220 | 10 |
| scan: Ezek 21:14 w9 to Ezek 21:25 w5 | 0.636 | 9.20e-4 | 1 | 0.584 | 0.0037 | 22 |
| scan: Amos 2:10 w1 to Amos 3:4 w13 | 0.719 | 9.20e-4 | 1 | 0.573 | 0.0380 | 15 |
| scan: Zech 12:13 w7 to Zech 14:2 w13 | 0.479 | 9.20e-4 | 1 | 0.285 | 0.0491 | 20 |
| scan: Gen 44:26 w5 to Gen 45:4 w8 | 0.300 | 9.30e-4 | 1 | 0.428 | 6.38e-5 | 9 |
| scan: Exod 9:12 w1 to Exod 9:20 w13 | 0.435 | 9.30e-4 | 1 | 0.637 | 0.0135 | 7 |
| scan: Exod 39:32 w7 to Exod 40:2 w5 | 0.522 | 9.30e-4 | 0 | - | - | 8 |
| scan: Deut 25:1 w10 to Deut 25:13 w8 | 0.354 | 9.30e-4 | 1 | 0.082 | 0.2141 | 12 |
| scan: Deut 25:2 w1 to Deut 25:13 w6 | 0.354 | 9.30e-4 | 1 | 0.031 | 0.3906 | 9 |
| scan: Deut 26:9 w5 to Deut 26:16 w11 | 0.545 | 9.30e-4 | 1 | 0.341 | 0.0237 | 9 |
| scan: 1Sam 17:8 w12 to 1Sam 17:19 w10 | 0.409 | 9.30e-4 | 0 | - | - | 0 |
| scan: 1Kgs 12:14 w1 to 1Kgs 12:26 w3 | 0.313 | 9.30e-4 | 1 | 0.129 | 0.1372 | 17 |
| scan: 1Chr 9:33 w1 to 1Chr 9:44 w14 | 0.763 | 9.30e-4 | 1 | 0.640 | 0.0186 | 41 |
| scan: 1Chr 9:33 w8 to 1Chr 9:44 w14 | 0.660 | 9.30e-4 | 1 | 0.640 | 0.0186 | 41 |
| scan: 1Chr 16:33 w5 to 1Chr 16:42 w12 | 0.538 | 9.30e-4 | 1 | 0.396 | 0.0241 | 22 |
| scan: 1Chr 20:7 w4 to 1Chr 21:11 w4 | 0.307 | 9.30e-4 | 1 | -0.183 | 0.9048 | 22 |
| scan: 2Chr 35:21 w21 to 2Chr 36:5 w16 | 0.427 | 9.30e-4 | 1 | 0.054 | 0.2983 | 18 |
| scan: Isa 48:21 w9 to Isa 49:11 w6 | 0.366 | 9.30e-4 | 1 | 0.282 | 0.0092 | 14 |
| scan: Jer 26:3 w7 to Jer 26:14 w8 | 0.254 | 9.30e-4 | 1 | 0.208 | 0.0217 | 8 |
| scan: Jer 50:31 w8 to Jer 50:42 w13 | 0.496 | 9.30e-4 | 1 | 0.329 | 0.0429 | 27 |
| scan: Ezek 3:7 w12 to Ezek 3:19 w9 | 0.495 | 9.30e-4 | 1 | 0.398 | 0.0245 | 15 |
| scan: Ezek 22:15 w6 to Ezek 22:26 w15 | 0.449 | 9.30e-4 | 1 | 0.181 | 0.0629 | 25 |
| scan: Ezek 22:15 w6 to Ezek 22:26 w20 | 0.419 | 9.30e-4 | 1 | 0.021 | 0.4331 | 25 |
| scan: Ezek 31:18 w9 to Ezek 32:11 w9 | 0.407 | 9.30e-4 | 1 | 0.338 | 0.0299 | 15 |
| scan: Ezek 48:19 w1 to Ezek 48:32 w18 | 0.221 | 9.30e-4 | 1 | -0.035 | 0.7203 | 13 |
| scan: Amos 8:10 w16 to Amos 9:8 w21 | 0.383 | 9.30e-4 | 1 | 0.429 | 0.0011 | 30 |
| scan: Gen 1:28 w13 to Gen 2:6 w9 | 0.352 | 9.40e-4 | 1 | 0.039 | 0.3047 | 5 |
| scan: Gen 31:2 w6 to Gen 31:11 w8 | 0.391 | 9.40e-4 | 1 | 0.393 | 0.0132 | 9 |
| scan: Exod 26:33 w1 to Exod 27:5 w6 | 0.599 | 9.40e-4 | 1 | -0.600 | 0.8333 | 20 |
| scan: Lev 21:21 w15 to Lev 22:8 w6 | 0.350 | 9.40e-4 | 1 | -0.243 | 0.9112 | 12 |
| scan: Num 28:12 w1 to Num 28:21 w5 | 0.409 | 9.40e-4 | 1 | 0.085 | 0.1230 | 26 |
| scan: Judg 4:5 w1 to Judg 4:11 w16 | 0.463 | 9.40e-4 | 1 | 0.129 | 0.3419 | 23 |
| scan: Judg 11:37 w8 to Judg 12:6 w24 | 0.436 | 9.40e-4 | 1 | 0.402 | 0.0010 | 26 |
| scan: 1Sam 28:12 w1 to 1Sam 28:21 w23 | 0.406 | 9.40e-4 | 1 | 0.389 | 4.50e-4 | 8 |
| scan: 1Kgs 3:20 w12 to 1Kgs 4:4 w5 | 0.267 | 9.40e-4 | 1 | 0.413 | 1.90e-4 | 10 |
| scan: 1Kgs 15:9 w1 to 1Kgs 15:18 w17 | 0.441 | 9.40e-4 | 1 | 0.031 | 0.4066 | 17 |
| scan: 1Chr 2:30 w5 to 1Chr 2:45 w3 | 0.489 | 9.40e-4 | 1 | 0.470 | 5.90e-4 | 55 |
| scan: Neh 7:63 w1 to Neh 8:1 w24 | 0.401 | 9.40e-4 | 1 | 0.177 | 0.1927 | 20 |
| scan: Isa 2:11 w8 to Isa 2:21 w13 | 0.834 | 9.40e-4 | 1 | -0.310 | 0.8438 | 15 |
| scan: Isa 23:16 w1 to Isa 24:9 w7 | 0.430 | 9.40e-4 | 1 | 0.163 | 0.2014 | 20 |
| scan: Ezek 3:14 w1 to Ezek 3:23 w15 | 0.636 | 9.40e-4 | 1 | 0.011 | 0.4790 | 11 |
| scan: Ezek 22:15 w1 to Ezek 22:27 w12 | 0.410 | 9.40e-4 | 1 | -0.028 | 0.5978 | 26 |
| scan: Ezek 41:1 w1 to Ezek 41:13 w6 | 0.149 | 9.40e-4 | 1 | 0.157 | 2.37e-5 | 35 |
| scan: Ezek 43:8 w11 to Ezek 43:19 w18 | 0.636 | 9.40e-4 | 1 | 0.425 | 0.0048 | 35 |
| scan: Amos 4:11 w1 to Amos 5:8 w9 | 0.484 | 9.40e-4 | 1 | -0.070 | 0.6898 | 19 |
| scan: Zech 2:2 w5 to Zech 3:1 w9 | 0.319 | 9.40e-4 | 1 | 0.344 | 0.0065 | 15 |
| scan: Zech 9:17 w6 to Zech 10:8 w5 | 0.524 | 9.40e-4 | 1 | 0.402 | 0.0224 | 17 |
| scan: Gen 32:17 w1 to Gen 32:26 w11 | 0.513 | 9.50e-4 | 1 | 0.204 | 0.2429 | 9 |
| scan: Exod 25:26 w6 to Exod 25:38 w4 | 0.485 | 9.50e-4 | 1 | 0.344 | 0.0022 | 45 |
| scan: Exod 36:4 w1 to Exod 36:13 w4 | 0.389 | 9.50e-4 | 0 | - | - | 0 |
| scan: Num 1:3 w1 to Num 1:17 w3 | 0.312 | 9.50e-4 | 1 | 0.402 | 1.10e-4 | 23 |
| scan: Num 1:4 w1 to Num 1:16 w10 | 0.439 | 9.50e-4 | 1 | 0.258 | 0.0415 | 20 |
| scan: Num 33:35 w1 to Num 33:43 w4 | 0.510 | 9.50e-4 | 1 | 0.440 | 0.5000 | 38 |
| scan: Deut 13:14 w5 to Deut 14:7 w10 | 0.511 | 9.50e-4 | 1 | 0.665 | 0.0111 | 34 |
| scan: Josh 15:3 w12 to Josh 15:11 w18 | 0.153 | 9.50e-4 | 1 | -0.038 | 0.7716 | 44 |
| scan: Judg 11:33 w14 to Judg 12:2 w17 | 0.505 | 9.50e-4 | 1 | 0.349 | 0.0053 | 21 |
| scan: Judg 11:40 w1 to Judg 12:12 w7 | 0.392 | 9.50e-4 | 1 | 0.592 | 1.27e-5 | 28 |
| scan: 1Kgs 13:9 w1 to 1Kgs 13:17 w12 | 0.547 | 9.50e-4 | 1 | 0.273 | 0.1065 | 10 |
| scan: 1Kgs 22:17 w1 to 1Kgs 22:27 w17 | 0.323 | 9.50e-4 | 1 | 0.121 | 0.1202 | 9 |
| scan: 2Kgs 17:24 w15 to 2Kgs 17:36 w15 | 0.242 | 9.50e-4 | 1 | 0.051 | 0.2768 | 36 |
| scan: Eccl 2:9 w1 to Eccl 2:20 w11 | 0.313 | 9.50e-4 | 1 | 0.280 | 0.0141 | 12 |
| scan: Song 5:2 w1 to Song 5:11 w7 | 0.343 | 9.50e-4 | 1 | 1.000 | 0.3333 | 26 |
| scan: Isa 2:11 w8 to Isa 2:21 w5 | 0.853 | 9.50e-4 | 1 | -0.310 | 0.8438 | 15 |
| scan: Isa 30:12 w10 to Isa 30:24 w7 | 0.502 | 9.50e-4 | 1 | 0.085 | 0.3555 | 23 |
| scan: Isa 30:13 w1 to Isa 30:23 w19 | 0.502 | 9.50e-4 | 1 | 0.345 | 0.1047 | 20 |
| scan: Dan 2:45 w1 to Dan 3:6 w5 | 0.300 | 9.50e-4 | 1 | 0.275 | 0.0597 | 27 |
| scan: Obad 1:6 w1 to Obad 1:18 w13 | 0.436 | 9.50e-4 | 1 | 0.488 | 0.0016 | 26 |
| scan: Zech 4:2 w6 to Zech 4:12 w16 | 0.436 | 9.50e-4 | 1 | 0.499 | 1.20e-4 | 11 |
| scan: Gen 38:7 w8 to Gen 38:17 w13 | 0.396 | 9.60e-4 | 1 | 0.144 | 0.1894 | 19 |
| scan: Exod 12:40 w1 to Exod 12:51 w13 | 0.357 | 9.60e-4 | 1 | 0.343 | 0.0274 | 11 |
| scan: Exod 25:18 w1 to Exod 25:25 w10 | 0.555 | 9.60e-4 | 1 | 0.175 | 0.2001 | 18 |
| scan: Exod 33:4 w8 to Exod 33:14 w5 | 0.353 | 9.60e-4 | 1 | 0.241 | 0.0033 | 11 |
| scan: Num 7:2 w7 to Num 7:12 w11 | 0.473 | 9.60e-4 | 1 | 0.462 | 0.0014 | 14 |
| scan: Num 15:16 w1 to Num 15:25 w9 | 0.698 | 9.60e-4 | 1 | 0.566 | 0.0123 | 7 |
| scan: Num 31:7 w9 to Num 31:18 w10 | 0.427 | 9.60e-4 | 1 | 0.115 | 0.2742 | 19 |
| scan: Deut 21:12 w5 to Deut 21:19 w12 | 0.561 | 9.60e-4 | 1 | 0.900 | 0.1111 | 14 |
| scan: Deut 22:28 w1 to Deut 23:7 w13 | 0.403 | 9.60e-4 | 1 | 0.000 | 1.0000 | 10 |
| scan: Judg 11:34 w1 to Judg 12:1 w21 | 0.586 | 9.60e-4 | 1 | 0.465 | 0.0016 | 15 |
| scan: 1Chr 1:32 w13 to 1Chr 1:44 w2 | 0.277 | 9.60e-4 | 1 | 0.000 | 1.0000 | 61 |
| scan: 2Chr 11:13 w6 to 2Chr 12:2 w11 | 0.310 | 9.60e-4 | 1 | 0.389 | 0.0017 | 21 |
| scan: 2Chr 12:13 w1 to 2Chr 13:8 w10 | 0.367 | 9.60e-4 | 1 | 0.323 | 0.0209 | 27 |
| scan: 2Chr 25:8 w1 to 2Chr 25:16 w26 | 0.366 | 9.60e-4 | 1 | 0.315 | 0.0136 | 18 |
| scan: Ps 69:9 w5 to Ps 69:20 w4 | 0.685 | 9.60e-4 | 1 | 0.622 | 0.0080 | 7 |
| scan: Song 5:2 w1 to Song 5:12 w10 | 0.367 | 9.60e-4 | 1 | 1.000 | 0.1667 | 26 |
| scan: Isa 2:13 w1 to Isa 3:2 w3 | 0.819 | 9.60e-4 | 1 | 0.383 | 0.1667 | 18 |
| scan: Isa 2:13 w1 to Isa 3:2 w7 | 0.819 | 9.60e-4 | 1 | 0.236 | 0.2778 | 18 |
| scan: Jer 25:36 w7 to Jer 26:9 w21 | 0.345 | 9.60e-4 | 1 | 0.202 | 0.0752 | 15 |
| scan: Jer 36:29 w1 to Jer 37:9 w11 | 0.287 | 9.60e-4 | 1 | 0.352 | 0.0049 | 18 |
| scan: Jer 48:18 w1 to Jer 48:27 w14 | 0.368 | 9.60e-4 | 1 | 0.000 | 1.0000 | 33 |
| scan: Ezek 17:4 w1 to Ezek 17:13 w13 | 0.532 | 9.60e-4 | 1 | 0.576 | 0.0056 | 28 |
| scan: Ezek 41:4 w1 to Ezek 41:15 w18 | 0.173 | 9.60e-4 | 1 | 0.042 | 0.2061 | 32 |
| scan: Dan 5:15 w1 to Dan 5:26 w3 | 0.223 | 9.60e-4 | 1 | 0.308 | 0.0250 | 25 |
| scan: Zech 8:14 w16 to Zech 9:3 w10 | 0.309 | 9.60e-4 | 1 | 0.222 | 0.0018 | 11 |
| scan: Zech 8:15 w1 to Zech 9:3 w4 | 0.309 | 9.60e-4 | 1 | 0.320 | 0.0012 | 10 |
| scan: Gen 16:3 w16 to Gen 16:15 w4 | 0.352 | 9.70e-4 | 1 | 0.411 | 9.90e-4 | 19 |
| scan: Exod 38:19 w1 to Exod 38:31 w8 | 0.328 | 9.70e-4 | 1 | 0.066 | 0.1951 | 44 |
| scan: Exod 39:32 w7 to Exod 40:1 w5 | 0.533 | 9.70e-4 | 1 | 0.262 | 0.0522 | 7 |
| scan: Num 34:28 w5 to Num 35:9 w5 | 0.261 | 9.70e-4 | 1 | 0.366 | 1.30e-4 | 21 |
| scan: 1Sam 30:24 w1 to 1Sam 31:4 w28 | 0.711 | 9.70e-4 | 1 | 0.229 | 0.2753 | 25 |
| scan: 1Kgs 17:24 w1 to 1Kgs 18:10 w23 | 0.341 | 9.70e-4 | 1 | 0.085 | 0.1957 | 18 |
| scan: 1Kgs 18:23 w1 to 1Kgs 18:34 w16 | 0.403 | 9.70e-4 | 1 | 0.007 | 0.4704 | 29 |
| scan: 2Chr 8:4 w1 to 2Chr 8:11 w11 | 0.497 | 9.70e-4 | 1 | 0.373 | 0.0065 | 15 |
| scan: Job 1:3 w1 to Job 1:11 w13 | 0.468 | 9.70e-4 | 1 | 0.412 | 0.0176 | 14 |
| scan: Ps 29:1 w7 to Ps 29:11 w4 | 0.270 | 9.70e-4 | 1 | 0.121 | 0.0248 | 11 |
| scan: Ps 79:1 w11 to Ps 79:11 w9 | 0.848 | 9.70e-4 | 1 | 0.237 | 0.2082 | 9 |
| scan: Ps 79:2 w1 to Ps 79:11 w6 | 0.848 | 9.70e-4 | 1 | 0.684 | 0.0345 | 7 |
| scan: Ps 79:2 w1 to Ps 79:11 w9 | 0.848 | 9.70e-4 | 1 | 0.684 | 0.0345 | 7 |
| scan: Isa 2:2 w1 to Isa 2:12 w12 | 0.685 | 9.70e-4 | 1 | 0.575 | 0.0032 | 12 |
| scan: Isa 66:11 w6 to Isa 66:19 w15 | 0.588 | 9.70e-4 | 1 | 0.328 | 0.0565 | 20 |
| scan: Jer 14:14 w15 to Jer 15:3 w20 | 0.347 | 9.70e-4 | 1 | -0.089 | 0.7896 | 20 |
| scan: Zech 3:9 w1 to Zech 4:10 w20 | 0.436 | 9.70e-4 | 1 | 0.299 | 0.0209 | 8 |
| scan: Gen 5:30 w13 to Gen 6:10 w10 | 0.460 | 9.80e-4 | 1 | 0.389 | 9.10e-4 | 16 |
| scan: Exod 14:7 w9 to Exod 14:17 w14 | 0.434 | 9.80e-4 | 1 | 0.250 | 0.0267 | 15 |
| scan: Exod 15:15 w9 to Exod 15:26 w15 | 0.497 | 9.80e-4 | 1 | 0.368 | 0.0100 | 21 |
| scan: Exod 37:14 w1 to Exod 37:23 w8 | 0.426 | 9.80e-4 | 0 | - | - | 0 |
| scan: Judg 7:6 w10 to Judg 7:13 w7 | 0.581 | 9.80e-4 | 1 | 0.367 | 0.0078 | 6 |
| scan: 1Kgs 8:7 w8 to 1Kgs 8:17 w5 | 0.421 | 9.80e-4 | 0 | - | - | 8 |
| scan: 1Chr 2:1 w4 to 1Chr 2:14 w4 | 0.472 | 9.80e-4 | 1 | 0.322 | 0.0549 | 17 |
| scan: Job 27:22 w1 to Job 28:9 w6 | 0.713 | 9.80e-4 | 1 | 0.605 | 0.0407 | 13 |
| scan: Job 27:22 w1 to Job 28:10 w3 | 0.713 | 9.80e-4 | 1 | 0.605 | 0.0407 | 14 |
| scan: Isa 30:13 w11 to Isa 30:20 w7 | 0.703 | 9.80e-4 | 1 | 0.818 | 0.0022 | 14 |
| scan: Isa 49:4 w9 to Isa 49:15 w6 | 0.601 | 9.80e-4 | 1 | 0.330 | 0.0139 | 11 |
| scan: Isa 49:4 w9 to Isa 49:15 w12 | 0.601 | 9.80e-4 | 1 | 0.330 | 0.0139 | 11 |
| scan: Jer 12:17 w1 to Jer 13:12 w24 | 0.316 | 9.80e-4 | 1 | 0.269 | 0.0350 | 14 |
| scan: Ezek 33:21 w9 to Ezek 33:32 w14 | 0.378 | 9.80e-4 | 1 | 0.532 | 6.90e-4 | 16 |
| scan: Ezek 36:29 w1 to Ezek 37:2 w4 | 0.566 | 9.80e-4 | 1 | 0.184 | 0.1704 | 15 |
| scan: Dan 8:16 w6 to Dan 8:25 w10 | 0.693 | 9.80e-4 | 1 | 0.218 | 0.1747 | 9 |
| scan: Zeph 1:18 w16 to Zeph 2:11 w9 | 0.559 | 9.80e-4 | 1 | 0.148 | 0.1568 | 24 |
| scan: Gen 3:24 w4 to Gen 4:11 w3 | 0.197 | 9.90e-4 | 1 | 0.196 | 0.0123 | 4 |
| scan: Gen 42:20 w10 to Gen 42:32 w6 | 0.370 | 9.90e-4 | 1 | 0.406 | 0.0124 | 11 |
| scan: Exod 6:5 w1 to Exod 6:15 w10 | 0.231 | 9.90e-4 | 1 | 0.183 | 0.0333 | 18 |
| scan: Exod 18:6 w1 to Exod 18:13 w15 | 0.435 | 9.90e-4 | 1 | 0.708 | 3.50e-4 | 12 |
| scan: Num 7:2 w7 to Num 7:12 w6 | 0.505 | 9.90e-4 | 1 | 0.310 | 0.0082 | 14 |
| scan: Num 33:33 w4 to Num 33:45 w2 | 0.391 | 9.90e-4 | 1 | 0.716 | 0.1667 | 55 |
| scan: Deut 21:22 w8 to Deut 22:6 w21 | 0.497 | 9.90e-4 | 1 | 0.468 | 0.0300 | 9 |
| scan: Deut 26:7 w6 to Deut 26:18 w10 | 0.425 | 9.90e-4 | 1 | 0.283 | 0.0189 | 13 |
| scan: 1Sam 14:3 w1 to 1Sam 14:14 w14 | 0.207 | 9.90e-4 | 1 | 0.088 | 0.1851 | 27 |
| scan: 1Sam 15:7 w5 to 1Sam 15:15 w18 | 0.454 | 9.90e-4 | 1 | 0.156 | 0.1031 | 18 |
| scan: 1Sam 30:8 w1 to 1Sam 30:15 w21 | 0.570 | 9.90e-4 | 1 | 0.522 | 0.0031 | 17 |
| scan: 2Kgs 18:1 w1 to 2Kgs 18:10 w7 | 0.509 | 9.90e-4 | 1 | 0.417 | 0.0094 | 18 |
| scan: 1Chr 2:31 w4 to 1Chr 2:43 w2 | 0.763 | 9.90e-4 | 1 | 0.000 | 1.0000 | 43 |
| scan: 2Chr 6:3 w1 to 2Chr 6:13 w17 | 0.389 | 9.90e-4 | 1 | 0.344 | 0.0017 | 4 |
| scan: 2Chr 18:16 w14 to 2Chr 18:26 w16 | 0.330 | 9.90e-4 | 1 | 0.146 | 0.0451 | 11 |
| scan: Ezek 42:14 w18 to Ezek 43:3 w21 | 0.532 | 9.90e-4 | 1 | 0.339 | 0.0247 | 16 |
| scan: Ezek 45:8 w1 to Ezek 45:17 w13 | 0.503 | 9.90e-4 | 1 | 0.642 | 1.20e-4 | 21 |
| scan: Mic 5:5 w4 to Mic 6:1 w13 | 0.439 | 9.90e-4 | 1 | 0.229 | 0.1291 | 21 |
| scan: Zech 12:8 w1 to Zech 13:4 w14 | 0.524 | 9.90e-4 | 1 | 0.414 | 0.0012 | 18 |
