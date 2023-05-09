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
