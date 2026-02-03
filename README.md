# ESPHome Dashboard in Gitpod (Pinned Version)

This repository provides a **fully browser-based ESPHome Dashboard** running in **Gitpod**, with **ESPHome pinned to a specific Docker image version**.

The goal is to ensure **reproducible and stable firmware builds**, independent of future ESPHome updates.

---

## 🚀 How it works

- ESPHome is run inside an official Docker container
- The container image is pinned to a **specific ESPHome release**
- Gitpod starts the container automatically
- ESPHome Dashboard is exposed via the browser
- Firmware is compiled **entirely in the cloud**

No local ESPHome installation is required.

---

## 📌 ESPHome Version Pinning (IMPORTANT)

This project **does NOT use `latest` or `stable` images**.

Instead, ESPHome is pinned explicitly in `docker-compose.yml`, for example:

```yaml
image: ghcr.io/esphome/esphome:2025.12.2
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
image: ghcr.io/esphome/esphome:2025.12.2

