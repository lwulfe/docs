Communities
===========

Fichtenfunk
-----------
Übersicht
^^^^^^^^^

Admins
^^^^^^

* JJX
* limlug
* ling

BGP-Server
^^^^^^^^^^

+-----------------+----+--------------+-------------+------+------------------+------------------+------------------+------------------+
|Name             |    |IP            |Nat IP       |GRE   |Berlin A          |Berlin B          |Düsseldorf A      |Düsseldorf B      |
+-----------------+----+--------------+-------------+------+------------------+------------------+------------------+------------------+
|                 |    |              |             |remote|100.64.4.40       |100.64.4.44       |100.64.4.42       |100.64.4.46       |
+                 +IPv4+164.132.13.113+185.66.195.54+------+------------------+------------------+------------------+------------------+
|                 |    |              |             |lokal |100.64.4.41       |100.64.4.45       |100.64.4.43       |100.64.4.47       |
+Fichtenbackbone-1+----+--------------+-------------+------+------------------+------------------+------------------+------------------+
|                 |    |              |             |remote|2a03:2260:0:21c::1|2a03:2260:0:21e::1|2a03:2260:0:21d::1|2a03:2260:0:21f::1|
+                 +IPv6+164.132.13.113+             +------+------------------+------------------+------------------+------------------+
|                 |    |              |             |lokal |2a03:2260:0:21c::2|2a03:2260:0:21e::2|2a03:2260:0:21d::2|2a03:2260:0:21f::2|
+-----------------+----+--------------+-------------+------+------------------+------------------+------------------+------------------+

Subdomänen
^^^^^^^^^^

+--------------+-------------+-------------------+----------+----------------+----------+-------------+
|Server        |IPv4         |IPv6               |br0 IPv4  |br0 IPv6        |DHCP Start|DHCP Ende    |
+--------------+-------------+-------------------+----------+----------------+----------+-------------+
|Altena-1      |51.255.115.97|2001:41d0:2:b546::2|172.16.0.1|2a03:2260:120::1|172.17.1.1|172.17.10.254|
+--------------+-------------+-------------------+----------+----------------+----------+-------------+
|Iserlohn-1    |51.255.115.97|2001:41d0:2:b546::2|172.16.0.1|2a03:2260:120::1|172.16.1.1|172.16.10.254|
+--------------+-------------+-------------------+----------+----------------+----------+-------------+
|Meinerzhagen-1|51.255.115.97|2001:41d0:2:b546::2|172.16.0.1|2a03:2260:120::1|172.18.1.1|172.18.10.254|
+--------------+-------------+-------------------+----------+----------------+----------+-------------+

Neanderfunk
-----------

Düsseldorf-Flingern
-------------------

Übersicht
^^^^^^^^^

Admins
^^^^^^

* Trickster (Silas)
* Petabyteboy (Milan)
* Adorfer (Andreas)



Infrastruktur
=============

gemietete Hosts
^^^^^^^^^^^^^^^

name	owner	hoster	loc	typ			os	IPv4 (base) 	ipv4 (pool) 		IPv6
dags1	Silas	OVH	RBX6	M-4C8T-32G-2x2T-500M	PM4	51.254.47.239	5.196.175.52-55 	51.255.150.68-71 2001:41d0:1008:07ef::/64
paz	Sabine	SYS	RBX4	M-4C8T-32G-2x2T-250M	PM4	46.105.121.209	51.255.233.208-215 	2001:41d0:2:e8d1::/64
vpn	Andreas NC		V-2C-6G-112G-100M	arch	37.120.171.253	2a03:4000:6:5100::/64	52:54:bb:f0:15:12
ffgek0	Andreas NC		V-1C-2G-40G-100M	arch	46.38.238.147	2a03:4000:2:83::/64	52:54:27:00:19:46
ffdus0	Andreas NC		V-1C-2G-30G-100M	arch	46.38.234.225	2a03:4000:2:bb::/64  	96:6d:cc:64:88:af
pbbpg	Andreas	NC		V-2C-6G-230G-100M	arch	 5.45.96.247	2a03:4000:5:11e::/64	ea:83:a2:c2:e5:f8


