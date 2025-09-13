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
