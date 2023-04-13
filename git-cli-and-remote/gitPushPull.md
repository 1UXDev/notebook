# How to work with branches

## 

Einen branch erstellen ```git branch```
Namen festlegen
Committen ```git commit -m "meine Notiz"```

Push to github ```git push origin nameDesBranch```


**Pull Request**
Ask Maintainer to pull in our changes into their repository
1. New Pull Request on Github
2. Define with Dropdown Menu which branch is merged into which other branch <br>
does Git accept the merge? ("Able to merge" -> if no, talk to other Dev / PO)
3. Create Pull Request by clicking on Button (but this is just the request)
4. Usually a member of the team approves the request (not oneself)


**Merge**
1. Open file in your repository with the Pull Request
2. Approving / Merging Branches into main


**Switch between branches**
- ```git switch```
- to create a new branch AND switch ```git switch -c nameOfNewBranch```

**Pull in Changes to local**
- It makes sense to pull the whole repository when there were changes by multiple people ```git pull origin main``` <br>
basically what you do every morning
- if there's only changes by Myself, I can simply merge my latest changes with the main branch locally (why tho? prob saves time for big repos...)
