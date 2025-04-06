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
