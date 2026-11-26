# GitHub Issues

Use `gh` from the repository root. Target `BASEDONG/EdgeOne` explicitly with `--repo BASEDONG/EdgeOne` when reading or writing issues. Verify the destination with `gh repo view` before the first write.

If `gh` needs authentication, use an active GitHub CLI login or pass the existing Git credential for this repository to the `gh` process through `GH_TOKEN`.

## Issue operations

- Publish a ticket or spec with `gh issue create --title "<title>" --body-file "<file>"`.
- Fetch a ticket with `gh issue view <number> --json number,title,body,labels,comments`.
- List tickets with `gh issue list --state open --json number,title,body,labels,comments`. Use `--label` and `--state` to narrow the results.
- Link a sub-issue with `gh issue create --parent <parent>` or `gh issue edit <parent> --add-sub-issue <child>`.
- Record a blocker with `gh issue create --blocked-by <blocker>` or `gh issue edit <child> --add-blocked-by <blocker>`. Inspect blockers with `gh issue view <child> --json blockedBy`. A ticket is unblocked once every blocker is closed.
- If native relationships are unavailable, record parent and blocker issue numbers at the top of the child body using `Part of #<parent>` and `Blocked by: #<blocker>`.
- Apply or remove labels with `gh issue edit <number> --add-label "<label>"` or `--remove-label "<label>"`.
- Comment with `gh issue comment <number> --body-file "<file>"`. To close a ticket, post the explanation first, then run `gh issue close <number>`.

## Pull requests as a triage surface

**PRs as a request surface: no.**

If enabled, read external PRs with `gh pr list`, `gh pr view`, and `gh pr diff`. Apply the same triage states through `gh pr edit`, `gh pr comment`, and `gh pr close`. GitHub issues and PRs share a number space. Resolve an ambiguous reference with `gh pr view` first and fall back to `gh issue view`.

## Wayfinding operations

- Store the map in an issue labelled `wayfinder:map`. Link tickets as sub-issues and label them `wayfinder:research`, `wayfinder:prototype`, `wayfinder:grilling`, or `wayfinder:task`.
- If native sub-issues are unavailable, list the children in a task list in the map body and put `Part of #<map>` in each child.
- Select the first open, unassigned child in map order with zero open blockers.
- Claim it with `gh issue edit <number> --add-assignee @me`.
- To resolve it, post the answer, close the issue, and add a summary and link to the map's Decisions so far.
