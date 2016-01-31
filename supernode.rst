Supernode
=========

Anleitung zur Einrichtung eines Freifunk Supernodes auf Basis von Proxmox 4.0 und Ubuntu Server 14.04.3 LTS

Proxmox
-------

Installation
^^^^^^^^^^^^

Proxmox kommt entweder per klick als Template vom Provider auf den Server oder muss von Hand installiert werden.

Konfiguration
^^^^^^^^^^^^^

Im laufenden Betrieb erfolgt die komplette Konfiguration über das Webinterface, trotzdem ist es wichtig sich für Notfälle SSH Zugriff einzurichten und den SSH Server abzusichern.

Per SSH mit dem Server verbinden
```
ssh root@111.222.333.444
```
Nun den SSH Public Key auf dem Server hinterlegen
```
mkdir .ssh
cd .ssh
nano authorized_keys
```
In die noch leere Datei den Key eintragen und den Editor wieder verlassen.

Als nächstes die SSH Verbindung beenden
```exit```

Und unter Verwendung des SSH Keys erneut verbinden
```
ssh root@111.222.333.444
```
Wenn der Key nicht als default im System hinterlegt ist muss zusätzlich der Pfad zum Key angeben werden.
Liegt der Key meinsshkey im Benutzerordner
```
ssh -i ~/meinsshkey root@111.222.333.444
```
Nun den Password login auf dem Server deaktivieren, dazu die sshd_conf editieren
```
nano /etc/ssh/sshd_conf
```
Die Zeile
```
#PasswordAuthentication yes
```
ändern in
```
PasswordAuthentication no
```
Achtung, auch wenn yes auskommentiert ist besteht die Möglichkeit sich per Password zu verbinden, erst wenn no gesetzt ist und nicht auskommentiert ist, ist der Zugriff nurnoch per Key möglich.
Den Editor wieder verlassen und den SSH Server neu starten um die Einstellungen zu übernehmen
```
/etc/init.d/ssh restart
```
