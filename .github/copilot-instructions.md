# GitHub Copilot Instructions

- When a pull request addresses a GitHub issue, include an explicit closing reference in the PR description, such as `Closes #123` or `Closes iricigor/3dns#123`.
- When updating a PR description later (for example via progress reporting), preserve any existing issue-closing reference and re-include it in every updated `prDescription`, even when the rest of the body is checklist-only.
- When a pull request modifies UI in generated HTML (for example `index.html`), include at least one screenshot of the implemented functionality in the PR (before/after screenshots are preferred when applicable).
- Each time `index.html` is modified, update the Settings drawer `About` section with the latest timestamp, a short explanation of the HTML change, and a link to the last PR.
