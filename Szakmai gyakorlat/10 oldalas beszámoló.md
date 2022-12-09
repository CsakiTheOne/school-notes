# 10 oldalas beszámoló

## TODO

- [x] előlap elkészítése
- [x] tartalomjegyzék elkészítése
- ábrák elhelyezése
  - [ ] FCM
  - [ ] biometrikus azonosítás és bejelentkezés
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
    - [ ] kliens
      - fontosabb használt könyvtárak
        - [ ] react-native-device-info
        - [ ] react-native-biometrics
    - [ ] szerver
      - [ ] cél
    - [ ] dokumentáció

## Piszkozat

### idealApp cross-platform alkalmazáskeret

#### kliens

A kliens alkalmazás egy webview-t tartalmaz és egy gombot, ami a bejelentkezést indítja el. Az alkalmazás forráskódja mellett található a konfigurációs fájl is, amellyel a kollégák könnyen testreszabhatják az appot a különböző projektjeikhez. Például itt adhatják meg a webview kezdő url-jét és hogy mi az API címe, amit a bejelentkezéshez kell használnia.

##### fontosabb használt könyvtárak

###### react-native-device-info

Az alkalmazásnak és a szervernek tudnia kell, hogy melyik biztonsági kulcs kié és a jövőben a felhasználók beállításait is valamihez kötni kell. Ebben segít a react-native-device-info nevű könyvtár. A segítségével a felhasználó eszközének tudjuk lekérni bizonyos adatait és azt azonosítónak használni vagy ezekből azonosítót generálni. Az utóbbira Android rendszeren van szükség, mert a Google Play áruház szabályai között megtalálható, hogy az egyedi eszköz azonosítót nem használhatjuk nagyon sok esetben.

###### react-native-biometrics

Ez a könyvtár a biometrikus azonosításért és biztonságos bejelentkezésért felelős. Nem csaj az iOS és Android eszközök szenzoraihoz nyújt hozzáférést, ezen kívül SHA256-os kulcsokat is tud generálni, amelyekkel biztonságossá tehetjük a bejelentkezés folyamatát a megfelelő szerver oldali kóddal.

#### szerver

![Bejelentkezés működése](https://github.com/SelfLender/react-native-biometrics/blob/master/assets/biometricsdiagram.png?raw=true)

[Kép forrása: https://github.com/SelfLender/react-native-biometrics](https://github.com/SelfLender/react-native-biometrics)

##### cél

#### dokumentáció
