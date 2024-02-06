# GIT

Downloading a repo
===
* initialize an existing directory as local git repo
```
git init
```

* clone a remote repo:
```
git clone https://www.site.com/repo.git
git clone https://www.site.com/repo.git MyChosenFolderName
```
* clone only a specific branch of a remote repo:
```
git clone --single-branch --branch testBranch https://www.site.com/repo.git 
```

Configuring a repo
===
* see local configuration:
```
git config --list --local
```

* set SSH key for commits to remote repo (eg GitHub)
```
git config --local core.sshCommand 'ssh -i ~/.ssh/id_rsa_github_tchan'
```
* TODO: set author, ... ?
```
git config --local user.name "T_chan"
git config --local user.email "me@hotmail.com"
```

Branches
===
* create & switch to:
```
git status
git checkout -b MyBranch
```
* switch to:
```
git checkout MyBranch
```
* delete:
```
git branch -D MyBranch
```
* list:
```
git branch --list

git branch -r              (to view remote branches)
	(If you don't have a local existing branch with same name as a remote branch, 
	 you can just switch directly to the branch with git checkout branchname)
```

Stage (locally)
===
* stage MyModifiedFile:
```
git status

git add MyModifiedFile

git add --all
```
* unstage MyModifiedFile:
```
git restore --staged MyModifiedFile
```
* remove untracked files/folders:
```
git clean -nd         (list what would be considered for cleaning)
git clean -fd         (remove untracked files & folders)
```

Commit (locally)
===
* commit without sign-off
```
git -c commiter.name="T_chan" -c committer.email="" commit --no-signoff -v -m "my_commit_comment" --author="T_chan <>"
git commit --no-signoff -v -m "my_commit_comment" --author="T_chan <me@hotmail.com>"
```
* commit with sign-off
```
git commit -s -v -m "my_commit_comment" --author="T_chan <me@hotmail.com>"
```


Commit (to remote, after local commit)
===
* push local branch to remote repo
```
git push origin MyLocalBranchname
```

Diffs & Patches
===
* List commits
```
git log --after="2023-20-04T10:36:00-07:00" --pretty=format:"%H - %an - %ci"          (List commits after a certain date)
git log origin/master --after="2023-20-04T10:36:00-07:00" --pretty=format:"%H - %an - %ci"          (same as above, but for the remote branch)
git log -n 15  --pretty=format:"%H - %an - %ci"                                       (List last 15 commits)

```
* List files changed in a commit
```
git diff --name-only COMMITHASH~1 COMMITHASH
```
* Create patch based on a diff
```
git diff --patch COMMITHASH~1 COMMITHASH > patches/mypatch.patch
```
* Apply patch based on current branch
```
git apply --reject --whitespace=fix mypatch.patch
```

## References
* [Azure Devops - Run Git commands in a script](https://learn.microsoft.com/en-us/azure/devops/pipelines/scripts/git-commands?view=azure-devops&tabs=yaml)
* [Git pretty formats](https://git-scm.com/docs/pretty-formats)
