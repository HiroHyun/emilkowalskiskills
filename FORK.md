# HiroHyun's Codex installation

`origin` is https://github.com/HiroHyun/emilkowalskiskills.git.
`upstream` is https://github.com/emilkowalski/skills.git.

The local checkout is `C:\Users\HiroHyun\.codex\repos\emilkowalskiskills`.
Installed folders under `C:\Users\HiroHyun\.codex\skills` link to this checkout
for these skills:

- animation-vocabulary
- apple-design
- emil-design-eng
- find-animation-opportunities
- improve-animations
- pick-ui-library
- prototype
- review-animations

Edits through either path change the same files. Commit and push useful edits
from this repository to preserve them on GitHub.

## Incorporating upstream updates

Start with a clean main checkout and fetch upstream. Create a temporary branch
and worktree from main, then merge `upstream/main` there. Review the resulting
instructions, including changes that merge without conflicts. Compare behavior
and preserve local guidance when it remains more effective; Git cannot make
that judgment. Follow `AGENTS.md` when resolving overlapping instructions.

Validate the affected skills and check their reference links in the temporary
worktree. Once reviewed, fast-forward the main checkout to that branch and push
main to origin. The installed links then use the merged files. Start a new Codex
task to load changed skill instructions.

Keep customizations committed before updating. Avoid resetting main to upstream
or reinstalling over the linked folders, which can discard customizations.

## Migration backup

Original installed folders and the original Codex configuration were copied to
`C:\Users\HiroHyun\.codex\backups\emilkowalskiskills-20260925-191506`.
