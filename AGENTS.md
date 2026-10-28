# Maintaining this collection

This is the user's editable Pi skills collection, not a managed upstream installation.

- Read `README.md` and `UPSTREAM.md` before changing its structure or importing upstream changes.
- Canonical instructions live in `skills/<name>/SKILL.md`; `prompts/` only provides thin short-command aliases.
- Preserve the user's refinements. Do not reinstall or synchronize the whole upstream collection.
- Keep supporting files beside their skill and resolve relative references from that directory.
- Keep the collection small. Do not add workflow dependencies or new skills without agreement.
- Keep project configuration in the target project; do not hard-code its tracker or domain conventions here.
- Record intentional deviations from the imported baseline in `UPSTREAM.md`.
- After changes, check skill frontmatter, referenced files, alias paths, and Pi resource diagnostics; tell the user to `/reload`.
