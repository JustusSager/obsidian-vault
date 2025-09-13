Bei der Digitalen Signatur wird zu einer Nachricht, mithilfe des Private-Key, eine Signatur erzeugt. Diese Signatur kann daraufhin, mithilfe des Public-Key und der empfangenen Nachricht, geprüft werden.

Überlegen Sie sich, welche Funktionen handschriftliche Unterschriften im täglichen Leben haben.
	Digitale Signaturen sind eine Bestätigung, dass eine Person an einer "Transaktion" beteiligt war. Wenn man z.B. in einem Geschäft mit Karte bezahlt, ist die Unterschrift dafür da, dass das Unternehmen nachweisen kann das die Transaktion mit der Person stattgefunden hat und das Geld abbuchen darf. Ein anderes Beispiel ist, dass Mieter und Vermieter beide den Mietvertrag zur Kenntnis genommen haben und einverstanden mit den Bedingungen sind. 

Welche Konstellationen können beim Verifizieren einer Signatur zum Ergebnis "ungültig" führen?
- Der Public-Key und der Private-Key bilden kein zusammenpassendes Schlüsselpaar.
- Die Nachricht hat sich verändert.

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
