# Scripture research, track 5 results: manuscript family trees (2026-10-20)

Track 5 of the class A programme, run against the pre-registration in
[scripture-research-class-a.md](scripture-research-class-a.md) (track 5). The
manuscript data is the Institut für Neutestamentliche Textforschung's New
Testament Virtual Manuscript Room transcriptions, licensed CC BY 4.0. The 64
files are pinned in `data/scripture/research/ntvmr.tsv`; they total 1,147,231
bytes and are never committed. The generated report is reproduced in full
below the reading. Reproduce it (about 8 seconds, after the first fetch) with:

```bash
cargo run --release -p flock-api-server --bin flock-scripture-import -- research stemma
```

## Reading

* **The builders are not validated as pre-registered, and the diagnostic says
  why.**
  * The bar was a mean normalized Robinson-Foulds distance of 0.25 or less at
    kappa = 0. Neighbour joining and parsimony both score 0.272.
  * Both recover 100% of the true copying tree's splits at kappa = 0, and
    still 88-93% at kappa = 0.2.
  * The whole error is the splits a binary tree must invent where one
    exemplar was copied several times. The bar measured that, not a wrong
    tree.
  * By the pre-registration's rule, the application below is descriptive
    only.
* **The data is thinner than the catalogue suggested.** Of the 92 early
  witnesses to Mark 16:8 and 95 to John 7:52 that the NTVMR catalogue lists,
  23 have a published transcription of Mark 15-16 and 10 of John 7-8. These
  are mostly the majuscules, as the ECM Mark and IGNTP John projects
  transcribed them.
* **Mark 16:9-20, descriptively: presence at the root is the more
  parsimonious history.**
  * 01 and 03 lack it, and 19 placed witnesses have it.
  * Under equal costs, 36 of the 39 possible root edges, and the midpoint
    root, favour presence. When loss is cheaper than gain, all 39 do.
  * 01 and 03 sit together, so one loss explains them. This is the
    parsimony reading, not a verdict on the ending. Parsimony counts events
    on a tree built from 21 witnesses, and the age and quality of 01 and 03
    weigh in no part of it. That is the external evidence the method leaves
    out by design.
* **John 7:53-8:11, descriptively: the cost switch decides.**
  * Six of the eight placed witnesses lack it: P66, P75, 01, 03, 038 and 33.
  * Under equal costs, every root edge that is not a tie, and the midpoint
    root, favour absence.
  * When loss costs a third of gain, every edge that is not a tie favours
    presence, and so does the midpoint root.
  * With eight witnesses, the tree cannot separate these hypotheses. That is
    the honest answer.

## What changed after the application first ran

* **Placeholder gaps.** The API pads every verse a document lacks with an
  empty-reason `<gap reason=""/>`. The first run read those as lacunae, which
  made 01 and 03 "undecidable" for Mark although both end at 16:8. Every real
  lacuna or illegible stretch in the 64 files names its reason (`lacuna`,
  `illegible`, `unspecified`), so empty-reason gaps are now read as absent
  verses. Only the Mark result changed.
* **INTF verse ids.** Some John transcriptions label verses `B04K8V1`. The
  parser reads that form as well as `John.8.1`. This was fixed before the
  application ran.
* **Damage and the movable nu, corrected before merge.** Review found ways
  the first runs departed from the registration.
  * *Damage.* A word lost to damage, or supplied whole by the editor, was
    dropped and then collated as an omission, so two fragmentary witnesses
    shared "om" wherever both were damaged. Lost text now leaves the base
    words and gaps around it missing, as a witness without the verse is,
    and that includes illegible letters between words (5 such gaps in the 64
    files). Text wholly lost at a passage's place (ending the verse before,
    in the passage, opening the verse after, or a leaf lost between chapter
    files) makes its witness undecidable rather than absent. A damaged word
    whose first letters survive does not, so P75, whose John 8:12 opens
    with πα and supplied letters, stays absent. No witness's state moved.
  * *The movable nu.* The fold took any final ν after ε or ι once the
    itacisms had run, so τήν met τῇ and λέγειν met λέγει. It now folds the
    itacisms first and then supplies a movable ν where Greek may drop it
    (-σι, ἐστί, a third-person -ε), so every real ν stays and a phonetic
    spelling still meets the standard one (ἔρχεσθε, ἔρχεσθαι). The known
    cost: a dative κρίσει meets the accusative κρίσιν. Supplying the ν before
    folding was tried and split every itacistic -σει, -ται and -σθαι from
    its standard spelling, inventing variation in the papyri.
  * *Effect.* The units went from 319 to 280 for Mark and from 267 to 219
    for John, and 083 dropped under the 30% attestation floor. Mark's edge
    tallies were 38 / 2 / 1 and 41 / 0 / 0 on 22 witnesses; John's are
    unchanged. Every reading above is unchanged. The validation, which uses
    generated traditions, did not move.

