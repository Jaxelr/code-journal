# Git commands

- Prune branches from remote origin: `git remote prune origin`
- Remove origin: `git remote rm origin`
- Amend date of previous commit: `git commit --amend --no-edit --date="yyyy.mm.dd hh:mm"`
- Amend author of previous commit: `git commit --amend --author="Name Lastname <email@email.com>"`
- Count commits for a given date: git shortlog -sne --author="\(Name\)" --after="01 Jan 2022" --before="22 Oct 2022"
For more snippets, check my [dotfiles](https://github.com/Jaxelr/dotfiles/blob/master/git/.gitconfig.aliases)
