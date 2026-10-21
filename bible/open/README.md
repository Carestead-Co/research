# Bible research: open tier (CC BY 4.0)

Data we wrote ourselves, and data built only from public domain or CC BY 4.0
sources. Nothing here is built from [`../share-alike/`](../share-alike/).
Credit: [ATTRIBUTION.md](ATTRIBUTION.md).

| Dataset | What it is | Built from |
|---|---|---|
| [`lxx-bridge/`](lxx-bridge/) | How the Septuagint renders each Hebrew lemma (17,775 Strong's-number pairs with weights), hand-checked pairs, and an audit against Abbott-Smith's Septuagint notes | Brenton's Septuagint (PD), STEPBible TAHOT, TAGNT, TVTMS, TBESH and TBESG (CC BY 4.0) |
| [`pericopes/`](pericopes/) | 487 Gospel passage units | BSB section headings (PD) |
| [`set-b-formulas/`](set-b-formulas/) | The closed list of citation formulas ("it is written", ...) that select Gospel quotations of the Old Testament | Ours, over the BSB (PD) |
| [`genealogies/`](genealogies/) | Every name in the Bible's genealogies of Jesus' line, and the identities that join them | BSB (PD) |
| [`monarchy/`](monarchy/) | The divided monarchy's reigns and cross-kingdom synchronisms | BSB (PD) |
| [`ntvmr/`](ntvmr/) | A ledger of the INTF manuscript transcriptions the research read, by URL and sha256 | INTF NTVMR (CC BY 4.0) |
| [`reports/`](reports/) | Pre-registrations, data notes and results | All of the above |
| [`sources.toml`](sources.toml) | Every third-party dataset the work reads, pinned by URL and sha256 | |

Header comments in the files sometimes name paths in Carestead's internal
repository (`docs/...`, `crates/...`, `flock-scripture-import`). They record
where a file came from; those paths are not published.
