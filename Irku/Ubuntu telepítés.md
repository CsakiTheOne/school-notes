# Ubuntu telepítés

## Telepítő

1. Nem kell frissítés
2. DHCP nem kell, statikusan beállítjuk. Home hálózathoz megfelelő beállítások:

    ```
    Subnet:           192.168.1.0/24
    Address:          192.168.1.100
    Gateway:          192.168.1.1
    Name servers:
    - Kari hálózat: 193.6.33.2
    - Mobilnet:     8.8.8.8 (Google DNS)
    ```

3. Custom storage layout
   1. Create software RAID
   2. RAID Level: 1 (mirror)
   3. A kész eszközön GPT partíció: teljes méret, ext4, mount: `/tukor`
   4. Maradék 1 eszköz felosztása: 1GB /boot, 1-2GB SWAP, maradék /
4. Minden név `Ubuntu` és jelszó `admin123`
5. Nem kell semmi plusz csomag, mehet a telepítés
6. Telepítés után gép leállítása és a tárolók átvariálása valahogy

## Konfigurálás