Virtuelle Hosts
^^^^^^^^^^^^^^^
fqdn				host	os	RAM	HDD 	mac			ipv4
map.eulenfunk.de		dags1	arch			02:00:00:d6:a0:10 	51.255.150.71
map2.eulenfunk.de 0		paz	arch 			02:00:00:06:2c:d0 	51.255.233.214
flingern-3.ffdus.de 		paz	lts14.2			02:00:00:58:04:81 	51.255.233.215
iserlohn-2.freifunk-mk.de	dags1	lts14.2			02:00:00:69:ee:4b	5.196.175.52
flingern-1.ffdus.de		dags1	lts14.2			02:00:00:a1:81:5f	51.255.150.68
neander-2.ffnef.de		dags1				02:00:00:77:fe:8b	51.255.150.69
service.ffdus.de		dags1	ipfire			02:00:00:d6:2e:36	51.255.150.70
horst.ffdus			LES	arch	33G	500G	36:e2:87:5e:a4:87	10.155.6.112



Public Keys (persons)
=====================

ssh
---
user    key
pandur	ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAIEAmLQ1QW341TIu6csTplCM1xAKpU8uRLCbcDcQb3P2coBj993PMYhmTwVV7vlo2pihToAXSg5DRf1trPG9vt+h87xLvrAzYflBat8rKIEkFLLN2NfkC4FH+40dfwBxA3PGihKYFv9bB1H+8XYZHIx0A7m2YUg1gK5uesW59+GmwyE= Pandur
sunta	ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC3SPq75cC/tZJ9sWKHXIs1XOuzwc1oIOHzn2TrfpNab5AOZDZ1bXnbn7f5HMMlHLkpPrJLqj2FQ5Qaosd3OLnsFre5JzJJyycUfXy/TnWMEQzls7wsWxSSS7xWSjqrnDMibY/kP4/i6B+3+gaYXOywxCAMFqXWlhcQxGG2ELBcWosySC1YYF2JB6fEdo/N3tAGz05d5T7w4gQUyAtcqdZTTqJtlynEIXDixh/VH513/NnFl1y1kORh0kAEXNUTpEbkJg4K+sHJYMm6k96L57jGjIKTr1W3VyNdjBLAaHCvzc6eh39vrylOV+B3h760RRCkzHpy0Vp7KpJ4oSNJDv6X cw@bianca
mathias	ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDBgeaL3Fap41iwHYPG/7khPINzeknkdvtoPWXJJrhTyUGwA/3RbRYleKVzmaOzKhhSe5zp7us2YE2bMgTm845RWghRGlCMS+RM8/A81HnylytEicNhANQlzESwRUxaucYLn3C7CRWWFoy3Ej96d091twUozpIvSJVXEw2agb1ljlf2vxiScLKXws5wenKaYaO5ZjCN0aT2YzbuYIrm9QmayOZvcl7BmVtLnXh8NqwiloKnQIVa3UHikRxmRjfQ8MDewoj7fU7Cw+vDDc7MnQC/3/+i6c+HNKDYNsJxcp4NrhVjTyasgDZHZbyY3XMVKlIvNMum8Yc6hrRFQBXwQWjH mathias
lingling	ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCzSsGrVSdBhrQb94S2fqtUUbwi3aYJnRAGcu2CTiVCNoSlEKYbjXK0ApbHIzVSR+InK9SJLLnblPb88TaVqrhGt9PA+oWzISjhvDFrbyAA6EbAbusGb8VVy2LiYlqaTV1nKqq0jAVJxzxY0u4QfAkSGCyyaJe+jWu1Fa9uKSiDq/PphIVmx4dXetRoqwkPsKMMlfLul3GKKsVBZ70ZqmBTMp+naGEBdIZLomLridRqUO5VwaJ8LbtZWT8IAKe/B4znKflpUOnGtj+OalPF2EqgHFJ9jA3mTzAQDwGKlrfgMd2SyK19n9S2FoOBLIeQ/fyX9rzT5O9KIAy5AcbPpfTfAA0hL7cB4Kgb2eUA5nS9ikjG3rrkVQXXNJVLXAmKMXwFqy0Db1ZA0ai8eiqSBqV0lmh89UZT/gdZLWVeKgw+O3gyDEjm/TbTYNJDkIHhL4qBvGHU5EwVniGLVTzp5V76Bnb6ditu7EH27mC6N71jfFE6K2Ay2dToy+M4NXosvTEVzB1ugZ/il2Yspvv07JvzPRiCG8kU2LcWm7a3GpaQ8N0oL1pqdN2emtRyIXew2mKZduaczraOEgOrdtjhHG32/YwAeocn6uGHDqR3d/lPgMB4hoEU0ySTuDqKvQMvub3juOsVpNYBnLGPYEXGyDwXT8dpk6UCcS2VOgrobKj9dQ== ling@ling
pbb	ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDGwGwwqw9qSoEq8L+r7U+FRkGN30iBBA2ohc+fnJK7qSCJ3T9bWJzUXMobWPTkjZtDGmBZ/wXmxFxH0mgpG4gGoxOThyIbDF2hkz0TPId1FPugtua7DYmaSc7c7SekA4PyeGuGT4/g9eayGJ5wjHhic5FlxY9WXt/qL2KWwvmsTZRRPTTjdsi9Rcbyq39Fom6DAam8R+3FSg7GVdEmlDOB2annTxOsqP3BHX+wfg2cZP76OCkU2Uk5XCYwAXSipomFmiVBh+3/EVnUNEEeJQHwqamtZzbOd0PII/Ten9GR3co1NlG9r1tUop0/uzzAu/YNVjaaE4V51D+0FJpIYC3K+uUKFZ3KBpfU/tYqKa+cg88KmMOVZltQmMHKtZ/5lTmKsZeCQfqBl33wYJJZrpCJxlQyNKTlHTzE25EtA7snmOYqdQmSf5Q4Szib8DFq7zE5cZhBxXtFv9MYNVAggnNo80EJLotLUT+dVvvjqeO+knfPCAPRjk74u9TOMrw+PZ7xDThuqjfrK+qldZWsI7r1SOkUt8IER0OVHtd/JiPG99E3PKbwDw2cWk7+QWHEnjHtUnyTkQvibIA7SvD/hGG2Zz1R+XAPmCa4qpIHNAjVY6OWX9w65nwkwTzoraj73k2VWfeAzMa4HWjfgZ05OPC0xcsCGZm342qh1e4jieeKUQ== petabyteboy@pbb-e3
adorfer	ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAIEAufGE6eK/iZTeLKCduy4UEyQpkXX+Z/0SAbYCbkJhJjNpYJaAaMhPI9yPWqsSJlQ9NSMVHMWF+3fTYb8uXEMFxEAXLqgYWhc7fs45FwvP7Ki9q5vZlvrKdB0MOPkQsY1sI3AEtcFwoft0uemW9QZUJ9jxBSi82BDbSZnFykv81ds= adorfer
benedict	ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC9o5jgZqeWNYM7hpoEnbsCEbKI2NDqIXlUKk6Ty8ftXsvY2MUy9cAklW12D4qom+88NLZQmSwPVkm90aPsVpWHJAltNurMTHRHagWq/EqC/MnudoI8MOCDy6L/6cAE720tz32b9ZXWYNsC44EJRtUbKKO7yc5OgTKIsP3n3UaB5p0pc6oHH9HGHJwvjq1f455BfVaCvKTNaa+hVm0yX2RQkMAmhFPT3SFvLSqkO/91hM0wAY6qG4BXPinuv9jYGAAlio60YKPqEXh41LjBIWkE+OhUqfGWO8ww00sxPx3HKCDozneC6Q+Ono0h2WiJ2eVvNYQsnxox1/0NXNKVH9zL benedikt@kampo
julian	ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC+/qANS2vRvc8w7d2v6avmzE0LvzEzQrcjNAKDeo490g3GbnnsuS8Z4K83CNUiQGRYOuAFzaoLvBqWqaLgasuxjxLm0XzZ/APevvQnVOksLMAFUMPpm5ZIUvquJIezzIjAXyvH1gws14Fs652hfN7OFH6p/TkMFwyFE6CK2rkA5hso4rxwQLcxCAhIgY5DktfyQKFQg//Vd0ywbmHyWuiOz3vhZ39F2yJNU2xaKeFiImePHzOGeYjwRlxHMk9qNDl6U+a6XafIDt4IeCq1oVNEKhManKVJuH1ExUnMQNrcUPBGW9KZojpYXVPckvIRxe0Elz4bbxQRL3gF5okpPk8F x@x
plaste	ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCvMCy/RjnGc/ppzxIqvyv3WnaQ3Tj495MLw8qV4FpTkVndjIuqrY7heW4G1W4AFV97QpwCnBTOVmL6xg8kS+zPWN8/pFbIWF1tDBBocZuIYQhOzyd4KPewgu/GXPhmDTtAqdU/MC1CL9Zmd5P+YTzTTVYvvJmLx8ZNWx1KVU9BTePF1y6ekhLduvzOfGDW4rhPhjGGeEIW15sLpM/JnlLMP0nZvbmTQQH91g3qKsabxmYPH6W/s+rTja2ds+SfrNzj4VrRRNUaNFaUo/2G/m5lr/yYTgF2bDb1D7MijMs/u0Z6cdvlOXzdESII8jgVsa942KdEiskak0cRFEDLhf7Qomjamf/fGfQyrhQeH+XBDVlPbumN5LrHpO68U9kbpRpPxX/IRlsjKG6fYj5LIOQqpfWBqvlCuAFacUcp8EglQVKlB5yuSpEcwhH4vb03z+hLQndmGkzlp2yqcM/+sDpIzeQHK58MyLXXIiNJW7cUoExqmaGSrvXl1duncpBNVEgBfCYaWA9PwnTxWOf5Ywl2Zei5W9p5G8vJSSaEV+SyxrCUl2MGbAQob01KrsgSRQ5lK1Uhjzq62ewVmUWvfu+1dy/NKwTNLofd957pd4f0BpB0wRd4c5EQDtyHyKjGT27EdzoukUdlELWBCXvt7i/W0MBco/spgL+05YqDrJJNbw== plaste@stephan-plarre.de
Wurstbrot	ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAnrO+trdNZO5/S4tBRXgWJGKljz4DMB9YODxqm7HiHZZC2RuMZaAo5cemFN546+Pe4lGjw/BNCQ61qT6KndRreEErzJ+f9QqRG2tF1Anq88jSPcgOQwHYw85daXf6AjV3OCvWhQbWkVoYTlCuPaP6prNWomvkdwi2AGcOSHvYVzfK4pL2OFVncmS2DKhF6Fe7qxaI4i9cPxojhmWrTbIoZc1hSmYzpOz3rtmI2NAVzXGFFcKcl+yXVSbbhJR/ENN40QAcHG61FHT9No+Xw5/jSzHup6mdmSl48oNyff3JRqNYMDKfCEfITMJan6zW3v5sfzSCZEG1AapqowM/RaKAQ== wurstbrot
plaste	ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCvMCy/RjnGc/ppzxIqvyv3WnaQ3Tj495MLw8qV4FpTkVndjIuqrY7heW4G1W4AFV97QpwCnBTOVmL6xg8kS+zPWN8/pFbIWF1tDBBocZuIYQhOzyd4KPewgu/GXPhmDTtAqdU/MC1CL9Zmd5P+YTzTTVYvvJmLx8ZNWx1KVU9BTePF1y6ekhLduvzOfGDW4rhPhjGGeEIW15sLpM/JnlLMP0nZvbmTQQH91g3qKsabxmYPH6W/s+rTja2ds+SfrNzj4VrRRNUaNFaUo/2G/m5lr/yYTgF2bDb1D7MijMs/u0Z6cdvlOXzdESII8jgVsa942KdEiskak0cRFEDLhf7Qomjamf/fGfQyrhQeH+XBDVlPbumN5LrHpO68U9kbpRpPxX/IRlsjKG6fYj5LIOQqpfWBqvlCuAFacUcp8EglQVKlB5yuSpEcwhH4vb03z+hLQndmGkzlp2yqcM/+sDpIzeQHK58MyLXXIiNJW7cUoExqmaGSrvXl1duncpBNVEgBfCYaWA9PwnTxWOf5Ywl2Zei5W9p5G8vJSSaEV+SyxrCUl2MGbAQob01KrsgSRQ5lK1Uhjzq62ewVmUWvfu+1dy/NKwTNLofd957pd4f0BpB0wRd4c5EQDtyHyKjGT27EdzoukUdlELWBCXvt7i/W0MBco/spgL+05YqDrJJNbw== plaste@stephan-plarre.de
faithinchaos	ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAj/IcUJ8h4RrgEwrBc0QIYs53pS5sdQnAC9b+7Q31h0EIL3PwKj3eWs2fQpXDAyP7pHCd87++KBBDqVidlQBpW3oPB/WXIgTAMtJ5VnSVeiBK1LCyJ8PXRq/FEtBNfDh7MvBqsIaXeXFhC5rpYGyNmckYvS2QgtIFkltg0ZoH7k4TGsfaVayOlQQYB3YJvhZdsHWfBdkt/1MqjH3Iz4D9ahS3H4rwqAZRg4zK3lPsSw/TxV64XdfXA4jnZVnrlB2pfHtAdm/oIUDctWou9dGOtw2eBRH+Br3aCeMoKtN2epzgNfcqjXiParh/gT3t0AHmF/yMWcByy682n23M1oggJQ== faithinchaos
robot	ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDQjdRIoLwaN3DdV7jusUDlLfUK4etdS6zhBdpJb5vFxtT8/sb6+iIvQzrvstnssBgpaMr2mz9VSXXQlkXZsGokSYg+Z859ut11Z288VQ5lP4V59QLG6IUGNYbO1QdeTq+K2Gk8E4vwLrJrtEXt+5iih189joMJ8fOy5kfsoh2VNNmKiyUmObZG6ZIxKT0P2nkLcEgMdfDZHFXBewQPyZXjicCRob332NiCElWgb+9jwEzZajlvDiBNFDjjI7wRW30ngLGy07oDCjB1b+0tiKuV68nuQ7SiWN3LAOa64KoRcrLRVASPgaXtroB+rGRP3/D9nUgur0uCLwyeaBZgI+IB ffdusrobot


firmware-pubkeys
----------------
'19a02dd7b50ffc2b59e2cd1f9e76b26b46e33c43ebf641554572e4a677af35cc', -- SenorCafe
'2aa020a8860e5c3f638ed77d313148c7e7c5899be4bebf2cb3406875ef03e835', -- Goldwaage
'fb919d4adc69bd404f5093ce6b43badf351f9e642ad458406be986baf6096247', -- PetaByteBoy
'2a61930930a240c027f6ca4197203d400b6e4a32f9e92041e5f086907796c9bc', -- adorfer
'd02f8e60fb7a5069556500694ebe512b6017b01e9950476e4cfcf10d5130c296', -- JJX
'7afe187ceb34e83b2cb33c244ab5c8a7e80829c3e83b8d3fc471d2642eb6a602', -- limlug
'610e9acf4d550c3a272b88ec5b4cf0a0e382be203f98b860181fb1bcb1641abd', -- mathias
'01aff79cb3079b5b343cdc099a342434f284329890230e0f23850a488570b8c2', -- AKA47

