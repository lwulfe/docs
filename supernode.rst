Supernode
=========

Anleitung zur Einrichtung eines Freifunk Supernodes auf Basis von Proxmox 4.0 und Ubuntu Server 14.04.3 LTS

Proxmox
-------

Installation
^^^^^^^^^^^^

Proxmox kommt entweder per Klick als Template vom Provider auf den Server oder muss von Hand installiert werden.

SSH
^^^

Im laufenden Betrieb erfolgt die komplette Konfiguration über das Webinterface, trotzdem ist es wichtig, sich für Notfälle einen SSH Zugriff einzurichten und natürlich auch den SSH Server abzusichern.

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

Achtung, auch wenn yes auskommentiert ist besteht die Möglichkeit sich per Password zu verbinden, erst wenn 'no' gesetzt ist und nicht (mehr) auskommentiert ist, ist der Zugriff nur noch per Key möglich.
Den Editor wieder verlassen und den SSH Server neu starten um die Einstellungen zu übernehmen


::

	/etc/init.d/ssh restart

::  
        optional: kein direkter Root-Login

_ToDo_: Als zusätzliche Sicherheitsstufe ist es möglich, (direkte) root-Logins komplett untersagen. 
Dann muss der Login über einen zusätzlicn anzulegenden Benutzer (sshkey siehe oben) erfolgen. 
Zudem hinreichend sicheres Passwort setzen und den User in die sudoers-Gruppe aufnehmen.


Monitoring
^^^^^^^^^^

Den Check_MK Agent steht in der Check_MK Weboberfläche als .deb Paket bereit, dieses kann herunter geladen und dann per SCP auf den Server kopiert werden.
Auf dem lokalen Rechner nicht in der SSH Session

::

	scp /pfadzurdatei root@111.222.333.444:~


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

Netzwerk einrichten
^^^^^^^^^^^^^^^^^^^

Das Webinterface ist unter folgender Adresse erreichbar

::

	https://111.222.333.444:8006

Die Anmeldung erfolgt mit Benutzername und Kennwort.

Nachdem links in der Seitenleiste das Blech asugewählt wurde rechts im Reiter Network zusätzlich zur vorhandenen vmbr0 über die das Internet rein kommt noch iene vmbr1 anlegen, über die die Supernodes mit dem Backbone Server kommunizieren.

Die vmbr steht erst nach dem Neustart des Blechs zu Verfügung, daher in der Ecke oben rechts reboot auswählen.

BGP Konzentrator einrichten
---------------------------

Nachdem der Server neu gestartet ist und das Webinterface wieder erreichbar ist auf der linken Seite den Server auswählen und dann oben rechts 'Create VM'

Im Reiter 'General' eine Freie ID und einen Namen festlegen.

Im Reiter 'OS' 'Linux 4.x/3.x/2.6 Kernel auswählen.

Im Reiter 'CD/DVD' das ISO Image auswählen.

Im Reiter 'Hard Disk' als 'Bus' 'VirtIO' einstellen, die Festplattengröße auf 8GB begrenzen und als Format 'qcow2' wählen.

Im Reiter 'CPU' zwei Prozessorkerne zuweisen.

Im Reiter 'Memory' unter 'Automatically allocate memory within this range' 256 -1024MB festlegen.

Im Reiter 'Network' als Netzwerkkarte 'VirtIO' auswählen und die MAC Adresse der für diesen Vserver zu verwendenden öffentlichen IPv4 Adresse eintragen.

Bestätigen und Anlegen, anschließend starten. 

Fehlermeldungen während der Startphase werden unten im Log-Fenster angezeigt, erscheinen immer "oben", jedoch mit einigen Sekunden verzögerung. Details lassen sich ausklappen. Auf einigen Systemen ist es notwendig, die Harddisk auf "Writeback(insecure)" zu schalten, um das System zu starten zu können.

Hinweis: Wenn das System später läuft, nicht vergesse, den Starttyp "at boot time" zu stellen.

Ubuntu Server Installieren
^^^^^^^^^^^^^^^^^^^^^^^^^^

Die VM Links auswählen und oben rechts starten und die Konsole öffnen.


Deutsch als Sprache auswählen und nun Ubuntu Server Installieren

Als Installationssprache jetzt nochmal Deutsch auswählen, die auswahl trotz unvollständiger Unterstützung bestätigen und als nächstes das Tastaturlayout auswählen.

Sobald der Server versucht das Netzwerk automatisch zu konfigurieren, dies abbrechen und die Manuelle Netzwerkkonfiguration auswählen.

