# Scripture research data notes: the genealogies

The judgement calls and open textual issues behind
`data/scripture/research/genealogies.tsv` and `genealogy-people.tsv`, the inputs
of research track 4 ([pre-registration](scripture-research-class-a.md)). Dashes
inside quotations are rendered as hyphens (project Markdown convention).

Source text: Berean Standard Bible USFM (`\id GEN - Berean Study Bible`, files dated
2025-07-26). Verse numbers are the BSB's English versification. Text in curly
double quotes is copied from the BSB verse or BSB footnote named next to it, and a
script checked each one against the USFM (see "How this was verified"). Text in
'single quotes' is not BSB wording.

## 1. Two premises in the request do not match this BSB text

### 1a. Luke 3:23 does not say "so it was thought"

Luke 3:23 “Jesus Himself was about thirty years old when He began His ministry. He was regarded as the son of Joseph, the son of Heli,”

The words 'so it was thought' are not in this BSB edition. Its wording is
“He was regarded as the son of Joseph” (Luke 3:23). The Greek it translates is ὡς ἐνομίζετο,
which STEPBible TAGNT glosses 'as was supposed'. I put Joseph at luke pos 2 as
asked, and the note quotes the BSB's actual wording, not the requested wording.

### 1b. Luke 3:33 does not say "Amminadab, son of Ram"

Luke 3:33 “the son of Amminadab, the son of Admin, the son of Arni, the son of Hezron, the son of Perez, the son of Judah,”

The BSB follows the NA28 text: there are THREE names between Nahshon and Hezron
(Amminadab, Admin, Arni). Matthew, Ruth and 1 Chronicles have TWO (Amminadab, Ram).
I recorded what the BSB prints, as luke pos 49-51. The BSB has two footnotes:

* On Admin: “BYZ and TR Aram; others Ram; see Ruth 4:19 and Matthew 1:3-4.” (Luke 3:33)
* On Arni: “WH, BYZ, and TR do not include the son of Arni.” (Luke 3:33)

So the Byzantine/TR reading is 'Amminadab, son of Aram, son of Hezron', which
matches Matthew. That reading is not what the BSB prints.

I did not resolve one point. STEPBible TAGNT lists the editions for each word. For
Amminadab it lists `NA28+NA27+Tyn+SBL+Treg+TR+Byz` (no WH). For Admin and for Arni
it lists `NA28+NA27+Tyn+SBL+WH`. That says WH has Admin and Arni but not Amminadab.
The BSB footnote says WH lacks Arni. The two sources disagree about the WH reading.

Generation-count effect: Abraham to David is 14 names in Matthew (matt pos 1-14)
and 15 in Luke (luke pos 57 down to 43).

## 2. Spelling variants (BSB prints the Hebrew-style form; its footnote gives the Greek)

* Matt 1:3 Ram: “Greek Aram, a variant of Ram; also in verse 4; see 1 Chronicles 2:9-10.” (Matt 1:3)
* Matt 1:7 Asa: “Greek Asaph, a variant of Asa; also in verse 8; see 1 Chronicles 3:10.” (Matt 1:7) STEPBible tags the Greek as G760 Ἀσάφ.
* Matt 1:10 Amon: “Greek Amōs, a variant spelling of Amon; twice in this verse; see 1 Chronicles 3:14.” (Matt 1:10) STEPBible tags it G301, the SAME number as Luke 3:25's Amos, who is a different person.
* Luke 3:32 Sala for Salmon: “BYZ and TR Salmon; see Ruth 4:20-21 and Matthew 1:4-5.” (Luke 3:32) The Hebrew has Salma: “most Hebrew manuscripts Salma” (Ruth 4:20) and “Hebrew Salma; twice in this verse” (1 Chr 2:11). The BSB prints Salmon in both places. I treat Sala and Salmon as one person (`salmon`).
* Luke 3:38 Enosh: “Greek Enōs, a variant spelling of Enosh; see Genesis 5:6.” (Luke 3:38)
* Kenan (Gen 5:9) = Cainan (Luke 3:37). Luke has no footnote, and the BSB tags both Cainans in Luke with the same G2536.
* Abijah (Matt 1:7; 1 Chr 3:10) = Abijam (1 Kgs 14:31): “Abijam is a variant of Abijah; some Hebrew manuscripts and LXX Abijah; see 2 Chronicles 12:16.” (1 Kgs 14:31)
* Joram (Matt 1:8; 1 Chr 3:11) = Jehoram (1 Kgs 22:50): “Joram is a variant spelling of Jehoram.” (1 Chr 3:11)
* Uzziah (Matt 1:8) = Azariah (1 Chr 3:12; 2 Kgs 14:21): “Azariah is also called Uzziah; see 2 Chronicles 26:1.” (1 Chr 3:12)
* Jeconiah (Matt 1:11; 1 Chr 3:16) = Jehoiachin (2 Kgs 24:6): “Jeconiah is a variant of Jehoiachin; also in verse 17; see 2 Kings 24:6.” (1 Chr 3:16)
* Joash (2 Kgs 11:21): “Hebrew Jehoash, a variant of Joash (son of Ahaziah) as in verse 2” (2 Kgs 11:21)
* Abram (Gen 11:26) = Abraham (Matt 1:2; Luke 3:34). The BSB has no footnote here; the name changes at Gen 17:5.

