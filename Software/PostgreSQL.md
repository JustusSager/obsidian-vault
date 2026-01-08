#Informatik 
# Backups
Es gibt grundsätzlich 3 verschiedene Herangehensweisen:
- SQL Dump
- File system level backup
- Continuous archiving

# Erweiterungen
## pg_cron
### cron_job für eine andere Datenbank erstellen:
``` sql
SELECT cron.schedule_in_database(
	'<Name des cron_jobs>',
	'<schedule>',
	'<SQL Skript, dass ausgeführt werden soll>',
	'<Datenbank>',
	'<User mit dem ausgeführt wird>',
	TRUE -- Effective or not
```
### Wiederholrate/Schedule
``` sql
┌───────────── Minutes:0~59
│ ┌────────────── Hours:0~23
│ │ ┌─────────────── Date:1~31
│ │ │ ┌──────────────── Month:1~12
│ │ │ │ ┌───────────────── Day of the week: 0 to 6, 0 representing Sunday.
│ │ │ │ │
* * * * *
```
**Beispiel:**
``` sql
'00 03 * * *' -- entspricht jeden Tag um 03:00 Uhr
```

## PostGIS
### Geometriefunktionen
``` SQL
-- Zentroid einer geometrie berechnen
ST_CENTROID(geom)
-- Prüfen, ob eine geometrie in einer anderen ist
ST_CONTAINS(geom, geom)

```
### Aggregationsfunktionen
``` SQL
-- Geometrien aggregieren
ST_UNION(geom)
```

