# Rollback on remote

Sometimes it is required to revert commits already pushed to a remote. We could just change the code back and push the changes as a new commit.
This does however pollute the history when it is not needed. It would be better if we can roll this back by deleting the actual commits.

To do this we need a target version of the source on the remote. When we know a series of commits can require reverting the commits it might be very useful to add a tag to a known good commit.

## General flow
First we need to reset the local repo to a specific commit. We can use a commit-ish identifier.
```bash
# Reset the local repo AND discard all changes following <commit-ish>
# commit-ish can be a commit id (=hash), a tag, ...
git reset --hard <commit-ish>
# Push the changes to the remote
# --force is required in order to overwrite the history
git push --force origin <branch>
```

This is straightforward but dangerous. Furthermore collaborators need to perform a pull AND reset their local repo to the remote repo. This means they can lose their work.

```bash
# Fetch the latest changes from the remote
git pull
# Reset the local repo to the remote HEAD of the specified <branch>
git reset --hard origin/<branch>
```

# Remarks

This is a heavy-handed and dangerous usage of git. It can cause a serious loss of data.