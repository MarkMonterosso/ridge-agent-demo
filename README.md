# ridge-agent-demo

A small, public, throwaway project archive. Its only purpose is to
let anyone run [RIDGE](https://github.com/MarkMonterosso/ridge-agent)
against a real project and see real output, without needing access
to RIDGE's own private design archive.

RIDGE's actual notes (`ridge-agent-notes`) stay private, because they
hold in-progress strategic thinking. Nothing in this repo is real —
every file here is sample data, written only to be read by RIDGE.

## What's in here

This folder is a "project archive" in RIDGE's terms: a `ridge.yml`
marker file, plus a few sample markdown records under
`docs/sessions/`. Three records, three outcomes:

| File | What it demonstrates |
| --- | --- |
| `2026-09-21-demo-001-valid-sample.md` | A record with everything RIDGE requires (`id`, a real `date`). Counted as valid. |
| `2026-09-21-demo-002-missing-date.md` | Has an `id` but no `date`. RIDGE skips it and logs why, instead of failing the run. |
| `2026-09-21-demo-003-malformed-yaml.md` | Frontmatter that isn't valid YAML at all. RIDGE skips it and logs the parse error. |

## Running it yourself

1. Clone [`ridge-agent`](https://github.com/MarkMonterosso/ridge-agent)
   and install its dependencies (see that repo's README).
2. Clone this repo as a sibling folder to `ridge-agent`.
3. In `ridge-agent`, point `config.yml` at this folder:
   ```yaml
   projects:
     - ../ridge-agent-demo
   ```
4. Run `py main.py`.

Actual output from this exact archive, using RIDGE's real, unmodified
`main.py` (captured 2026-09-21):

```
Discovering records for convention: ('sessions', 'docs/sessions/')
!!! SKIPPING ../ridge-agent-demo/docs/sessions/2026-09-21-demo-003-malformed-yaml.md — malformed YAML frontmatter: mapping values are not allowed here
  in "<unicode string>", line 4, column 18:
      bad indentation: [this is not valid yaml
                     ^
Validation error in ../ridge-agent-demo/docs/sessions/2026-09-21-demo-002-missing-date.md: Record is missing 'date' in metadata.
Discovered 1 valid records in project at ../ridge-agent-demo.
No duplicate ids found.
```

## Where this fits

RIDGE is built one milestone at a time. Right now (M1) it can find a
project's records and validate them; it can't yet read git history
(M2) or generate a field note (M6). As each new milestone ships,
this repo gets a new sample pair showing the new behavior, so it
stays an honest, up-to-date demonstration of what RIDGE actually
does, not what it will eventually do.

See [redmountainindustries.com/projects/ridge](https://www.redmountainindustries.com/projects/ridge)
for the weekly progress writeup.