## 3. Do NOT use the Strong's number as a person key

The same Strong's number covers different people:

* G2501 Joseph: luke pos 2, 8 and 36 are three different men.
* G4527: Sala (Luke 3:32, i.e. Salmon) AND Shelah (Luke 3:35).
* G2424: Jesus AND Joshua (Luke 3:29).
* G2536: both Cainans (Luke 3:36 and Luke 3:37).
* G301: Matthew's Amon (STEPBible) and Luke's Amos.
* G1662 Eliakim (Matt 1:13 and Luke 3:30), G2455 Judah (Luke 3:30 and 3:33), G3158 Matthat, G3017 Levi, G3197 Melchi, G3161 Mattathias.
* H5152 Nahor: Abram's grandfather (Gen 11:22) and his brother (Gen 11:26).

Use `people.tsv` for identity.

## 4. Strong's tagging in the BSB USFM is sparse

The `strongs` column holds only what the BSB tags on that name in the cited verse.
Results over the 210 rows:

* 127 rows are tagged. In 126 of them the number agrees with the proper noun
  STEPBible (TAHOT/TAGNT) has for that name in the same verse. The other row is
  `God` at Luke 3:38 (G2316). STEPBible marks that word as a common noun, so there
  was no proper-noun match. The number itself is correct.
* No row has a name tagged with two different numbers in one verse.
* 83 rows are untagged. Most of the OT rows (all of Ruth 4:19-22 and 1 Chr 2-3) are
  untagged, and so are many in Matthew: Abraham, Ram, Amminadab, Abijah, Asa, Ahaz,
  Amon, Abiud, Azor, Achim. Their `strongs` cell is empty; a cross-check
  against STEPBible gave the number for each one. Two untagged rows have no STEPBible gloss
  match and were checked by hand:
  * Matt 1:10 Amon is G301 (Greek Amōs, glossed Amos).
  * Luke 3:27 Joanan is G2490 Ἰωανάν (glossed Joannan).
* STEPBible numbers for Admin (G6002) and Arni (G6095) are STEPBible extensions.
  They are not classic Strong's numbers.
* The BSB tags are misaligned on some common words, for example Matt 1:17 “In” is
  tagged G2532. That is why every tagged name was cross-checked.

## 5. Matthew's omissions and the fourteens

Matt 1:8 “Asa was the father of Jehoshaphat, Jehoshaphat the father of Joram, and Joram the father of Uzziah.”

* Between Joram and Uzziah (Azariah), 1 Chr 3:11-12 and 2 Kings list Ahaziah, Joash
  and Amaziah. They are chr_kings pos 7-9 and kings_judah pos 6, 8 and 9.

Matt 1:11 “and Josiah the father of Jeconiah and his brothers at the time of the exile to Babylon.”

* Jehoiakim stands between Josiah and Jeconiah: “The successors of Jehoiakim: Jeconiah his son, and Zedekiah.” (1 Chr 3:16) Also 2 Kgs 24:6.

Matt 1:17 “In all, then, there were fourteen generations from Abraham to David, fourteen from David to the exile to Babylon, and fourteen from the exile to the Christ.”

* With one row per name, the matt rows give Abraham-David = 14 (pos 1-14),
  Solomon-Jeconiah = 14 (pos 15-28) and Shealtiel-Jesus = 13 (pos 29-41). How to
  reach 14 in the third group (count Jeconiah twice, count Mary, and so on) is left
  to the model.

