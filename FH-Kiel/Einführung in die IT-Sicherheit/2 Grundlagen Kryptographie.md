Quellbezug: 
 - Übung 1 (26.03.2025)

#TODO Mathematischen Teil erstellen.
# Verschlüsslung mit symmetrischem Schlüssel
Bei der symmetrischen Verschlüsselung ist der selbe Schlüssel zum Ver- und Entschlüsseln verwendet.

## Caesar
``` python
import random

def Gen():
    return random.randint(0,25)

def Enc(k, m):
    c = ""
    m = m.upper()
    for m_buchst in m:
        if ord(m_buchst) >= 65 and ord(m_buchst) <= 90:
            c_buchst = chr((((ord(m_buchst)-65) + k) % 26) + 65)
            c += c_buchst
    return c

def Dec(k, c):
    m = ""
    c = c.upper()
    for c_buchst in c:
        if ord(c_buchst) >= 65 and ord(c_buchst) <= 90:
            m_buchst = chr((((ord(c_buchst)-65) - k) % 26) + 65)
            m += m_buchst
    return m
```

Jeder Buchstabe wird um 3 Stellen verschoben:
``` python
k = 3
m = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
print("Nachrichtenalphabet: " + m)
print("Geheimtextalphabet:  " + Enc(3, m))
```
Ergebnis:
```
Nachrichtenalphabet: ABCDEFGHIJKLMNOPQRSTUVWXYZ
Geheimtextalphabet:  DEFGHIJKLMNOPQRSTUVWXYZABC
```

Verschlüsselung:
``` python
import random
k = Gen()
m = "Justus"
c = Enc(k, m)
print(c)
```
Ergebnis:
```
HSQRSQ
```

Entschlüsselung:
``` python
k = 17
c = "XLKXVDRTYKURJZJKIZTYKZX"
m = Dec(k, c)
print(m)
```
Ergebnis:
```
GUTGEMACHTDASISTRICHTIG
```

Mithilfe einer simplen for-Schleife lassen sich alles 26 Möglichkeiten durchspielen:
``` python
c = "WTLBLMLNIXKZXAXBF"

print ("Brute Force:")
for i in range(26):
    print(i , Dec(i, c))

print (f"Result: 19 {Dec(19, c)}")
```
Ergebnis:
```
Brute Force:
0 WTLBLMLNIXKZXAXBF
1 VSKAKLKMHWJYWZWAE
2 URJZJKJLGVIXVYVZD
3 TQIYIJIKFUHWUXUYC
4 SPHXHIHJETGVTWTXB
5 ROGWGHGIDSFUSVSWA
6 QNFVFGFHCRETRURVZ
7 PMEUEFEGBQDSQTQUY
8 OLDTDEDFAPCRPSPTX
9 NKCSCDCEZOBQOROSW
10 MJBRBCBDYNAPNQNRV
11 LIAQABACXMZOMPMQU
12 KHZPZAZBWLYNLOLPT
13 JGYOYZYAVKXMKNKOS
14 IFXNXYXZUJWLJMJNR
15 HEWMWXWYTIVKILIMQ
16 GDVLVWVXSHUJHKHLP
17 FCUKUVUWRGTIGJGKO
18 EBTJTUTVQFSHFIFJN
19 DASISTSUPERGEHEIM
20 CZRHRSRTODQFDGDHL
21 BYQGQRQSNCPECFCGK
22 AXPFPQPRMBODBEBFJ
23 ZWOEOPOQLANCADAEI
24 YVNDNONPKZMBZCZDH
25 XUMCMNMOJYLAYBYCG
Result: 19 DASISTSUPERGEHEIM
```

<b>Überlegen Sie sich, welche Gründe gegen den Einsatz der Caesar-Chiffre heutzutage sprechen!</b>
Die Caesar-Chiffre ist heute sehr einfach zu knacken, da es nur 26 mögliche Kombinationen gibt. Mithilfe einer einfachen Schleife kann man sich alle möglichen Kombinationen erstellen lassen, und dann die Möglichkeiten durchgehen, welche einen sinnvollen Satz ergibt.

## AES 
### mit ECB Mode
ECB Mode = Electronic Code Blocks Mode

``` python
from Crypto.Cipher import AES
from Crypto.Random import get_random_bytes

def Gen(n=128): # 128 bits als Standard-Schlüssellänge, falls kein Parameter übergeben wird
    if n == 192: # Schlüssellänge 192 bits
        k = get_random_bytes(24)
    elif n == 256: # Schlüssellänge 256 bits
        k = get_random_bytes(32)
    else: # Schlüssellänge 128 bits als Standard, falls irgend etwas anderes als Parameter übergeben wird
        k = get_random_bytes(16)
    return k

def Enc(k, m):
    aes = AES.new(k, AES.MODE_ECB)
    c = aes.encrypt(m)
    return c

def Dec(k, c):
    aes = AES.new(k, AES.MODE_ECB)
    m = aes.decrypt(c)
    return m
```

