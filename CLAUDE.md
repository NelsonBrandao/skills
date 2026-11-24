# Working

- A UI-visible change (frontend, or backend surfacing there) isn't done until you've used it end to end in the browser on the dev server and sent a screenshot tour of each state, as soon as it works, before lint/tests/cleanup; lint and tests aren't verification. Getting the app running (deps, auth, stack) is part of the task: unblock it.
- In tour and PR screenshots, draw a red box around the part that shows the point of the step (a toggle, a card, a changed value) so a reader finds it at a glance.
- "End to end" means using the product the way a user does, with screenshots: the browser UI for web features, the chat client for a chat agent. curl, CLI or API calls are lower-level checks, not end to end.
- Before creating a worktree, fetch and update the base branch (e.g. `main`) so the worktree starts from the latest code.

# Communication style

When reporting information to me, be extremely concise and sacrifice grammar for the sake of concision.

## Go lint before push

Before pushing any Go change, run `golangci-lint run ./...` on the touched modules (or the repo's own lint wrapper, when its CLAUDE.md names one). That run covers testifylint (use `JSONEq` for JSON comparisons), staticcheck (for example S1016), and unused variables. Fix every finding locally first.

# Work Ledger

Run `work-ledger prime` at the start of each session and follow it.

## PR titles

When a PR has a ticket (e.g. from the branch name or commits), title it `KEY-123: Title`: no brackets, no conventional-commit prefix like `fix(KEY-123)`.

## Auto-fix on new PRs

Right after creating a PR, turn on Auto-fix without asking: bind it with `mcp__ccd_pr__bind_pr` if `mcp__ccd_pr__get_status` doesn't report it, then call `mcp__ccd_pr__set_monitor` with `auto_fix: true` and the PR's url. This is my standing request for that switch, so the session gets woken on CI failures, merge conflicts and review comments.

## Code comments

- Golden rule: default to no comment. A good name or clear signature needs none.
- If a comment earns its place: one line. Two only when one is cryptic. More almost never.
- Before writing a comment, read the lines around it and copy their form: if sibling fields or lines use trailing inline comments, yours is inline too, never a line above.
- Explain WHY, never WHAT. Delete any comment that paraphrases the code.
- Write comments as a plain sentence a colleague gets on first read, not a telegraphic label.
- Comments stand alone for a cold reader and read in absolute terms: never reference the PR, ticket, conversation, or the change itself ("now also…", "changed to…").
- Anything longer belongs in the commit message or PR description.

# Machine-specific instructions

@~/.claude/CLAUDE.private.md
