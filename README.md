# ESPHome Cloud Builder 
## Kompiluj w chmurze dla dowolnej wersji wydania, dzięki platformie ONA
https://ona.com/stories/gitpod-is-now-ona


To repozytorium udostępnia możliwość łatwego uruchomienia **ESPHome Dashboard działający w przeglądarce**, dzięki **Ona (dawniej Gitpod).**

**Możesz wybrać konkretną wersją wydania ESPHome edytując plik docker-compose.yml.**

**Możesz konwersować z Agentem AI, który zmieni to za Ciebie w locie.**

Celem jest zapewnienie **łatwych, powtarzalnych i stabilnych kompilacji firmware**, niezależnych od aktualnego wydania ESPHome oraz sprzętu, który już Cię nie ograniczy.

---

## 🤔 Co to jest platforma Ona (dawniej Gitpod)?

**Platforma Ona Gitpod to taki komputer w chmurze, którego obsługa działa w przeglądarce. Ale to też dużo więcej, to całe środowisko programistyczne ze wsparciem AI.**

Wyobraź sobie, że:
- Klikasz link w przeglądarce
- Dostajesz gotowy do użycia komputer z zainstalowanym ESPHome Device Builder
- Kompilujesz firmware bez instalowania czegokolwiek na swoim komputerze
- Wszystko działa w przeglądarce (Chrome, Firefox, Edge) 

**Nie musisz:**
- ❌ Instalować ESPHome na swoim komputerze
- ❌ Posiadać instancji Home Assistant
- ❌ Instalować Pythona, Docker, czy innych narzędzi
- ❌ Martwić się o system operacyjny (działa na Windows, Mac, Linux, ChromeOS)
- ❌ Mieć mocnego komputera (kompilacja odbywa się w chmurze)

**Wystarczy:**
- ✅ Przeglądarka internetowa
- ✅ Darmowe konto na Gitpod (logowanie przez GitHub/GitLab/Bitbucket)
- ✅ Połączenie z internetem

To jak mieć **tymczasowy komputer do wynajęcia za darmo**, który znika po zakończeniu pracy.

---

## 🚀 Jak to działa

- ESPHome uruchamiany jest wewnątrz oficjalnego kontenera Docker
- Obraz kontenera jest przypięty do **konkretnej wersji ESPHome**
- ONA/Gitpod automatycznie uruchamia kontener z przypisanym portem 6052
- ESPHome Dashboard jest dostępny w przeglądarce internetowej 
- Firmware kompilowany jest **w całości w chmurze**

Nie jest wymagana żadna lokalna instalacja ESPHome, wystarczy dostęp do internetu.

---

## 📖 Jak używać

### 1. Uruchom środowisko w Ona/Gitpod

Kliknij poniższy przycisk lub otwórz link w przeglądarce:

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/Cezar8421/esphome-gitpod)

**Lub użyj linku bezpośrednio:**
```
https://gitpod.io/#https://github.com/Cezar8421/esphome-gitpod
```

### 2. Poczekaj na uruchomienie

Gitpod automatycznie:
- Pobierze obraz Docker z ESPHome
- Uruchomi kontener
- Pozwoli na otwarcie strony z ESPHome Dashboard w przeglądarce pod wskazanym portem

#### 3. Dodaj posiadane już pliki YAML do katalogu `esphome/`.

Lub

Utwórz nowy plik w katalogu `esphome/`, np. `esphome/moj-esp32.yaml`:

```yaml
esphome:
  name: moj-esp32
  platform: ESP32
  board: esp32dev

wifi:
  ssid: "MojaWiFi"
  password: "mojehaslo"

# Enable logging
logger:

# Enable Home Assistant API
api:

ota:
```
Możesz w trakcie korzystać z narzędzi deweloperskich platformy.

### 4. Skompiluj firmware

- W ESPHome Dashboard kliknij na swoją konfigurację
- Kliknij **"INSTALL"** → **"Manual download"**
- Poczekaj na zakończenie kompilacji
- Pobierz plik `.bin` na swój komputer

---
## 📌 Przypięcie wersji ESPHome (WAŻNE)

Ten projekt **NIE używa obrazów `latest` ani `stable`**.

Zamiast tego wersja ESPHome jest jawnie określona w pliku `docker-compose.yml`:

```yaml
image: ghcr.io/esphome/esphome:2025.12.2
```
## 👥 Nie czujesz się na siłach aby zmieniać plik `docker-compose.yml`? Nic nie szkodzi, napisz Agentowi AI co ma zrobić za Ciebie:
<img width="1904" height="865" alt="image" src="https://github.com/user-attachments/assets/f45b01fe-eeb9-4508-a791-08b1f14fcfbd" />



Dzięki temu:
- ✅ Kompilacje są **powtarzalne**
- ✅ Nie ma niespodzianek po aktualizacjach ESPHome
- ✅ Możesz powrócić do starszych wydań

