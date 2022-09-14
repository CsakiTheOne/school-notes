# Időpont foglalós alkalmazás

- [Időpont foglalós alkalmazás](#időpont-foglalós-alkalmazás)
  - [Ihletek](#ihletek)
  - [Specifikáció](#specifikáció)
  - [Technikai megoldások](#technikai-megoldások)
    - [Firestore database felépítése](#firestore-database-felépítése)
    - [Tech magyarázat](#tech-magyarázat)
  - [Felmerülő kérdések](#felmerülő-kérdések)
  - [Java vagy Kotlin?](#java-vagy-kotlin)
    - [Java - az ismerős](#java---az-ismerős)
    - [Kotlin - a modern](#kotlin---a-modern)
    - [Egyéb megjegyzések](#egyéb-megjegyzések)
  - [Hogy kapcsoljuk a felületet logikához?](#hogy-kapcsoljuk-a-felületet-logikához)
  - [Android stuff](#android-stuff)

## Ihletek

[Pony bar](https://ponybar.hu/fooldal/szolgaltatasok/)

[Braid me and more](https://braidmeandmore.hu/)

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
- felhasználók
  - **id**
  - név (ha email jelszó kombós módon jelentkeztek be)

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

<details>
<summary>Miért kéne külön tárolni az üzletet vagy szolgáltatást a kommentjeitől és értékeléseitől?</summary>
Lesznek az alkalmazásban felületek, ahol üzletek vagy szolgáltatások listája jelenik meg. Ha minden alkalommal betöltenénk ezekhez a kommenteket akkor az fölöslegesen sok netet használna. Így viszont betölthető teljesen külön minden egymástól. (Pl.: Nem töltenek be a kommentek, amíg le nem görget a felhasználó odáig.)
</details>

<details>
<summary>Mivel jelentkezzenek be a felhasználók?</summary>
A Firebase sokmindenben tud segíteni. A legegyszerűbb az email jelszó kombós megoldás és a Google fiókos bejelentkezés sem vészes. Viszont nem akar mindenki kommentelni, adhatunk lehetőséget a bejelentkezés kihagyására. Van is lehetőség anonim bejelentkezésre. Várjunk, az minek? Nem elég simán kihagyni. A jogosultságok miatt és az adatbázis biztonsága érdekében ajánlott használni ezt.
</details>

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
- több tartalom a neten (de ez nem nagy előny, mert ha Java kódot másolsz Kotlin fájlba akkor az Android Studio (és még pár program is) automatikusan átírja Kotlinra)

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
- (Csáki boldog :D)

Hátrányok

- ismeretlen, még nem találkoztunk vele iskolában
- szintaxis különbségeg: sok esetben hasonlít a TypeScript-re és nincsenek pontos vesszők (az talán előny)

### Egyéb megjegyzések

- több előnyt írtam Kotlinhoz... komolyan? manipuláció? NEM, tényleg ennyi jutott eszembe és szeretném, hogy ez a ti döntésetek legyen és **teljesen számíthattok rám** akkor is ha a Javát választjátok. ezeket csak azért írtam, hogy átláthatóbb legyen a két lehetőség
- mindkét nyelvet jól ismeri az internet és a fiatal Kotlinhoz is már rengeteg stackoverflow válasz érkezett
- a hivatalos Android és Firebase dokumentációkban mindkét nyelvre vannak példa kódok
- a Java régebb óta jelen van ezért lehet, hogy csak ebben a nyelvben találunk megoldást... de ez nem baj! másolás, beleillesztés a kt fájlba és az Android Studio átírja magától a Java kódot Kotlinra
- mindkét nyelv tud hivatkozni a másikra: Java-ban meg lehet hívni Kotlin függvényeket és Kotlinban lehet használni Java osztályokat
- mindkettő bytecodera fordul, tehát az újabb nyelv NEM egy plusz réteg, hanem egy lehetőség
- az Android Studio a C++-t is támogatja szóval 3 lehetőség van, de szerintem abban nem akartok dolgozni xd

## Hogy kapcsoljuk a felületet logikához?

- XML
  - hagyománys módszer: hasonlít a JavaScriptes `document.getElementById()`-hoz
  - **Kotlin extension: egyszerű, könnyen olvasható, de nem ajánlott, mert sok hibalehetőség van benne ha figyelmetlen az ember**
  - **viewBinding: ajánlott módszer, kevesebb hibalehetőség, de kissé macerás a setup**
- Jetpack Compose: brutál menő, nagyon modern, de még nagyon kiforratlan és nagyon más gondolkodást igényel

Amit vastaggal jelöltem, azokat tartom olyannak, hogy nektek jó lehet, de felsoroltam minden lehetőséget, hátha...

## Android stuff

- [Design nyelv, amit használni fogunk](https://m3.material.io/)
