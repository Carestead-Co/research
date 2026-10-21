<!-- SPDX-License-Identifier: CC-BY-4.0 -->

# Scripture research, track 2b results: short-passage style with power (2026-10-20)

Track 2b of the class A programme, run once against the frozen
pre-registration in
[scripture-research-class-a.md](scripture-research-class-a.md) (track 2b),
which was committed and pushed before any of its code was written. The corpus
is track 1's (fingerprint `95c126c59cd9af8d`, the one track 2 read). Nothing
was changed after the run. The generated report is reproduced in full below
the reading. Reproduce it with:

```bash
cargo run --release -p flock-api-server --bin flock-scripture-import -- research style-short
```

## Reading

* **The statistic.** The selection study planted Matthew into Acts and Acts
  into Matthew and read no target. It chose **S5**: the function-word
  bigram ratio plus the grammar-code bigram ratio, each asking whether a
  window fits New Testament Greek in general better than it fits its own
  book. Its mean detection rate was 0.449, ahead of S4 (0.420) and S3
  (0.414). The two profile divergences (S1, S2) were far behind. The
  passages were scored by S5 alone.
* **M (Mark 16:9-20 against Mark): underpowered, power 0.085.** Luke windows
  of 169 tokens planted into Mark were detected 8.5% of the time, against a
  floor of 50%. Track 2's vocabulary test managed 10%. The observed p = 0.094
  is not evidence either way.
* **J against John: departs, p = 0.0012, power 0.985.** Luke windows planted
  into John were detected 98.5% of the time. John 7:53-8:11 fits general New
  Testament Greek better than it fits John's: its function words, the order
  they come in, and its grammar sequences. None of John's 859 same-length
  stretches scores as high (p = 1/860). The result survives a Bonferroni
  correction over the three tests (p < 0.0033).
* **J against Luke: underpowered, power 0.020.** The lower of the two gate
  pairs: John into Luke (0.050) and Mark into Luke (0.020). The observed
  p = 0.57 is not read. So the second half of the question, "does it fit Luke
  better?", stays open, exactly as in track 2.
* **What the two tracks now say together.** For John 7:53-8:11, two different
  features of the text both say "not John". Track 2 measured its vocabulary
  (p = 0.0047, power 0.900). Track 2b measures its function words and grammar
  (p = 0.0012, power 0.985). The two are not independent replications: same
  passage, same edition, same null construction. But neither statistic sees
  what the other measures, since novelty asks only whether a lemma is new and
  S5 masks every content word. For Mark 16:9-20 and for "Luke rather than
  John", neither track has the power to answer.

### Why the Synoptic hosts stay underpowered

This is an explanation of a pre-registered failure, not a retune. Both
planted pairs that failed share a feature the design did not set out to
test: the donor and the host are Synoptic texts that share a source.

* Roughly a third of Luke is material taken from Mark. So a "foreign" Luke
  window planted into Mark is often Mark's own text, lightly edited. The test is asked to find
  Mark in Mark.
