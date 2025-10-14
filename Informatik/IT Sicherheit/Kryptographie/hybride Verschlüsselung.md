Bei der hybriden Verschlüsselung wird für die aktuelle Sitzung der Übertragung ein [[symmetrische Verschlüsselung|symmetrischer Schlüssel]] erzeugt mit dem (mit einer guten Performance) die Nachrichten übermittelt werden können. Dieser symmetrische Schlüssel muss jedoch sicher an die Übertragungsteilnehmer übermittelt werden, ohne das vorher ein Nachrichtenaustausch stattgefunden hat. Hierfür kann die [[asymmetrische Verschlüsselung|asymmetrische Verschlüsselung]] verwendet werden.

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
