# Hebrew-to-Greek bridge: checked pairs and audit

How a Hebrew word of the Old Testament is rendered in the Septuagint's Greek,
as Strong's numbers. Method and measurement:
[`../reports/scripture-lxx-bridge-measurement-2026-10-19.md`](../reports/scripture-lxx-bridge-measurement-2026-10-19.md).

* `lxx-bridge-gold.tsv`: 99 hand-checked pairs (63 common equivalences and 36
  mid- and low-frequency ones). Each was checked against STEPBible's TBESH and
  TBESG glosses. A Greek lemma listed is an acceptable rendering of the Hebrew
  one. A sanity check, single-annotated.
* `lxx-bridge-b1-audit.tsv`: the bridge's 808 top choices that Abbott-Smith's
  Septuagint notes (via TBESG) contradict, for a reviewer. The bridge is not
  changed by it.

Sources: Brenton (public domain); STEPBible TAHOT, TBESH and TBESG (CC BY
4.0). See [`../ATTRIBUTION.md`](../ATTRIBUTION.md).