Verschlüsselung:
``` python
# Erzeugung eines zufälligen Schlüssels
k = Gen(128)
print('k = ' + str(k.hex()))

# Verschlüsselung einer Nachricht (hier: Länge 48 Zeichen, also 3 Blöcke)
m = b'Verschluesselung mit AES ist gar nicht so schwer'
c = Enc(k, m)
print('c = ' + str(c.hex()))

# Entschlüsselung des Geheimtextes
print('Entschlüsselter Geheimtext: m = ' + str(Dec(k, c)))
```
Ergebnis:
```
k = ffada0ce9c49c493ff8d53430b33caa1
c = 80e4c00f596248e9c0f0fe11744329c52e3b87bbfd6dd5247333b8dd18a97e426c93ef9be6009c97f2ea6aa8aad2d5b7
Entschlüsselter Geheimtext: m = b'Verschluesselung mit AES ist gar nicht so schwer'
```

Verschlüsselung mit 2 identischen Blöcken:
``` python
k = Gen(128)

m = b'DiesIstEinText16DiesIstEinText16'
print("m: ", m.hex())

c = Enc(k, m)
print("c: ", c.hex())
```
Ergebnis:
```
m:  4469657349737445696e5465787431364469657349737445696e546578743136
c:  a66ecf074d8132d1464ee3eb88a9657aa66ecf074d8132d1464ee3eb88a9657a
```

<b>Was fällt Ihnen bei diesem kleinen Experiment auf und welche Folgerung ziehen Sie daraus bzgl. der Sicherheit des ECB-Modus?</b>
Beim Verschlüsseln von zwei identischen Blöcken mit der AES Verschlüsselung im ECB Modus haben beide Blöcke am Ende den selben verschlüsselten Wert. Daraus lässt sich schonmal nur anhand des verschlüsselten Texts schließen, dass der erste Block und der zweite Block identisch ist. 

``` 
m:  4469657349737445696e546578743136 4469657349737445696e546578743136
c:  a66ecf074d8132d1464ee3eb88a9657a a66ecf074d8132d1464ee3eb88a9657a
```
hier einmal durch Leerzeichen verdeutlicht, die wären sonst nicht vorhanden

### mit CTR Mode
CTR Mode = Counter Mode
``` python
from Crypto.Cipher import AES
from Crypto.Random import get_random_bytes

def Gen(n=128): # der Gen-Algorithmus ist unverändert
    if n == 192: # Schlüssellänge 192 bits
        k = get_random_bytes(24)
    elif n == 256: # Schlüssellänge 256 bits
        k = get_random_bytes(32)
    else: # Schlüssellänge 128 bits als Standard, falls irgend etwas anderes als Parameter übergeben wird
        k = get_random_bytes(16)
    return k

def Enc(k, m):
    aes = AES.new(k, AES.MODE_CTR)
    c = aes.nonce # Zählerstand nonce steht zu Beginn des Geheimtextes
    c += aes.encrypt(m) # der eigentliche Geheimtext wird an den Zählerstand angehängt
    return c

def Dec(k, c):
    aes = AES.new(k, AES.MODE_CTR, nonce = c[0:8]) # die ersten 8 bytes des Geheimtextes sind der Anfangszählerstand
    return aes.decrypt(c[8:]) # entschlüsselt und ausgegeben wird nur der eigentliche Geheimtext
```

Verschlüsselung:
``` python
k = Gen(128)
m = b"Justus Sager"
print("m: ", m.hex())

c = Enc(k, m)
print("c: ", c.hex())
```
Ergebnis:
```
m: 4a7573747573205361676572
c: 3639143c47025048ff7a56d363f77623a0bb186f
```
Bei der Verschlüsselung wird ein Counter verwendet, der zur Entschlüsselung wieder benötigt wird. Dieser Counter wird dem verschlüsseltem Text vorangestellt. Dadurch ist der verschlüsselte Text um X Bytes länger als der zu Verschlüsselnde. 

Verschlüsselung mit 2 identischen Blöcken:
``` python
k = Gen(128)
m = b"DiesIstEinText16DiesIstEinText16"
print("m: ", m.hex())

c = Enc(k, m)
print("c: ", c.hex())
```
Ergebnis:
```
m: 4469657349737445696e5465787431364469657349737445696e546578743136
c: 5aac05b9965eb829f64890676b394233f8bd10182cad68ee077257c2ad580716aca201734ee3b598
```

<b>Was fällt Ihnen bei dieser Durchführung des Experiments auf? Wie bewerten Sie die Sicherheit des CTR-Modus im Vergleich zum ECB-Modus?</b>
Beim Verschlüsseln im CTR-Modus ergeben identische Blöcke nicht mehr identische verschlüsselte Nachrichten. Es lässt sich aus dem verschlüsseltem Text nicht mehr ablesen, dass der erste und der zweite Block identisch ist.

```
m:
				 4469657349737445696e546578743136 4469657349737445696e546578743136
c:
0027484d36a66c63 38e70dab489eb7987fa5ec05e7306e68 3f55988cbdc13ac187bf896a3c61d943
```

# Verschlüsslung mit asymmetrischem Schlüssel
