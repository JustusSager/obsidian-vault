# Git konfigurieren
``` bash
git config --global user.name "<name>"
git config --global user.email "<email>"

git config --global core.editor "notepad" # für Windows
```

# Lokal

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
git diff [<commit hash>]
	--word-diff # unterschiede wortweise anzeigen
```

Versionshistorie der Commits anzeigen
``` bash
git log [--graph] [--all]
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
git checkout <branch name/commit hash>
	-b # einen neuen Branch erstellen und reinwechseln
```

Neuen Branch erstellen
``` bash
git branch <name>
```

```

# Remote

Ein bestehendes Projekt lokal erstellen
``` bash
git clone <URL> // Im Ordner wo das Projekt angelegt werden soll
```

# Remotes


# gitignore
Git Anweisen bestimmte Dateien, Dateimuster und Ordner zu ignorieren
Eine .gitignore Datei wird neben dem .git-Ordner erstellt. 

Beispielinhalt:
``` .gitignore
*.txt      # .txt-Dateien ignorieren
/.idea/    # .idea Ordner ignorieren
```
