tags:: [[tagGit]]

- 查看本地仓库有哪些远端已不存在，但本地存在的分支
	- `git remote prune --dry-run origin`
- 删除本地仓库有哪些远端已不存在，但本地存在的分支
	- `git remote prune origin`
- 查看是否删除本地仓库有哪些远端已不存在，但本地存在的分支
	- `git fetch --prune origin`