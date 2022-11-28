network: 192.168.50.0/24

ubuntu / admin123

sudo -s

apt install csomagnév

apt-get update --fix-missing

apt install mc

nano /etc/netplan/00-...

ip address: 192.168.50.150
gateway: 192.168.50.1
dns: 193.6.33.2

utána:

netplan apply

ping teszt:

ping index.hu

apt install mc

adduser proba   (password: proba123)

mcedit /etc/samba/smb.conf

workgroup = HELLO
security = user

lapozz a végére, print$-t kommenteld ki
(minden sorát)

[printers] - átírjuk

[valami]
comment = barmi
browseable = yes
path = /tukor
guest ok = no
read only = no
create mask = 0777
directory mask = 0777
valid users = proba

utána:

smbpasswd -a proba (password: proba123)

chown -R proba:proba /tukor

service smbd restart
service nmbd restart


nfs:

mcedit /etc/exports

/tukor		*(rw,sync,no_subtree_check)

mentés

service nfs-kernel-server restart

ls -l /

chmod -R 757 /tukor

kliens oldalon:

mount -t nfs -o nolock 192.168.50.150:/tukor /mnt

cd /mnt

mcedit teszt.txt

ls -l

cd /tukor

ls -l

proxy (squid)

mcedit /etc/squid/squid.conf

F7 - Search: http_access deny all (implicit tiltás)

elé beszúrni:

acl lista1 url_regex "/tukor/fekete1.txt"
http_access deny lista1

acl halozat src 192.168.50.0/24
http_access allow halozat

/etc/init.d/squid restart

szerkesszük meg: fekete1.txt

mcedit /tukor/fekete1.txt

\tesco\.hu
\blackfriday\.hu
\index\.hu
\facebook\.com
\magyarorszag\.hu

B variáns:

acl lista2 dstdomain "/tukor/fekete2.txt"
http_access deny lista2

acl halozat src 192.168.50.0/24
http_access allow halozat

mcedit /tukor/fekete2.txt

.tesco.hu
.blackfriday.hu
.index.hu
.facebook.com
.magyarorszag.hu

halt

letöltés: bitnami-owncloud-eredeti (kicsomagolás)

felhasználónév: bitnami / bitnami (jelszót kell változtatni)

sudo -s

ip a

ping index.hu

apt install mc

mcedit /etc/network/interfaces

# source-directory (comment)

auto enp0s3
iface enp0s3 inet static
address 192.168.50.151
netmask 255.255.255.0
gateway 192.168.50.1
dns-nameservers 193.6.33.2

mentés

/etc/init.d/networking restart   2x

ip a

ping index.hu

find / -name config.php

találatok közül: .../config/config.php

mcedit .../config/config.php

átírni: trusted domains 1-es bejegyzést

1 => 192.168.50.151

továbbiak:
-windows alatt kliens telepítés
-előtte: webes felületen adminként belépni
         (user/random jelszó)

random jelszó helye:

/home/bitnami/bitnami_credentials fájl

halt

FreeNAS telepítése

-rendszer lemez és tároló lemezek létrehozása

menüben: 1-es pont
1-es interfész
remove the current settings: no
dhcp: no
ipv4: yes
int name: em0
address: 192.168.50.152
netmask: 255.255.255.0
ipv6: no

Meghajtó csatolása Win-re:
This PC jobb klikk -> Map network drive

\\192.168.50.150\valami

proba / proba123

owncloud - felho

ifconfig

more /etc/network/interfaces

/etc/init.d/networking restart  2x

find / -name config.php

találatok közül: .../config/config.php

mcedit .../config/config.php

átírni: trusted domains 1-es bejegyzést

böngészőbe: 192.168.50.151

felhasználónév: user
jelszó: /home/bitnami/bitnami_credentials fájlban

FreeNAS:

\\192.168.50.152\eb

NFS Server Ubuntu alatt:

távolról csatlakozni így lehet:

mount -t nfs -o nolock 192.168.50.150:/tukor /mnt

ubuntu alatt ellenőrizni: van-e az other-nek írási joga

másik gépen:

cd /mnt

nano .... (írás teszt)

eredeti gépen (szerveren): ott van-e a könyvtárban a fájl

partimage