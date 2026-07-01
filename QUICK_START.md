## 5-Minutowy Quick Start! ⚡

### Wymagane:
- Home Assistant OS na 192.168.1.86:8123
- Token HA (posiadasz)

---

### Krok 1️⃣ Zainstaluj Addon'y (2 min)

```
HA → Settings → Add-ons and integrations → Add-on Store

1. Szukaj: InfluxDB
   ✅ Install → Start → Start on boot

2. Szukaj: Grafana  
   ✅ Install → Start → Start on boot
```

**Czekaj 2-3 minuty na inicjalizację!**

---

### Krok 2️⃣ Konfiguruj Home Assistant (2 min)

1. Otwórz `/config/configuration.yaml` w HA
2. Skopiuj zawartość z repozytorium `config/configuration.yaml`
3. Zamień `YOUR_INFLUXDB_TOKEN_HERE` na token z InfluxDB Addon

4. Skopiuj `config/input_number.yaml` do folderu `/config/`
5. Skopiuj `config/automations.yaml` do folderu `/config/`

6. **Restart Home Assistant!**

---

### Krok 3️⃣ Uruchom Web App (1 min)

```bash
cd web-app
npm install
npm start
```

Aplikacja otworzy się automatycznie na `http://localhost:3000`

---

## 🌐 Dostępy

| Usługa | Adres |
|--------|-------|
| Home Assistant | http://192.168.1.86:8123 |
| Grafana | http://192.168.1.86:3000 |
| Web App | http://localhost:3000 |

**Grafana login**: admin / admin (zmień hasło!)

---

## 📱 Z Telefonu

```
http://192.168.1.86:3000 (Grafana)
lub
http://192.168.1.86:5000 (Web App - jeśli Docker)
```

---

## ⚙️ Zmiana Entity'ów

Dla **Kacperki** i **Piwnicy**:

1. Otwórz `config/input_number.yaml`
2. Zmień:
   ```yaml
   sensor.YOUR_TEMP → sensor.kacperka_temperatura
   sensor.YOUR_HUMIDITY → sensor.kacperka_wilgotnosc
   switch.YOUR_VALVE → switch.zawar_kacperka
   ```

3. Otwórz `config/automations.yaml`
4. Zmień entity'y dla Kacperki i Piwnicy

5. **Restart HA**

---

## ✅ Weryfikacja

- [ ] InfluxDB Addon uruchomiony
- [ ] Grafana dostępna na porcie 3000
- [ ] HA restartnięty
- [ ] Web App działa
- [ ] Suwaki widoczne w HA
- [ ] Wykresy w Grafanie pokazują dane (czekaj 5 minut)

---

**Gotowe! 🎉 System jest teraz w pełni operacyjny!**

Jeśli coś się nie ładuje - sprawdź **INSTALLATION.md** dla troubleshootingu.