Die IP zur mac ist beispielsweise die 555.666.777.888

Die subnetzmaske von 255.255.255.0 bleibt in der Regel so

Die Gateway Adresse sollte man beim Rechenzentrum bekannt sein.

Bei einem großen Französichen RZ ist das IPv4 Gateway immer auf der 254, also 555.666.777.254

Als DNS geht z.B. der 8.8.8.8 von google.

Der Rechnername ist frei wählbar

Ebenso der Benutzername.

Das Kennwort sollte sicher sein und nicht bereits für einen anderen Zweck in Verwendung.

Da auf dem Server keine Persönlichen Dateien gespeichert werden sollen ist es nicht notwendig den Persönlichen Ordner zu verschlüsseln.

Zeitzone Prüfen und bestätigen.

Festpaltte manuell formatieren

Freien speicherplatz auswählen und enter

Partitionstabelle erstellen

Freien speicherplatz auswählen und enter

Partitionsgröße 7 GB Primär am Anfang

Bootflag auf 'ein' setzen und 'Anlegen beenden'

Freien Speicherplatz auswählen und enter

Einen neue Partition erstellen

Größe bestätigen

Primär

Benutzen als 'Auslagerungsspeicher (SWAP)'

'Anlegen beenden'

'Partitionierung beenden'

Ja schreiben, noch sind ja keine Daten vorhanden, die überschrieben werden könnten.

Warten...

Proxy leer lassen

Warten...

Automatische Sicherheitsaktualisierungen auswählen

Openssh server auswählen (Leertaste benutzen) und weiter

Warten...

Die Installation des GRUB Bootloader bestätigen

Weiter

SSH
^^^

Die weitere Konfiguration soll per SSH Zugriff erfolgen, daher richten wir diesen zuerst ein und sichern den SSH Server ab.

vom PC aus per SSH mit dem Server verbinden

::
	
	ssh root@555.666.777.888

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

	ssh root@555.666.777.888

Wenn der Key nicht als default im System hinterlegt ist muss zusätzlich der Pfad zum Key angeben werden.

Liegt der Key meinsshkey im Benutzerordner

::

	ssh -i ~/meinsshkey root@555.666.777.888

Nun den Password login auf dem Server deaktivieren, dazu die sshd_conf editieren

::

	nano /etc/ssh/sshd_conf

Die Zeile

::

	#PasswordAuthentication yes

ändern in

::

	PasswordAuthentication no
	UsePAM no

Achtung, auch wenn yes auskommentiert ist besteht die Möglichkeit sich per Password zu verbinden, erst wenn no gesetzt ist und nicht auskommentiert ist, ist der Zugriff nur noch per Key möglich.
Den Editor wieder verlassen und den SSH Server neu starten um die Einstellungen zu übernehmen

::

	/etc/init.d/ssh restart


Systemaktualisierung
^^^^^^^^^^^^^^^^^^^^

Als nächstes steht die Systemaktualisierung an, dafür einmal

::

	sudo apt-get update
	sudo apt-get dist-upgrade
	
Pakete installieren
^^^^^^^^^^^^^^^^^^^

::

	sudo apt-get install bird bird6 xinetd vnstat vnstati gdebi lighttpd ferm
	
* bird übernimmt das BGP routing
* bird6 tut das selbe für IPv6
* ferm hilf beim erstellen von IPtables Regeln
* vnstat monitort den Netzwerktraffic
* vnstati erzeugt daraus Grafiken
* lighttpd stellt diese zum Abruf bereit
* gdebi ermöglicht uns die Installation des Check_mk Agents
* xinetd übernimmt die Übertragung der Monitoring Daten

Nat IPv4 einrichten
^^^^^^^^^^^^^^^^^^^

Um die IP Adresse über die die Daten zum Freifunk Rheinland gehen sollen einzurichten muss folgender Abschitt in die 'interfaces' eingetragen werden.

::

	sudo nano /etc/network/interfaces
	
::

	auto tun-ffrl-uplink
	iface tun-ffrl-uplink inet static
        address 185.66.195.xx
        netmask 255.255.255.255
        pre-up ip link add $IFACE type dummy
        post-down ip link del $IFACE

Um die 'Kabelverbindung' zum Rheinland herzustellen werden GRE Tunnel für jeden Backbone Standort angelegt

