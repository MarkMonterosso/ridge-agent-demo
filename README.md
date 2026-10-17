# ridge-agent-demo

A small, public, throwaway project archive. Its only purpose is to
let anyone run [RIDGE](https://github.com/MarkMonterosso/ridge-agent)
against a real project and see real output, without needing access
to RIDGE's own private design archive.

RIDGE's actual notes (`ridge-agent-notes`) stay private, because they
hold in-progress strategic thinking. Nothing in this repo is real —
every file here is sample data, written only to be read by RIDGE.

RIDGE itself is also a learning project — building an agent from
scratch, instead of using a framework or a no-code tool, is how I'm
teaching myself to do it. See the
[ridge-agent README](https://github.com/MarkMonterosso/ridge-agent)
for more on that.

## What's in here

This folder is a "project archive" in RIDGE's terms: a `ridge.yml`
marker file, plus sample markdown records in the folders it lists:
`docs/sessions/`, `docs/decisions/` and `docs/milestones/`.

RIDGE's own tests read this repo too, so each file below is here
for a reason. Change one and a test will probably notice.

| File | What it demonstrates |
| --- | --- |
| `docs/sessions/2026-09-21-demo-001-valid-sample.md` | A record with everything RIDGE requires (`id`, a real `date`). Counted as valid. |
| `docs/sessions/2026-09-21-demo-002-missing-date.md` | Has an `id` but no `date`. RIDGE skips it and logs why, instead of failing the run. |
| `docs/sessions/2026-09-21-demo-003-malformed-yaml.md` | Frontmatter that isn't valid YAML at all. RIDGE skips it and logs the parse error. |
| `docs/decisions/0001-sample-decision.md` | A decision record, RIDGE's third convention. Its `session` field links it back to the sample session above, the same way a real decision here traces back to the working session that made the call. Counted as valid. |
| `docs/decisions/2026-09-21-demo-004-session-in-decisions-folder.md` | Says `type: session` but sits in the decisions folder. When a file says what it is, RIDGE should go by the file. |
| `docs/sessions/2026-09-21-demo-005-no-type-line.md` | A valid session with no `type` line. It sits in the sessions folder, so RIDGE should treat it as a session. |
| `docs/milestones/P1-M1-sample-milestone.md` | A milestone record. Like RIDGE's real ones, it has no `date`. It uses `completed` instead, and RIDGE should read it anyway. |

Known issue: RIDGE currently skips the milestone file. Its checker
wants a `date` on every record, and milestone records don't have
one. This is being fixed in RIDGE's milestone M3. Until then, the
milestone file shows up in the output as a validation error.

## Running it yourself

1. Clone [`ridge-agent`](https://github.com/MarkMonterosso/ridge-agent)
   and install its dependencies (see that repo's README).
2. Clone this repo as a sibling folder to `ridge-agent`.
3. In `ridge-agent`, copy `config.example.yml` to `config.yml`. The
   example already points at this folder, so you don't need to
   change anything.
4. Run `py main.py`.

Actual output from this exact archive, using RIDGE's real, unmodified
`main.py` (captured 2026-10-14, once `ridge-agent-demo`'s `ridge.yml`
had `git_repo` pointed at `ridge-agent` itself):

```
Discovering records for convention: ('sessions', 'docs/sessions/')
Validation error in ..\ridge-agent-demo\docs\sessions\2026-09-21-demo-002-missing-date.md: Record is missing 'date' in metadata.
!!! SKIPPING ..\ridge-agent-demo\docs\sessions\2026-09-21-demo-003-malformed-yaml.md — malformed YAML frontmatter: mapping values are not allowed in this context
  in "<unicode string>", line 4, column 18
Discovering records for convention: ('decisions', 'docs/decisions/')
Found 1 commit(s) in the last 7 days, 0:00:00.
Discovered 2 valid records in project at ../ridge-agent-demo.
No duplicate ids found.
```

## Where this fits

RIDGE is built one milestone at a time. Right now (M1, M2) it can
find a project's records, sort them by convention, and validate
them, and it reads a project's git history for commit activity in a
configured lookback window; it can't yet assemble weekly facts (M3),
write the summary prose (M4), or publish the result (M6). As each
new milestone ships, this repo gets a new sample showing the new
behavior, so it stays an honest, up-to-date demonstration of what
RIDGE actually does, not what it will eventually do.

See [redmountainindustries.com/projects/ridge](https://www.redmountainindustries.com/projects/ridge)
for the weekly progress writeup.
