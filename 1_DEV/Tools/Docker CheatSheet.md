# BASH Befehle

## Docker Grundlagen
#### Container anzeigen
``` bash
sudo docker ps []
	-a # Alle anzeigen
	-q Nur IDs anzeigen
	-f status=exited # Filtern nach status=exited
```

#### Images anzeigen
``` bash
sudo docker images
```

#### Container stoppen
``` bash
sudo docker stop <Container ID>
```

#### Alle beendeten Container entfernen
``` bash
sudo docker rm $(sudo docker ps -a -q -f status=exited)
```

#### Shell in einem detatched container öffnen
``` bash
sudo docker exec -ti CONTAINER-ID bash
```

#### Mit Prozess im detatched Container verbinden
``` bash
sudo docker attach <CONTAINER ID>
```
Falls -ti im Container gesetzt ist, mit STRG+P STRG+Q wieder verlassen

## Container starten
### BusyBox starten
``` bash
sudo docker run BusyBox <COMMAND>
```

### nginx WebServer
``` bash
sudo docker run -p 80:80 -v ~/html:/usr/share/nginx/html -d -ti nginx
	-p HOST-PORT:DOCKER-PORT # Leite Host-Port 80 an Docker-Port 80 weiter
	-v HOST-FOLDER:CONTAINER-FOLDER # Ordner zwischen Host und Container verknüpfen
	-d # Im Detached Modus starten
	-ti	# So starten dass man sich attachen kann ohne den Container danach beenden zu müssen
```
