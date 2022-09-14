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

### Tech magyarázat

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

## Java vagy Kotlin?

### Java - az ismerős

```java
String text = "Hello, World";
System.out.println(text);

List<String> list = Arrays.asList("foo", "bar");
System.out.println(String.join(", ", list));

int min = 3;
int max = 24;
int random = (int)Math.floor(Math.random()*(max-min+1)+min);
```

Előnyök

- ismerős: ezt már tanultuk
- tanár jobban ismeri, jobban tud segíteni

Hátrányok

- rengeteg boilerplate: többet kell írni, hogy ugyanazt csinálja
- "elavult"? (ma is használják, de hiányoznak modern nyelv funkciók)

### Kotlin - a modern

```kotlin
val text = "Hello, World"
println(text)

val list = listOf("foo", "bar")
println(list.joinToString())

val random = (3..24).random()
```

Előnyök

- átlátható, egyszerű, könnyen olvasható
- modern nyelv funkciók, mint például adat osztályok, extension függvények
- null biztonság: futtatás előtt szól ha valahol null refrence exception lehet
- Csáki boldog :D

Hátrányok

- ismeretlen, még nem találkoztunk vele iskolában
- szintaxis különbségeg: sok esetben hasonlít a TypeScript-re és nincsenek pontos vesszők (az talán előny)

### Egyéb megjegyzések

- mindkét nyelvet jól ismeri az internet és a fiatal Kotlinhoz is már rengeteg stackoverflow válasz érkezett
- a hivatalos Android és Firebase dokumentációkban mindkét nyelvre vannak példa kódok
- a Java régebb óta jelen van ezért lehet, hogy csak ebben a nyelvben találunk megoldást... de ez nem baj! másolás, beleillesztés a kt fájlba és az Android Studio átírja magától a Java kódot Kotlinra
- mindkét nyelv tud hivatkozni a másikra: Java-ban meg lehet hívni Kotlin függvényeket és Kotlinban lehet használni Java osztályokat
- mindkettő bytecodera fordul, tehát az újabb nyelv NEM egy plusz réteg, hanem egy lehetőség
