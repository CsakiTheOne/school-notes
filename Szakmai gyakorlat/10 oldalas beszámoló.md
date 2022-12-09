# 10 oldalas beszámoló

## TODO

- [x] előlap elkészítése
- [x] tartalomjegyzék elkészítése
- ábrák elhelyezése
  - [x] FCM
  - [x] biometrikus azonosítás és bejelentkezés
- érdemi rész megírása (min. 10 oldal)
  - fejlesztéshez használt szoftverek és eszközök
    - [x] Visual Studio Code
      - [x] Fontosabb bővítmények
    - [x] Git
    - [x] GitHub
    - [x] React Native
    - [x] XAMPP
    - [x] Postman
    - [x] Xcode
    - [x] Android Studio
    - [x] Firebase
      - [x] FCM
  - fejlesztéshez használt programnyelvek
    - [x] JavaScript
    - [x] TypeScript
    - [x] Swift
    - [x] Kotlin
    - [x] PHP
  - [x] munka home office-ban
    - [x] idő követése
    - [x] fejlődés (péntekek)
    - [x] kommunikáció
  - idealApp cross-platform alkalmazáskeret
    - [x] specifikáció
    - [x] feladataim
    - [x] kliens
      - fontosabb használt könyvtárak
        - [x] react-native-device-info
        - [x] react-native-biometrics
    - [x] szerver
      - [x] cél
    - [ ] dokumentáció

## Piszkozat

### idealApp cross-platform alkalmazáskeret

#### kliens

A kliens alkalmazás egy webview-t tartalmaz, amiben megjelenik az aktuális keretbe foglalni kívánt webalkalmazás. Emellett az alkalmazásban van egy gomb is, ami a bejelentkezési folyamatot indítja el. Az alkalmazás forráskódja mellett található a konfigurációs fájl is, amellyel a kollégák könnyen testreszabhatják az appot a különböző projektjeikhez. Például itt adhatják meg a webview kezdő url-jét és hogy mi az API címe, amit a bejelentkezéshez kell használnia.

##### fontosabb használt könyvtárak

###### react-native-device-info

Az alkalmazásnak és a szervernek tudnia kell, hogy melyik biztonsági kulcs kihez tartozik és a jövőben a felhasználók beállításait is valamihez kötni kell. Ebben segít a react-native-device-info nevű könyvtár. A segítségével a felhasználó eszközének tudjuk lekérni bizonyos adatait és azt azonosítónak használni vagy néhány esetben ezekből azonosítót generálni. Az utóbbira Android rendszerű eszközökön van szükség, mert a Google Play áruház és a Huawei saját áruházának szabályai között megtalálható, hogy az egyedi eszköz azonosítót nem használhatuk nagyon sok esetben, mert ezek érfékeny információnak számítanak.

###### react-native-biometrics

Ez a könyvtár a biometrikus azonosításért és biztonságos bejelentkezésért felelős. Az iOS és Android eszközök szenzoraihoz hozzáférést nyújt, felhasználói felületet biztosít a felhasználónak a bejelentkezés során és ezeken kívül SHA256-os kulcsokat is tud generálni, amelyekkel biztonságossá tehetjük a bejelentkezés folyamatát a megfelelő szerver oldali ellenőrző logikával.

#### szerver

##### Prototípus célja

Bár a feladatom egy cross-platform mobil alkalmazás fejlesztése, egy PHP szervert is készítettem. Ez csak egy prototípus szerver, melynek két célja van: Az alkalmazás tesztelése, hogy megfelelően tud-e kommunikálni egy szerverrel és így elvégezni egy felhasználó bejelentkeztetését és prezentálás a bemutatón, ezzel segítséget nyújtva a kollégáknak, akik majd a végleges szervert készítik el.

##### A prototípus működése

![Bejelentkezés működése](https://github.com/SelfLender/react-native-biometrics/blob/master/assets/biometricsdiagram.png?raw=true)

#### dokumentáció
