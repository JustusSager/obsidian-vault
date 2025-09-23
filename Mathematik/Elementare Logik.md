# Aussage
Ein Satz bei dem eindeutig gesagt werden kann, ob er wahr oder falsch ist. Aussagen können auch negiert oder miteinander verknüpft werden.
## Operatoren (von Aussagen)
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
### Subjunktion
Ist eine Aussage, deren Wahrheitswert von A und B abhängt. 
Ist nur dann falsch, wenn $A$ wahr ist und $B$ falsch.
Nicht zu verwechseln mit [[#Implikation]], wenn auch quasi das selbe, nur das es bei der Subjunktion um den Wert einer Aussage geht und nicht um den Zusammenhang zwischen zwei Aussagen.
$A \to B$ 
### Bijunktion
Ist eine Aussage, deren Wahrheitswert von A und B abhängt. 
Ist genau dann wahr, wenn $A$ und $B$ wahr sind, oder wenn $A$ und $B$ falsch sind (Beide gleich sind). 
Nicht zu verwechseln mit [[#Äquivalenz]], wenn auch quasi das selbe, nur das es bei der Bijunktion um den Wert einer Aussage geht und nicht um den Zusammenhang zwischen zwei Aussagen.
$A \operatorname{hier sollte ein doppelseitiger einfacher Pfeil sein, aber gibts nicht} B$ 
### Implikation
Relation zwischen zwei Aussagen, welche immer nur genau dann falsch ist, wenn $A$ wahr ist und $B$ falsch.
Wird fälschlicherweise häufig wie eine [[#Subjunktion]] verwendet. Entspricht einer [[#Subjunktion]] die immer wahr ist.
$A \implies B$ 
### Äquivalenz
Relation zwischen zwei Aussagen, welche immer genau dann wahr ist, wenn beide Aussagen ($A$ und $B$) wahr sind, oder beide Aussagen ($A$ und $B$) falsch sind.
Wird fälschlicherweise häufig wie eine [[#Bijunktion]] verwendet. Entspricht einer [[#Bijunktion]] die immer wahr ist.
$A \iff B$ bedeutet $A \implies B \land B \implies A$ 
### Wahrheitstabelle

| $A$ | $B$ | $A \land B$ | $A \lor B$ | $A \setminus B$ | $A \oplus B$ | $A \to B$ | $A \implies B$ | $A \iff B$ |
| --- | --- | ----------- | ---------- | --------------- | ------------ | --------- | -------------- | ---------- |
| f   | f   | f           | f          | f               | f            | w         | w              | w          |
| f   | w   | f           | w          | f               | w            | w         | w              | f          |
| w   | f   | f           | w          | w               | w            | f         | f              | f          |
| w   | w   | w           | w          | f               | f            | w         | w              | w          |

|                                          | Boolesche Algebra            | Mengenlehre              | Logik                     | Bedeutung                           |
| ---------------------------------------- | ---------------------------- | ------------------------ | ------------------------- | ----------------------------------- |
| Summe bzw. Vereinigung (Disjunktion)     | $A+B$ oder $A \lor B$        | $A \cup B$               | oder                      | A oder B oder beides                |
| Produkt bzw. Schnitt (Konjuktion)        | $A \cdot B$ oder $A \land B$ | $A \cap B$               | und                       | A und B gemeinsam                   |
| Differenz (Subtraktion)                  | $A \setminus B$              | $A \setminus B$          | ohne                      | A ohne die Elemente von B           |
| Symmetrische Differenz (Exklusives Oder) | $A \oplus B$                 | $A \operatorname{xor} B$ | entweder (...) oder (...) | Entweder (A ohne B) oder (B ohne A) |
## 1-Bit Adder

| X   | Y   | Übertrag C | Summe S |
| --- | --- | ---------- | ------- |
| 0   | 0   | 0          | 0       |
| 0   | 1   | 0          | 1       |
| 1   | 0   | 0          | 1       |
| 1   | 1   | 1          | 0       |
Summe S entspricht der logischen Verknüpfung $S=X \oplus Y$
Übertrag C entspricht der logischen Verknüpfung $C=X \cdot Y$
# Aussagenform
Eine Aussagenform $A(x)$ ist ähnlich zu einer [[#Aussage]], nur das sie eine Variable enthält. Sie können mit den selben [[#Operatoren (von Aussagen)|Operatoren]] wie Aussagen verwendet werden und zusätzlich noch mit weiteren.
## Operatoren (von Aussagenformen)
### All-Quantor
Für alle $x$ aus der Menge $M$ ist $A(x)$ wahr.
$\forall x \in M: A(x)$ 
### Existenz-Quantor
Es existiert ein $x$ in $M$, für das $A(x)$ wahr ist.
$\exists x \in M : A(x)$
# Rechenregeln
## Negation von All und Existenz Quantor
$\overline{\forall x \in M:A(x)} \iff \exists x \in M:\overline{A(x)}$ 
$\overline{\exists x \in M:A(x)} \iff \forall x \in M:\overline{A(x)}$ 
## De Morgansche Regeln
$\overline{A + B} \iff \bar A \cdot \bar B$ 
$\overline{A \cdot B} \iff \bar A + \bar B$ 
gilt auch für mehr als 2 Aussagen in Folge.
## idempotent
$A + A = A$
$A \cdot A = A$ 
## kommutativ
$A+B=B+A$
$A \cdot B=B \cdot A$
## assoziativ
$A+(B+C)=(A+B)+C$
$A \cdot (B \cdot C) = (A \cdot B) \cdot C$ 
## distributiv
$A \cdot (B + C) = (A \cdot B) + (A \cdot C)$ 
$A + (B \cdot C) = (A + B) \cdot (A + C)$ 
$+$ und $\cdot$ sind gleichberechtigt (also kein Punkt vor Strich), daher müssen immer Klammern gesetzt werden!
## weitere
$A \setminus B \iff A \cdot \bar B$ 
$A \oplus B \iff (A \setminus B) + (B \setminus A) \iff (A \cdot \bar B) + (B \cdot \bar A)$ 
$(A \implies B) \iff (\bar B \implies \bar A)$ 
$(A \implies B) \iff (\bar A \lor B)$ 
$\overline{(A \implies B)} \iff (A \land \bar B)$ 
