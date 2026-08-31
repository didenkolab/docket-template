# The docket vault template

This repository is what a new docket project starts as. `docket init` clones it, drops its
history, stamps in the project's key and name, and makes the new repository's first commit.

It is a repository rather than something inside the `docket` binary so that it can be changed
without releasing a new binary — the scaffold is exactly the part a team wants to make its own:
its own `AGENTS.md`, its own conventions, its own CI.

```bash
docket init --key ACME --name "Acme Platform"        # uses this template
docket init --key ACME --template git@example.com:us/our-template.git
```

## What is in it

| Path | What a new project gets |
|---|---|
| `docket.yaml` | The vocabulary: statuses, types with levels, priorities. `init` replaces the project key and name; everything else is yours to set here. |
| `AGENTS.md` | How an agent works in the vault. The normative rules an agent must follow when it edits files directly rather than going through the board. |
| `CLAUDE.md` | A pointer to `AGENTS.md`, so Claude Code reads the same file. |
| `boards/` | Obsidian Bases views. Regenerated from `docket.yaml` by `docket check --fix`, so editing them here is pointless — change the vocabulary instead. |
| `docs/index.md` | The front page of the knowledge base. |
| `templates/` | Templates for a new task and a new page. |
| `.obsidian/` | Enough settings that opening the folder in Obsidian works without configuring anything. |

## Editing it

Anything you add comes along into every new project: a CI workflow, a `CODEOWNERS`, a pull
request template. Two exceptions, which exist so this repository can explain itself without
every project inheriting the explanation:

- **`TEMPLATE.md`** — this file. Removed when a vault is made.
- **`.template/`** — anything about the template itself. Removed when a vault is made.

The one rule: the result has to be a vault. `docket init` validates it after copying, so a
template that has drifted into something docket cannot read fails at `init` with a clear reason
rather than confusing somebody later.

## PROJ

`PROJ` is a placeholder project, so that this repository is itself a valid vault you can open in
Obsidian and look at — and so that the prose has a key to speak about. `init` replaces the token
`PROJ` with the real key everywhere it stands as a word, which is why `AGENTS.md` here can say
`PROJ-12` and a new project reads `ACME-12`. `PROJECT-NUMBER` is left alone: the match is on
word boundaries.

The vault name works the same way, and `docket.yaml` does not: it is rewritten from a parsed
value rather than substituted, because replacing text inside YAML is how a template quietly
produces a vault that will not parse.

So: write the prose against `PROJ`, and keep the placeholder project empty. A task left in it
is treated as content and comes along.
