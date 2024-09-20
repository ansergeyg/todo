Fast-forward pros and cons:

Fast-forward merges occur when there is a linear path from the base branch to the target branch, allowing the head of the base branch to be simply moved forward to point to the target branch. The target branch's pointer is moved forward to the head of the source branch if no divergent work has been done on the target branch. This effectively brings the history of the target branch in line with the source branch.

### Pros:

Simpler history: Fast-forward merges keep the repository history linear and clean, which can simplify the understanding and navigation of the history.
Less overhead: No extra merge commits are created, which can be preferable in small projects or projects with fewer parallel developments.

### Cons:
Loss of context: The major downside is the loss of context regarding the feature's development process. Without a dedicated merge commit, it's harder to see the boundary between different features or to identify when a feature was merged.
Complicated reverts: Reverting a specific feature becomes more difficult as there's no single merge commit to revert. You would need to individually revert all commits pertaining to that feature.

### Disabling fast forward merge
Sometimes, you might want to preserve the exact history of changes, including the fact that a feature branch was created and merged. For this, you can disable the fast forward merge:

```
git merge --no-ff feature
```

This forces Git to create a new merge commit even if a fast forward merge is possible, thus preserving the history of a separate branch and merge.

### Fast forwarding when pulling
When you pull changes from a remote repository, you can explicitly ask for a fast forward merge:

```
git pull --ff-only
```

This command updates your current branch only if the pull can be resolved as a fast forward.

### Fast forwarding a local branch
If you want to fast forward your local branch to catch up with changes in another branch (like main), you can use:

```
git checkout feature
git merge main
```

This will fast forward the feature branch if no divergent changes have been made on feature.

### Checking if fast forward is possible
Before attempting a fast forward merge, you might want to check if it's possible:

```
git merge-base --is-ancestor main feature
```

This command returns 0 (true) if main can be fast forwarded to feature, and 1 (false) otherwise.

### When to use fast forward
The decision between using fast-forward and non-fast-forward merges largely depends on the project's requirements for history visibility and management. For larger, collaborative projects where tracking the development and integration of features separately is crucial, the non-fast-forward approach recommended by the git-flow model is beneficial. It provides explicit markers in the project history that denote the start and end of feature integrations, facilitating easier troubleshooting and version management.

Conversely, for smaller projects or those with a more streamlined development process, fast-forward merges might be preferred for their simplicity and cleaner history. In any case, it's important to choose a strategy that aligns with the team's workflow and project requirements.

Taken from: https://graphite.dev/guides/git-fast-forward-merge
