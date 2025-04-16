- Software zum aussenden und Tracken von Phishing E-Mails
- Linux
- Webbasiert

# Sending Profile
- Hier wird die Verbindung zu einem E-Mail Server konfiguriert, von dem die Mail versendet werden

# Landing Pages
- Hier können Fake Websites konfiguriert werden, auf die der Link in der Mail verweist.

# Email Templates
- Hier können E-Mails formuliert werden, die rausgeschickt werden.

## Mail im HTML Format
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

## Link zur Landing Page einbinden
``` html
<a href="{{.URL}}">TEXT</a>
```
Hiermit kann ein Link zu der in der Campaign angegebenen Landing Page eingebettet werden.

# Users & Groups
- Hier werden die Empfänger der Mails angegeben.

# Campaigns
- Hier läuft alles zusammen.