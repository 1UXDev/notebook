# Git und CLI nutzen

## Erstelle ein lokales Projekt :ghost: 

1. Ordner erstellen ```mkdir "Mein Ordner"```
2. In den Ordner navigieren ```cd Mein_Ordner```
3. Readme Dokument erstellen ```touch "README.md"```

<br>

## Git lokal nutzen :floppy_disk:

1. Git initialisieren ```git init``` -> Erstellt eine .git Datei
2. Änderungen im Ordner (inkl. Datei) auf Stage platzieren ```git add ." 
3. Änderungen Committen ```git commit -m "Hier steht die Beschreibung meiner Änderung"```
4. Status prüfen ```git status```

<br>

## Git und Github verbinden :mortar_board:
1. Repository "MeinRepository" auf eigenem Github.com Profil erstellen <br>
-> Ohne eine eigene README-Datei erstellen
2. Verbinden von erstelltem Repository "MeinRepository" mit Ordner der Git CLI
<br>```git remote add origin git@github.com:MeinNutzername/MeinRepository.git```
3. Branch festlegen ```git branch -M main```
4. Push von CLI zu github.com ```git push -u origin main```

<br>
---------
<br>

## Weiterführendes: Reppositories Clonen :moyai:
1. git clone ```<ssh URL copied from the github.com "Code" Dropdown menu on the repository index page>```
