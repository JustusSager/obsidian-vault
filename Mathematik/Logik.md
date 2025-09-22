# Elementare Logik
## Aussage
Ein Satz bei dem eindeutig gesagt werden kann, ob er wahr oder falsch ist.
## Operatoren
### Negation
Verneinung einer [[#Aussage]].
$\bar{A}$ oder $\neg A$
### UND
Ist genau dann wahr wenn beide Aussagen A und B wahr sind.
$A \land B$ oder $A \cdot B$
### ODER
Ist dann wahr wenn einer der beiden (oder beide) Aussagen wahr sind.
$A \lor B$ oder $A + B$
### OHNE
Ist genau dann wahr, wenn A wahr und B falsch ist.
$A \setminus B$ 
### EX-ODER
Ist dann wahr wenn genau eine der beiden Aussagen wahr ist.
$\dots$ oder $A \oplus B$ (oder $A \operatorname{xor} B$)
### Wahrheitstabelle

| $A$ | $B$ | $A \land B$ | $A \lor B$ | $A \setminus B$ | $A \oplus B$ |
| --- | --- | ----------- | ---------- | --------------- | ------------ |
| f   | f   | f           | f          | f               | f            |
| f   | w   | f           | w          | f               | w            |
| w   | f   | f           | w          | w               | w            |
| w   | w   | w           | w          | f               | f            |
