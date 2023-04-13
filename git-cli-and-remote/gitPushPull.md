# How to work with branches

| :exclamation: **Remember** Nothing works automatically in GIT |
| ------------------------------------------------------------- |

<br>

## The Basics

> **Note**
> before branching, make sure to have pulled the most recent version of main

- Lokale Branches auflisten `git branch`
- Alle Branches (local und remote auflisten `git branch -a`
- Einen branch erstellen `git branch MeinBranchName`
- Committen `git commit -m "meine Notiz"`
- Push to github `git push -u origin MeinBranchName`
- Branch löschen `git branch -d MeinBranchName`
- Switch between branches `git switch`

<br>

**Pull Request**

> **Note** > _You ask the Maintainer to pull in Your changes into Their repository_

1. :dizzy: Create new branch with `git switch -c MeinBranchName`
2. :rocket: Do Awesome Changes to the files
3. :muscle: add, commit, push!
4. :raising_hand: Create Pull Request on Github.com <br>
   _Define with Dropdown Menu which branch is merged into which other branch (but this is just the request, not the Merge!)_
5. :family: Share Pull Request with Team <br>
   _Usually a member of the team approves the request (not oneself) to pull the changes into Main_
6. 🪓: Delete the Branch on Github and locally

<br>

---

## Further Notes

**Being the Merger**

1. Open file in your repository with the Pull Request
2. Review Changes, if there is a conflict resolve with Devs or PO
3. Approving / Merging Branches into main

<br>

**Pull in Changes to local**

- It makes sense to pull the whole repository when there were changes by multiple people `git pull origin main` <br>
  basically what you do every morning, we are merging branches with all their changes by (possibly) different folks who pushed to that branch
- if there's only changes by Myself, I can simply merge my latest changes with the main branch locally (why tho? prob saves time for big repos...)

<br>

**Deleting branches**

- Local branches are easily deleted with ````git branch -d MeinBranchName```, but will create an error message about "not yet being merged to head", meaning you deleted it locally but not online
- to also delete online ```git push --delete origin `MeinBranchName```

<br>

> **Note**
> For the Features I'm working on currently I possibly dont always need the newest update (time is always short...)
