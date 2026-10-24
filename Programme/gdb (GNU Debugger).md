#Informatik 
CLI Debugger
# Befehle
## Debugger starten
``` bash
gdb <executable> # Debugger starten
```

## In der Debugger Konsole
``` bash
# Code anzeigen
list <Zeilennummer>

# Breakpoint in einer bestimmten Programmzeile setzen
break <line number> 

# Programm starten
run <CLI-Argumente>

# Inhalt des Speichers ab einer bestimmten Variable
x /<Anzahl Bytes>bx <Variablenname>

# Breakpointunterbrechung fortsetzen
continue
c

# Zeige detaillierte Informationen zum aktuellen Stack Frame (Frame Pointer, Rücksprungadresse etc.)
info frame

# physische Adresse einer Funktion ermitteln
print &<Funktionsname>

```

### `info frame`
`info frame` Zeige detaillierte Informationen zum aktuellen Stack Frame (Frame Pointer, Rücksprungadresse etc.) 
![[gdb_info_frame.png]]

`eip = <Adresse> in <Funktionsname> (<Datei>:<Zeile>)`
Die nächste auszuführende Anweisung im Programm an Adresse (...) in Funktion (...) der Datei (...) in Zeile (...)
Programm Counter
`saved eip = <Adresse>`
Rücksprungadresse nachdem diesem Funktionsaufruf.




# Konsolenargument mit python generieren
Mithilfe von python lässt sich ein `<CLI-Argument>` bei der Programmausführung generieren
``` bash
# 128 A`s als Konsolenargument übergeben
run `python -c "print('A'*128)"`

# 132 A`s und 2 Bytes (als hex) übergeben
run `python -c "print('A'*132 + '\x<byte>' + '\x<byte>')"`
```
