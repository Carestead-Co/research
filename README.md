# Carestead Research

Open research data and reports from Carestead LLC. The Bible research is
published at <https://research.carestead.co/bible> and lives under
[`bible/`](bible/).

## Licences

Two licences, by directory. Every file's licence is recorded in
[`REUSE.toml`](REUSE.toml), and the full texts are in [`LICENSES/`](LICENSES/).

| Directory | Licence | What it holds |
|---|---|---|
| everything except the row below | [CC BY 4.0](LICENSES/CC-BY-4.0.txt) | Data we wrote ourselves, and data built only from public domain or CC BY 4.0 sources |
| [`bible/share-alike/`](bible/share-alike/) | [CC BY-SA 4.0](LICENSES/CC-BY-SA-4.0.txt) | Data built from a ShareAlike source. Each source is admitted by name. |

The root [`LICENSE`](LICENSE) is the CC BY 4.0 text, because CC BY 4.0 is
the default. It does not cover `bible/share-alike/`.

Nothing here uses a non-commercial (NC) source unless its licensor has given
written permission, which is filed next to the data it covers.

## Attribution

When you use a CC BY 4.0 file, credit "Carestead Research" and link to this
repository. Also credit the upstream sources named in that dataset's
README. A CC BY-SA 4.0 file needs the same credit, and anything you build
from it and share must also be CC BY-SA 4.0.

## How the data is kept

* Third-party datasets are not copied in. Each one is named in a manifest by
  URL and sha256, and is fetched from the publisher.
* Our own tables are TSV files with a header comment that names their
  sources and method.
* Reports quote aggregate figures.

## Contributing

Corrections are welcome as issues. Pull requests are reviewed by Carestead
before merge.
