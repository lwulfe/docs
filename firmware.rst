Firmware
========


Flingern
^^^^^^^^

+----------------+-----------+-------------------+--------------------+-----------+--------------------------------------+
|TREE            |Gluon      |status             | releasename        | date      | url                                  |
+----------------+-----------+-------------------+--------------------+-----------+--------------------------------------+
|Stable          |2015.1.2   |nur Wupper Server  |20150911-stable     |2015-09-11 |http://images.ffdus.de/stable/        |
+----------------+-----------+-------------------+--------------------+-----------+--------------------------------------+
|beta            |2015.1.2   |nicht nutzen!      |20151009-beta       |2015-10-09 |http://images.ffdus.de/beta/          |
+----------------+-----------+-------------------+--------------------+-----------+--------------------------------------+
|Experimental    |2015.2pre  |MoW defekt         |2016011502-exp-ssid |2016-01-15 |http://images.ffdus.de/experimental/  |
+----------------+-----------+-------------------+--------------------+-----------+--------------------------------------+
|Broken (nightly)|2016.1pre  |untested packates  |2016020403-exp      |2015-02-04 |http://images.ffdus.de/broken/        |
+----------------+-----------+-------------------+--------------------+-----------+--------------------------------------+

*Stand 2016-02-01:* 

Vorarbeiten am Gluon Releasekanidaten herumgeschraubt, um beim offizielen Release schnellstmöglich auch eine stable bringen zu können.<br>
Ein Testkanidat von Mitte Januar hat erhebliche Probleme mit "MoW" wenn zur Bootzeit kein Ethernetlink auf LAN(!) besteht. 


Was in der Release dazukommt:

a) einen wöchentlichen Reboot (freitag morgens zwischen 3 und 5)

b) einen verbesserten Wifi-Powerfix (einige Router haben beim Neuflaschen

etwa 3dB zu wenig Sendeleistung eingestellt. Das ist ein Bug aus dem ChaosCalmer. Da werden die RegDomain-Limits leider nicht augeschöpft)

c) eine "Vorrüstung" für "Clientnetz tagsüber 'aus'" oder "Clientnetz über Nacht 'aus'".

Müssen nur zwei uci-statements abgesetzt werden, dann ist das aktiv. Inhaltlich mag ich es nicht, aber es ist für mich das kleinere Übel im Vergleich zu "gar kein Freifunk an Standort x"

d) eine "Vorrüstung" für "Bandbreiten-Limit Zeitschaltuhr für den VPN-Link", ebenfalls wahlweise tagsüber oder nachts.

(Frage in die Runde: soll ich zu c und d noch was bauen, dass man zwischen Mo-Fr & Sa-So unterschiedlich setzen kann? Irgenwann wäre dann eine Seite im Advanced-Websetup sinnvoll. Falls sich jemand berufen fühlen sollte, den Kampf mit lua-scripts aufzunehmen.)

e) den Wifineighborcheck, um hängende CPE210er (und andere) bei sonst unerkennbarem Verlust des Wifimoduls neu zu starten.

Was ich trotz diverser Versuche nicht hinbekomme und wo Petabyteboy mir aus der Patsche helfen darf ist der
"Radiochannel-Keep": Damit die einmal verstellen Frequenzen beim Update nicht wieder auf Default stehen.

(Damit die Kabelmesh-Nodes in den Unterkünften mit ihren verteilten Wlan-Kanälen nicht nach einem Update komplett händisch nachgepflegt werden müssen.)
