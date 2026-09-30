# golang-pair-dev

A Claude skill for pair programming on Go projects, including [templ](https://templ.guide) (`.templ`) files.

Claude is the pair, not the pilot. You make the calls. Claude works inside your project's existing conventions, flags anything that departs from them, and never skips its review step.

Most Go skills teach the agent a style guide. This one does the opposite: it makes Claude find and follow the patterns your codebase already uses, and ask before it introduces new ones.

## What it does

- **You lead.** Claude proposes; you decide. No new libraries, abstractions, error-handling styles or folder layouts "because it's better".
- **Reuse before invent.** Before writing code, Claude looks for how the project already solves the same kind of problem and follows that shape. If it finds conflicting precedents, it asks which one to follow.
- **Plan first.** For anything non-trivial, Claude states the plan and which existing pattern it's following, and waits for a go-ahead.
- **Stale-plan check.** Claude records the commit a plan was based on and re-checks it before coding, so a plan parked for a few days isn't built against a codebase that has moved on.
- **Pause-and-ask moments.** New dependencies and new exported API surface need your OK before they're written, not after.
- **Mandatory self-review.** Before presenting code as done, Claude walks through a visible checklist: reuse, simplicity, performance, concurrency correctness, modern Go, exported API, tests, scope, requirements, templ regeneration and commit freshness.
- **Honest about existing code.** "That's how the project does it" is a reason to match style, not proof it's right. Claude flags code that looks buggy, fragile or outdated, but doesn't fix it unasked.
- **Never commits without asking.** "Looks good" for the code is not permission to commit, push or rewrite history.
- **templ-aware.** Reuses existing components instead of duplicating them, never hand-edits generated `_templ.go` files, and reminds you to run `templ generate`.

## Install

### Claude Code (plugin)

```
/plugin marketplace add stuartaccent/golang-pair-dev
/plugin install golang-pair-dev@golang-pair-dev
```

### Claude Code (manual)

Copy the skill folder into your personal or project skills directory:

```
# all projects
cp -r skills/golang-pair-dev ~/.claude/skills/

# one project
cp -r skills/golang-pair-dev .claude/skills/
```

### Other agents (`npx skills`)

```
npx skills add stuartaccent/golang-pair-dev
```

### Claude apps

Zip the `skills/golang-pair-dev` folder and upload it as a custom skill.

## When it triggers

Any coding work in a Go project: writing or editing `.go` or `.templ` files, reviewing a diff, or "how should I implement X" questions.

## Customising

The skill is a single [SKILL.md](skills/golang-pair-dev/SKILL.md). Fork it and add team-specific checks to the Step 3 checklist. For example, if your project keeps a record of business rules, you can add a checklist item requiring that record to be updated in the same change as any rule it describes.

## License

[MIT](LICENSE)
