# Felkészülés ZH-ra

## Teendők

- [ ] tananyag videók megnézése (16/25)
- [ ] zh fájlok előkészítése
  - [x] letöltés
  - [ ] importálás VirtualBox-ba
  - [ ] kipróbálás
- [ ] puska pendrive előkészítése
  - [x] videók
  - [x] megmentő.txt
  - [x] zh fájlok
  - [ ] linkek hasznos weboldalakra

## Videók

- [x] cloud (2)
- [x] password (2)
- [x] virtualizacio
- [x] virtualbox (4)
- [x] freenas (3)
- [ ] ubuntu (2/7)
- [ ] sysresccd (1/3)
- [ ] cms (1/3)

## Jegyzetek

### Ubuntu

#### Telepítés

enp0s3 > Edit IPv4 > Manual

```
Subnet:       192.168.1.0/24
Address:      192.168.1.150
Gateway:      192.168.1.1
Name servers: 193.6.33.2
```

(X) Custom storage layout

1. lemez
   1. `1G /boot`
   2. `1G Format: swap`
   3. maradék `/`
2. Create software RAID (md)
   1. RAID Level: 1 (mirrored)
   2. mindkét maradék lemezt kijelöljük
   3. md0: összes hely `/tukor`

Név, jelszó, stb. megadása, nem kell semmi, mehet a telepítés aztán reboot kísérlet és bezárás ha nem megy.

#### Konfigurálás

```
sudo -s
apt install net-tools
cd /etc/netplan
nano <fájl 00 kezdetű névvel>
// fájlban 1 sort, a címet kell átírni: 192.168.1.151-re
// mentés és kilépés
netplan apply
apt install openssh-server samba squid3 nfs-common nfs-kernel-server
apt-get update --fix-missing
apt install openssh-server samba squid3 nfs-common nfs-kernel-server
```

Leállítás: `halt` vagy `shutdown now`

// innen nem tudtam tovább írni

### cloud_2.mp4

Owncloud fájlszerver létrehozása

```
sudo -s
mcedit /etc/network/interfaces
```

`/etc/network/interfaces` fájl tartalma:

```
auto enp0s3
iface enp0s3 inet static
    address 192.168.1.152
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 192.6.33.2
```

```
ifdown enp0s3
ifup enp0s3
/etc/init.d/networking stop
/etc/init.d/networking start
```

ping-nek itt működnie kell

```
mcedit /opt/bitnami/apps/owncloud/htdocs/config/config.php
```

A szerkesztett fájlban a `trusted_domains` kulcs értékét szerkesztjük át, hogy tartalmazza a mi általunk megadott címet.

```php
$CONFIG = array (
    'trusted_domains' =>
    array (
        0 => '127.0.0.1',
        1 => '192.168.1.152',
    ).
)
```

```
cd /home/bitnami
mcedit bitnami_credentials
```

A megnyitott fájlban találhatók a hitelesítő adatok a bejelentkezéshez. Windows alatt megpróübálhatunk csatlakozni a szerver IP címével és belépni. Felhasználók kezelése és kliensprogram telepítése már grafikus varázsolás.

### Windows jelszó kiiktatás

[Hiren's BootCD](https://www.hirensbootcd.org/)

Jelszó kiiktató eszköz elérési útja: `(...)/Desktop/Utilitie/Security/Passwords/NT Password Edit`

### SystemRescueCd

[SystemRescueCd](https://www.system-rescue-cd.org/)

### FreeNAS

#### Telepítés

- FreeBSD alapú rendszer
- plusz AHCI vezérlő kell, hogy több merevlemezt tudjunk csatlakoztatni

1. Install/Upgrade
2. Yes
3. ada0
4. root-nak jelszó adás
5. Boot via BIOS
6. Reboot System

Konfigurálás:

1. <kbd>1</kbd> Configure Network Interfaces
2. <kbd>n</kbd>
3. <kbd>n</kbd>
4. <kbd>y</kbd>
5. `192.168.1.154`
6. `255.255.255.0`
7. <kbd>n</kbd>

Távoli beállítás tárhely szolgáltatásra:

Windows rendszer alól a FreeNAS IP címével elérhető a config felület. Belépési adatok a telepítésnél megadott jelszó + `root`.

1. Storage > Pools > Add
2. Create Pool
3. Name: `raid`, ada1-ada4 kiválaszt, `Raid-z`
4. Create
5. Add Dataset
6. Name: `megosztas`, Save
7. Accounts > Users > Add
8. Kötelező mezőket kitölteni `user`
9. Microsoft Account opciót bepipálni
10. Storage > Pools > `megosztas` Edit Permissions
11. `user` lesz a tulaj és neki, csoportjának minden joga lesz
12. Apply Permissions Recursively, Save
13. Services
14. SMB protokolt bekapcsolni majd Configure
15. File- és Directory Mask: `0765`, Save
16. Sharing > Windows Shares (SMB) > Add
17. `/mnt/raid/megosztas`
18. Advanced Mode
    - Enabled
    - Browsable to Network Clients
    - Export Recycle Bin
    - Show Hidden Files
19. Save > Configure Now > Cancel

Csatlakozás:

1. Ez a gép-re jobb klikk
2. Hálózati meghajtó csatlakoztatása...
3. `\\192.168.1.154\megosztas`
4. Csatlakozás különböző hitelesítő adatokkal
5. Befejezés
6. `user` és megadott jelszó
