## 📖 Instrukcja Instalacji - HA Ogrzewanie System

Kompletny guide do wdrożenia całego systemu.

---

## 📋 Wymagania

- Home Assistant OS (HAOS) na x86-64
- IP: `192.168.1.86:8123`
- Docker (dla Web App - opcjonalne)
- Czujniki THS zainstalowane w HAOS
- Przekaźniki sterujące zaworami skonfigurowane

---

## 🔧 Krok 1: Instalacja Addon'ów w HAOS (5 min)

### 1.1 InfluxDB Addon

1. Otwórz **Home Assistant**: `http://192.168.1.86:8123/`

2. Idź do: **Settings** → **Add-ons and integrations** → **Add-on Store** (prawy górny róg)

3. Wyszukaj: `influxdb`

4. Kliknij na **InfluxDB**

5. Kliknij **Install** i czekaj (1-2 min)

6. Po instalacji:
   - Kliknij **Start** 
   - Włącz opcję **"Start on boot"** (checkbox)
   - Sprawdź logi - powinny być zielone

**⏳ CZEKAJ 2-3 MINUTY NA INICJALIZACJĘ BAZY!**

---

### 1.2 Grafana Addon

1. W Add-on Store wyszukaj: `grafana`

2. Kliknij na **Grafana**

3. Kliknij **Install** i czekaj

4. Po instalacji:
   - Kliknij **Start**
   - Włącz **"Start on boot"**

**Grafana będzie dostępna pod:** `http://192.168.1.86:3000/`

---

## ⚙️ Krok 2: Konfiguracja Home Assistant (10 min)

### 2.1 Dodaj pliki konfiguracyjne

#### A) File Editor w HA

1. Home Assistant → menu (≡) → **Settings** → **File Editor** (lub `/developer_tools/service`)

2. Folder `/config/` powinien być już otwarty

3. Jeśli nie ma, kliknij folder ikona (📁) w lewym panelu

---

#### B) Utwórz `configuration.yaml`

1. Kliknij **Create file** → wpisz: `configuration.yaml`

2. Skopiuj zawartość z repozytorium `config/configuration.yaml`

3. **WAŻNE**: Zmień linię:
```yaml
token: YOUR_INFLUXDB_TOKEN_HERE
```

**Na token z InfluxDB Addon'u:**
- Settings HA → Devices & Services → Integrations
- Szukaj InfluxDB → kliknij
- Skopiuj token

4. Kliknij **Save** (Ctrl+S)

---

#### C) Utwórz `input_number.yaml`

1. **Create file** → `input_number.yaml`

2. Skopiuj zawartość z `config/input_number.yaml`

3. **Save**

---

#### D) Utwórz `automations.yaml`

1. **Create file** → `automations.yaml`

2. Skopiuj zawartość z `config/automations.yaml`

3. **ZMIEŃ dla Kacperki i Piwnicy:**
```yaml
# Zmień te linie z twoimi entity'ami:
entity_id: switch.YOUR_ZAWAR_SWITCH_HERE
# Na np: switch.zawar_kacperka

data:
  entity_id: sensor.YOUR_TEMP_SENSOR
# Na np: sensor.kacperka_temperatura
```

4. **Save**

---

### 2.2 Restart Home Assistant

1. Home Assistant → menu → **Settings** → **System**

2. Prawy górny róg → **Restart Home Assistant** (niebieskie przyciski)

3. **Czekaj 3-5 minut** na restart

4. Wejdź na HA znowu - powinno załadować się bez błędów

---

## 📊 Krok 3: Konfiguracja Grafany (10 min)

### 3.1 Logowanie

1. Otwórz: `http://192.168.1.86:3000/`

2. **Username**: `admin`

3. **Password**: `admin`

4. Zmień hasło na początek (wejdź w profil)

---

### 3.2 Dodaj Datasource (InfluxDB)

1. Menu (≡) → **Connections** → **Data sources**

2. **Add data source**

3. Wybierz **InfluxDB**

4. Wypełnij pola:
   - **Name**: `InfluxDB HA`
   - **URL**: `http://localhost:8086`
   - **Auth**: None
   - **Organization**: `home-assistant`
   - **Token**: (skopiuj z InfluxDB Addon Settings)
   - **Default bucket**: `home-assistant`

5. **Save & Test** (powinno być zielone: "datasource is working")

---

### 3.3 Importuj Dashboards

**Dashboards będą dodane do repozytorium wkrótce!**

Na razie możesz stworzyć własne:

1. **+** (prawy górny) → **New dashboard**

2. **+ Add panel**

3. Wybierz **Visualization** → **Time series**

4. Wybierz datasource: `InfluxDB HA`

5. Kliknij na **Queries** i skonfiguruj metryki

---

## 🎨 Krok 4: Instalacja Web App (5 min)

### Opcja A: Lokalnie (npm)

```bash
cd web-app
npm install
npm start
```

**Aplikacja będzie dostępna na:** `http://localhost:3000`

---

### Opcja B: Docker

```bash
docker-compose up --build
```

**Aplikacja będzie dostępna na:** `http://192.168.1.86:5000`

---

## ✅ Weryfikacja Wszystkiego

Sprawdź czy wszystko działa:

### Home Assistant
- [ ] Czujniki temperatury widoczne (`sensor.ths_*`)
- [ ] Suwaki kontrolne widoczne (`input_number.*`)
- [ ] Automata uruchamiają się (Settings → Automations)
- [ ] Brak błędów w logach

### InfluxDB
- [ ] Addon uruchomiony
- [ ] Settings HA → Integrations → InfluxDB (zielone)

### Grafana
- [ ] Dostępna pod `http://192.168.1.86:3000/`
- [ ] Datasource InfluxDB podłączony
- [ ] Dashboards załadowane

### Web App
- [ ] Dostępna pod `http://localhost:3000`
- [ ] Dark mode włączony
- [ ] Suwaki działają
- [ ] Wykresy pokazują dane

---

## 🐛 Troubleshooting

### Problem: Grafana nie widzi InfluxDB

```
Settings HA → Add-ons → InfluxDB → Logs
```

Sprawdź czy są błędy. Uruchom restart InfluxDB addon'u.

---

### Problem: Wykresy są puste

1. Czekaj 5-10 minut - InfluxDB musi zebrać dane z czujników
2. Sprawdź czy entity'y są prawidłowe
3. Sprawdź czy automata działają (Settings → Automations)

---

### Problem: Suwaki nie działają

1. Sprawdź czy `input_number.yaml` został załadowany
2. Restart HA
3. Sprawdź Developer Tools → States (czy entity'y tam są)

---

### Problem: Brak dostępu z telefonu

Upewnij się że:
- Telefon jest w tej samej sieci WiFi
- IP `192.168.1.86` jest prawidłowy
- Firewall nie blokuje portu 3000/5000

---

## 📱 Dostęp z Telefonu/Tabletu

1. Upewnij się że jesteś w tej samej sieci WiFi co laptop
2. Wpisz w przeglądarce:
   - **Grafana**: `http://192.168.1.86:3000`
   - **Web App**: `http://192.168.1.86:5000`

---

## 🔐 Bezpieczeństwo - Ważne!

⚠️ **Nigdy nie udostępniaj publicznie:**
- InfluxDB token
- Grafana credentials
- HA token dostępu
- IP adresu poza siecią lokalną

---

## 🎉 Gotowe!

Teraz masz pełny system z:
- ✅ Automatyzacją ogrzewania
- ✅ Dashboards w Grafanie
- ✅ Nowoczesną Web App
- ✅ Dostępem z telefonu

**Powodzenia!** 🚀
