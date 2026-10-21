<!-- SPDX-License-Identifier: CC-BY-4.0 -->

# Scripture research, track 5c part 2 results: roots placed by the witnesses' dates (2026-10-20)

Track 5c, part 2, of the class A programme, run against the pre-registration in
[scripture-research-class-a.md](scripture-research-class-a.md) (track 5c, part
2). The pre-registration was committed before any run, and amended before any
application run. It roots
[part 1](scripture-research-results-stemma-collapsed-2026-10-20.md)'s
collapsed neighbour-joining tree by root-to-tip regression on each witness's
date, so the evidence scholars weigh most, a witness's age, enters the root
analysis. The generated report is reproduced in full below the reading.
Reproduce it (about 2 seconds) with:

```bash
cargo run --release -p flock-api-server --bin flock-scripture-import -- research stemma-dated
```

## Reading

* **The dated root is validated, at both passages' witness counts.**
  * Under equal costs at kappa = 0 and q = 0.05, the dated root gives the
    true archetype state in 0.88 of traditions at 21 witnesses (Mark's
    count) and 0.92 at 8 (John's), in scenario P and in scenario A. The bar
    is 0.80 in each, so it passes for both passages.
  * It holds across the rows beside the bar: 0.79-0.94. The one row under
    0.80 is 21 witnesses at q = 0.10, at 0.79.
* **Two things make the bar easier than it looks. Both are disclosed here,
  and neither changes the verdict.**
  * *P and A are mirror images under equal costs.* The two scenarios share
    seeds, and the registered flip is symmetric (loss and gain both at q),
    so scenario A's states are scenario P's complemented and score the same.
    The registration meant A to test a late insertion. Under equal costs it
    adds no test beyond P. Only the cheap-loss column separates them, and
    there A is the hard case: at the bar's setting, 0.77-0.80 against
    0.98-0.99 for P.
  * *Many traditions are trivial.* At q = 0.05, every observed witness
    agrees in 33% of traditions at 21 witnesses and in 66% at 8, and any
    root is right there. Both real passages split, so the column that
    matters is the one added after the first run:
    * at 8 witnesses (John's count), the dated root is right in **0.82** of
      the informative traditions, and part 1's midpoint root in 0.68;
    * at 21 witnesses (Mark's count), the dated root is right in **0.84**,
      and the midpoint root in 0.90.

    So on this model the dates help a small tree and cost a little on a
    larger one.
* **The application has not run, and waits for the one registered date
  source.**
  * The witness dates must be the INTF's Kurzgefasste Liste as the NTVMR
    catalogue gives it. That catalogue refused connections all of
    2026-10-20.
  * Wikipedia's manuscript lists hold all 26 dates. Only the uncial table
    attributes its dates to the INTF, and its P66 and P75 ranges are not
    the Liste's figures. By the owner's ruling, a registered study does not
    rest on an unsourced input. So `data/scripture/research/witness-dates.tsv`
    is empty, and the report stops after validation.
  * When the catalogue answers, the rows are transcribed with their
    source in a reviewed PR, and the application runs exactly as
    registered: the three year switches, both cost switches, and the
    1,000-draw range sensitivity.
* **No verdict on Mark 16:9-20 or John 7:53-8:11 comes from this part
  yet.** Part 1's validated parsimony reading stands, and it gives no weight
  to age.

## Deviations and post-run changes

* **The "when both are observed" columns** were added after the first
  validation run, once it showed how many traditions were trivial. They
  decide nothing, and the bar and its verdict are as registered.
* **The amendment** (in the pre-registration, marked *amended*) came
  after the validation run and before any application run.
  * It narrowed the date source to the INTF's Liste via the NTVMR catalogue
    alone.
  * It added the range-sensitivity analysis, because palaeographic dates are
    ranges, not points.
  * It does not touch the validation.
* **No fetch for an application that cannot run.** While the date table is
  empty, `research stemma-dated` does not load the NTVMR transcriptions, so
  it needs no cache and downloads nothing.
* **A test fixture fixed before merge.** The first range-sensitivity test
  used a star tree whose best root was exactly the centre node, so jittered
  dates moved it among equal branches. The fixture now puts the best root
  two thirds of the way along one branch. No validation figure moved.

## What would change the answer

* **The NTVMR catalogue answering.** Then the application runs as
  registered.
* **A clock that is not steady.** The validation's copies change at one
  rate per copying, with random copy gaps. A scriptorium that copied
  carefully (as 03's scribes may have) would sit closer to the root than its
  date suggests, and that is not modelled.
* **Contamination of the real tradition,** as in part 1.

## Generated report

Generated by `flock-scripture-import research`. Inputs (datasets pinned in `data/scripture/manifest.toml`, or tables committed under `data/scripture/research/`):

* `data/scripture/research/ntvmr.tsv` sha256 `678830897dc9`
* `data/scripture/research/witness-dates.tsv` sha256 `14f8ce352b41`

### Validation: generated traditions with copy dates

Part 1's generator (mu = 0.02, rho = 0.05, 500 units, a third of copies lost), with the observed witness count fixed at each passage's placed count, 100 traditions per scenario (seeds from 20261022). The archetype is dated AD 100 and each copy 20-100 years after its exemplar; each observed witness is dated only to its century (the midpoint is used). A passage starts present (scenario P) or absent (A) and flips with probability q at each copy. The truth is its state at the observed witnesses' latest common ancestor. The share is of traditions whose answer is that state; a tie or no temporal signal is wrong. Bar per passage: under equal costs at kappa = 0 and q = 0.05, the dated root's share is 0.80 or more in P and in A. Part 1's midpoint root is shown beside it and decides nothing. Under equal costs P and A score alike by construction: they share seeds and the flips are symmetric, so A's states are P's complemented.

### Validation: results

21 witnesses: **passed**; 8 witnesses: **passed**.

| Observed witnesses | Setting | Dated root, equal costs (P / A) | Dated root, cheap loss (P / A) | Midpoint root, equal costs (P / A) | Midpoint root, cheap loss (P / A) | Both states observed (P / A) | Dated root when both are observed (P / A; added after the first run) | Midpoint root when both are observed (P / A; added after the first run) |
|---|---|---|---|---|---|---|---|---|
| 21 | kappa 0, q 0.05 (the bar) | 0.88 / 0.88 | 0.99 / 0.80 | 0.92 / 0.92 | 0.96 / 0.76 | 0.67 / 0.67 | 0.84 / 0.84 | 0.90 / 0.90 |
| 21 | kappa 0.1, q 0.05 | 0.93 / 0.93 | 1.00 / 0.77 | 0.93 / 0.93 | 1.00 / 0.71 | 0.72 / 0.72 | 0.90 / 0.90 | 0.90 / 0.90 |
| 21 | kappa 0, q 0.02 | 0.93 / 0.93 | 1.00 / 0.89 | 0.93 / 0.93 | 0.97 / 0.89 | 0.31 / 0.31 | 0.77 / 0.77 | 0.77 / 0.77 |
| 21 | kappa 0, q 0.10 | 0.79 / 0.79 | 0.97 / 0.55 | 0.84 / 0.84 | 0.95 / 0.55 | 0.93 / 0.93 | 0.77 / 0.77 | 0.83 / 0.83 |
| 8 | kappa 0, q 0.05 (the bar) | 0.92 / 0.92 | 0.98 / 0.77 | 0.88 / 0.88 | 0.94 / 0.75 | 0.34 / 0.34 | 0.82 / 0.82 | 0.68 / 0.68 |
| 8 | kappa 0.1, q 0.05 | 0.93 / 0.93 | 0.99 / 0.77 | 0.88 / 0.88 | 0.99 / 0.75 | 0.31 / 0.31 | 0.77 / 0.77 | 0.61 / 0.61 |
| 8 | kappa 0, q 0.02 | 0.94 / 0.94 | 0.99 / 0.89 | 0.93 / 0.93 | 0.96 / 0.88 | 0.17 / 0.17 | 0.71 / 0.71 | 0.59 / 0.59 |
| 8 | kappa 0, q 0.10 | 0.86 / 0.86 | 0.97 / 0.61 | 0.83 / 0.83 | 0.93 / 0.58 | 0.57 / 0.57 | 0.79 / 0.79 | 0.72 / 0.72 |

### Application

The date table is empty. Its one registered source, the INTF's Kurzgefasste Liste as the NTVMR catalogue gives it, has not been transcribed (the catalogue refused connections on 2026-10-20), so the report stops after validation.

