# Notes for AI assistants

This checkout is Lev's fork (`kik4311/1401`), branch work often on `linux-support`.
AI-assisted coding, commits, PRs on the **fork**, and `gh` usage are welcome here.

Upstream `nullmoth/1401` still rejects AI-written contributions (`CONTRIBUTING.md`).
Do not open or update PRs against `origin`/`nullmoth` unless Lev explicitly asks;
when he does, he must own and be able to explain every line before submit.

## Product

1401 installs macOS on a PC (OpenCore reverse of Boot Camp). Shared engine in `p1401/`;
Windows UI in `windows/App/`; Linux GTK 4 UI in `linux/`; Mac post-install app in `mac/`.
Pinned upstream trees live in `upstream/` — do not edit them; pins are in `PINNED.json`.

Read `DEVELOPING.md` and `docs/HOW-IT-WORKS.md` before changing a step.

## Remotes and GitHub

| Remote | Repo |
|---|---|
| `fork` | `kik4311/1401` (push target) |
| `origin` | `nullmoth/1401` (upstream) |

Use `gh` for issues/PRs/checks on the fork. Prefer `gh` over raw API curls.
If `gh auth status` fails, stop and tell Lev to run `gh auth login -h github.com`.

## How to work

- Change code directly; run the relevant tests before claiming done.
- One focused change per branch/PR on the fork.
- Sign off commits when Lev asks to commit (`git commit -s`) — DCO still applies.
- English in project files, docs, commit messages, and PR text unless Lev asks otherwise.
- Never commit secrets, real hardware dumps, or Apple binaries/SDK material.
- Fail loud: a step that cannot finish must stop with a clear reason.

## Tests (minimum)

```bash
python3 -m unittest discover -s tests -t . -p 'test_*.py'
```

Linux UI / writer:

```bash
python3 -m unittest tests.test_linux_usb tests.test_linux_root
python3 linux/1401.py --selftest   # needs a display
```

Corpus (rules / `engine.py` / `nullmoth.py`):

```bash
python3 tests/corpus/fetch.py
python3 tests/run_corpus.py build
```
