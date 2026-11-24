# skills

Claude Code skills I wrote, each installable on its own, plus the global
`CLAUDE.md` I work with, published for reference.

## Skills

| Skill | What it does |
| --- | --- |
| [`show-me`](skills/show-me/SKILL.md) | Shows how a PR, branch, diff or proposal works before you read its code: the problem, the idea, the before and after, and the decisions worth feedback. Prints terminal visuals, or writes an HTML page with [archify](https://github.com/tt-a1i/archify). Run `/show-me 123 html`. |
| [`review-loop`](skills/review-loop/SKILL.md) | Runs a blind review-and-fix loop over the branch diff. Each cycle starts a fresh reviewer agent that sees only the code, never the conversation. Run `/review-loop` before opening a PR. |

## Install one skill

As a Claude Code plugin (updates through `/plugin`):

```text
/plugin install show-me --marketplace NelsonBrandao/skills
/plugin install review-loop --marketplace NelsonBrandao/skills
```

With the [`skills`](https://www.npmjs.com/package/skills) CLI, for Claude Code or another agent:

```bash
npx skills add NelsonBrandao/skills --skill show-me
```

Requirements:

- `show-me` needs the [archify](https://github.com/tt-a1i/archify) skill for HTML pages (`npx skills add tt-a1i/archify`). Without it, `show-me` prints to the terminal only.
- `review-loop` ships its `blind-reviewer` agent in [`skills/review-loop/agents/`](skills/review-loop/agents/blind-reviewer.md). The plugin installs it. With the `skills` CLI, copy that file to `~/.claude/agents/`, or let the skill fall back to a general-purpose agent that carries the same instructions.

## CLAUDE.md

[`CLAUDE.md`](CLAUDE.md) is my global instruction file, shared as an example rather than
something to install. It imports a `~/.claude/CLAUDE.private.md` for machine- and
employer-specific rules, which stay out of this repo.

## Credits

`show-me` adapts the visual vocabulary of [humanlayer's show-me skill](https://github.com/humanlayer/skills/tree/main/plugins/show-me),
MIT licensed; see [`licenses/humanlayer-skills-LICENSE`](licenses/humanlayer-skills-LICENSE).

## License

MIT; see [LICENSE](LICENSE).
