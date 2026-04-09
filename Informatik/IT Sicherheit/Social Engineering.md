#Informatik #IT-Sicherheit 
Social Engineering Angriffe bewähren sich, da sie 
- häufig zu schnelleren Resultaten und 
- mit weniger technischen Aufwand 
umsetzbar sind.

# Psychologische Grundlagen der Manipulation
**Wie treffen Menschen Entscheidungen:**
Menschen entscheiden **automatisch**:
- Entscheidungen anhand von Handlungsmustern und Urteilsheuristiken
- schnellere Entscheidung 
**Kontrolliertes** Verhalten:
- Alle Entscheidungsoptionen werden gründlich abgewogen und entscheidet sich bewusst für die sinnvollste
- führt zu einem längeren Entscheidungsprozess

 Für Social Engineering Angriffe sollen **automatische Entscheidungen gefördert** werden, um den Nutzer vom Nachdenken abzuhalten.

**Hinweis:** Es gibt wenige Bücher zu Social Engineering, aber Bücher zu Werbepsychologie sind quasi Bücher zu Social Engineering. 
 
## Reziprozität
_Die Regel der Reziprozität besagt, dass wir uns für erhaltene Gefälligkeiten, Geschenke usw. revanchieren müssen._
Kondition, dass Geschenke und Gefälligkeiten erwidert werden sollen.
Beispiele:
- Wenn man einen Drink spendiert bekommt, neigt man eher dazu auch einen Drink zurück zu spendieren.
- Ein Gutschein mit einem Fragebogen mitschicken, da dann der Rücklauf an Fragebögen höher ist, als wenn man erst nach Ausfüllen des Fragebogens etwas bekommt.
Alternative Sichtweise:
- Ist ein "Geschenk" bei dem man danach das Gefühl hat etwas zurückgeben zu müssen nicht eher ein Bestechungsversuch?

## Commitment und Kosistenz
_Menschen agieren stets in Konsistenz mit ihren früheren Handlungen. Wurde einmal eine Entscheidung getroffen (Commitment), treten intra- und interpsychologische Vorgänge in Kraft, die Menschen dazu drängen, konsistent zu bleiben._
Von Außen: Jeder möchte als Zuverlässig und Konsistent von Freunden und Familie gesehen werden, daher bleibt man eher bei demselben Standpunkt, den man einmal angenommen hat.
Von Innen: Einen neuen Standpunkt anzunehmen setzt voraus, das man sich selbst gegenüber eingesteht, das man falsch lag.  

## Soziale Bewährtheit
_Das Verhalten anderer wird als richtig angenommen und ggf. kopiert bzw. adaptiert._
Wenns die anderen machen, wird das schon ok sein.
Beispiele:
- Bei Rot über die Ampel gehen
- "Ihre Nachbarn haben's auch schon" ~ Tür-Verkäufer
## Sympathie
_Menschen, die uns sympathisch erscheinen, können uns eher verleiten._
- <b>Halo-Effekt</b> - Attraktiven Personen wird von Haus aus eine höhere Sympathie entgegen gebracht. Im Extremfall überstrahlt dies auch negative Eigenschaften.
- <b>Ähnlichkeiten</b> - (vorgeben) von Ähnlichkeiten, z.B. ähnliche Hobbies und Interessen fördern Sympathie.
- <b>Sympathiebekundungen</b> - Herausheben von Sympathie gegenüber dem anderen, fördert Sympathie
- <b>Flirten</b>
- <b>(scheinbare) Unterstützung</b> - z.B. good Cop, bad Cop. der good Cop scheint umso Sympathischer im Vergleich zum bad Cop.
- <b>Assoziation</b> - Assoziation mit Dingen/Personen herstellen, für die die Person bereits Sympathie empfindet. z.B. In der Werbung, werben mit bekannten Personen als Werbeträger.
- <b>Mitgefühl</b> 

## Autorität
_Menschen vertrauen meistens Autoritätspersonen._
- Wenn eine Person eine höhere Autorität hat (oder vorgibt zu haben) wird eher auf diese Person gehört.
- z.B. Hauptmann von Köpenick - (...)
  https://de.wikipedia.org/wiki/Hauptmann_von_K%C3%B6penick
- z.B. Milgram-Experiment - Ein Experiment bei dem sich Wortpaare gemerkt werden sollten.  Ein "Prüfer" sollte bei falscher Antwort dem Lernenden als "Lernhilfe" Stromschläge verpassen. Das Experiment war wie weit der "Prüfer" geht, wenn sie von einem Arzt angeleitet wird höher zu gehen.
  https://de.wikipedia.org/wiki/Milgram-Experiment 

## Knappheit
_Je knapper eine Ware ist, desto mehr gewinnt sie an Wert. So führt beispielsweise die Vorenthaltung von Informationen dazu, dass Menschen stärker daran interessiert sind, diese Informationen zu bekommen._

# Varianten des Social Engineering
## Generelle Vorgehensweise
1. Informationen sammeln.
2. Zielperson auswählen.
3. Kontakt aufnehmen, Beziehung aufbauen.
4. Sensible Informationen entlocken und ausbeuten.

## Human-based Social Engineering
- Vortäuschen einer anderen Identität
- `Shoulder Surfing` - Über die Schulter schauen, während sie an schützenswerten Informationen arbeiten
- `Eavesdropping` - Mithören von Gesprächen, z.B. Telefongesprächen
- `Dumpster Diving` - Weggeworfene Dokumente durchforsten
- `Piggybacking` - Eine Person um Hilfe bei einer Tätigkeit bitten, da man gerade "keine Hand" frei hat und dadurch die Authentifizierung umgehen. 
	- z.B. Kisten schleppen -> Ich kann meinen Ausweis gerade nicht rauskramen.
- `Tailgating` - Ähnlich zu `Piggybacking`

## Computer-based Social Engineering
- `Phishing`
	- `Pharming` - `Phishing` mit `DNS-Spoofing`. Es wird auf eine gefälschte IP Adresse / Website umgeleitet.
	- `Spear Phishing` - gezielter `Phishing`-Angriff gegen eine bestimmte Person / ein bestimmtes Unternehmen.
	- `Whaling` - `Phishing` gegen hochrangige Oper, z.B. Vorstände, Geschäftsführer, Präsidenten, Abgeordnete, ...
	- `Quishing` - Link ist als QR-Code übermittelt
- `Drive-by Download` - Herunterladen von Schadsoftware über eine manipulierte Website.
- `gefälschte Viren-Warnungen`
- `Sextortion` - Erpressung mit Nacktfotos / -videos.

# Phishing Mails
Hier wird auf eine große Masse an Mails (oder ähnlichem) gesetzt, um einen möglichst hohen Rücklauf zu erhalten
## Werkzeuge für eine Phishing Kampagne
- [[MailHog]] 
- [[GoPhish]] 
