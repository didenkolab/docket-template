# A new project

A [docket](https://github.com/didenkolab/docket) vault: a task board and a knowledge base
kept as Markdown files in git.

Clone it, open the folder in Obsidian, and you get a board, a backlog and a wiki. There is
nothing to install and nothing to run — tasks and pages are plain Markdown with YAML
frontmatter, and git is the history. The same folder served by the docket binary is that board
in a browser, and neither view is an export of the other.

## Quick start

Open the folder in Obsidian:

```bash
open -a Obsidian .     # macOS. Elsewhere: Obsidian → Open folder as vault
```

The left pane is the file tree: the project folder is the work, `docs/` is the wiki. Open
`boards/board`, `boards/backlog`, and the graph view for how it all connects.

Or a board in a browser, with the [docket](https://github.com/didenkolab/docket) binary:

```bash
docket serve --auth none --author "Your Name <you@example.com>"
```

Open <http://127.0.0.1:8080>: the same tasks as a board, the same pages as a wiki, and a search
across both — and dragging a card between columns lands in git as a commit.

## Requirements

git, and then Obsidian or the docket binary or neither — the files are Markdown and a text
editor reads them. Nothing here needs Go, Python or Docker.

## Install

Nothing to install — this is a vault, not a program. The tool that reads it is a separate,
optional download; see [docket](https://github.com/didenkolab/docket).

## Usage

A key is `PROJ-12`, and the file is named after the task, so the graph and the file
explorer say what each note is. Link to one by its whole name: `[[PROJ-12 Its title]]`.

```bash
docket new "Something to do"          # the next key, from the project's template
docket check                          # ten rules, with a file and a line for each finding
docket check --fix                    # rename drifted files, link up relationships, redraw the boards
```

Or write the file yourself — a task is frontmatter and prose, and nothing here is generated
from anything you cannot read.

## Configuration

`docket.yaml` at the root is the whole of it: the projects this vault holds, the statuses and
their categories, the types and their levels, the priorities, the fields and relations any
installed apps brought, and the workflow that says which status may move to which. Leave the
workflow out and anything can move to anything, which is what this vault does today. Change it
and commit it — `docket check --fix` regenerates the boards to agree with it.

## How it works

Tasks and pages are one file tree, and a wikilink is the only pointer that joins them: `parent`,
`labels` and the relations are links, so an epic has an edge to each of its tasks and a label is
a hub joining everything that carries it. That is why the graph is worth opening, and why
Obsidian's backlinks pane answers questions no field was added for.

The format is specified in
[docket-board](https://github.com/didenkolab/docket-board/blob/main/docs/spec/vault-format.md),
and `docs/spec/documents.md` here says what a page under `docs/` is.

### What `docket init` does with this

A vault like this one is made by `docket init`, which clones a template repository, drops its
history, stamps in the project's key and name, and makes the new repository's first commit:

```bash
mkdir acme && cd acme && git init -q
docket init --key ACME --name "Acme Platform"
docket init --key ACME --template git@example.com:us/our-template.git   # or your own
```

The default template is
[docket-template](https://github.com/didenkolab/docket-template), a repository rather than
something inside the binary so that a team can make the scaffold its own — its own `AGENTS.md`,
its own conventions, its own CI — without waiting for a release. Anything added there comes
along into every project made afterwards, and `TEMPLATE.md` in that repository says what is in
it, what is removed on the way out, and how the placeholder project is replaced.

## Where things are

| Path | What |
|---|---|
| `docket.yaml` | The projects this vault holds and the vocabulary they share |
| `PROJ/` | One folder per project. `PROJ-12 Its title.md` is the task `PROJ-12` |
| `docs/` | Knowledge base — pages, decisions, specs and sprints. `docs/spec/documents.md` says what each one is |
| `boards/` | Obsidian Bases views: board, backlog, my tasks |
| `templates/` | Templates for a new task and a new page |
| `AGENTS.md` | How an agent works in this vault |

The family: [`docket`](https://github.com/didenkolab/docket) is the tool;
[`docket-apps`](https://github.com/didenkolab/docket-apps) is twelve packs of vocabulary and
files a vault can take on; [`docket-board`](https://github.com/didenkolab/docket-board) holds
the specification, the decisions and the project's own board;
[`docket-demo`](https://github.com/didenkolab/docket-demo) is a small vault to open and look
at; `docket-showcase` is an invented company's vault, with
[`northlight`](https://github.com/didenkolab/northlight) its code beside it. Only
`docket-template` is public today; the rest need access.

## Contributing

Read [AGENTS.md](AGENTS.md) first — the normative account of how to edit this vault, and the
same file whether the editor is a person or an agent. Then `docket check .`: it exits non-zero
when it finds anything, so it works as a pre-commit hook.

## License

MIT — see [LICENSE](LICENSE).
