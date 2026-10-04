# Contributing

Thanks for helping out! Contributions are welcome, especially on the
[Geekstober issues](README.md#geekstober-contribution-opportunities).

## How to contribute

1. **Fork** the repository.
2. **Create a branch.** Use a descriptive name:

   ```text
   feature/improve-toolbar
   fix/dashboard-ui
   docs/improve-readme
   ```

3. **Make your change.** Keep it focused on a single issue.
4. **Test it.**

   ```bash
   cd frontend && npm run build
   cd backend && npm test
   ```

   For UI changes, run both servers and click through your change in the browser.

5. **Commit** with a clear message, for example `feat: group toolbar tools` or
   `fix: room code copy feedback`.
6. **Open a pull request** and mention the issue you are solving.

## Before you start

- Comment on the issue so nobody works on the same thing twice.
- Check existing open pull requests to avoid duplicate work.
- One issue per pull request. Unrelated refactors slow down review.

## Code style

- JavaScript only. Please do not add TypeScript.
- Follow the style of the surrounding code; do not rewrite working code just for formatting.
- Keep changes focused. No unrelated edits, dependency bumps or formatting sweeps.
- Remove unused imports, components and variables before you commit.
- Keep components readable and split anything that grows too large.

## Good pull requests

Tell us what changed, why, and how you tested it. Add a screenshot for anything visual. If you left
part of the issue undone, say so.

---

Find a bug or have an idea that is not covered by an issue? Open a new one and describe what you
expected, what happened, and how to reproduce it.

[MIT](LICENSE) licensed. Built by the Geekstober open source community.