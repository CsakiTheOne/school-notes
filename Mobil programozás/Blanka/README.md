# Időpont foglalós alkalmazás

[Ihlet: Pony bar](https://ponybar.hu/fooldal/szolgaltatasok/)

[Ihlet: Braid me and more](https://braidmeandmore.hu/)

## Specifikáció

Blankánál

## Technikai megoldások

- GPS a legközelebbi üzlet megkereséséhez
- Google térkép az üzletek helyéhez
- Firebase
  - Authentication (felhasználóknak opcionális)
    - kommentek és értékelések
  - Firestore database
    - üzletek és helyük
    - szolgáltatások és árak
    - időpont foglalás
    - kommentek és értékelések (az üzletektől és szolgáltatásoktól KÜLÖN)
  - Storage
    - képek a kommentekhez

### Firestore database felépítése

Valami ilyesmi

- üzletek
  - **id**
  - név
  - hely
  - szolgáltatások
    - **id**
    - név
    - ár
- időpontok
  - **id**
  - szolgáltatás
  - dátum és idő
- vélemények (komment és értékelés)
  - **id**
  - felhasználó azonosítója
  - szolgáltatás azonosítója
  - szöveg
  - értékelés (szám)

### Magyarázat

<details>
<summary>Authentication</summary>
A Firebase teljesen tudja intézni a felhasználókezelést. Tud bejelentkeztetni email jelszó kombóval, Google fiókkal, Facebook-kal, bármivel.
</details>

<details>
<summary>Firestore database</summary>
Ez egy NoSQL adatbázis. Hasonló felépítésű objektumok gyűjteményét lehet tárolni benne. Tökéletes lesz az szolgáltatások tárolásához.
</details>

<details>
<summary>Realtime database</summary>
Egy gyors kulcs-érték párokat tároló adatbázis. (Mintha egy JSON fájl lenne.) Tökéletes kisebb adatok tárolására.
</details>

<details>
<summary>Storage</summary>
Egy fájl adatbázis. Olyan mintha egy FTP szerver lenne. Teljesen jó lesz képek tárolására.
</details>

## Felmerülő kérdések

> Miért tároljuk külön az üzletet vagy szolgáltatást a kommentjeitől és értékeléseitől?

Lesznek az alkalmazásban felületek, ahol üzletek vagy szolgáltatások listája jelenik meg. Ha minden alkalommal betöltenénk ezekhez a kommenteket akkor az fölöslegesen sok netet használna. Így viszont betölthető teljesen külön minden egymástól. (Pl.: Nem töltenek be a kommentek, amíg le nem görget a felhasználó odáig.)
