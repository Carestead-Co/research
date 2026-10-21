# Scripture research data notes: the divided monarchy

The open textual issues behind `data/scripture/research/kings.tsv` and
`synchronisms.tsv`, the inputs of research track 3a
([pre-registration](scripture-research-class-a.md)). Source: the Berean Standard
Bible USFM (1KI, 2KI, 2CH; public domain), English versification. A script
checked every quotation below as an exact substring of its cited verse, and
every number in the two tables against the verse it cites. "BSB footnote" means
a `\f` note in the USFM. The tables record what the text says; reconciling it
is the model's job, so nothing here is resolved.

## 1. Textual oddities in the synchronisms

### 1.1 Joram of Israel dated two ways (2Kgs.1.17 vs 2Kgs.3.1)
- 2Kgs.1.17: "Jehoram succeeded him in the second year of the reign of Jehoram son of Jehoshaphat over Judah."
- 2Kgs.3.1: "In the eighteenth year of Jehoshaphat’s reign over Judah, Jehoram son of Ahab became king of Israel"

Both are kept as accession rows. They agree only if Jehoram of Judah was co-regent
with Jehoshaphat (Jehoshaphat 18 = Jehoram of Judah 2), which the text does not say.

### 1.2 Jehoram of Judah's accession (2Kgs.8.16)
- 2Kgs.8.16: "In the fifth year of the reign of Joram son of Ahab over Israel, Jehoram son of Jehoshaphat succeeded his father as king of Judah."

