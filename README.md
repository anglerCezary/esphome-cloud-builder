---

# ESPHome Dashboard w Gitpod (przypięta wersja)

To repozytorium udostępnia **ESPHome Dashboard działający w całości w przeglądarce**, uruchamiany w **Gitpod**, z **jawnie przypiętą wersją ESPHome w obrazie Docker**.

Celem jest zapewnienie **powtarzalnych i stabilnych kompilacji firmware**, niezależnych od przyszłych aktualizacji ESPHome.

---

## 🚀 Jak to działa

- ESPHome uruchamiany jest wewnątrz oficjalnego kontenera Docker
- Obraz kontenera jest przypięty do **konkretnej wersji ESPHome**
- Gitpod automatycznie uruchamia kontener
- ESPHome Dashboard jest dostępny w przeglądarce
- Firmware kompilowany jest **w całości w chmurze**

Nie jest wymagana żadna lokalna instalacja ESPHome.

---

## 📌 Przypięcie wersji ESPHome (WAŻNE)

Ten projekt **NIE używa obrazów `latest` ani `stable`**.

Zamiast tego wersja ESPHome jest jawnie określona w pliku `docker-compose.yml`, np.:

```yaml
image: ghcr.io/esphome/esphome:2025.5.0
