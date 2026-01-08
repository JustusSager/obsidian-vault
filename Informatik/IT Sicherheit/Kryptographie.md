#Informatik #IT-Sicherheit 
# symmetrische Verschlüsselung
Bei der symmetrischen Verschlüsselung wird der selbe Schlüssel zum Ver- und Entschlüsseln verwendet.
Dabei müssen sich die Gesprächsteilnehmer auf einen gemeinsamen Schlüssel einigen. Dies hat den Nachteil, dass es einen direkten Kontakt gegeben haben muss, um diesen Schlüssel auszutauschen.

## Caesar-Verschlüsselung
- Es wird jeder Buchstabe innerhalb der Nachricht einzeln betrachtet.
- Jeder Buchstabe wird um eine bestimmte Anzahl $k$ relativ zum Alphabet verschoben.
- z.B. Bei dem Schlüssel $k=3$ wird der Buchstabe $A$ der Nachricht zu einem $D$ in der Nachricht.
Für den Mathematischen Ansatz siehe [[modulare Arithmetik#Cäsar-Verschlüsselung]].
### Python Beispiel
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
m = "Dies ist eine sehr geheime Nachricht"
c = Enc(k, m)
print(c)
```
Ergebnis:
```
GLHVLVWHLQHVHKUJHKHLPHQDFKULFKW
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

### Schwachstelle
Da es bei der Caesar-Verschlüsselung nur 26 mögliche Schlüssel gibt, ist das Knacken der Verschlüsselung nicht weiter schwierig. Man kann sich einfach alle Kombinationen ausgeben lassen und schauen, bei welcher ein sinnvoller Text herauskommt.
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

## AES-Verschlüsselung
### Python Beispiel
#### mit ECB Mode
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

#### mit CTR Mode
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

#### GCM Modus
GCM basiert auf CTR und hat damit ähnliche Sicherheitsfeatures. 
Für Details siehe https://de.wikipedia.org/wiki/Galois/Counter_Mode
### Schwachstellen
#TODO
# asymmetrische Verschlüsselung
Es gibt hierbei nicht mehr einen Schlüssel, der zum Ver- und Entschlüsseln verwendet werden kann, sondern ein Schlüsselpaar. Dieses Schlüsselpaar beseht aus 2 Schlüsseln.
- Der Public-Key wird zum Verschlüsseln einer Botschaft verwendet und ist, wie der Name schon sagt, öffentlich (d.h. für alle Zugänglich). 
- Der Private-Key wird zum entschlüsseln einer verschlüsselten Botschaft verwendet. Dieser Schlüssel muss vom Empfänger der Botschaft geheim gehalten werden.
Eine Botschaft die mit einem Public-Key verschlüsselt wurde, kann nur mit dem zum Public-Key Verbundenen Private-Key entschlüsselt werden.

Dabei muss jedoch folgendes beachtet werden:
1. Jeder hat Zugriff auf den Public-Key von jedem. Auch Angreifer.
2. Wenn der Private-Key von jemandem bekannt ist, können sämtliche Nachrichten an diese Person entschlüsselt werden. Es darf nicht möglich sein aus dem Public-Key Rückschlüsse auf den Private-Key zu ziehen.
3. Es muss sichergestellt werden, dass der veröffentlichte Public-Key auch wirklich zu der Person gehört, der dabei angegeben ist. Siehe dazu #TODO Zertifikate.
4. Eine asymmetrische Verschlüsselung ist deutlich rechenintensiver als eine Symmetrische.
Für den mathematischen Ansatz siehe [[modulare Arithmetik#RSA-Verschlüsselung]].
## RSA
### Python Beispiel
``` python 
from Crypto.Cipher import PKCS1_OAEP
from Crypto.PublicKey import RSA
from base64 import b64decode

def Gen(bits=3072):
    '''
Erzeugt ein Schlüsselpaar für RSA im PEM-Format unter Verwendung von e=65537.
Eingabe: Sicherheitsparameter/"Schlüssellänge" (optional, Default ist n=3072 gem. aktueller Empfehlung des BSI)
Ausgabe: Schlüsselpaar bestehend aus public key und private key
    '''
    keypair = RSA.generate(bits, e=65537)
    public_key = keypair.publickey().exportKey("PEM")
    private_key = keypair.exportKey("PEM")
    return public_key, private_key

def Enc(public_key, message):
    '''
Verschlüsselung gem. PKCS#1_OAEP
Eingaben: * öffentlicher Schlüssel Empfänger/-in (als String)
          * zu verschlüsselnde Nachricht
Ausgabe:  Geheimtext
    '''
    pk = RSA.importKey(public_key)
    rsa_oaep_es = PKCS1_OAEP.new(pk)
    ciphertext = rsa_oaep_es.encrypt(message)
    return ciphertext

def Dec(private_key, ciphertext):
    '''
Entschlüsselung gem. PKCS#1_OAEP
Eingaben: * privater Schlüssel Besitzer/-in
          * zu entschlüsselnder Geheimtext
Ausgabe:  (entschlüsselte) Nachricht
    '''
    sk = RSA.importKey(private_key)
    rsa_oaep_es = PKCS1_OAEP.new(sk)
    message = rsa_oaep_es.decrypt(ciphertext)
    return message
```

Schlüsselpaar generieren und ausgeben:
``` python
[pk,sk] = Gen()
print(pk.decode('ascii'))
print(sk.decode('ascii'))
```

Drei Geheimtexte generieren:
``` python
m1 = b'Justus'
m2 = b'Justus'
m3 = b'Justus'
c1 = Enc(pk, m1)
c2 = Enc(pk, m2)
c3 = Enc(pk, m3)
print("c1 = " + c1.hex())
print("c2 = " + c2.hex())
print("c3 = " + c3.hex())
```
Ausgabe:
```
c1 = 1ab233e61fefa1c5e52de08222ccdb219c031b27fb4c0efdacdb76afd7379a0a1c85c646d5f90d25fb8f23e38ff46c30d98b533161357ac5981d43a0966d91be1cd4a330683133f1cb8703dbd4b6e4e9865fea322452ecfd791c3662c5d23db4c6ff84fb96853050f1bf80e8e991e31760b4fd89065d5e84d62dc28e72be54faba273689c60abcb8443aace883cfe7cfb686811263388848b3db4569d588454f56daac350be4f771eec7ae0c064ee1aa0cf802104c156fc4374568263d1035d276f9a42e75e62342c5994b6b9e25d594e02ff451cf2eee1a39cd2b4fd937b5688925e5357532863ecab6bd7943b39898f2dc24fb1e3c1c58b95112ee8d141de62db327dbc9afb5247396563d07fdccedcf6bdaabd6385f49843a1faab2dc98775780634840c6429b43a4f582bbe5639b65610eedc2c8bf29880b8dd241f2f858c6439879851ac0237c4736ebfd04f77a9370f8c262ae1c89391848b31b7efbb8ae678eafbab5ba66a1fcdeb690c02edd3b1dd4a472078c0d86d9b9fa3218b023
c2 = 7ac7980f13117aa965685aca99f6cb51f6d8d96e05c6e12a2d4fa2802179895ab17dc5d964b0b0ffb6b3b0abc5cca8e385d028607e6170933557b4fd51005ea422a53547c4d249417b0c55d36379b5578378fd6ff47eb07d595ffdf8fb40acac510d922aa5e7dfd717c2c8541ebdd2393a0bd56a53a04612c590b893aa17dfba4ef739b66f543a6eaa24173c436c4270eb1c360e5386a91d2d8f0b80dbd710df4164fb21dec223f29dcdb1c3d11a3524f1a3ad01e4fd9c5a34a1dab05489484ce445a5b744c02464090c8ba787d310858a4e8f3c90b45b449f01983663cc3909c83d99de950a5d716ae930a4785cdee3bf81bc4ed813b47ff0a674f9ebfcb42003f9a9e89cc9c5ff1f1ad41b2acc58b16c957e5e39d643310522717bf7051ad2618afc3473b40650b78c163cbab6edf047808f304661365df11826998c688111fe288d165fea3d22201d2370712aeb1a0b1aa74fd8e858ce05072a0612d17799a65c068f9add33bb02a4cd99c5bc4705e34d63dd74fcf7f6ff0d766e49c086f5
c3 = 2f7f3b9acf318b04da6323e0a15611429515f0f176c1f11e07bfca1327c212f1d25afd87289933110406fcb7d7fbfcaeeeb97bc8338b00c5291b87461323f603a87627fc439401d4591ad41ffe118931eae09d9b48833eb811984c4e295885cfaa7a2e100bc282e6d913ba2422ea117ce2a80cb54a3248c92674a1aa8b457c7076b9605f1afbe1d73191a95a97505c339fa32049ade92d0294d9a3c00884df4eb9a463204f425fa389ef4ea55388ee141eefb8016e3775c4923a382d1cacf3139e6acc1d2f6bfd3cc111ae1b51ea43d43fc4b29aaf75aa2bfef9266c7e13ea8c1a005c8477d9b184fdf59d40676e24e511bb8cb1986aba235eaf0f64f32e6ee561bcb2ce8327379603632c5252b1fbb7537bba9e6c4c8f6e9959a76b11ac7fd3bab7d73eee288a6bde3577115205be373653843630bb377ab69252e13c61eb184612d857da6be35a508efd6e5a55eca444e5e42b6e34a574daaf200227a7945a0bd87e593d95fc78c5c70881bd9f07d377101f49c9d3096d4115f30c9e76dffc
```

Vergleichen Sie die drei erzeugten Geheimtexte. Was fällt Ihnen auf?
- Obwohl alle 3 Eingaben die selben waren und der verwendete Public-Key der selbe war ergeben sich bei nach der Verschlüsselung drei verschiedene verschlüsselte Ausgaben.

Wie nennt man diese Art der Verschlüsselung?
- Asymmetrische Verschlüsselung ?
- RSA ?
- randomisiert bzw. probabilistisch

Weshalb ist diese Art der Verschlüsselung bei einer Public-Key-Verschlüsselung besonders wichtig?
- #TODO

Entschlüsseln der Geheimtexte:
``` python
_m1 = Dec(sk, c1)
_m2 = Dec(sk, c2)
_m3 = Dec(sk, c3)
print(_m1)
print(_m2)
print(_m3)
```
Ausgabe:
```
b'Justus'
b'Justus'
b'Justus'
```
# hybride Verschlüsselung
Bei der hybriden Verschlüsselung wird für die aktuelle Sitzung der Übertragung ein [[#symmetrische Verschlüsselung|symmetrischer Schlüssel]] erzeugt mit dem (mit einer guten Performance) die Nachrichten übermittelt werden können. Dieser symmetrische Schlüssel muss jedoch sicher an die Übertragungsteilnehmer übermittelt werden, ohne das vorher ein Nachrichtenaustausch stattgefunden hat. Hierfür kann die [[#asymmetrische Verschlüsselung|asymmetrische Verschlüsselung]] verwendet werden.
## Python Beispiel

``` python
from Crypto.Cipher import PKCS1_OAEP
from Crypto.PublicKey import RSA
from base64 import b64decode

def Gen_sym(n=128):
    if n == 192:
        k = get_random_bytes(24)
    elif n == 256:
        k = get_random_bytes(32)
    else:
        k = get_random_bytes(16)
    return k

def Enc_sym(k, m):
    aes = AES.new(k, AES.MODE_CTR)
    c = aes.nonce
    c += aes.encrypt(m)
    return c

def Dec_sym(k, c):
    aes = AES.new(k, AES.MODE_CTR, nonce = c[0:8])
    return aes.decrypt(c[8:])

def Gen_asym(bits=3072):
    keypair = RSA.generate(bits, e=65537)
    public_key = keypair.publickey().exportKey("PEM")
    private_key = keypair.exportKey("PEM")
    return public_key, private_key

def Enc_asym(public_key, message):
    pk = RSA.importKey(public_key)
    rsa_oaep_es = PKCS1_OAEP.new(pk)
    ciphertext = rsa_oaep_es.encrypt(message)
    return ciphertext

def Dec_asym(private_key, ciphertext):
    sk = RSA.importKey(private_key)
    rsa_oaep_es = PKCS1_OAEP.new(sk)
    message = rsa_oaep_es.decrypt(ciphertext)
    return message

def Gen():
    return Gen_asym()

def Enc(public_key, message):
    k = Gen_sym()
    cm = Enc_sym(k, message)
    ck = Enc_asym(public_key, k)
    return (ck, cm)

def Dec(private_key, c):
    k = Dec_asym(private_key, c[0])
    return Dec_sym(k, c[1])
    
```
Verschlüsseln:
``` python
[pk,sk] = Gen()
m = b'Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magn'
c = Enc(pk, m)
print(c[0].hex(), "\n", c[1].hex())
```
Ausgabe:
```
a51a143d2898dec3188eedb9e112f8eacf44a85a58fe9dda0d6fb84e156e2cf46ce1f3dd5eedd25f6f81d77c41cbf4ce0e869676160af1cb6dc248ca3f9a21b02c506567c36b3db6af1d37ef8a3a35dced4617199bf93f386dfa775cdbcc6a66fa40b98fa6eead4db888a67dac6be10f057bbe08dfe4f5487114ac22ad449b73e9e13dd6e26a9331f6e4e1bd5e4be8aa0e3aa62e38265307f83f23e75ae6f3aaf564cbbf6b6c96b5acd486b6a26046c5fe42545c01d7159c2058b370591b8ba5e2f8ab20d8240d5d91bc2a8934a52f7f389f40b0e7cccceeb4a35b4d8032b63814df6bcb63c919d1a1854a684c705a6eebf26e8fa8582f162b3f6f42def9a7f92114b81d5819f5dcf0187ba89fee14956f1628b218cea575cf8649c63d32c61e3c558e990adb1dc63414f8ebc70a02f90a6be1d8594b3c172aecb5c587ff480ce45bfd65a6f8805fccd6c101fea95c40ae3a6b9073410efef66ebd2a8ab9eeb72ee5b77533f4d9093454dc103781694f68c190f79ffa2861c0e62f1ed802027b 
 9c08fd52fc6066fe88efff7c23265eef77baa23909c09b81e1de02f2c8f7e6c3aa95f9f3e44f12f6b293d2d370d088afc77571d9d0869344fce5343d860a05d9ba916834ede055fe79d82e02ed49860103293e8f217d02d21297133b88a4d820c24d5779aee8b9d151747c746ad61887246fe6c0811b0864a4276e0c6a4dd20d
```
Entschlüsseln:
``` python
_m = Dec(sk, c)
print(_m)
```
Ausgabe:
```
b'Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magn'
```
Warum ist es notwendig, für jede Verschlüsselung einen neuen Sitzungsschlüssel zu erzeugen?
#TODO
Stellen Sie sich vor, Sie haben die hybride Verschlüsselung über einen längeren Zeitraum genutzt. Welche Konsequenzen hat es, wenn Eve zu einem späteren Zeitpunkt an den privaten Schlüssel gelangt?
#TODO
# Hash Funktionen
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
### Python Beispiel
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
### Python Beispiel
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

Welche beiden [[Bedrohungen und Risiken#Schutzziele|Schutzziele]] sollen somit durch MACs gewährleistet werden?
- Authentizität
- Integrität
### Python Beispiel
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
# Digitale Signaturen
Bei der Digitalen Signatur wird zu einer Nachricht, mithilfe des Private-Key, eine Signatur erzeugt. Diese Signatur kann daraufhin, mithilfe des Public-Key und der empfangenen Nachricht, geprüft werden.

Überlegen Sie sich, welche Funktionen handschriftliche Unterschriften im täglichen Leben haben.
	Digitale Signaturen sind eine Bestätigung, dass eine Person an einer "Transaktion" beteiligt war. Wenn man z.B. in einem Geschäft mit Karte bezahlt, ist die Unterschrift dafür da, dass das Unternehmen nachweisen kann das die Transaktion mit der Person stattgefunden hat und das Geld abbuchen darf. Ein anderes Beispiel ist, dass Mieter und Vermieter beide den Mietvertrag zur Kenntnis genommen haben und einverstanden mit den Bedingungen sind. 

Welche Konstellationen können beim Verifizieren einer Signatur zum Ergebnis "ungültig" führen?
- Der Public-Key und der Private-Key bilden kein zusammenpassendes Schlüsselpaar.
- Die Nachricht hat sich verändert.
## Python Beispiel
#TODO Irgendwas stimmt hier nicht (Crypto Signatur)
``` python
from Crypto.Signature import pkcs1_15
from Crypto.Hash import SHA256
from Crypto.PublicKey import RSA

def Gen(bits=3072):
    keypair = RSA.generate(bits, e=65537)
    public_key = keypair.publickey().exportKey("PEM")
    private_key = keypair.exportKey("PEM")
    return public_key, private_key

def Sign(private_key, m):
    sk = RSA.importKey(private_key)
    h = SHA256.new(m)
    signature = pkcs1_15.new(sk).sign(h)
    return signature

def Vrfy(public_key, m, signature):
    pk = RSA.import_key(public_key)
    h = SHA256.new(m)
    try:
        pkcs1_15.new(public_key).verify(h, signature)
        return 1
    except (ValueError, TypeError):
        return 0
```

``` python
# Schlüsselpaar generieren
public_key, private_key = Gen()

# Nachricht signieren
message = b'Dies ist eine aeusserst wichtige Nachricht von mir!'
signature = Sign(private_key, message)

# Signatur überprüfen
result = Vrfy(public_key, message, signature)
print(result)
```