The BSB has no clause "while Jehoshaphat was king of Judah" and no footnote about
it. The Masoretic Text is commonly reported to carry such a clause (often read as
evidence of a co-regency); that could not be confirmed from this source file.
The BSB's "succeeded his father" implies Jehoshaphat was dead, which sits badly
with 1.1 (Joram of Israel acceding in Jehoram of Judah's 2nd year, 2Kgs.1.17, but
Jehoram of Judah acceding in Joram's 5th, 2Kgs.8.16).

### 1.3 Ahaziah of Judah: twelfth or eleventh year of Joram (2Kgs.8.25 vs 2Kgs.9.29)
- 2Kgs.8.25: "In the twelfth year of the reign of Joram son of Ahab over Israel, Ahaziah son of Jehoram became king of Judah."
- 2Kgs.9.29: "(In the eleventh year of Joram son of Ahab, Ahaziah had become king over Judah.)"

Both kept. Usually explained by different year-counting (accession vs
non-accession); the text does not say.

### 1.4 Hoshea dated by Jotham's 20th year (2Kgs.15.30)
- 2Kgs.15.30: "In the twentieth year of Jotham son of Uzziah, Hoshea attacked Pekah, killed him, and reigned in his place."
- 2Kgs.15.33: "he reigned in Jerusalem sixteen years"
- 2Kgs.17.1: "In the twelfth year of the reign of Ahaz over Judah, Hoshea son of Elah became king of Israel"

Jotham reigned 16 years, so a "20th year of Jotham" counts past his death (into
Ahaz's reign, roughly Ahaz's 4th). It also disagrees with 2Kgs.17.1 (Ahaz's 12th).
Recorded as two accession rows for Hoshea. 2Kgs.15.5 may bear on Jotham's count
(he governed while Azariah was alive):
- 2Kgs.15.5: "his son Jotham had charge of the palace and governed the people of the land."

### 1.5 Pekah's twenty years (2Kgs.15.27)
- 2Kgs.15.27: "Pekah son of Remaliah became king of Israel, and he reigned in Samaria twenty years."

Chain of synchronisms: Pekah accedes in Azariah's 52nd (15:27); Jotham accedes in
Pekah's 2nd (15:32) and reigns 16 years; Ahaz accedes in Pekah's 17th (16:1);
Hoshea accedes in Ahaz's 12th (17:1). Counted that way, Pekah dies about his 28th
year, not his 20th. 2Kgs.15.30 (Jotham's "20th", about Pekah's 20th or 21st) fits
the 20 years; 2Kgs.17.1 does not. The row keeps the stated 20 years.

### 1.6 Baasha in Asa's 36th year (2Chr.16.1)
- 2Chr.16.1: "In the thirty-sixth year of Asa’s reign, Baasha king of Israel went up against Judah and fortified Ramah"
- 1Kgs.16.8: "In the twenty-sixth year of Asa’s reign over Judah, Elah son of Baasha became king of Israel"
- 2Chr.15.19: "And there was no war until the thirty-fifth year of Asa’s reign."
- 1Kgs.15.16: "Now there was war between Asa and Baasha king of Israel throughout their days."

By Kings, Baasha was dead by Asa's 26th year, so he cannot act in Asa's 36th.
Kept as kind `other` (it ties an Israelite king to a Judahite regnal year) with
no Baasha year in the note, because the text gives none.

### 1.7 Omri, Tibni and the 31st year of Asa (1Kgs.16.15-29)
- 1Kgs.16.21: "Half of the people supported Tibni son of Ginath as king, and half supported Omri."
- 1Kgs.16.23: "In the thirty-first year of Asa’s reign over Judah, Omri became king of Israel, and he reigned twelve years, six of them in Tirzah."
- 1Kgs.16.29: "In the thirty-eighth year of Asa’s reign over Judah, Ahab son of Omri became king of Israel"

Zimri died in Asa's 27th. Omri's 12 years fit Asa 27 to 38, not Asa 31 to 38, so
the 31st year likely marks the end of the Tibni division. Tibni has no stated
reign length, so he is only a note on Omri's row.

### 1.8 Shallum dated by "Uzziah" (2Kgs.15.13)
- 2Kgs.15.13: "In the thirty-ninth year of Uzziah’s reign over Judah, Shallum son of Jabesh became king"

Uzziah is the same king the neighbouring verses call Azariah (BSB footnote at
2Chr.26.1). Mapped to `azariah`. The verse also omits "of Israel".

### 1.9 Jehoiachin: three months, or three months and ten days
- 2Kgs.24.8: "he reigned in Jerusalem three months."
- 2Chr.36.9: "he reigned in Jerusalem three months and ten days."

Kings' value (0 years, 3 months) is in the row. Chronicles' extra ten days is in
the note. The same Chronicles verse has an age variant (BSB footnote: "most Hebrew
manuscripts eight" for "eighteen"). That is an age, not a reign length, so it is
not in the dataset.

### 1.10 Athaliah has no regnal formula
- 2Kgs.11.3: "And Joash remained hidden with his nurse in the house of the LORD for six years while Athaliah ruled the land."
- 2Kgs.11.4: "Then in the seventh year, Jehoiada sent for the commanders of hundreds"

The six years are inferred from how long Joash was hidden. There is no
accession synchronism for her or for Jehu.

## 2. Encoding decisions a reviewer should check

- Duplicate statements are kept, one row each, as instructed: Baasha (1Kgs.15.28
  and 1Kgs.15.33), Zimri (1Kgs.16.10 and 1Kgs.16.15), Ahaziah of Judah (2Kgs.8.25
  and 2Kgs.9.29), Abijam (1Kgs.15.1 and 2Chr.13.1, where Chronicles calls him
  Abijah), Joram of Israel (2Kgs.1.17 and 2Kgs.3.1), Hoshea (2Kgs.15.30 and
  2Kgs.17.1). That gives 34 accession rows for 32 distinct accessions.
- Accession rows with no "In the Nth year ... became king" wording: 1Kgs.15.28,
  1Kgs.16.10, 2Kgs.15.30 ("killed ... and reigned in his place"), 1Kgs.16.15
  ("Zimri reigned in Tirzah for seven days"), 2Kgs.1.17 ("Jehoram succeeded
  him"), 2Kgs.8.16 ("succeeded his father as king"), 2Kgs.9.29 ("had become
  king"). They are included because each dates an accession by the other
  kingdom's regnal year.
- Kind `other` rows (2Kgs.18.9, 2Kgs.18.10, 2Chr.16.1): `king`/`kingdom` hold the
  Israelite king the event concerns, and `in_year`/`of_king` hold the Judahite
  year the verse leads with. That king's own year, where given, is `king_year`.
- Kind `coincidence` (2Kgs.9.24-2Kgs.9.27): `ref` is an OSIS range, not a single
  verse. The text narrates both deaths in one episode. It never says "same year".
  - 2Kgs.9.24: "Then Jehu drew his bow and shot Joram between the shoulders."
  - 2Kgs.9.27: "So they shot Ahaziah in his chariot on the Ascent of Gur, near Ibleam, and he fled to Megiddo and died there."
  BSB footnote at 9:27 says the Hebrew wording differs and the BSB follows Syriac,
  Vulgate and LXX.
- Names: BSB spells Judah's king "Joash" (Hebrew Jehoash per footnote at 2Kgs.12.1)
  and Israel's "Jehoash" (Hebrew Joash per footnotes at 2Kgs.13.9 and 14.1). Ids are
  `joash_j` and `jehoash_i`. Israel's Joram is "Jehoram" in 2Kgs.1.17 and "Jehoram son of
  Ahab" in 2Kgs.3.1 (`joram_i`). Both Jehoahaz and Ahaziah got `_j`/`_i` suffixes.
- Statements left out of synchronisms.tsv:
  - 2Kgs.14.17: "Amaziah son of Joash king of Judah lived for fifteen years after the death of Joash son of Jehoahaz king of Israel."
    Its parallel is 2Chr.25.25. It ties the kingdoms by an interval, not by a regnal year.
  - 2Kgs.17.6: "In the ninth year of Hoshea, the king of Assyria captured Samaria"
    It only uses Israel's count, though it agrees with 2Kgs.18.10.
  - 1Kgs.22.2: "However, in the third year, Jehoshaphat king of Judah went down to visit the king of Israel,"
    This is the third year of peace (1Kgs.22.1), not a regnal year.
  - 2Kgs.11.4 ("the seventh year", of Athaliah, intra-Judah) is also left out.

## 3. Arithmetic tensions noticed (not exhaustive, not resolved)

These are left for the model to solve. The rows record what the text says.
- Jehoahaz of Israel accedes in Joash's 23rd and reigns 17 years (2Kgs.13.1), but
  his son accedes in Joash's 37th (2Kgs.13.10), not his 40th.
- Jeroboam II accedes in Amaziah's 15th (2Kgs.14.23) and Amaziah reigns 29 years.
  By that count Azariah should accede near Jeroboam's 15th, not his 27th
  (2Kgs.15.1). Zechariah's accession in Azariah's 38th (2Kgs.15.8) also leaves
  roughly a decade more than Jeroboam's 41 years cover.
- Hezekiah accedes in Hoshea's 3rd (2Kgs.18.1), which is about Ahaz's 14th by
  2Kgs.17.1, yet Ahaz reigned 16 years (2Kgs.16.2).
- Nadab accedes in Asa's 2nd and reigns 2 years, and Baasha accedes in Asa's 3rd
  (1Kgs.15.25, 1Kgs.15.33). Elah reigns 2 years from Asa's 26th, and Zimri accedes
  in Asa's 27th (1Kgs.16.8, 1Kgs.16.10). Both pairs point to inclusive counting.
