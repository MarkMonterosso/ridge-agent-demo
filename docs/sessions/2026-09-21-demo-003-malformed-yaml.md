---
id: demo-2026-09-21-003
date: 2026-09-21
  bad indentation: [this is not valid yaml
---

# Sample session note — intentionally malformed

This record's frontmatter is broken YAML on purpose (bad
indentation, unclosed bracket). RIDGE should skip it and log the
parse error, the same way it does for a real corrupted file,
instead of crashing the whole run.
