# Constellation Churches Database — release 2026-10-21

229,941 churches, 1,514 retired identifiers.

## Identifiers are the stable reference — the path is not

Every church has a Constellation Church ID: nine characters, the last two of them check digits,
always starting with a letter. Its official form is `https://constellation.church/{id}`.

Files are filed as `data/{state}/{zip3}/{id}.json` so you can browse by place
(`data/ca/921/` is the city of San Diego). A church whose address is corrected moves to another
folder, so **cite and join on the identifier, never the path**. A church with no usable ZIP is in
`data/{state}/no-zip/`, and one with no state in `data/unknown/`.

## What is here

- `data/` — one JSON file per public church: identifier, names, address, coordinates, website,
  denominational listing URL, its visible external identifiers (EIN, directory ids that have a
  page, website and social pages) and its public advisories. `name` is spelled exactly as the
  church's source record spells it (`POLO COMMUNITY CHURCH INC`); `displayName` is ours, the
  name we publish it under (`Polo Community Church`), and changes when our naming rules do.
- `retired-identifiers.json` / `.parquet` / `.csv` — every identifier that was merged into
  another church or split into several, with the churches it leads to now. If you hold an old
  identifier, look it up here.
- `churches.parquet` / `churches.csv` — the same churches in one file each, built from the JSON.
  Identifiers and ZIP codes are text; do not let a spreadsheet convert them.

In the public repository each release is the commit tagged with its date. Its Parquet and CSV
files are attached to the GitHub release of the same date and to `latest`, not committed.

## Licence

The identifiers and `retired-identifiers.*` are **CC0**: use them without restriction, in your own
systems. Everything else is CC BY-NC 4.0.

The IRS Business Master File is public domain. Where a church has a map match, its coordinates
come from [Overture Maps Foundation](https://overturemaps.org) data (CDLA Permissive 2.0).
