# Irku prezentáció

- [Irku prezentáció](#irku-prezentáció)
  - [Gyakorlati bemutató Ubuntu alatt](#gyakorlati-bemutató-ubuntu-alatt)
    - [Telepítés](#telepítés)
      - [NFS](#nfs)
        - [NFS Szerver](#nfs-szerver)
        - [NFS Kliens](#nfs-kliens)
      - [FTP](#ftp)
        - [FTP Szerver](#ftp-szerver)
        - [FTP Kliens](#ftp-kliens)
      - [SAMBA](#samba)
        - [SAMBA Szerver](#samba-szerver)
        - [SAMBA Kliens](#samba-kliens)

Téma:

Fájlkiszolgálók a hálózatban, nyílt forrású megoldások (az NFS az FTP és a SAMBA használata gyakorlati eszközökkel szemléltetve)

## Gyakorlati bemutató Ubuntu alatt

### Telepítés

#### NFS

##### NFS Szerver

```
sudo apt install nfs-kernel-server
# mappa létrehozása megosztáshoz
sudo chown -R nobody:nogroup mappa
sudo chmod 775 mappa
```

`/etc/exports` fájlba:

```
/home/csaki/Asztal/nfs-shared *(rw,sync,no_subtree_check)
```

```
sudo exportfs -a
sudo systemctl restart nfs-kernel-server
```

##### NFS Kliens

```
sudo apt install nfs-common
sudo mount szerver-címe:mappa cél-mappa
```

#### FTP

##### FTP Szerver

```
sudo apt install vsftpd
# config állítgatás /etc/vsftpd.conf fájlban
sudo systemctl restart vsftpd.service
```

##### FTP Kliens

Nautilus fájlkezelőbe: `ftp://localhost`

#### SAMBA

##### SAMBA Szerver

```
sudo apt install samba
# mappa létrehozása samba-nak
```

`/etc/samba/smb.conf` tartalma:

```
[smbshare]
    path = /home/csaki/Asztal/samba-shared
    read only = no
    browsable = yes
```

```
sudo smbpasswd -a felhasználónév
sudo service smbd restart
```

##### SAMBA Kliens

Nautilus fájlkezelőbe: `smb://localhost/smbshare`