kings_judah is a SUCCESSION list, not a father-son line. It includes:

* Athaliah, pos 7. She ruled but was not a descendant of David. Source: 2 Kgs 11:3 “for six years while Athaliah ruled the land.”
* Jehoahaz, pos 17. He was a brother of Jehoiakim.
* Zedekiah, pos 20. He was Jehoiachin's uncle.

Each of these notes says so. Drop them before comparing pos order with Matthew.

## 6. 1 Chronicles 3:16-24 (chr_kings)

### 6a. Zedekiah in 3:16

1 Chr 3:16 “The successors of Jehoiakim: Jeconiah his son, and Zedekiah.”

This could be a son of Jehoiakim, or the Zedekiah of 3:15 (Josiah's son, the last
king). I did not record him as a row.

### 6b. "Jeconiah the captive" (3:17)

1 Chr 3:17 “The descendants of Jeconiah the captive: Shealtiel his son,”

The BSB reads Hebrew אַסִּר as 'the captive'. STEPBible TAHOT tags it H0616
'prisoner', and lists H0617 (the personal name Assir) as an alternative. Reading it
as a name would add a generation (Assir) between Jeconiah and Shealtiel. I followed
the BSB.

### 6c. Shealtiel and Pedaiah (3:17-19)

1 Chr 3:18 “Malchiram, Pedaiah, Shenazzar, Jekamiah, Hoshama, and Nedabiah.”

1 Chr 3:19 “The sons of Pedaiah: Zerubbabel and Shimei.”

The plain reading is that Pedaiah is one of Jeconiah's sons, and so Shealtiel's
brother. The request asked for the line "through Shealtiel, Pedaiah, Zerubbabel". I
therefore kept Shealtiel at pos 19 and Pedaiah at pos 20.

The step from pos 19 to pos 20 is list order. The text does not state a father-son
link there, and both rows' notes say so. A model that reads consecutive pos values
as parent and child will be wrong at this point.

1 Chr 3:19 names Pedaiah as Zerubbabel's father. Ezra 3:2, Ezra 3:8, Hag 1:1 and
Matt 1:12 name Shealtiel.

### 6d. Hananiah, Abiud and Rhesa (3:19-20)

1 Chr 3:19 “The children of Zerubbabel: Meshullam and Hananiah, their sister Shelomith,”

1 Chr 3:20 “and five others: Hashubah, Ohel, Berechiah, Hasadiah, and Jushab-hesed.”

Neither Abiud (Matt 1:13) nor Rhesa (Luke 3:27) is among them.

### 6e. Shecaniah (3:21)

1 Chr 3:21 “The descendants of Hananiah: Pelatiah, Jeshaiah, and the sons of Rephaiah, of Arnan, of Obadiah, and of Shecaniah.”

How Shecaniah relates to Hananiah is not stated. He could be a son, or a member of
a later or collateral generation. I recorded him because 3:22 continues his line.

### 6f. The count of six (3:22)

1 Chr 3:22 “The six descendants of Shecaniah were Shemaiah and his sons: Hattush, Igal, Bariah, Neariah, and Shaphat.”

Five sons are named. The count of six works only if Shemaiah is counted. I recorded
Shemaiah, then Neariah as his son.

### 6g. The last generation (3:24)

1 Chr 3:24 “The sons of Elioenai: Hodaviah, Eliashib, Pelaiah, Akkub, Johanan, Delaiah, and Anani - seven in all.”

The chapter follows none of the seven further, so I put them in the note on
Elioenai (pos 26) and gave them no rows. If the model counts generations after
Zerubbabel, it should add one for this generation.

## 7. Luke 3:36: Cainan, absent from Hebrew Genesis 11

Luke 3:36 “the son of Cainan, the son of Arphaxad, the son of Shem, the son of Noah, the son of Lamech,”

Gen 11:12 “When Arphaxad was 35 years old, he became the father of Shelah.”

The BSB footnote at Gen 11:13 gives the LXX reading. It begins: “Hebrew; LXX (see also Luke 3:35-36)” (Gen 11:13). It goes on: “When Arphaxad was 135 years old, he became the father of Cainan.” (Gen 11:13). It also says: “Note that LXX also adds 100 years to the ages of Shelah, Eber, Peleg, Reu, Serug, and Nahor in this genealogy.” (Gen 11:13)

