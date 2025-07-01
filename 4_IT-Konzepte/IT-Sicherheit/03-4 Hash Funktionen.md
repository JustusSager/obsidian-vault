(im Deutschen auch "Streuwertfunktionen").
Eine Funktion welche bei einer Eingabe von beliebiger Länge zu einer Ausgabe mit fest vorgegebener Länge führt. Dabei sollen zusätzlich die Bedingungen gelten: 
- Die selbe Eingabe führt immer zu der selben Ausgabe.
- Zwei verschiedene Eingaben sollen zu zwei verschiedenen Ausgaben führen.
- Die Funktion soll schnell und einfach sein.
- Die Umkehrung einer Hash Funktion soll praktisch unmöglich sein.
Diese Ausgabe (bzw. Hash oder Hashwert) kann dadurch als eine Art Fingerabdruck der Eingabedaten gesehen werden.

Überlegen Sie sich, ob es grundsätzlich (also ungeachtet des jeweiligen Algorithmus) möglich ist, dass eine Hashfunktion keinerlei Kollisionen erzeugt?
	Nein, ist es nicht, da eine unendliche Menge an Eingabemöglichkeiten nicht zu einer begrenzten Menge an Ausgaben führen kann, welche niemals kollidieren. 

## Anwendung
- speichern von Passwörtern (nur zum Abgleich der Richtigkeit eines Passworts)
- Schlüsselableitungsfunktionen (Passwort führt z.B. zu AES Schlüssel)
- Authentizität von Daten überprüfen
- digitale Signaturen
- Blockchains

## SHA2
``` python
from Crypto.Hash import SHA256
h = SHA256.new()
h.update(b'Hier steht die Eingabe in die Hashfunktion')
print(h.hexdigest())
```
Ausgabe:
```
b8bcf11ccfbe1e2fc48e75b92162d3081fca28366004954c5dcabc2b5caa0fd9
```

Erzeugen sie dein SHA512 für ihren Namen:
``` python
from Crypto.Hash import SHA512
h = SHA512.new()
h.update(b'Justus')
print(h.hexdigest())
```
Ausgabe:
```
39e8e434b4072a471a2ec471b3b744610dfd8519b1cb1a206ba186704f31371455f93da74352b5cbc573c571bda2395083f5b1572717cf61bc647678e9db2052
```

## SHA3
``` python
from Crypto.Hash import SHA3_512
h = SHA3_512.new()
h.update(b'Justus')
print(h.hexdigest())
```
Ausgabe:
```
23e208e6d6c2e8e4af383aa85e435f3c349d547f02968b1d5825396d58ee136474c42559ad7cf650dd23820594ebb27c3f69f12bbb2252348280ff5b578aa3e2
```

## HMAC mit SHA256 
(Hasch Message Authentication Code)
Siehe auch CMAC (Cypher Message Authentication Code)
Mit HMAC soll der Empfänger einer Nachricht einen Nachweis haben, dass die übermittelte Nachricht wirklich von dem Absender kommt und das die Nachricht im Transit nicht manipuliert wurde.

Welche beiden [[1 Bedrohungen und Risiken#^b9a4e3|Schutzziele]] sollen somit durch MACs gewährleistet werden?
- Authentizität
- Integrität

``` python 
from Crypto.Hash import HMAC, SHA256
from Crypto.Random import get_random_bytes

k = get_random_bytes(16)
hmac = HMAC.new(k, digestmod=SHA256)
m = b'Lieber Bob, das ist meine Nachricht. Viele Gruesse, Alice'
hmac.update(m)
tag = hmac.hexdigest()

print(tag)
```

Erzeugen Sie einen anderen Schlüssel und verwenden Sie diesen zur Verifizierung:
``` python 
from Crypto.Hash import HMAC, SHA256
from Crypto.Random import get_random_bytes

k_ = get_random_bytes(16)

hmac = HMAC.new(k_, digestmod=SHA256)
hmac.update(m)

try:
    hmac.hexverify(tag)
    print("Die Nachricht '%s' ist authentisch." % m)
except ValueError:
    print("Nachricht oder MAC wurden manipuliert oder es wurde ein falscher Schlüssel verwendet.")
```
Ergebnis:
``` 
Nachricht oder MAC wurden manipuliert oder es wurde ein falscher Schlüssel verwendet.
```

Ändern Sie vor dem Verifizieren die Nachricht $m$:
``` python
from Crypto.Hash import HMAC, SHA256
from Crypto.Random import get_random_bytes

hmac = HMAC.new(k, digestmod=SHA256)
hmac.update(m)

m = b'Lieber Bob, das ist meine Nachricht. Viele Gruesse, Alice und noch jemand anderes'

try:
    hmac.hexverify(tag)
    print("Die Nachricht '%s' ist authentisch." % m)
except ValueError:
    print("Nachricht oder MAC wurden manipuliert oder es wurde ein falscher Schlüssel verwendet.")
```
Ergebnis:
```
Nachricht oder MAC wurden manipuliert oder es wurde ein falscher Schlüssel verwendet.
```

Ändern Sie vor dem Verifizieren den Message Authentication Code $tag$:
``` python
from Crypto.Hash import HMAC, SHA256
from Crypto.Random import get_random_bytes

hmac = HMAC.new(k, digestmod=SHA256)
hmac.update(m)

tag = hmac.hexdigest()

try:
    hmac.hexverify(tag)
    print("Die Nachricht '%s' ist authentisch." % m)
except ValueError:
    print("Nachricht oder MAC wurden manipuliert oder es wurde ein falscher Schlüssel verwendet.")
```
Ergebnis:
```
Die Nachricht 'b'Lieber Bob, das ist meine Nachricht. Viele Gruesse, Alice und noch jemand anderes'' ist authentisch.
```
