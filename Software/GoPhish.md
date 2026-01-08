#Informatik #IT-Sicherheit 
Software zum aussenden und überwachen von Phishing E-Mails.
- Linux
- Web-basiert
### Konfiguration
- Default Admin Webpage Port: 3333
- Default Username: admin
- Default Passwort: phishing
### Sending Profile
Hier wird die Verbindung zu einem E-Mail Server konfiguriert, von dem die Mails versendet werden.
#### Konfiguration:
- Interface Type: SMTP
- SMTP From: (vorgespielte) Absende-Adresse des Mailservers
- Host: Serveradresse des SMTP Mailservers. 
	- Siehe dazu: [[MailHog]].
- Username/Password: Anmeldedaten des Mailservers

### Landing Pages
Hier können Fake Websites konfiguriert werden, auf die der Link in der Mail verweist.
### Email Templates
Hier können E-Mails formuliert werden, die rausgeschickt werden.
#### Mail im HTML Format
``` html
<html>
<head>
	<title></title>
	<meta charset="utf-8">
</head>
<body>
<!-- Hier den Inhalt der Mail reinschreiben -->
</body>
</html>
```
#### Link zur Landing Page einbinden
``` html
<a href="{{.URL}}">TEXT</a>
```
Hiermit kann ein Link zu der in der Campaign angegebenen Landing Page eingebettet werden.
### Users & Groups
Hier werden die Empfänger der Mails angegeben.
### Campaigns
Hier läuft alles zusammen.
#### Konfiguration
- Email Template: Das erstellte Email Template wählen. Siehe weiter oben.
- Landing Page: Die erstellte Landing Page wählen. Siehe weiter oben.
- URL: die URL des GoPhish Servers. z.B. "http://192.169.233.5"
