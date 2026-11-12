# DataFrame Contract Studio — User Guide

DataFrame Contract Studio reviews local CSV schema evidence inside PyCharm. It does not upload customer files, install Python packages, or run arbitrary Python schema files.

## Supported first release

- PyCharm 2024.2.x; PyCharm 2024.2.6 on Linux is the verified runtime.
- Local comma-separated CSV files.
- Safe declarative JSON contracts.
- Python 3.13.5, pandas 2.2.3, Pandera 0.26.1, and pytest 8.4.2 are the tested toolchain.
- UTF-8 (with optional BOM) by default; explicit cp1252 is available.

Excel, Parquet, databases, cloud files, other DataFrame engines, and untested platform combinations are not supported.

## Start an analysis

1. Open **Tools > DataFrame Contract Studio**.
2. Select a local CSV.
3. Choose **Free summary** for a bounded column and lexical-type overview, or choose the licensed **Pro** workflow.
4. For Pro, select a declarative JSON contract and optional workflow settings.
5. Explicitly approve a trusted absolute Python 3 interpreter path. The plugin never installs packages.
6. Review the status before the findings:
   - **sample** — only the configured first rows were checked;
   - **full** — the whole file was checked within the limits;
   - **incomplete** — no whole-file assurance is available.

Inferred types are suggestions based on observed rows, not guaranteed business rules.

## Declarative contract

The top-level `columns` object maps column names to rules:

- `dtype`: `int`, `float`, `string`, `date`, `datetime`, or `bool`
- `nullable` and `unique`: booleans
- `min` and `max`: numeric bounds
- `categories`: an array of allowed strings

Unknown rules are rejected. Empty CSV fields are null. Booleans are lowercase `true`/`false`, dates use `YYYY-MM-DD`, and datetimes require an ISO `T` separator.

## Evidence and Pro workflow

Findings separate missing and extra columns, dtype mismatches, nulls, uniqueness failures, range failures, category failures, and malformed rows. Values are masked by default while row and column coordinates remain available.

Pro can compare prior and current fingerprints, distinguish data changes from rule changes, apply hash-scoped reviewed exceptions, open explicitly supplied project-confined Python source references, approve a baseline only after a completed full scan, and export local JSON, HTML, and a reviewable pytest draft.

Generated tests are never executed automatically. Review them and run them manually in a controlled environment.

## Limits

- CSV size: 32 MiB
- Rows: 100,000
- Columns: 200
- Field size: 256 KiB
- Findings: 1,000
- Unique-value digests: 100,000
- Worker deadline: 30 seconds; IDE deadline: 40 seconds

Files exceeding a limit or containing malformed input are reported as incomplete.

## Privacy and support

All analysis stays local. See [Privacy Policy](PRIVACY.md) and [EULA](EULA.txt).

For support, open an issue in this repository without attaching customer data, secrets, or proprietary datasets.
