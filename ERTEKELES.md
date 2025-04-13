# 🌱 **TÉMAZÁRÓ ÉRTÉKELÉSI ÚTMUTATÓ**

## 🔖 Általános értékelési szempontok (beadás formátuma)

| Szempont | Leírás |
|----------|--------|
| ✅ Helyes mappanév | A hallgató a nevét kisbetűvel, ékezet nélkül és szóköz nélkül írta, pl.: `kissbela` | 
| ✅ Projektmappák létrehozása | Mindhárom mappa (`customer-app`, `moneytr-app`, `debt-app`) létrehozva, a megfelelő fájlokkal |

> [!CAUTION]
> **Megjegyzés:** Ha a mappaszerkezet nem megfelelő vagy nem a kért fájlokat tartalmazza, a teljes projekt érvénytelennek minősülhet („nem egyes”).

---

## 1️⃣ **Banki ügyfél lekérdező rendszer** (`customer-app/`)

### ✅ **Alapvető funkciók működése (`GET` lekérdezés)**

| Szempont | Leírás |
|----------|--------|
| Fetch metódus helyes használata | `fetch()` helyes alkalmazása, GET metódussal |
| Respons dekódolása | `.json()` helyesen használva |
| Adatfeldolgozás | `.then()` blokk használata és a tömb elemeinek DOM-ba helyes renderelése. |
| Hibakezelés | `.catch()` blokk használata |
| Hibára való reagálás | Hiba esetén értelmezhető hibaüzenet megjelenítése |
| Node környezet használata | A szerver működik, `npm init`, `express` telepítve és `node server.js`-szel indítható |

---

## 2️⃣ **Pénz küldő rendszer** (`moneytr-app/`)

### ⚙️ **POST kérés konfigurálása**

| Szempont | Leírás |
|----------|--------|
| Fetch helyes használata | megfelelő metódus alkalmazása a végpontra |
| Respons dekódolása | `.json()` hívás |
| Adatfeldolgozás | Válasz alapján visszajelzés (`console.log`, `alert`) |


### 🧾 **Konfigurációs beállítások**

| Szempont | Leírás |
|----------|--------|
| Metódus konfigurálás | `method` megadása a fetch-ben |
| Header beállítás | `Content-Type:` helyes megadása |
| Body helyes beállítása | `JSON.stringify()`  helyes objektum megadással |

### 💬 **Felhasználói visszajelzések**

| Szempont | Leírás |
|----------|--------|
| `.then` blokk – console.log | A sikeres válasz konzolra kerül |
| `.then` blokk – alert | Alert jelenik meg a sikeres mentés után |
| `.catch` blokk – console.log | Hibát konzolra írja |
| `.catch` blokk – alert | Hibát alertként is jelzi |

### ✅ **Tesztelés**

| Szempont | Leírás |
|----------|--------|
| Elvárt teszt rögzítve | A rekordok sikeresen bekerültek a JSON fájlba |
| Node környezet | Express, JSON fájl írása működik |

---

## 3️⃣ **Inkasszó kezelő rendszer** (`debt-app/`)

### 🔄 **DELETE kérés működése**

| Szempont | Leírás |
|----------|--------|
| Fetch használat | Helyes metódus alkalmazása a végpontra |
| Respons dekódolás | A szerver válaszát `.json()`-nal értelmezi |
| Adatfeldolgozás | Válasz alapján visszajelzés (`console.log`, `alert`) |

### 🧾 **Konfigurációs beállítások**

| Szempont | Leírás |
|----------|--------|
| Metódus konfigurálása | `method:` megadva |
| Header | `Content-Type:` helyes |
| Body | `JSON.stringify()` helyes objektum megadás |

### 💬 **Felhasználói visszajelzések**

| Szempont | Leírás |
|----------|--------|
| `.then` blokk – console.log | A szerver visszajelzését naplózza |
| `.then` blokk – alert | Alert formájában is jelez |
| `.catch` blokk – console.log | Hibát naplózza |
| `.catch` blokk – alert | Hibát alert formában is közli |

### ✅ **Tesztelés**

| Szempont | Leírás |
|----------|--------|
| Elvárt rekord törölve | A rekordok törlése sikeres |
| Node környezet | Szerver működik, fájlfrissítés megvalósul |

---


## 🎯 **Összpontszám kiszámítási javaslat**

> [!NOTE]
> - **Általános formai rész (mappastruktúra és fileok a helyükön):** hogy ne legyen egyes
> - **1. projekt (GET művelet):** max. 6 pont
> - **2. projekt (POST művelet):** max. 17 pont
> - **3. projekt (DELETE művelet):** max. 17 pont
> - **Teljes értékelés:** **max. 40 pont**
