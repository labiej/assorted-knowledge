# Pushing commits

Usually we push commits to the remote repository by using the command `git push`. However there are some cases where want to push only some commits.

Git supports this by allowing to specify commit-ids when pushing to a specific branch for example

```git
git push origin <commit-id>:<branch>
```

Here the commit-id is the **local** identifier of a commit.

If the history looks like

> commit-4
> commit-3
> commit-2
> commit-1
> HEAD <-- latest commit on remote

and we push using commit-3 in the command above, this means we will push commits 1 through 3 to the remote while commit-4 remains a local commit.

When a commit exists in the range that you do not want to push use [[Rebasing]] to re-order the commits until you can push only what you want to push.