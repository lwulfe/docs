Supernode
=========

Anleitung zur Einrichtung eines Freifunk Supernodes auf Basis von Proxmox 4.0 und Ubuntu Server 14.04.3 LTS

Proxmox
-------

Installation
^^^^^^^^^^^^

Proxmox kommt entweder per klick als Template vom Provider auf den Server oder muss von Hand installiert werden.

SSH
^^^^^^^^^^^^^

Im laufenden Betrieb erfolgt die komplette Konfiguration über das Webinterface, trotzdem ist es wichtig sich für Notfälle SSH Zugriff einzurichten und den SSH Server abzusichern.

Per SSH mit dem Server verbinden

::
	
	ssh root@111.222.333.444

Nun den SSH Public Key auf dem Server hinterlegen

::

	mkdir .ssh
	cd .ssh
	nano authorized_keys

In die noch leere Datei den Key eintragen und den Editor wieder verlassen.

Als nächstes die SSH Verbindung beenden

::

	exit

Und unter Verwendung des SSH Keys erneut verbinden

::

	ssh root@111.222.333.444

Wenn der Key nicht als default im System hinterlegt ist muss zusätzlich der Pfad zum Key angeben werden.
Liegt der Key meinsshkey im Benutzerordner

::

	ssh -i ~/meinsshkey root@111.222.333.444

Nun den Password login auf dem Server deaktivieren, dazu die sshd_conf editieren

::

	nano /etc/ssh/sshd_conf

Die Zeile

::

	#PasswordAuthentication yes

ändern in

::

	PasswordAuthentication no

Achtung, auch wenn yes auskommentiert ist besteht die Möglichkeit sich per Password zu verbinden, erst wenn no gesetzt ist und nicht auskommentiert ist, ist der Zugriff nur noch per Key möglich.
Den Editor wieder verlassen und den SSH Server neu starten um die Einstellungen zu übernehmen

::

	/etc/init.d/ssh restart

Monitoring
^^^^^^^^^^

Den Check_MK Agent steht in der Check_MK Weboberfläche als .deb Paket bereit, dieses kann herunter geladen und dann per SCP auf den Server kopiert werden.
Auf dem lokalen Rechner nicht in der SSH Session

::

	scp /pfadzurdatei/ root@111.222.333.444:~


Der Agent liegt jetzt im Benutzerordner des Servers.
Um das .deb Paket zu installieren wird gdebi empfohlen, ausserdem benötigt der Agent xinetd zum ausliefern der monitoring Daten.
Per SSH auf dem Server

::

	apt-get install gdebi xinetd
	gdebi checkmkagent.deb

Images hochladen
^^^^^^^^^^^^^^^^
Iso Files zur installation können zwar über das Webinterface hochgeladen werden, aber je nach Internetanbindung dauert das lange. Per wget wird das Image direkt auf den Server geladen.

::
	
	cd /vz/template/iso
	wget http://releases.ubuntu.com/14.04.3/ubuntu-14.04.3-server-amd64.iso


Ab jetzt geht es im Browser weiter.

Supernode anlegen
^^^^^^^^^^^^^^^^^

Das Webinterface ist unter folgender Adresse erreichbar

::

	https://111.222.333.444:8006

Die Anmeldung erfolgt mit Benutzername und Kennwort.

Auf der linken Seite den Server auswählen und dann oben rechts 'Create VM'

Im Reiter 'General' eine Freie ID und einen Namen festlegen.

Im Reiter 'OS' 'Linux 4.x/3.x/2.6 Kernel auswählen.

Im Reiter 'CD/DVD' das ISO Image auswählen.

Im Reiter 'Hard Disk' als 'Bus' 'VirtIO' einstellen, die Festplattengröße auf 8GB begrenzen und als Format 'qcow2' wählen.

Im Reiter 'CPU' zwei Prozessorkerne zuweisen.

Im Reiter 'Memory' unter 'Automatically allocate memory within this range' 256 -1024MB festlegen.

Im Reiter 'Network' als Netzwerkkarte 'VirtIO' auswählen und die MAC Adresse der für diesen Supernode zu verwendenden öffentlichen IPv4 Adresse eintragen.

Bestätigen und Anlegen

Die VM Links auswählen und oben rechts starten und die Konsole öffnen.
