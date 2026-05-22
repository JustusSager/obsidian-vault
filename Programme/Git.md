#Informatik 
# Lokal
## Konfigurieren
``` bash
git config --global user.name "<name>"
git config --global user.email "<email>"

git config --global core.editor "notepad" # für Windows
```

## Befehle

aktuellen Status anzeigen
``` bash
git status
```

Eine Veränderung im Work Tree dem Index hinzufügen [[#^c7ba56]]
``` bash
git add <file>
```

Die indizierten Änderungen dem Local Repository hinzufügen (Commit)
``` bash
git commit -m "<commit message>"
	-a # alle Änderungen im Work Tree indizieren und committen
	--amend # dem letzten bereits existierenden commit hinzufügen
```

Unterschiede des Work Tree zum Index anzeigen
	oder unterschied eines bestimmten Commits zum aktuellen Work Tree 
``` bash
git diff [] [<commit hash>]
	--word-diff # unterschiede wortweise anzeigen
```

Versionshistorie der Commits anzeigen
``` bash
git log []
	--graph # graphische Darstellung anzeigen
	--all # Alle Branches anzeigen
```

Änderungen an einer Datei rückgängig machen^c7ba56
	Der Stand des letzten commits wird wieder hergestellt.
``` bash
git restore <file>
	--staged # git add <file> rückgängig machen
```

Änderungen eines bestimmten commits rückgängig machen
	Erstellt einen neuen commit, in der die Änderungen des übergebenen commits rückgängig gemacht werden
``` bash
git revert <commit hash>
```

In einen Branch/Commit wechseln 
``` bash
git checkout [] <branch name/commit hash>
	-b # einen neuen Branch erstellen und reinwechseln
git checkout []
	--theirs #TODO
git switch [] <branch name>
	-c # erstellt Branch und wechselt rein
```

Branch
``` bash
git branch [] <branch name> # erstellt den Branch ohne Checkout
	-d # löscht den Branch <branch name>, warnt bei "unmerged changes"
	-D # erzwungenes Löschen des Branches <branch name>
	-m # den aktuellen Branch umbenennen zu <branch name>

git branch []
	--show-current # aktuellen Branch ausgeben
	--list  # Branches im Local Repository ausgeben 
	-a # Alle Branches ausgeben (local und remote)
	
```

Einen anderen Branch in den aktuellen HEAD "mergen"
``` bash
git merge <>
```

# Remotes

## Konfigurieren
``` bash
git remote add <name> <url> # neue remote Verknüpfung hinzufügen
git remote show
git remote rename
git remote remove
```
Standardmäßig sollte als Name der remote Verknüpfung 'origin' verwendet werden, da andere Befehle dann ohne weitere Argumente darauf zugreifen. origin ist "primus inter pares" (erster unter gleichen)

## Befehle

Ein Online Repository lokal erstellen
``` bash
git clone <url>
```

Local Repository zum Remote Repository "hochladen"
``` bash
git push
	-u <remote name> <branch name> # setzt für den Branch den remote, erstellt den Branch im remote
	--set-upstream <remote name> <branch name> # einen bestimmten branch in ein bestimmtes remote pushen
```

Remote Repository in das Local Repository "herunterladen"
``` bash
git fetch []
	--all # Alle Branches im Local Repository aktualisieren
```

Remote Repository in das Local Repository und den Work Tree "herunterladen"
``` bash
git pull
```

# conflicts
#TODO

# gitignore
Git Anweisen bestimmte Dateien, Dateimuster und Ordner zu ignorieren
Eine .gitignore Datei wird neben dem .git-Ordner erstellt. 

Beispielinhalt:
``` .gitignore
*.txt      # .txt-Dateien ignorieren
/.idea/    # .idea Ordner ignorieren
```