::

	auto  tun-ffrl-ber-a #Startet das Interface automatisch (Namen anpassen)
	iface tun-ffrl-ber-a inet tunnel #Legt das Interface an (Namen anpassen)
        mode            gre											#modus GRE Tunnel
        netmask         255.255.255.254								#Die netzmaske bleibt immer gleich
        address         100.64.2.xxx								#Die Interne IP vom eigenen Tunnelende
        dstaddr         100.64.2.xxx								#Die interne IP vom Backbone Tunnelende
        endpoint        185.66.195.0								#Die öffentliche IPv4 vom Backbone Standort
        local          	xx.xxx.xx.xx 								#Die eigene öffentliche IPv4
        ttl             255											#Die TTL bleibt immer gleich
        mtu             1400										#Die Mtu bleibt auch gleich
        post-up ip -6 addr add 2a03:2260:0:xxx::2/64 dev $IFACE		#Die interne IPv6 vom eigenen Tunnelende
        
Aktuell gibt es zwei Standorte die je redundant ausgebaut sind:
============	==============	============
Standort		Devicename		Endpoint
============	==============	============
Berlin a		tun-ffrl-ber-a	185.66.195.0
Berlin b		tun-ffrl-ber-b	185.66.195.1
Düsseldorf a	tun-ffrl-dus-a	185.66.193.0
Düsseldorf b	tun-ffrl-dus-b	185.66.193.1
============	==============	============

Bird einrichten
^^^^^^^^^^^^^^^

::

	sudo nano /etc/bird/bird.conf

Die Bird conf für IPv4

::

	router id 185.66.195.xx;					#Hier muss die Nat IPv4 angegeben werden

	protocol direct announce {
        table master; # implizit
        import where net ~ [185.66.195.xx/32];	#Hier muss die Nat IPv4 angegeben werden
        interface "tun-ffrl-uplink";
	};

	protocol kernel {
        table master;
        device routes;
        import none;
        export filter {
			krt_prefsrc = 185.66.195.xx;		#Hier muss die Nat IPv4 angegeben werden
            accept;
        };
        kernel table 42;
	};

	protocol device {
        scan time 15;
	};

	function is_default() {
        return (net ~ [0.0.0.0/0]);
	};

	template bgp uplink {						#Das Temlate wendet wiederkehrende Werte auf die einzelnen BGP Sessions an
        local as 65xxx;							#Hier muss die eigene AS Nummer eingetragen werden
        import where is_default();
        export where proto = "announce";
	};

	protocol bgp ffrl_ber_a from uplink {		#Dieser Block muss für alle Backbone Standorte wiederholt werden
        source address 100.64.2.xxx;			#Dies ist die eigene Adresse im GRE Tunnel
        neighbor 100.64.2.xxx as 201701;		#Dies ist die Bakbone Adresse im GRE Tunnel und das AS des FFRL
	};

Die Bird conf für IPv6

::

	router id 185.66.195.xx;													#Auch bei IPv6 muss als Router ID die IPv4 Nat angegeben werden

	protocol direct announce {
        table master; # implizit
        import where net ~ [2a03:2260:120:xxx::/56];							#Das eigene (vom FFRL zugeteilte) IPv6 Netz
        interface "tun-ffrl-uplink";
	};

	protocol kernel {
        table master;
        device routes;
        import none;
        export filter {
			#  setze src addr beim route-export in kernel tabelle
			krt_prefsrc = 2a03:2260:120:xxx::1;									#Das eigene (vom FFRL zugeteilte) IPv6 Netz als Quelladresse
			accept;
        };
        kernel table 42;
	};

	protocol device {
        scan time 15;
	};

	function is_default() {
        return (net ~ [::/0]);
	};

	template bgp uplink {
        local as 65xxx;															#Die eigene AS Numemr
        import where is_default();
        export where proto = "announce";
	};

	protocol bgp ffrl_ber_a from uplink {										#Dieser Block wird je standort wiederholt
        source address 2a03:2260:0:xxx::2;										#Eigene IPv6 im GRE Tunnel
        neighbor 2a03:2260:0:xxx::1 as 201701;									#Backbone IPv6 im GRE Tunnel und AS des FFRL
	};


Ergänzungen
^^^^^^^^^^^
* sysctl ip forwarding in v4 und v6
* Einrichtung einer zweiten netzwerkkarte auf vmbr1 des proxmox
* Einrichtung einer Bridge
* Ferm mit snat für v4
* ip rules zum Päckchen schubsen

BGP Konzentrator einrichten
---------------------------

Nachdem der Server neu gestartet ist und das Webinterface wieder erreichbar ist auf der linken Seite den Server auswählen und dann oben rechts 'Create VM'

