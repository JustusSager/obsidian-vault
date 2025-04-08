# ARRAY_CAT als Aggregationsfunktion
Standardmäßig gibt es keine Aggregationsfunktion von ARRAY_CAT() in PostgreSQL. Mit folgendem Skript kann eine erstellt werden:
``` SQL
CREATE AGGREGATE array_accum (anycompatiblearray) (
    sfunc = array_cat,
    stype = anycompatiblearray,
    initcond = '{}'
);
```
Wird in public angelegt.

# Tabellenberechtigungen eines Benutzers anzeigen
``` SQL
SELECT *
FROM information_schema.role_table_grants 
WHERE grantee = 'BENUTZER';
```

# Tabellen die einem bestimmten Benutzer gehören anzeigen
``` SQL
SELECT *
FROM pg_tables 
WHERE tableowner = 'BENUTZER';
```