# ESPHome Dashboard w dowolnej wersji wydania dzięki platformie ### ONA
https://ona.com/stories/gitpod-is-now-ona


To repozytorium udostępnia **ESPHome Dashboard działający w całości w przeglądarce**, uruchamiany w **Ona (dawniej Gitpod)**

**jawnie przypiętą wersją ESPHome w obrazie Docker**.

Celem jest zapewnienie **powtarzalnych i stabilnych kompilacji firmware**, niezależnych od przyszłych aktualizacji ESPHome.

---

## 🤔 Co to jest platforma Ona (dawniej Gitpod)?

**platforma Ona Gitpod to taki komputer dla w chmurze, którego obsługa działa w przeglądarce. Ale to też dużo więcej, to całe środowisko programistyczne ze wsparciem AI**



Wyobraź sobie, że:
- Klikasz link w przeglądarce
- Dostajesz gotowy do użycia komputer z zainstalowanym ESPHome
- Kompilujesz firmware bez instalowania czegokolwiek na swoim komputerze
- Wszystko działa w przeglądarce (Chrome, Firefox, Edge)

**Nie musisz:**
- ❌ Instalować ESPHome na swoim komputerze
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
- Gitpod automatycznie uruchamia kontener
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
- Otworzy ESPHome Dashboard w przeglądarce

### 3. Dodaj swoją konfigurację YAML

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

### 4. Skompiluj firmware

- W ESPHome Dashboard kliknij na swoją konfigurację
- Kliknij **"INSTALL"** → **"Manual download"**
- Poczekaj na zakończenie kompilacji
- Pobierz plik `.bin` na swój komputer

---

## ⚠️ Ważne ograniczenia

### 🚫 Flashowanie NIE JEST MOŻLIWE bezpośrednio z Gitpod

**Gitpod działa w chmurze** i **nie ma dostępu** do:
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

## 📌 Przypięcie wersji ESPHome (WAŻNE)

Ten projekt **NIE używa obrazów `latest` ani `stable`**.

Zamiast tego wersja ESPHome jest jawnie określona w pliku `docker-compose.yml`:

```yaml
image: ghcr.io/esphome/esphome:2025.12.2
```

Dzięki temu:
- ✅ Kompilacje są **powtarzalne**
- ✅ Nie ma niespodzianek po aktualizacjach ESPHome
- ✅ Wszystkie osoby używające tego repo dostaną **identyczny firmware**

### Jak zaktualizować wersję ESPHome

1. Sprawdź dostępne wersje: https://github.com/esphome/esphome/releases
2. Edytuj `docker-compose.yml` i zmień numer wersji
3. Zrestartuj kontener w Gitpod

---

## 💡 Dla kogo jest to rozwiązanie

### ✅ Idealne dla:
- Osób ze **słabym sprzętem** (kompilacja w chmurze)
- Kompilacji na **Chromebooku** lub **tablecie**
- Uczenia się ESPHome bez instalacji
- Walidacji konfiguracji YAML
- Współpracy zespołowej (wszyscy używają tej samej wersji)

### ❌ NIE zastąpi:
- Bezpośredniego flashowania urządzeń (potrzebujesz dodatkowo ESP_Flasher lub podobne narzędzie)
- Pełnej integracji z Home Assistant

---

## 🕐 Limity Gitpod

**Plan darmowy:**
- 50 godzin workspace/miesiąc
- 4 równoległe workspace

**Plan Pro:**
- 100 godzin/miesiąc

Kompilacja pojedynczego firmware zwykle zajmuje **2-5 minut**, więc spokojnie zmieścisz się w limicie.

---

## 🗂️ Struktura projektu

```
esphome-gitpod/
├── .gitpod.yml              # Konfiguracja Gitpod
├── docker-compose.yml       # Definicja kontenera ESPHome
├── README.md                # Ten plik
└── esphome/                 # Katalog na twoje konfiguracje YAML
    └── .gitkeep             # (pusty plik do utrzymania katalogu w git)
```

---

## 🛠️ Rozwiązywanie problemów

### Dashboard się nie otwiera automatycznie
- Sprawdź zakładkę "Ports" w Gitpod
- Kliknij na port `6052` aby otworzyć ręcznie

### Kompilacja się nie udaje
- Sprawdź składnię YAML w dashboard (kliknij "VALIDATE")
- Upewnij się, że używasz kompatybilnej wersji składni dla ESPHome 2025.12.2

### Chcę użyć nowszej wersji ESPHome
- Edytuj `docker-compose.yml`
- Zmień `2025.12.2` na wybraną wersję
- Zrestartuj workspace

---

## 📝 Licencja

MIT License - używaj swobodnie!

---

## 🙏 Podziękowania

- [ESPHome](https://esphome.io) - za świetne narzędzie
- [Gitpod](https://gitpod.io) - za darmowe środowisko developerskie w chmurze
