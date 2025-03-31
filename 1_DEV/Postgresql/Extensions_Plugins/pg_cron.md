
# cron_job für eine andere Datenbank erstellen:
``` sql
SELECT cron.schedule_in_database(
	'<Name des cron_jobs>',
	'<schedule>',
	'<SQL Skript, dass ausgeführt werden soll>',
	'<Datenbank>',
	'<User mit dem ausgeführt wird>',
	TRUE -- Effective or not
```

# Wiederholrate/Schedule
``` sql
┌───────────── Minutes:0~59
│ ┌────────────── Hours:0~23
│ │ ┌─────────────── Date:1~31
│ │ │ ┌──────────────── Month:1~12
│ │ │ │ ┌───────────────── Day of the week: 0 to 6, 0 representing Sunday.
│ │ │ │ │
* * * * *
```

## Beispiel:
``` sql
'00 03 * * *' -- entspricht jeden Tag um 03:00 Uhr
```
