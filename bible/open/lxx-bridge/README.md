# Hebrew-to-Greek bridge

How a Hebrew word of the Old Testament is rendered in the Septuagint's Greek,
as Strong's numbers. Method and measurement:
[`../reports/scripture-lxx-bridge-measurement-2026-10-19.md`](../reports/scripture-lxx-bridge-measurement-2026-10-19.md).

* `lxx-bridge.tsv`: the table itself, 17,775 rows over 7,792 Hebrew lemmas.
  Each row is a Hebrew Strong's number, the rank of a Greek candidate (1 is
  the most likely rendering, at most 3 per Hebrew lemma), the Greek Strong's
  number, and IBM Model 1's t(g | h). Fitted over 22,683 Brenton verses
  paired with their TAHOT verses; the header comment gives the counts. On the
  99 checked pairs below its top candidate is right 98% of the time (P@1
  0.98) and an acceptable one is always in its top 3 (hit@3 1.00).
* `lxx-bridge-gold.tsv`: 99 hand-checked pairs (63 common equivalences and 36
  mid- and low-frequency ones). Each was checked against STEPBible's TBESH and
  TBESG glosses. A Greek lemma listed is an acceptable rendering of the Hebrew
  one. A sanity check, single-annotated.
* `lxx-bridge-b1-audit.tsv`: the bridge's 808 top choices that Abbott-Smith's
  Septuagint notes (via TBESG) contradict, for a reviewer. The bridge is not
  changed by it.

Sources: Brenton (public domain); STEPBible TAHOT, TAGNT, TVTMS, TBESH and
TBESG (CC BY 4.0). See [`../ATTRIBUTION.md`](../ATTRIBUTION.md).
