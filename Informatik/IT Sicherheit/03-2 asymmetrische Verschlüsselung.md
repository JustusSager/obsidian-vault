Es gibt hierbei nicht mehr einen Schlüssel, der zum Ver- und Entschlüsseln verwendet werden kann, sondern ein Schlüsselpaar. Dieses Schlüsselpaar beseht aus 2 Schlüsseln.
- Der Public-Key wird zum Verschlüsseln einer Botschaft verwendet und ist, wie der Name schon sagt, öffentlich (d.h. für alle Zugänglich). 
- Der Private-Key wird zum entschlüsseln einer verschlüsselten Botschaft verwendet. Dieser Schlüssel muss vom Empfänger der Botschaft geheim gehalten werden.
Eine Botschaft die mit einem Public-Key verschlüsselt wurde, kann nur mit dem zum Public-Key Verbundenen Private-Key entschlüsselt werden.

Dabei muss jedoch folgendes beachtet werden:
1. Jeder hat Zugriff auf den Public-Key von jedem. Auch Angreifer.
2. Wenn der Private-Key von jemandem bekannt ist, können sämtliche Nachrichten an diese Person entschlüsselt werden. Es darf nicht möglich sein aus dem Public-Key Rückschlüsse auf den Private-Key zu ziehen.
3. Es muss sichergestellt werden, dass der veröffentlichte Public-Key auch wirklich zu der Person gehört, der dabei angegeben ist. Siehe dazu #TODO Zertifikate.
4. Eine asymmetrische Verschlüsselung ist deutlich rechenintensiver als eine Symmetrische.

## RSA
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