# Zusätzliche Funktionen
## ARRAY_CAT als Aggregationsfunktion
Standardmäßig gibt es keine Aggregationsfunktion von ARRAY_CAT() in PostgreSQL. Mit folgendem Skript kann eine erstellt werden.
Wird in public angelegt.
### Funktion
``` SQL
CREATE AGGREGATE array_accum (anycompatiblearray) (
    sfunc = array_cat,
    stype = anycompatiblearray,
    initcond = '{}'
);
```
## Mittelwert über mehrere Spalten
Standardmäßig lässt sich der Mittelwert nur als Aggregation einer Spalte erzeugen. Mithilfe dieser Funktionen lässt sich der Mittelwert von mehreren ( 2 - 8 ) Spalten bilden.
Nullwerte werden bei der Berechnung ausgelassen.
Quelle: https://stackoverflow.com/questions/7367750/average-of-multiple-columns
### Funktion
``` sql
CREATE OR REPLACE FUNCTION AVERAGE (
V1 NUMERIC,
V2 NUMERIC)
RETURNS NUMERIC
AS $FUNCTION$
DECLARE
    COUNT NUMERIC;
    TOTAL NUMERIC;
BEGIN
    COUNT=0;
    TOTAL=0;
    IF V1 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V1; END IF;
    IF V2 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V2; END IF;
    RETURN TOTAL/COUNT;
    EXCEPTION WHEN DIVISION_BY_ZERO THEN RETURN NULL;
END
$FUNCTION$ LANGUAGE PLPGSQL;

CREATE OR REPLACE FUNCTION AVERAGE (
V1 NUMERIC,
V2 NUMERIC,
V3 NUMERIC)
RETURNS NUMERIC
AS $FUNCTION$
DECLARE
    COUNT NUMERIC;
    TOTAL NUMERIC;
BEGIN
    COUNT=0;
    TOTAL=0;
    IF V1 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V1; END IF;
    IF V2 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V2; END IF;
    IF V3 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V3; END IF;
    RETURN TOTAL/COUNT;
    EXCEPTION WHEN DIVISION_BY_ZERO THEN RETURN NULL;
END
$FUNCTION$ LANGUAGE PLPGSQL;

CREATE OR REPLACE FUNCTION AVERAGE (
V1 NUMERIC,
V2 NUMERIC,
V3 NUMERIC,
V4 NUMERIC)
RETURNS NUMERIC
AS $FUNCTION$
DECLARE
    COUNT NUMERIC;
    TOTAL NUMERIC;
BEGIN
    COUNT=0;
    TOTAL=0;
    IF V1 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V1; END IF;
    IF V2 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V2; END IF;
    IF V3 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V3; END IF;
    IF V4 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V4; END IF;
    RETURN TOTAL/COUNT;
    EXCEPTION WHEN DIVISION_BY_ZERO THEN RETURN NULL;
END
$FUNCTION$ LANGUAGE PLPGSQL;

CREATE OR REPLACE FUNCTION AVERAGE (
V1 NUMERIC,
V2 NUMERIC,
V3 NUMERIC,
V4 NUMERIC,
V5 NUMERIC)
RETURNS NUMERIC
AS $FUNCTION$
DECLARE
    COUNT NUMERIC;
    TOTAL NUMERIC;
BEGIN
    COUNT=0;
    TOTAL=0;
    IF V1 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V1; END IF;
    IF V2 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V2; END IF;
    IF V3 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V3; END IF;
    IF V4 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V4; END IF;
    IF V5 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V5; END IF;
    RETURN TOTAL/COUNT;
    EXCEPTION WHEN DIVISION_BY_ZERO THEN RETURN NULL;
END
$FUNCTION$ LANGUAGE PLPGSQL;

CREATE OR REPLACE FUNCTION AVERAGE (
V1 NUMERIC,
V2 NUMERIC,
V3 NUMERIC,
V4 NUMERIC,
V5 NUMERIC,
V6 NUMERIC)
RETURNS NUMERIC
AS $FUNCTION$
DECLARE
    COUNT NUMERIC;
    TOTAL NUMERIC;
BEGIN
    COUNT=0;
    TOTAL=0;
    IF V1 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V1; END IF;
    IF V2 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V2; END IF;
    IF V3 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V3; END IF;
    IF V4 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V4; END IF;
    IF V5 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V5; END IF;
    IF V6 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V6; END IF;
    RETURN TOTAL/COUNT;
    EXCEPTION WHEN DIVISION_BY_ZERO THEN RETURN NULL;
END
$FUNCTION$ LANGUAGE PLPGSQL;

CREATE OR REPLACE FUNCTION AVERAGE (
V1 NUMERIC,
V2 NUMERIC,
V3 NUMERIC,
V4 NUMERIC,
V5 NUMERIC,
V6 NUMERIC,
V7 NUMERIC)
RETURNS NUMERIC
AS $FUNCTION$
DECLARE
    COUNT NUMERIC;
    TOTAL NUMERIC;
BEGIN
    COUNT=0;
    TOTAL=0;
    IF V1 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V1; END IF;
    IF V2 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V2; END IF;
    IF V3 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V3; END IF;
    IF V4 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V4; END IF;
    IF V5 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V5; END IF;
    IF V6 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V6; END IF;
    IF V7 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V7; END IF;
    RETURN TOTAL/COUNT;
    EXCEPTION WHEN DIVISION_BY_ZERO THEN RETURN NULL;
END
$FUNCTION$ LANGUAGE PLPGSQL;

CREATE OR REPLACE FUNCTION AVERAGE (
V1 NUMERIC,
V2 NUMERIC,
V3 NUMERIC,
V4 NUMERIC,
V5 NUMERIC,
V6 NUMERIC,
V7 NUMERIC,
V8 NUMERIC)
RETURNS NUMERIC
AS $FUNCTION$
DECLARE
    COUNT NUMERIC;
    TOTAL NUMERIC;
BEGIN
    COUNT=0;
    TOTAL=0;
    IF V1 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V1; END IF;
    IF V2 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V2; END IF;
    IF V3 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V3; END IF;
    IF V4 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V4; END IF;
    IF V5 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V5; END IF;
    IF V6 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V6; END IF;
    IF V7 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V7; END IF;
    IF V8 IS NOT NULL THEN COUNT=COUNT+1; TOTAL=TOTAL+V8; END IF;
    RETURN TOTAL/COUNT;
    EXCEPTION WHEN DIVISION_BY_ZERO THEN RETURN NULL;
END
$FUNCTION$ LANGUAGE PLPGSQL;
```
## Text zu Integer konvertieren
Von https://hawki.fh-kiel.de generiert und von mir angepasst.
Konvertiert einen String zu einer Zahl falls möglich. Falls nicht wird NULL zurückgegeben.
### Funktion
``` sql
CREATE OR REPLACE FUNCTION string_to_number(input_string TEXT)
RETURNS NUMERIC AS $FUNCTION$
DECLARE
    converted_number NUMERIC;
BEGIN
    BEGIN
        -- Versuch, den String in eine Zahl zu konvertieren
        converted_number := input_string::NUMERIC;
    EXCEPTION WHEN others THEN
        -- Wenn ein Fehler auftritt (z.B. ungültiges Format), gebe NULL zurück
        RETURN NULL;
    END;

    -- Wenn die Konvertierung erfolgreich war, gebe die Zahl zurück
    RETURN converted_number;
END
$FUNCTION$ LANGUAGE PLPGSQL;
```
## Nutzer ist Teil einer Gruppe
Überprüft ob ein Nutzer teil einer bestimmten Nutzergruppe ist.
### Funktion
``` sql
CREATE OR REPLACE FUNCTION is_member_of(
	groupname character varying)
    RETURNS boolean
    LANGUAGE 'sql'
    COST 100
    VOLATILE PARALLEL UNSAFE
AS $BODY$
  select exists (
    select 1 
    from pg_auth_members a, 
         pg_roles b, 
         pg_roles c  
    where a.roleid=b.oid 
      and a.member = c.oid 
      and b.rolname = groupname
      and c.rolname = (SELECT CURRENT_USER)::TEXT
  );
$BODY$;
```

# Code Schnipsel
## Tabellenberechtigungen eines Benutzers anzeigen
``` SQL
SELECT *
FROM information_schema.role_table_grants 
WHERE grantee = 'BENUTZER';
```
## Tabellen die einem bestimmten Benutzer gehören anzeigen
``` SQL
SELECT *
FROM pg_tables 
WHERE tableowner = 'BENUTZER';
```
