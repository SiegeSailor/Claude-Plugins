---
name: conventional-commit
description: Use whenever committing, amending, squashing, or drafting a commit message in any repository.
---

# Conventional Commit

A commit message is one [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) line and nothing else:

```text
<type>(<scope>)?: <subject>
```

| Part        | Rule                                                          |
| ----------- | ------------------------------------------------------------- |
| `<scope>`   | Only when it sharpens the subject, and most commits need none |
| `<subject>` | Imperative mood, lowercase, and no trailing period            |
| `<type>`    | Picks the release from the table below                        |

The subject is the whole message: no body, no footer, no trailers, and the line stays under 72 characters, type included. One concern per commit — split by concern rather than by file, even when the work was a single task.

## Scopes Come From the Repository

Read the repository's own `CLAUDE.md`, `CONTRIBUTING.md`, or existing `git log` before choosing a scope, and use the names it already uses. A change that spans scopes, or that sits at the repository root, takes none. Never invent a scope the repository does not already use.

```shell
git log --oneline -30    # the scopes and phrasing this repository actually uses
```

## Types and Releases

| Type                                                       | Release |
| ---------------------------------------------------------- | ------- |
| `feat!`, `fix!` (any type with `!`)                        | major   |
| `feat`                                                     | minor   |
| `fix`                                                      | patch   |
| `chore`, `ci`, `docs`, `perf`, `refactor`, `style`, `test` | none    |

> [!important]
> In a repository running Semantic Release or a similar tool, a careless type publishes a version. Check for `release.config.*`, `.releaserc*`, or a release workflow before picking one. Never use a `BREAKING CHANGE:` footer — it would need a body.

> [!important]
> A major version is a human's call. Prompt before wiring the `!`.

Example commit messages:

```text
feat(tooling): aggregate build and watch over their :* variants
ci: split workflows by task and rename them by trigger
fix: stop scalar exemption from leaking into arrays
```

## Before Committing

- **Let the Hook Run**: A failure means fixing the code, not passing `--no-verify`
- **Stage Deliberately**: `git add -A` sweeps in unrelated work, so read `git status` first and never stage generated output
- **Wait to Be Asked**: Commit only when asked, and push only when asked
- **Work on a Branch**: Check whether the default branch deploys or releases on push before committing to it

## Red Flags

| Thought | Reality |
| --- | --- |
| "This needs a body to explain it" | The subject is the whole message. A change needing paragraphs is usually several commits. |
| "I'll use `feat` — it's new code" | `feat` publishes a minor version. Ask what the change does for a user, not how much code it touched. |
| "These edits are all one task" | One task is not one concern. Split by concern. |
| "The hook is wrong, I'll skip it" | `--no-verify` hides a failure that lands on someone else. Fix the code. |
| "I'll add a trailer for attribution" | No trailers. The line is the message. |
