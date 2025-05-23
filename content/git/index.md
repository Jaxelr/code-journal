# Git commands

- Prune branches from remote origin: `git remote prune origin`
- Remove origin: `git remote rm origin`
- Amend date of previous commit: `git commit --amend --no-edit --date="yyyy.mm.dd hh:mm"`
- Amend author of previous commit: `git commit --amend --author="Name Lastname <email@email.com>"`
- Count commits for a given date: git shortlog -sne --author="\(Name\)" --after="01 Jan 2022" --before="22 Oct 2022"
For more snippets, check my [dotfiles](https://github.com/Jaxelr/dotfiles/blob/master/git/.gitconfig.aliases)
- Create an empty commit with a message: `git commit --allow-empty -m "message"`
- Count commits per user: `git shortlog --summary --numbered --all --no-merges`

## Git notes

Notes do not modify Commits, Tags, or Trees. They are separate objects that can be added, removed, and listed independently of other objects.

- Add notes to a commit: `git notes add -m "{message}`
- Show notes of a commit: `git notes show {commit}` if left empty, it takes the HEAD commit
- Remove notes of a commit: `git notes remove {commit}` if left empty, it takes the HEAD commit

## Git find old branches

This command finds old branches that have not been updated in the last 6 months.

``` bash
git for-each-ref --sort=-committerdate --format='%(refname:short) %(committerdate:iso8601)' refs/remotes | awk -v date="$(date -d '6 months ago' +%s)" '{ cmd = "date -d \"" $2 "\" +%s"; cmd | getline commit_date; close(cmd); if (commit_date < date) print $1 }'
```