* S5's reference for Mark holds Matthew and Luke, which both absorbed Mark.
  The reference therefore models Mark's phrasing well, and Mark's own windows
  score near the reference (null median +0.09, against John's -0.26).
* Matthew and Luke are long and stylistically mixed: Markan blocks, sayings
  material, Luke's Septuagintal birth narratives. A same-length stretch of
  either already varies widely, so a planted window rarely stands out. Under
  S5, Acts into Matthew reached at most 0.150 and John into Luke 0.050.

John is the opposite case. Its style is distinctive and uniform, and nothing
in the reference copies it.

## What would change the answer (a new pre-registration, not a retune)

Each of these is a new experiment with its own bar, registered before it
runs.

* **A source-independent donor and reference for Mark.** Plant Acts or a
  letter into Mark rather than Luke, and build the reference without Matthew
  and Luke. This tests whether Mark 16:9-20 departs from Mark against texts
  that did not copy Mark. Note what it gives up: the planted texts are less
  like Mark 16:9-20 in genre, so their power is an optimistic bound.
* **A discriminative model** (for example a regularised classifier of "this
  book" against "everything else" on these streams, cross-validated by
  window). It can weight the features that separate a book from the rest
  rather than counting every bigram equally.
* **The edition.** Both passages are TR text and every null window is
  NA27/28. TAGNT marks which editions carry each word, so the null windows
  could be read in their TR form, which would remove the caveat below from
  the John result.

## Caveats on the one answer

* **Edition (pre-registered).** A TR-specific particle or spelling habit
  would look foreign to John for the same reason the passage might. This
  run cannot separate the two.
* **Not authorship.** "Departs from John" says the passage's function words
  and grammar are unlike John's beyond John's own variation. It does not say
  who wrote it, and "fits Luke" was not decided.

## Generated report

Generated by `flock-scripture-import research`. Inputs (datasets pinned in `data/scripture/manifest.toml`, or tables committed under `data/scripture/research/`):

* `tagnt-mat-jhn` sha256 `ab8eaaeb68e1`
* `tagnt-act-rev` sha256 `524e32375361`

### Setup

Corpus fingerprint `95c126c59cd9af8d`. FW stream: 109 function lemmas with at least 20 function tokens keep their own symbol, everything else is its grammar class; 121 FW symbols in the counting corpus. GR stream: 464 truncated grammar codes. Alpha 0.01, power floor 0.5.

### Selection study (no target, no gate book planted)

200 seeded windows per cell (seeds 20261020 + 100 + i), detected at p < 0.01, reference without the host's and the donor's groups. **Chosen: S5 combined**, the highest mean.

| Planted | Tokens | S1 FW profile divergence | S2 GR profile divergence | S3 FW bigram ratio | S4 GR bigram ratio | S5 combined |
|---|---|---|---|---|---|---|
| Matt into Acts | 169 | 0.440 | 0.295 | 0.555 | 0.755 | 0.730 |
| Acts into Matt | 169 | 0.000 | 0.000 | 0.240 | 0.040 | 0.105 |
| Matt into Acts | 193 | 0.515 | 0.375 | 0.590 | 0.845 | 0.810 |
| Acts into Matt | 193 | 0.000 | 0.000 | 0.270 | 0.040 | 0.150 |
| Mean |  | 0.239 | 0.167 | 0.414 | 0.420 | 0.449 |

### Power gate

200 seeded windows per pair (seeds 20261020 + 200 + i), detected at p < 0.01. Only the S5 combined column gates; below 0.5 a test is underpowered. The other columns are descriptive and decide nothing.

| Planted | Tokens | S1 FW profile divergence | S2 GR profile divergence | S3 FW bigram ratio | S4 GR bigram ratio | S5 combined |
|---|---|---|---|---|---|---|
| Luke into Mark | 169 | 0.055 | 0.050 | 0.140 | 0.040 | 0.085 |
| Luke into John | 193 | 0.150 | 0.170 | 0.900 | 0.960 | 0.985 |
| John into Luke | 193 | 0.065 | 0.000 | 0.220 | 0.025 | 0.050 |
| Mark into Luke | 193 | 0.000 | 0.000 | 0.055 | 0.005 | 0.020 |

### The disputed passages

Scored by S5 combined alone. M: underpowered: the test against Mark detects planted foreign text less than half the time, so its p = 0.0942 is not read. J: John or Luke is not decided, because it departs from John (p = 0.0012); the test against Luke is underpowered and not read. Bonferroni over the three tests (descriptive): John 7:53-8:11 against John survives p < 0.0033.

| Passage | Against | Statistic | Null median | Windows | p | Power | Read |
|---|---|---|---|---|---|---|---|
| Mark 16:9-20 | Mark | 0.387 | 0.090 | 657 | 0.0942 | 0.085 | no (underpowered) |
| John 7:53-8:11 | John | 0.336 | -0.264 | 859 | 0.0012 | 0.985 | yes |
| John 7:53-8:11 | Luke | -0.026 | 0.007 | 1137 | 0.5721 | 0.020 | no (underpowered) |

