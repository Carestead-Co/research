# Sources and attribution

Everything in this directory is CC BY 4.0. Credit it as:

> Carestead Research, https://github.com/Carestead-Co/research, CC BY 4.0

A dataset built from a third party's data also needs that party's credit.

| Source | Licence | Credit to give | Used by |
|---|---|---|---|
| Berean Standard Bible (BSB), ebible.org `engbsb` | Public domain (dedicated by BSB Publishing, LLC, 2023) | None required. Credited as a courtesy: "The Holy Bible, Berean Standard Bible, BSB." | `pericopes/`, `set-b-formulas/`, `genealogies/`, `monarchy/`, reports |
| Brenton's Greek Septuagint (1851), ebible.org `grcbrent` | Public domain | None required. Credited as a courtesy. | `lxx-bridge/`, reports |
| STEPBible TAHOT, TAGNT, TVTMS, TBESH and TBESG (STEPBible-Data commit `aca7d691`) | CC BY 4.0 | "STEP Bible", linked to https://www.STEPBible.org. The data was created by Tyndale House Cambridge. | `lxx-bridge/`, reports |
| Abbott-Smith, *Manual Greek Lexicon of the New Testament* (1922), as digitized in TBESG | Public domain (the digitization is CC BY 4.0, above) | As for STEPBible | `lxx-bridge/lxx-bridge-b1-audit.tsv` |
| INTF, New Testament Virtual Manuscript Room transcriptions | CC BY 4.0, as each file's TEI header states | "Institut für Neutestamentliche Textforschung, New Testament Virtual Manuscript Room", linked to https://ntvmr.uni-muenster.de | `ntvmr/`, reports |

## Changes made to CC BY data

CC BY 4.0 asks that changes be indicated. The STEPBible files are read for
their Strong's numbers, word forms and glosses:

* Strong's numbers are used in their base form (the extended suffix letter
  dropped). Function words are left out of word sequences.
* The Hebrew-to-Greek bridge is a table fitted by IBM Model 1 over Brenton's
  verses and the TAHOT verses STEPBible's TVTMS maps them to. It is not a copy
  of any STEPBible file. Three TVTMS rows (Malachi 3:22-24) are corrected
  where its expanded and condensed tables disagree.
* The B1 audit quotes TBESH and TBESG lemmas, glosses and Hebrew words
  unchanged.

The INTF transcriptions are not copied here. `ntvmr/ntvmr.tsv` records which
files were read, and the reports give counts and verdicts drawn from them.
