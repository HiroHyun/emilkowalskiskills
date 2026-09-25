# Fork maintenance

This fork preserves HiroHyun's customized Codex skills. Treat the installed
customizations as the baseline when incorporating upstream changes.

- Fetch upstream and review its diff before merging. Use a temporary branch and
  worktree so the installed main checkout stays usable during conflict resolution.
- Compare overlapping guidance on intent, scope, correctness, and usefulness.
  Preserve local behavior when it remains more effective. Ask the user when the
  choice materially changes behavior and the evidence does not settle it.
- Review cleanly merged edits too; Git can combine instructions that disagree.
- Preserve conditional references and explicit-only invocation policies unless
  the user requests a change or a reviewed update justifies it.
- Validate affected skills and their reference links before updating main.
- Commit customizations and push them to origin. Keep upstream pointed at
  https://github.com/emilkowalski/skills.git.
