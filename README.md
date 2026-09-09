# util-scripts

A collection of utility scripts for common development workflows.

## Scripts

| Script | Description |
| --- | --- |
| `git-workflow.sh` | Automates common Git + GitHub tasks: init repo, create branch, push, open PR |

### git-workflow.sh

Automates common Git + GitHub tasks (SSH mode) for repos already cloned locally.

#### Usage

```
git-workflow.sh init   "commit message"           initial push to main
git-workflow.sh change "commit message" [branch]  new branch + PR
git-workflow.sh update "commit message"           commit + push current PR branch
git-workflow.sh pr     ["title"]                  open PR for current pushed branch
```

- **init** — Stages and commits all changes, creates a public GitHub repo if it
  doesn't exist, sets/overwrites the SSH remote, and pushes the current branch
  to `main`.
- **change** — Creates a new branch (auto-generated from the commit message if
  none is given), commits, pushes, and opens a PR against `main`.
- **update** — Commits and pushes additional changes to the current feature
  branch (must already be pushed to origin).
- **pr** — Opens a PR for the current pushed feature branch.

#### Requirements

- SSH key added to GitHub (`ssh -T git@github.com` should say `Hi <user>!`)
- [GitHub CLI](https://cli.github.com/) installed and authenticated
  (`gh auth login --git-protocol ssh`)
- Git configured: `git config --global user.name` / `user.email`

If SSH is unavailable, the script falls back to HTTPS via `gh`, which injects
auth transparently.