So Shem to Abram is 10 names in gen11 and 11 in Luke (luke pos 67 down to 57). I
gave the second Cainan no people.tsv id, because he is in one source only.

## 8. Other judgement calls

* `ref` convention. Each row cites the verse that links the person to the row
  before it, which is usually the verse that names them as a son. The first row of
  each source cites the first verse in range that names that person. Many people
  are named again in the next verse. The `strongs` value comes ONLY from the cited
  verse.
* Gen 5:32 “After Noah was 500 years old, he became the father of Shem, Ham, and Japheth.” The request asked for "Noah and his sons". I recorded only Shem, because his line continues in Gen 11:10. Ham and Japheth are in the note. This applies the brother rule that was specified for chr_kings to gen5. Adding them as pos 12-13 would make Ham look like Shem's son.
* Gen 11:26 “When Terah was 70 years old, he became the father of Abram, Nahor, and Haran.” Only Abram is recorded. Nahor and Haran are in the note.
* chr_judah starts with Judah at 1 Chr 2:1, in the list of Israel's sons. Israel (Jacob) has no row.
* ezra_hag contains exactly the three statements requested. The BSB has six more
  verses with the words “Zerubbabel son of Shealtiel” (Ezra 5:2). They are Ezra 5:2, Neh 12:1,
  Hag 1:12, Hag 1:14, Hag 2:2 and Hag 2:23. They are not in lines.tsv. Say if they
  should be added. Neh 12:1 would not fit the `ezra_hag` id.
* Ruth 4:17 gives a second, shorter statement: “they named him Obed. He became the father of Jesse, the father of David.” (Ruth 4:17) The ruth rows use 4:18-22 only.
* Josiah in kings_judah cites 2 Kgs 21:24 “they made his son Josiah king in his place.” 2 Kgs 21:26 says the same thing a second time.
* In the Hebrew versification, three Kings refs have different numbers. STEPBible gives 1 Kgs 22:50 = Heb 22:51, 2 Kgs 11:21 = Heb 12:1, and 2 Kgs 12:21 = Heb 12:22. The `ref` column keeps the BSB English numbers.
* Matthan (Matt 1:15) and Matthat (Luke 3:24) are both Joseph's grandfather and have
  similar names. Some reconciliations identify them. I did NOT link them in
  people.tsv. As with Jacob and Heli, that would be a hypothesis.
* `zerubbabel_matt` includes the 1 Chr 3:19 row (son of Pedaiah). That is the usual
  identification, but the texts do not state it. Its note says so.
* Luke 3:23 sets Joseph's paternity apart from the list (Luke 3:23 “He was regarded as the son of Joseph”). Matthew 1:16 also does not call Joseph Jesus's father: “Jacob the father of Joseph, the husband of Mary, of whom was born Jesus, who is called Christ.” (Matt 1:16)
* luke pos 78 is `God`, from “the son of Adam, the son of God.” (Luke 3:38) Leave it out of generation counts.

## How this was verified

A build script turned a hand-written spec into the tables, and failed the run if
any of these checks failed:

1. Every row's name occurs as a whole word in the plain text of its cited verse. The
   plain text is the USFM with the `\w` markup, footnotes and paragraph markers
   stripped. Every ref also has to fall inside the passage range for its source.
2. `strongs` is the BSB `strong` attribute on that exact word in that verse. The run
   fails if one name carries two different numbers in a verse.
3. Every curly-quoted string, in lines.tsv notes, in people.tsv notes and in this
   file, is a substring of the named verse's text or its BSB footnotes.
4. A separate regex pass reads the chains straight from the verse text and compares
   them with the rows, name by name and in order:
   * Matthew: 'X was the father of Y'. Each father must be the previous son.
   * Luke: 'the son of X'.
   * Ruth 4:18-22.
   * Gen 5 and Gen 11: 'When X was N years old'.
   * 1 Chr 3:10-14: 'X his son'.
   * 1 Chr 2:10-12.
5. Each name is checked against STEPBible TAHOT/TAGNT for the same verse. See
   section 4.
6. Every people.tsv member must resolve to exactly one row. Every person must span
   two or more sources, unless their note says "Single source". The run also lists
   same-spelled names that are not linked, for review: Eliakim, Joseph and Judah
   are distinct people.
