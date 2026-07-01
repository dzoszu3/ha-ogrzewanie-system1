# 🏠 Home Assistant Inteligentny System Ogrzewania

Kompletny system automatyzacji ogrzewania dla Home Assistant z Grafaną, InfluxDB i nowoczesnym interfejsem webowym.

## 📋 Zawartość Projektu

- **Instrukcja instalacji** - krok po kroku
- **Konfiguracja Home Assistant** - automacja + suwaki kontrolne
- **Grafana Dashboards** - wykresy 48h z zoomem
- **Custom Web App** - React aplikacja dark mode
- **Docker Compose** - dla Web App
- **Automacja** - harmonogramy temperatur dla każdego pokoju

---

## 🏠 Pomieszczenia

| Pokój | Temperatura Noc | Temperatura Dzień | Zawór |
|---|---|---|---|
| **Łazienka** | 25°C | 26-27°C | `switch.ogrzewanie_zawory_switch_3` |
| **Salon** | 22°C | 24°C | `switch.ogrzewanie_zawory_switch_4` |
| **Sypialnia** | 22°C | 24°C | `switch.ogrzewanie_zawory_switch_2` |
| **Pralnia** | 22°C | 24°C | `switch.ogrzewanie_zawory_switch_1` |
| **Kacperka** | 22°C | 24°C | - (template) |
| **Piwnica** | 22°C | 24°C | - (template) |

---

## ⚙️ Parametry Systemu

- **Zakres temperatur**: 18°C - 30°C
- **Zmiany godzin**: 30-minutowe interwały
- **Historia danych**: 48 godzin (z możliwością zoomu)
- **Interfejs**: Dark mode
- **Kontrolki**: Suwaki w Grafanie + Web App
- **Przechowywanie zmian**: Trwałe

---

## 🚀 Szybki Start

### Krok 1: Instalacja Addon'ów w HAOS

1. Otwórz Home Assistant: `http://192.168.1.86:8123/`
2. Settings → Add-ons → Add-on Store
3. Zainstaluj:
   - **InfluxDB**
   - **Grafana**

### Krok 2: Konfiguracja HA

1. Skopiuj `config/configuration.yaml` do Home Assistant
2. Skopiuj `config/automations.yaml` do Home Assistant
3. Restart Home Assistant

### Krok 3: Grafana Setup

1. Otwórz Grafana: `http://192.168.1.86:3000/`
2. Login: admin / admin (zmień hasło!)
3. Dodaj datasource InfluxDB
4. Importuj dashboards z folderu `grafana/`

### Krok 4: Web App

```bash
cd web-app
npm install
npm start
```

---

## 📊 Funkcje

✅ Wykresy temperatury + wilgotności (48h)  
✅ Status zaworu (graficzny na osi czasu)  
✅ Suwaki do zmiany temperatur (osobno dla każdego pokoju)  
✅ Zmiany godzin harmonogramu (30-min interwały)  
✅ Dark mode UI  
✅ Zoom i kadrowanie wykresów  
✅ Responsywny design (phone/tablet)  
✅ Zmiany zapisane trwale  

---

## 📁 Struktura Projektu

```
ha-ogrzewanie-system1/
├── README.md
├── INSTALLATION.md
├── config/
│   ├── configuration.yaml
│   ├── automations.yaml
│   └── input_number.yaml
├── grafana/
│   ├── dashboard-salon.json
│   ├── dashboard-sypialnia.json
│   ├── dashboard-lazienka.json
│   ├── dashboard-pralnia.json
│   ├── dashboard-kacperka.json
│   └── dashboard-piwnica.json
├── web-app/
│   ├── package.json
│   ├── src/
│   │   ├── App.jsx
│   │   ├── components/
│   │   │   ├── Dashboard.jsx
│   │   │   ├── RoomCard.jsx
│   │   │   ├── Chart.jsx
│   │   │   └── Controls.jsx
│   │   └── styles/
│   │       └── dark-mode.css
│   └── docker/
│       └── Dockerfile
└── docker-compose.yml
```

---

## 🔐 Bezpieczeństwo

⚠️ **WAŻNE**: Nigdy nie udostępniaj publicznie:
- Long-Lived Access Token
- Grafana credentials
- IP adresu laptopa poza siecią lokalną

---

## 📞 Wsparcie

Jeśli masz pytania lub problemy, sprawdź:
1. `INSTALLATION.md` - instrukcja instalacji
2. Logi Home Assistant
3. Logi Grafany

---

## 📝 Licencja

MIT

---

**Autor**: Copilot  
**Data**: 2026-01-07  
**Status**: 🚀 W budowie