Im Reiter 'General' eine Freie ID und einen Namen festlegen.

Im Reiter 'OS' 'Linux 4.x/3.x/2.6 Kernel auswählen.

Im Reiter 'CD/DVD' das ISO Image auswählen.

Im Reiter 'Hard Disk' als 'Bus' 'VirtIO' einstellen, die Festplattengröße auf 8GB begrenzen und als Format 'qcow2' wählen.

Im Reiter 'CPU' zwei Prozessorkerne zuweisen.

Im Reiter 'Memory' unter 'Automatically allocate memory within this range' 256 -1024MB festlegen.

Im Reiter 'Network' als Netzwerkkarte 'VirtIO' auswählen und die MAC Adresse der für diesen Vserver zu verwendenden öffentlichen IPv4 Adresse eintragen.

Bestätigen und Anlegen

Ubuntu Server Installieren
^^^^^^^^^^^^^^^^^^^^^^^^^^

Die VM Links auswählen und oben rechts starten und die Konsole öffnen.


Deutsch als Sprache auswählen und nun Ubuntu Server Installieren

Als Installationssprache jetzt nochmal Deutsch auswählen, die auswahl trotz unvollständiger Unterstützung bestätigen und als nächstes das Tastaturlayout auswählen.

Sobald der Server versucht das Netzwerk automatisch zu konfigurieren, dies abbrechen und die Manuelle Netzwerkkonfiguration auswählen.

Die IP zur mac ist beispielsweise die 555.666.777.888

Die subnetzmaske von 255.255.255.0 bleibt in der Regel so

Die Gateway Adresse sollte man beim Rechenzentrum bekannt sein.

Bei einem großen Französichen RZ ist das IPv4 Gateway immer auf der 254, also 555.666.777.254

Als DNS geht z.B. der 8.8.8.8 von google.

Der Rechnername ist frei wählbar

Ebenso der Benutzername.

Das Kennwort sollte sicher sein und nicht bereits für einen anderen Zweck in Verwendung.

Da auf dem Server keine Persönlichen Dateien gespeichert werden sollen ist es nicht notwendig den Persönlichen Ordner zu verschlüsseln.

Zeitzone Prüfen und bestätigen.

Festpaltte manuell formatieren

Freien speicherplatz auswählen und enter

Partitionstabelle erstellen

Freien speicherplatz auswählen und enter

Partitionsgröße 7 GB Primär am Anfang

Bootflag auf 'ein' setzen und 'Anlegen beenden'

Freien Speicherplatz auswählen und enter

Einen neue Partition erstellen

Größe bestätigen

Primär

Benutzen als 'Auslagerungsspeicher (SWAP)'

'Anlegen beenden'

'Partitionierung beenden'

Ja schreiben, noch sind ja keine Daten vorhanden, die überschrieben werden könnten.

Warten...

Proxy leer lassen

Warten...

Automatische Sicherheitsaktualisierungen auswählen

Openssh server auswählen (Leertaste benutzen) und weiter

Warten...

Die Installation des GRUB Bootloader bestätigen

Weiter

SSH
^^^

Die weitere Konfiguration soll per SSH Zugriff erfolgen, daher richten wir diesen zuerst ein und sichern den SSH Server ab.

vom PC aus per SSH mit dem Server verbinden

::
	
	ssh root@555.666.777.888

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

	ssh root@555.666.777.888

Wenn der Key nicht als default im System hinterlegt ist muss zusätzlich der Pfad zum Key angeben werden.

Liegt der Key meinsshkey im Benutzerordner

::

	ssh -i ~/meinsshkey root@555.666.777.888

Nun den Password login auf dem Server deaktivieren, dazu die sshd_conf editieren

::

	nano /etc/ssh/sshd_conf

Die Zeile

::

	#PasswordAuthentication yes

ändern in

::

	PasswordAuthentication no
	UsePAM no

Achtung, auch wenn yes auskommentiert ist besteht die Möglichkeit sich per Password zu verbinden, erst wenn no gesetzt ist und nicht auskommentiert ist, ist der Zugriff nur noch per Key möglich.
Den Editor wieder verlassen und den SSH Server neu starten um die Einstellungen zu übernehmen

::

	/etc/init.d/ssh restart


Systemaktualisierung
^^^^^^^^^^^^^^^^^^^^

Als nächstes steht die Systemaktualisierung an, dafür einmal

::

	sudo apt-get update
	sudo apt-get dist-upgrade
