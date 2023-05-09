# Teamwork & Git
* Pull Request = actually a merge Request, to be checked wether the code can be merged 
* "Never commit to Main"

## Multiple feature branches
* conflicts have to be actively resolved, dont work on the files until conflict is resolved
  * Thats why there should be commits often
  * Complex conflicts should not be resolved in the browser interface
* people should work on their individual feature-branches
* delete branches once merged

## Resolving Conflicts
-> bring conflict to my computer
1.  **Locate the conflict (e.g. `git log`)**
2.  **get the latest version of both conflicting branches**
    * 2.1 ___  `git switch main` (*"Your branch is up to date with "origin/main"* can be misleading, since my origin may not be the latest origin) 
    * 2.2 ___  `git pull origin main` **(only do this when on the main branch)**
    * 2.3 ___  `git log` -> look at the log </sub>
3.  **Pull latest main into my feature branch**
    * 3.1 ___  switch to feature branch
    * 3.2 ___  `git merge main` 
    * 3.3 ___  open file in VSC
    * 3.4 ___  Compare versions in the file
<br>    *a. ______ Either Accept Current / incoming Changes & Save*
<br>    *b. ______ Or manually create a version that uses the ideas of both versions & Save*
<br>    *c. ______ Check that all marker lines are removed*
    * 3.5 ___  `git add .`
    * 3.6 ___  `git commit --no-edit` -> uses default message
    * 3.7 ___  `git log` to check if merge was successfull
4.  **Pull Request to Merge my Repo back into main**
    * 4.1 ___  `git push origin myFeatureBranch`
    * 4.2 ___  check merge ability on github.com
    * 4.3 ___  merge pull-requests
    * 4.4 ___  conflict is not relevant anymore, branch can be deleted

<br>
<br>

***

### sidenotes: 
  * usually we clone existing repositories, instead of initializing our own (git init)
  * "head" in git means the last commit of my current branch
  * there should not be any uncommitted or unmerged changes if possible


<br>
<br>
***
<br>


# Git Advanced

## Learning Objectives

- [ ] deepen understanding of git in general
  - [ ] `git fetch`
  - [ ] `git pull`
- [ ] understand why and how git conflicts happen
- [ ] know how to combine branches:
  - [ ] `git merge`
  - [ ] `git rebase` / `git pull --rebase`
- [ ] know how to resolve git conflicts

---

## Understanding Advanced Git Commands

### `git fetch`

To check whether your local branches are up to date with the remote repository (by default:
`origin`), use `git fetch`.

If there are any differences,

- `git fetch` updates the remote-tracking branches
- this means that your local branch knows about all recent remote changes, but **does not contain
  these changes yet**
- you still need to merge these changes manually (using `git pull` or `git merge`).

![git fetch terminal output](assets/git-fetch.png)

> 💡 To see exactly which branches are up to date with origin/main, use `git fetch -v`.

### `git merge`

To join two branches together, you can use `git merge`.

Make sure to

- run `git fetch` first if you want to merge a remote branch
- switch to the branch where you want to incorporate the changes
- run `git merge <branchname>`

![git merge terminal output positive](assets/git-merge.png)

> 💡 Note that `git merge` is a fast-forward merge by default, which means that it will not create a
> merge commit if the history is clean.

> 💡 If a fast-forward merge isn't possible, `git merge` will create a merge commit, that
> incorporates the change. To avoid this and keep a clean history, you can use
> [git rebase](git-advanced.md#git-rebase).

### `git pull`

You can use `git pull` to fetch changes from a remote repository **and** merge them into the current
branch.

This is possible due to the fact that `git pull` runs `git fetch` and then `git merge`.

![git pull terminal output positive](assets/git-pull.png)

### `git rebase`

To join two branches together, you can also use `git rebase`. In contrast to `git merge`, it doesn't
create a merge commit, which results in a cleaner git history.

This strategy first applies all the changes of the branch we are rebasing to (the branch used after
the `rebase` command). Then it applies the changes of the branch we are rebasing from (the current
branch) on top of it commit by commit.

This is like "replaying" your latest changes on top of the changes from the other branch.

To rebase,

- switch to the branch where you want to incorporate the changes
- use `git rebase main` to incorporate the changes from the `main` branch into the branch you
  switched to
- if a conflict occurs,
  - [see below how to solve it in VSCode](git-advanced.md#how-to-solve-conflicts-in-vscode) and
  - [how to finish rebasing](git-advanced.md#option-2-git-rebase)

---

## How to Solve Conflicts

When your create a PR and want to merge the feature branch into the main branch, it happens that
somebody made changes to the same lines of code you were working on. Git cannot decide which code is
the right one and marks it as a conflict.

Conflicts have to be solved manually by developers.

### How to solve conflicts in VSCode

If a merge conflict occurs, you can use VSCode to solve it:

- go to the `Source Control` Tab of VSCode, and open the file marked with ❗️:

![VSCode choosing changes view](assets/vscode_source-control_conflict.png)

- choose one option to resolve the merge conflict:
  - `Accept Current Change`: keep content of the feature branch
  - `Accept Incoming Change`: keep content of the main branch (because we are merging main into the
    feature branch)
  - `Accept Both Changes`: keep both changes
- save the file and stage the changes (`git add <filename>`)
- follow the further steps along [git merge](git-advanced.md#option-1-git-merge) or
  [git rebase](git-advanced.md#option-2-git-rebase)

---

### How Common Conflict Emerge

#### Scenario 1: Feature Branch differs from Main Branch

![Conflict Message in GitHub pull request Page](assets/conflicts-message.png)

There are two ways to handle the conflict:

- solve the conflict locally ([see explanation below](git-advanced.md#solving-the-conflict-locally))
- solve the conflict directly on GitHub
  ([see explanation below](git-advanced.md#solving-the-conflict-remote-on-github))

#### Scenario 2: Fatal Error on `git pull`

Using `git pull` can result in the error message `fatal: Not possible to fast-forward, aborting`.
This happens when:

- You have done at least one commit locally.
- In the meantime, somebody else has committed to the branch you want to pull.
- The problem is that git does not know which commit(s) came first.

![git pull aborting](assets/git-pull-aborting.png)

To solve the conflict, follow these steps:

- `git pull --no-ff`
- resolve merge conflicts (if any)
  ([see explanation below](git-advanced.md#how-to-solve-conflicts-in-vscode))
- `git commit -m "resolve merge conflict"`
- `git push`

![git pull --no-ff output](assets/git-pull--no-ff.png)

---

### Solving Conflicts

#### Solving the Conflict Locally

##### Option 1: `git merge`

If the feature branch has conflicts with the main branch, you can use `git merge` to solve the
conflict:

- go to feature branch
- use `git merge main` to merge the main branch into the feature branch
- the terminal will output something like this:

  ![git merge main conflict output in terminal](assets/git-merge-main-conflict.png)

- resolve the conflict in VSCode
  ([as mentioned above](git-advanced.md#how-to-solve-conflicts-in-vscode))
- push the feature branch to GitHub
- conflict solved: you can merge the PR on GitHub 🎉

##### Option 2: `git rebase`

Instead of `git merge`, you can use `git rebase` to solve a conflict:

- go to feature branch
- use `git rebase main`
- resolve merge conflicts step-by-step
  ([as mentioned above](git-advanced.md#how-to-solve-conflicts-in-vscode))
- use `git rebase --continue` to continue (will open an editor for the merge commit message)
  > 💡 Most likely you're in vim. To save and close the editor type `:wq` and press `Enter`.
- `git push --force-with-lease` (protects the remote branch if different from local branch)

#### Solving the Conflict Remote on GitHub

Instead of solving a conflict locally, you can
[use the GitHub conflict manager](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-on-github).

---

## Resources

- [Git Handbook](https://www.git-scm.com/docs)
- [Visualizing Git](https://git-school.github.io/visualizing-git/#upstream-changes)
- [Git Emergency Help: ohshitgit.com](https://ohshitgit.com/)