### Jak zaktualizować wersję ESPHome

1. Sprawdź dostępne wersje: https://github.com/esphome/esphome/releases
2. Edytuj `docker-compose.yml` i zmień numer wersji
3. Zrestartuj kontener w Gitpod



---
## ⚠️ Ważne ograniczenia

### 🚫 Flashowanie NIE JEST MOŻLIWE bezpośrednio z ONA (Gitpod)

**ONA/Gitpod działa w chmurze** i **nie ma dostępu** do:
- Twoich lokalnych portów USB (gdzie podłączasz ESP32/ESP8266)
- Twojej sieci lokalnej (gdzie działają urządzenia ESP po WiFi)

### ✅ Co musisz zrobić po kompilacji

Po pobraniu pliku `.bin` z Gitpod, flashowanie wykonaj lokalnie jedną z metod:

#### Metoda 1: ESPHome Web (w przeglądarce, bez instalacji)
1. Otwórz https://web.esphome.io w przeglądarce Chrome/Edge
2. Podłącz ESP przez USB
3. Kliknij "CONNECT" i wybierz port
4. Wybierz pobrany plik `.bin`
5. Kliknij "INSTALL"

#### Metoda 2: ESP_Flasher (polecana - aplikacja desktopowa)
1. Pobierz ESP_Flasher: https://github.com/Jason2866/ESP_Flasher/releases
2. Uruchom aplikację (dostępna dla Windows, macOS, Linux)
3. Wybierz port COM/USB
4. Wybierz pobrany plik `.bin`
5. Kliknij "Flash ESP"

**Zalety:** graficzny interfejs, nie wymaga instalacji Pythona, automatyczna detekcja portów

#### Metoda 3: esptool.py (dla zaawansowanych)
```bash
pip install esptool
esptool.py --port /dev/ttyUSB0 write_flash 0x0 firmware.bin
```

---

## 💡 Dla kogo jest to rozwiązanie?

### ✅ Idealne dla:
- 🖥️ Osób ze **słabym sprzętem** (Chromebook, tablet, stary laptop)
- 🎓 **Nauki ESPHome** bez skomplikowanej instalacji
- ✅ **Walidacji konfiguracji** YAML
- 🔄 Testowania **różnych wersji** ESPHome
- 👥 **Zespołów** - wszyscy używają tej samej wersji
- 🌍 Pracy **z dowolnego urządzenia** z przeglądarką

### ❌ NIE zastąpi:
- Flashowania przez USB/OTA (potrzebujesz ESP_Flasher lub podobny)
- Pełnej integracji z Home Assistant
- Lokalnego ESPHome z auto-flashowaniem

---


## 🛠️ Rozwiązywanie problemów

## Strona z Dashboard ESPHome się nie otwiera.
<img width="600" alt="image" src="https://github.com/user-attachments/assets/bf8e0e71-3fa4-4edd-9013-a5cfb27eb2fb" />
<img width="600" alt="image" src="https://github.com/user-attachments/assets/d06eb8ed-a78d-41cf-bb81-ffa6bd0c3b84" />
<img width="600" alt="image" src="https://github.com/user-attachments/assets/69dc4bdb-41c8-4f19-a0c8-f02e94fb301e" />




### Zapytaj AI na czacie jeśli napotkasz inne problemy (błędy kompilacji, składni kodu). Podpowie co należy zmienić.

---
**MIT License** - używaj swobodnie!

Co to znaczy:
- ✅ Możesz używać, kopiować, modyfikować
- ✅ Możesz używać komercyjnie
- ✅ Wystarczy zachować informację o autorze
- ❌ Brak gwarancji - używasz na własną odpowiedzialność

Pełna licencja: https://opensource.org/licenses/MIT
---
## 📚 Dodatkowe zasoby

- **Dokumentacja ESPHome:** https://esphome.io
- **Przykłady konfiguracji:** https://esphome.io/guides/
- **Forum społeczności:** https://community.home-assistant.io/c/esphome
- **Forum społeczności PL:** https://forum.arturhome.pl/
- **Dokumentacja Ona:** https://ona.com/docs
- **ESP_Flasher:** https://github.com/Jason2866/ESP_Flasher

---

## 🙏 Podziękowania
- **[@benzino77](https://github.com/benzino77)** - za inspirację poprzez jego świetny projekt [tasmocompiler](https://github.com/benzino77/tasmocompiler)
- **[ESPHome Team](https://esphome.io)** - za fantastyczne narzędzie do programowania ESP32/ESP8266
- **[Ona](https://ona.com)** (dawniej Gitpod) - za świetną i darmową platformę cloud development
- **[Jason2866](https://github.com/Jason2866/ESP_Flasher)** - za ESP_Flasher
- **Społeczność ESPHome i Home Assistant** - za nieustającą pomoc w duchu open source

---
