# How to work with branches

| :exclamation: **Remember** Nothing works automatically in Git |
| ------------------------------------------------------------- |

<br>
Lokale Branches auflisten ```git branch```
Alle Branches (local und remote auflisten ```git branch -a```
Einen branch erstellen ```git branch MeinBranchName```
Committen ```git commit -m "meine Notiz"```
>before branching, make sure to have pulled the most recent version of main

Push to github `git push origin nameDesBranch`

Branch löschen `git branch -d MeinBranchName`

<br>

**Pull Request**
<br> _Ask Maintainer to pull in our changes into their repository_

1. New Pull Request on Github
2. Define with Dropdown Menu which branch is merged into which other branch <br>
   does Git accept the merge? ("Able to merge" -> if no, talk to other Dev / PO)
3. Create Pull Request by clicking on Button (but this is just the request)
4. Usually a member of the team approves the request (not oneself)

<br>

**Merge**

1. Open file in your repository with the Pull Request
2. Approving / Merging Branches into main

<br>

**Switch between branches**

- `git switch`
- to create a new branch AND switch `git switch -c nameOfNewBranch`

<br>

**Pull in Changes to local**

- It makes sense to pull the whole repository when there were changes by multiple people `git pull origin main` <br>
  basically what you do every morning, we are merging branches with all their changes by (possibly) different folks who pushed to that branch
- if there's only changes by Myself, I can simply merge my latest changes with the main branch locally (why tho? prob saves time for big repos...)

For the Feature I'm working on currently I possibly dont need the newest update (time is always short, like money)
