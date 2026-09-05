<!-- SPDX-License-Identifier: Apache-2.0
     SPDX-FileCopyrightText: 2026 Adam Sealey -->
# CLAUDE.md — heatSheetStamper

Coding project. Implementation detail (PDF-stamping internals, safety-limit
rationale, bugs, test coverage) lives here — in code, commit history, and
`README.md` — not in the SealVault Obsidian vault. The vault only holds a
one-line pointer back to this repo.

## What this is

Adds a DQ / NS / DFS scoring stamp (and optional SR/DR corner label) to
every page of a swim meet heat sheet PDF. Standalone tool; also
subtree-imported into `~/code/AOTools/heat-sheet-stamper/` — check both
locations if you're chasing a fix, they can drift (see README's own note on
current divergence, if any, before assuming the two are in sync).

## Run and test

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt          # runtime deps
pip install -r requirements-dev.txt      # + pytest, pylint
```

```bash
python3 stamp_pdf.py [--sr | --dr | --auto] input.pdf [output.pdf]
pytest test_stamp_pdf.py -v
pylint stamp_pdf.py
```

## Conventions

- Safety limits (`MAX_INPUT_BYTES`, `MAX_PAGES`) and the atomic-write
  pattern are deliberate hardening against malicious/malformed PDF input —
  don't relax them without updating the security test cases alongside.
- Keep the README's stated test count in sync with `test_stamp_pdf.py` when
  adding or removing tests.

## Where session memory goes

Don't write commit-by-commit narrative, bug lists, or PDF-format detail
into `Projects/*/context.md` or any SealVault `memory/` file. That detail
belongs here — git history and `README.md`. A vault session-close should
log only a one-line pointer: "heatSheetStamper: `<topic>`, see git log."