## What would change the answer (a new pre-registration, not a retune)

* **Collapse unsupported branches** in the inferred tree, those no unit
  changes on, before scoring RF. On this benchmark that would score what the
  builders actually recover. Track 5c ran this
  ([results](scripture-research-results-stemma-collapsed-2026-10-20.md)):
  the collapsed builders pass the bar, and the real trees lose no branch.
* **More witnesses.** Only 33 of the roughly 190 early witnesses have
  published transcriptions. The application should be re-run as the INTF
  publishes more, and the ledger regenerated in a reviewed PR.

## Generated report
Generated by `flock-scripture-import research`. Inputs (datasets pinned in `data/scripture/manifest.toml`, or tables committed under `data/scripture/research/`):

* `data/scripture/research/ntvmr.tsv` sha256 `678830897dc9`

### Validation: generated traditions

50 traditions per row: 20-40 observed witnesses, a third of all copies lost, 500 variation units, mu = 0.02, rho = 0.05, kappa as shown (seeds from 20261020). Mean normalized Robinson-Foulds distance (|A xor B| / (|A| + |B|) over the observed witnesses' splits). Bar at kappa = 0: 0.25 or less. Neighbour joining 0.272: **FAILED**. Parsimony 0.272: **FAILED**.

| kappa | NJ RF | Parsimony RF | NJ true splits found (diagnostic) | Parsimony true splits found (diagnostic) |
|---|---|---|---|---|
| 0.00 | 0.272 | 0.272 | 1.000 | 1.000 |
| 0.05 | 0.277 | 0.275 | 0.996 | 0.999 |
| 0.10 | 0.288 | 0.281 | 0.981 | 0.990 |
| 0.20 | 0.363 | 0.327 | 0.877 | 0.926 |

### Application: the data

64 transcriptions of 26 manuscripts from the INTF's New Testament Virtual Manuscript Room (CC BY 4.0, Institut für Neutestamentliche Textforschung), each pinned by sha256 in `data/scripture/research/ntvmr.tsv`: every Greek continuous-text manuscript in the NTVMR catalogue dated to AD 1000 or earlier (plus P66 and P75 for John) with a published transcription of the chapters. First hand only; spelling folded (nu-movable and the common itacisms).

### Application: Mark 16:9-20

21 witnesses placed on the trees from 280 variation units outside the passage (2 excluded for attesting under 30% of them: 083 099). Present at its place: 19. Absent there: 2 (01 03). Undecidable (lacuna or broken off): 0 (none).

| Tree | Costs | Midpoint root: least cost with the root | Root edges favouring presence / absence / tie |
|---|---|---|---|
| neighbour joining (not validated) | equal costs | present 1, absent 3 | 36 / 2 / 1 |
| neighbour joining (not validated) | loss a third of gain | present 1, absent 7 | 39 / 0 / 0 |
| parsimony (not validated) | equal costs | - | 36 / 2 / 1 |
| parsimony (not validated) | loss a third of gain | - | 39 / 0 / 0 |

### Application: John 7:53-8:11

8 witnesses placed on the trees from 219 variation units outside the passage (2 excluded for attesting under 30% of them: 019 037). Present at its place: 2. Absent there: 6 (P66 P75 01 03 038 33). Undecidable (lacuna or broken off): 0 (none).

| Tree | Costs | Midpoint root: least cost with the root | Root edges favouring presence / absence / tie |
|---|---|---|---|
| neighbour joining (not validated) | equal costs | present 4, absent 2 | 0 / 11 / 2 |
| neighbour joining (not validated) | loss a third of gain | present 5, absent 6 | 11 / 0 / 2 |
| parsimony (not validated) | equal costs | - | 0 / 11 / 2 |
| parsimony (not validated) | loss a third of gain | - | 13 / 0 / 0 |

