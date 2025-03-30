# Projektstruktur vorbereiten ^80e3ca

## 1. PostGIS Projektschema vorbereiten ^77870b
1. Schema erstellen
	1. Name: "GEBIETSKENNZIFFER_GEBIETSNAME"
2. cron_job in der 'pg_cron_projektdaten_projects_privilages.sql' hinzufügen.
	1. Siehe hierzu [[pg_cron]]
3. cron_job auf dem PostGIS Server ausführen.
4. Berechtigungsvergabe in der 'projektdaten_privileges.sql' hinzufügen.
5. 'projektdaten_privileges.sql' auf dem Server ausführen.

## 2. QGIS Projektdatei erstellen.
1. Variante: 
   QGIS Projektdatei wird auf dem PostGIS Server gespeichert.
	1.  Neues leeres Projekt öffnen
	2. Projekt auf dem PostGIS Server im entsprechenden [[#^77870b|Schema]] speichern
2. Variante: 
   QGIS Projektdatei wird im OneDrive gespeichert.
	1. Neues leeres Projekt öffnen
	2. Projekt auf OneDrive im 

# Standardtabellen hinzufügen
## 1. Gebietsgrenze ^357f61
### Voraussetzungen:
1. [[#^80e3ca|Projektstruktur]] ist vorbereitet.

### Umsetzung:
1. Variante (Aus deutschlandweitem Datensatz): 
	1. Gebietskennziffer ermitteln.
	2. GISELA Gebietsgrenze Skript ausführen.
2. Variante (z.B. Für Hessen oder wenn Gebietsgrenze nicht eine Gemeinde- oder Kreisgrenze ist):
	1. Gebietsgrenze händisch selektieren
3. Gebietsgrenze überprüfen:
	2. Prüfen das die Tabelle (echte oder view) nur einen Tupel enthält.
	3. Bei Gemeinde oder Kreisgrenze: 
		1. Abgleich der Grenze mit Google Maps
## 2. Marktstammdaten
### Voraussetzungen:
1. [[#^80e3ca|Projektstruktur]] ist vorbereitet.
2. 
### Umsetzung:
1. Marktstammdaten von 
	   https://www.marktstammdatenregister.de/MaStR/Einheit/Einheiten/ErweiterteOeffentlicheEinheitenuebersicht 
   herunterladen. Selektion über den Gemeindeschlüssel/Gebietskennziffer
2. Die heruntergeladene CSV in das QGIS Projekt laden
	1. Hierbei auf Koordinatenwahl als Geometrie und richtigen Datentypen der Spalten achten
3. Das Layer auf dem PostGIS Server hochladen
4. Die Datenquelle des MaStR Layers in QGIS auf den Datensatz des PostGIS Servers umstellen.
5. Den Stil laden.
6. Themen, Drucklayouts und Karten erstellen.

## 3. Zensus2022
### Voraussetzungen:
1. [[#^80e3ca|Projektstruktur]] ist vorbereitet.
2. [[#^357f61|Gebietsgrenze]] vorhanden.
3. 
### Umsetzung:
1. GISELA Zensus2022 Skript ausführen.
	1. Siehe hierzu [[#^357f61|Gebietsgrenze]].
2. Themen, Drucklayouts und Karten erstellen.

# Gebäude
#TODO 
## 1. ALKIS ^2581f3
### Voraussetzungen:
1. [[#^80e3ca|Projektstruktur]] ist vorbereitet.

## 2. Schornsteinfegerdaten
### Voraussetzungen:
1. [[#^80e3ca|Projektstruktur]] ist vorbereitet.
2. georeferenzierte Gebäudeadressen vorhanden (in nicht-aggregierter Form!)
	1. Hinweis [[#^2581f3|ALKIS]] 

## 3. Infas Daten und Berechnung ^8cdf30
### Voraussetzungen:
1. [[#^80e3ca|Projektstruktur]] ist vorbereitet.
2. georeferenzierte Gebäudeadressen vorhanden (in nicht-aggregierter Form!)
	1. Hinweis [[#^2581f3|ALKIS]] 

## 4. KWP Berechnung
Voraussetzungen:
1. [[#^80e3ca|Projektstruktur]] ist vorbereitet.
2. Endenergiesektor
	1. Variante: [[#^2581f3|ALKIS]] Gebäudefunktion übersetzt zu KWP Endenergiesektor.
3. Baualtersklassen in KWP Form
	1. gelieferte Baujahre
	2. Variante: [[#^8cdf30|Infas]] Baualtersklassen übersetzt zu KWP Baualtersklassen.
4. Bautyp in KWP Form
	1. Variante: [[#^8cdf30|Infas]] Bautypen übersetzt zu KWP Bautypen.
5. BGF (Bruttogrundfläche)
	1. Variante: $BGF = GGF * Geschosszahl$ 
		1. GGF über [[#^2581f3|ALKIS]] Gebäudepolygon.
		2. Geschosszahl über [[#^2581f3|ALKIS]] Geschosszahl.
	2. Variante: $BGF = GGF * Geschosszahl$ 
		1. GGF über [[#^2581f3|ALKIS]] Gebäudepolygon.
		2. Geschosszahl typologisch über [[#^8cdf30|Infas]].

## 5. gelieferte Energieverbräuche
### Voraussetzungen:
1. [[#^80e3ca|Projektstruktur]] ist vorbereitet.
2. georeferenzierte Gebäudeadressen vorhanden (in nicht-aggregierter Form!)
	1. Hinweis [[#^2581f3|ALKIS]] 
