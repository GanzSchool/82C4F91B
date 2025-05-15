
# 🌱 **TÉMAZÁRÓ | GYAKORLAT | Kliensoldali hálózati műveletek használatának alapjai JavaScriptben | 82C4F91B**

## 📁 Általános mappaszerkezet

Hozz létre egy mappát a teljes neveddel az alábbi formában:  
**kisbetű, ékezet nélkül, szóköz nélkül**  
**pl.: Kiss Béla → `kissbela/`**

Ezen belül 3 projekt gyökérmappát:

```bash
kissbela/
├── customer-app/         # Banki ügyfél lekérdező rendszer
├── moneytr-app/          # Pénz küldő rendszer
├── debt-app/             # Inkasszó kezelő rendszer
```

## Feladat

- Illeszd össze a projekt egyes elemeit a megadott topológia alapján.
- script.js fileokban írd meg a kliens oldali kéréseket fetch metódus segítségével.
- Kommentekben találod az utasításokat a logika kialakításához.
- Ahol kéri a feladat végezd el a szükséges tesztelést.
- Törekedj a rendezet kód kialakításához.


---

## 1️⃣ Projekt: **Banki ügyfél lekérdező rendszer**  
`customer-app/`

### 📁 Mappaszerkezet

```bash
customer-app/
├── server.js
├── data.json
└── public/
    ├── index.html
    ├── style.css
    └── script.js
```

### ⚙️ Funkciók

| Endpoint        | Metódus | Cél                    |
|-----------------|---------|------------------------|
| `/api/customers`  | `GET`   | Bank ügyfeleinek lekérdezése |

### 🧩 PROJEKT FILEOK

> `public/index.html`

```html
<!DOCTYPE html>
<html lang="hu">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Banki Ügyfelek</title>
  <link rel="stylesheet" href="style.css">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
</head>
<body>
  <div class="container">
    <header>
      <h1>Banki Ügyfelek</h1>
      <p class="subtitle">Ügyfél információs rendszer</p>
    </header>
    
    <button id="loadButton">
      <span class="icon">📜</span>
      <span>Ügyfelek betöltése</span>
    </button>
    
    <div id="customerData"></div>
    
    <footer>
      <p>© 2025 Bank Rendszer</p>
    </footer>
  </div>
  <script src="script.js"></script>
</body>
</html>
```

> `public/style.css`

```css
/* Alap beállítások */
:root {
  --primary: #0a6c74;
  --primary-light: #0d8a96;
  --primary-dark: #064e54;
  --secondary: #2e7d32;
  --secondary-light: #4caf50;
  --text-light: #ffffff;
  --text-dark: #333333;
  --background: #f5f7fa;
  --card-bg: #ffffff;
  --border-radius: 12px;
  --shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  --transition: all 0.3s ease;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: linear-gradient(135deg, var(--primary-dark), var(--primary));
  margin: 0;
  padding: 20px;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: "Poppins", sans-serif;
  color: var(--text-dark);
}

/* Konténer */
.container {
  background: var(--card-bg);
  padding: 40px;
  border-radius: var(--border-radius);
  box-shadow: var(--shadow);
  width: 100%;
  max-width: 500px;
  position: relative;
  overflow: hidden;
}

/* Fejléc */
header {
  text-align: center;
  margin-bottom: 30px;
}

h1 {
  color: var(--primary);
  font-size: 28px;
  font-weight: 600;
  margin-bottom: 8px;
}

.subtitle {
  color: #666;
  font-size: 16px;
  font-weight: 400;
}

/* Gomb */
button {
  background-color: var(--primary);
  color: var(--text-light);
  border: none;
  padding: 14px 24px;
  border-radius: var(--border-radius);
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  transition: var(--transition);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  width: 100%;
  margin-bottom: 25px;
}

button:hover {
  background-color: var(--primary-light);
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(10, 108, 116, 0.3);
}

button:active {
  transform: translateY(0);
}

.icon {
  font-size: 20px;
}

/* Ügyfelek adatait tartalmazó konténer */
#customerData {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  max-height: auto;
  overflow-y: auto;
  padding-right: 10px;
  margin-bottom: 20px;
}

/* Görgetősáv stílusozása */
#customerData::-webkit-scrollbar {
  width: 6px;
}

#customerData::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 10px;
}

#customerData::-webkit-scrollbar-thumb {
  background: var(--primary-light);
  border-radius: 10px;
}

#customerData::-webkit-scrollbar-thumb:hover {
  background: var(--primary);
}

/* Ügyfél kártya */
.customer-card {
  background: linear-gradient(135deg, var(--primary-light), var(--primary));
  padding: 20px;
  border-radius: var(--border-radius);
  box-shadow: 0 5px 15px rgba(10, 108, 116, 0.2);
  color: var(--text-light);
  transition: var(--transition);
  position: relative;
  overflow: hidden;
}

.customer-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(10, 108, 116, 0.3);
}

.customer-card h3 {
  font-size: 18px;
  font-weight: 600;
  margin-bottom: 12px;
  position: relative;
}

.customer-card p {
  font-size: 14px;
  margin-bottom: 8px;
  display: block; /* Changed from flex to block */
  color: var(--text-light);
}

/* Balance styling */
.customer-card .balance {
  font-weight: 600;
  font-size: 16px;
  margin-top: 10px;
  background-color: rgba(255, 255, 255, 0.2);
  padding: 8px 12px;
  border-radius: 6px;
  display: inline-block;
}

/* Lábléc */
footer {
  text-align: center;
  margin-top: 20px;
  font-size: 14px;
  color: #888;
}

/* Reszponzív beállítások */
@media (max-width: 600px) {
  .container {
    padding: 25px;
    margin: 15px;
  }

  h1 {
    font-size: 24px;
  }

  button {
    padding: 12px 20px;
  }

  .customer-card {
    padding: 15px;
  }
}
```
> `public/script.js`

```js
document.getElementById("loadButton").addEventListener("click", (event) => {

        // küld el a szervernek a kérést

        // kapd el a szerver válaszát

        // dolgozd fel a szerver válaszát

          // DOM - manipulációs logika
          
/*
        const container = document.getElementById("customerData");
        container.innerHTML = ""; // Korábbi tartalom törlése
  
        data.customers.map(customer => {
          const card = document.createElement("div");
          card.classList.add("customer-card");
  
          const name = document.createElement("h3");
          name.textContent = customer.name;
  
          const account = document.createElement("p");
          account.textContent = "Számlaszám: " + customer.accountNumber;
  
          const balance = document.createElement("p");
          balance.textContent = `Egyenleg: ${customer.balance} Ft`;
  
          card.append(name, account, balance);
          container.appendChild(card);
        });
*/
      // hiba esetén: "Hiba történt:"

  });
```

> `server.js`

```js
var express = require('express');
var path = require('path');
var app = express();
var port = process.env.PORT || 3001;

// Statikus fájlok kiszolgálása a public mappából
app.use(express.static(path.join(__dirname, 'public')));

// data.json kiszolgálása banki ügyfelek adataival
app.get('/api/customers', function(req, res) {
  res.sendFile(path.join(__dirname, 'data.json'));
});

// Szerver indítása
app.listen(port, function() {
  console.log(`Szerver fut a http://localhost:${port}`);
});
```

> `data.json`

```json
{
    "customers": [
      {
        "name": "Kiss József",
        "accountNumber": "BANK0001 CUST0001 ACCT0001",
        "balance": 5000
      },
      {
        "name": "Németh Ágnes",
        "accountNumber": "BANK0002 CUST0002 ACCT0002",
        "balance": 22000
      },
      {
        "name": "Tóth István",
        "accountNumber": "BANK0003 CUST0003 ACCT0003",
        "balance": 3000
      },
      {
        "name": "Kovács Erika",
        "accountNumber": "BANK0004 CUST0004 ACCT0004",
        "balance": 7500
      }
    ]
  }
```

---

## 2️⃣ Projekt: **Pénz küldő rendszer**  
`moneytr-app/`

### 📁 Mappaszerkezet

```bash
moneytr-app/
├── server.js
├── transactions.json
└── public/
    ├── index.html
    ├── style.css
    └── script.js
```

### ⚙️ Funkciók

| Endpoint       | Metódus | Cél                     |
|----------------|---------|--------------------------|
| `/api/bank`  | `POST`  | Pénz küldése a bank ügyfeleinek |

### 🧩 PROJEKT FILEOK

> `public/index.html`

```js
<!DOCTYPE html>
<html lang="hu">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Banki Tranzakció Rögzítése</title>
  <link rel="stylesheet" href="style.css" />
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap">
</head>
<body>
  <div class="page-container">
    <div class="form-container">
      <div class="form-header">
        <div class="logo">
          <div class="logo-icon">
            <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="logo-svg">
              <path d="M3 21H21M3 18H21M5 18V10M19 18V10M12 18V10M12 7H19C19.5523 7 20 6.55228 20 6V4C20 3.44772 19.5523 3 19 3H5C4.44772 3 4 3.44772 4 4V6C4 6.55228 4.44772 7 5 7H12Z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </div>
          <span>Big Business Bank</span>
        </div>
        <h1>Banki tranzakció űrlap</h1>
        <p class="subtitle">Kérjük, töltse ki az alábbi mezőket a tranzakció rögzítéséhez</p>
      </div>
      <form class="transaction-form">
        <div class="form-group">
          <label for="name">Ügyfél neve</label>
          <div class="input-container">
            <svg class="input-icon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M20 21V19C20 17.9391 19.5786 16.9217 18.8284 16.1716C18.0783 15.4214 17.0609 15 16 15H8C6.93913 15 5.92172 15.4214 5.17157 16.1716C4.42143 16.9217 4 17.9391 4 19V21M16 7C16 9.20914 14.2091 11 12 11C9.79086 11 8 9.20914 8 7C8 4.79086 9.79086 3 12 3C14.2091 3 16 4.79086 16 7Z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            <input type="text" id="name" placeholder="Add meg az ügyfél nevét" />
          </div>
        </div>
        <div class="form-group">
          <label for="accountNumber">Számlaszám</label>
          <div class="input-container">
            <svg class="input-icon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M3 10H21M7 15H8M12 15H13M17 15H18M5 19H19C20.1046 19 21 18.1046 21 17V7C21 5.89543 20.1046 5 19 5H5C3.89543 5 3 5.89543 3 7V17C3 18.1046 3.89543 19 5 19Z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            <input type="text" id="accountNumber" placeholder="Add meg a számlaszámot" />
          </div>
        </div>
        <div class="form-group">
          <label for="amount">Kívánt összeg</label>
          <div class="input-container">
            <svg class="input-icon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M12 1V23M17 5H9.5C8.57174 5 7.6815 5.36875 7.02513 6.02513C6.36875 6.6815 6 7.57174 6 8.5C6 9.42826 6.36875 10.3185 7.02513 10.9749C7.6815 11.6313 8.57174 12 9.5 12H14.5C15.4283 12 16.3185 12.3687 16.9749 13.0251C17.6313 13.6815 18 14.5717 18 15.5C18 16.4283 17.6313 17.3185 16.9749 17.9749C16.3185 18.6313 15.4283 19 14.5 19H6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            <input type="text" id="amount" placeholder="Add meg a kívánt összeget" />
          </div>
        </div>
        <button id="sendButton" type="submit" class="submit-button">
          <span>Tranzakció rögzítése</span>
          <svg class="button-icon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M5 12H19M19 12L12 5M19 12L12 19" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </button>
      </form>
      <div class="form-footer">
        <p>Biztonságos tranzakció feldolgozás</p>
        <div class="security-icons">
          <svg class="security-icon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M12 22C12 22 20 18 20 12V5L12 2L4 5V12C4 18 12 22 12 22Z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M9 12L11 14L15 10" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </div>
      </div>
    </div>
  </div>
  <script src="script.js"></script>
</body>
</html>
```

> `public/style.css`

```css
:root {
    --primary-color: #0052cc;
    --primary-light: #e6f0ff;
    --primary-dark: #003d99;
    --secondary-color: #00a3bf;
    --text-color: #333;
    --text-light: #666;
    --background-color: #051b3d;
    --white: #ffffff;
    --border-color: #e1ebe2;
    --success-color: #00875a;
    --error-color: #de350b;
    --shadow-sm: 0 2px 4px rgba(0, 0, 0, 0.05);
    --shadow-md: 0 4px 8px rgba(0, 0, 0, 0.1);
    --shadow-lg: 0 8px 16px rgba(0, 0, 0, 0.1);
    --radius-sm: 4px;
    --radius-md: 8px;
    --radius-lg: 12px;
  }
  
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  body {
    font-family: "Poppins", sans-serif;
    background-color: var(--background-color);
    color: var(--text-color);
    line-height: 1.6;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .page-container {
    width: 100%;
    max-width: 1200px;
    padding: 20px;
  }
  
  .form-container {
    background-color: var(--white);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-lg);
    overflow: hidden;
    width: 100%;
    max-width: 500px;
    margin: 0 auto;
    position: relative;
  }
  
  .form-header {
    padding: 30px 30px 20px;
    text-align: center;
    background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
    color: var(--white);
  }
  
  .logo {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 20px;
    font-weight: 600;
    font-size: 20px;
  }
  
  .logo-icon {
    width: 32px;
    height: 32px;
    background-color: var(--white);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-right: 10px;
  }
  
  .logo-svg {
    width: 20px;
    height: 20px;
    color: var(--primary-color);
  }
  
  h1 {
    font-size: 24px;
    font-weight: 600;
    margin-bottom: 8px;
  }
  
  .subtitle {
    font-size: 14px;
    opacity: 0.9;
    margin-bottom: 10px;
  }
  
  .transaction-form {
    padding: 30px;
  }
  
  .form-group {
    margin-bottom: 24px;
  }
  
  label {
    display: block;
    font-size: 14px;
    font-weight: 500;
    margin-bottom: 8px;
    color: var(--text-color);
  }
  
  .input-container {
    position: relative;
  }
  
  .input-icon {
    position: absolute;
    left: 12px;
    top: 50%;
    transform: translateY(-50%);
    width: 20px;
    height: 20px;
    color: var(--text-light);
  }
  
  input {
    width: 100%;
    padding: 12px 12px 12px 44px;
    border: 1px solid var(--border-color);
    border-radius: var(--radius-md);
    font-size: 15px;
    transition: all 0.3s ease;
    background-color: var(--white);
    color: var(--text-color);
    font-family: "Poppins", sans-serif;
  }
  
  input:focus {
    outline: none;
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgba(0, 82, 204, 0.15);
  }
  
  input::placeholder {
    color: #aab;
  }
  
  .submit-button {
    width: 100%;
    padding: 14px 20px;
    background: linear-gradient(135deg, var(--primary-color), var(--primary-dark));
    color: var(--white);
    border: none;
    border-radius: var(--radius-md);
    font-size: 16px;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: var(--shadow-sm);
    margin-top: 10px;
  }
  
  .submit-button:hover {
    background: linear-gradient(135deg, var(--primary-dark), var(--primary-color));
    box-shadow: var(--shadow-md);
    transform: translateY(-1px);
  }
  
  .submit-button:active {
    transform: translateY(1px);
    box-shadow: var(--shadow-sm);
  }
  
  .button-icon {
    width: 18px;
    height: 18px;
    margin-left: 8px;
  }
  
  .form-footer {
    padding: 15px 30px;
    background-color: var(--primary-light);
    text-align: center;
    font-size: 13px;
    color: var(--primary-dark);
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
  
  .security-icons {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 5px;
  }
  
  .security-icon {
    width: 20px;
    height: 20px;
    color: var(--primary-color);
  }
  
  /* Responsive adjustments */
  @media (max-width: 576px) {
    .form-container {
      border-radius: 0;
      box-shadow: none;
    }
  
    .page-container {
      padding: 0;
    }
  
    .form-header {
      padding: 25px 20px 15px;
    }
  
    .transaction-form {
      padding: 20px;
    }
  
    h1 {
      font-size: 22px;
    }
  }
  
  /* Animation for form elements */
  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(10px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  .form-group {
    animation: fadeIn 0.4s ease-out forwards;
  }
  
  .form-group:nth-child(1) {
    animation-delay: 0.1s;
  }
  
  .form-group:nth-child(2) {
    animation-delay: 0.2s;
  }
  
  .form-group:nth-child(3) {
    animation-delay: 0.3s;
  }
  
  .submit-button {
    animation: fadeIn 0.4s ease-out forwards;
    animation-delay: 0.4s;
  }
  
```

> `public/script.js`

```js
document.getElementById("sendButton").addEventListener("click", () => {
  
    // 1) Kinyerjük az input mezők értékeit
    const nameValue = document.getElementById("name").value;
    const accountValue = document.getElementById("accountNumber").value;
    const amountValue = document.getElementById("amount").value;
  
    const transactionData = {
      name: nameValue,
      accountNumber: accountValue,
      amount: amountValue
    };
  
      // küld el a szervernek a kérést és a bekért adatokat
  
      // kapd el a szerver válaszát
    
      // console logban jelenjen meg a szerver válasza: "Szerver válasza:" ...
      // alert formájában jelenjen ez meg: "Sikeres utalás!"

  
      // hiba esetén: "Hiba történt:" ...
      // Hiba esetén jelenjen meg ez az alert: "Hiba történt a küldés során!"
  });
  
```

> `server.js`

```js
const express = require("express");
const fs = require("fs");
const path = require("path");

const app = express();
const PORT = 3002;

app.use(express.json());
app.use(express.static("public"));

app.post("/api/bank", (req, res) => {
  try {
    const newTransaction = req.body;

    // A tranzakciókat tartalmazó JSON fájl útvonala
    const filePath = path.join(__dirname, "transactions.json");
    const fileData = fs.readFileSync(filePath, "utf-8");
    const dataObj = JSON.parse(fileData);

    // Hozzáadjuk az új tranzakciót
    dataObj.transactions.push(newTransaction);

    // Frissített adatok visszaírása a fájlba
    fs.writeFileSync(filePath, JSON.stringify(dataObj, null, 2), "utf-8");

    // Sikeres visszajelzés küldése
    res.json({ status: "success", message: "Tranzakció rögzítve" });
  } catch (error) {
    console.error("Hiba a tranzakció mentésekor:", error);
    res.status(500).json({ status: "error", message: "Szerver hiba történt" });
  }
});

app.listen(PORT, () => {
  console.log("Szerver fut a http://localhost:" + PORT + " címen");
});
```

> `transactions.json`

```json
{
  "transactions": []
}
```

### ❗TESZTELÉS❗

**Hozd létre az alábbi bejegyzést!**

**Ügyfél neve:** `Kiss Béla` 
**Számlaszám:** ˛`BANK0001 CUST0001 ACCT0001` 
**Kívánt összeg:** `5500`


---

## 3️⃣ Projekt: **Inkasszó kezelő rendszer**  
`debt-app/`

### 📁 Mappaszerkezet

```bash
debt-app/
├── server.js
├── bank.json
└── public/
    ├── index.html
    ├── style.css
    └── script.js
```

### ⚙️ Funkciók

| Endpoint      | Metódus   | Cél                           |
|---------------|-----------|--------------------------------|
| `/api/inkasso`  | `DELETE`  | Inkasszó levétele a számláról |

### 🧩 PROJEKT FILEOK

> `public/index.html`

```js
<!DOCTYPE html>
<html lang="hu">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Banki Inkasszó Törlése</title>
  <link rel="stylesheet" href="style.css">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap">
</head>
<body>
  <div class="page-container">
    <div class="form-container">
      <div class="form-header">
        <div class="logo">
          <div class="logo-icon">
            <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="logo-svg">
              <path d="M3 21H21M3 18H21M5 18V10M19 18V10M12 18V10M12 7H19C19.5523 7 20 6.55228 20 6V4C20 3.44772 19.5523 3 19 3H5C4.44772 3 4 3.44772 4 4V6C4 6.55228 4.44772 7 5 7H12Z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </div>
          <span>Big Business Bank</span>
        </div>
        <h1>Inkasszó törlése</h1>
        <p class="subtitle">Kérjük, adja meg az alábbi adatokat a törléshez</p>
      </div>

      <div class="alert-box">
        <svg class="alert-icon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M12 9V11M12 15H12.01M5.07183 19H18.9282C20.4678 19 21.4301 17.3333 20.6603 16L13.7321 4C12.9623 2.66667 11.0378 2.66667 10.268 4L3.33978 16C2.56998 17.3333 3.53223 19 5.07183 19Z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
        <div class="alert-content">
          <h3>Figyelem!</h3>
          <p>Az inkasszó törlése végleges művelet, amely nem vonható vissza.</p>
        </div>
      </div>

      <form class="deletion-form">
        <div class="form-group">
          <label for="accountNumber">Számlaszám</label>
          <div class="input-container">
            <svg class="input-icon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M3 10H21M7 15H8M12 15H13M17 15H18M5 19H19C20.1046 19 21 18.1046 21 17V7C21 5.89543 20.1046 5 19 5H5C3.89543 5 3 5.89543 3 7V17C3 18.1046 3.89543 19 5 19Z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            <input type="text" id="accountNumber" placeholder="Add meg a számlaszámot">
          </div>
        </div>

        <div class="form-group">
          <label for="inkassoId">Inkasszó azonosító</label>
          <div class="input-container">
            <svg class="input-icon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M9 14L15 8M10 8H15V13M21 12C21 16.9706 16.9706 21 12 21C7.02944 21 3 16.9706 3 12C3 7.02944 7.02944 3 12 3C16.9706 3 21 7.02944 21 12Z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            <input type="text" id="inkassoId" placeholder="Pl. INK001">
          </div>
        </div>

        <button id="deleteButton" type="button" class="delete-button">
          <svg class="button-icon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M19 7L18.1327 19.1425C18.0579 20.1891 17.187 21 16.1378 21H7.86224C6.81296 21 5.94208 20.1891 5.86732 19.1425L5 7M10 11V17M14 11V17M15 7V4C15 3.44772 14.5523 3 14 3H10C9.44772 3 9 3.44772 9 4V7M4 7H20" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <span>Inkasszó törlése</span>
        </button>
      </form>

      <div class="form-footer">
        <p>A művelet végrehajtásához szükséges jogosultságok ellenőrzése megtörténik</p>
      </div>
    </div>
  </div>
  <script src="script.js"></script>
</body>
</html>
```

> `public/style.css`

```css
:root {
    --primary-color: #0a1681;
    --primary-light: #e6f0ff;
    --primary-dark: #003d99;
    --danger-color: #d63031;
    --danger-light: #ffebee;
    --danger-dark: #b71c1c;
    --warning-color: #ff9800;
    --warning-light: #fff3e0;
    --text-color: #333;
    --text-light: #666;
    --background-color: #161d18;
    --white: #ffffff;
    --border-color: #e1e5eb;
    --shadow-sm: 0 2px 4px rgba(0, 0, 0, 0.05);
    --shadow-md: 0 4px 8px rgba(0, 0, 0, 0.1);
    --shadow-lg: 0 8px 16px rgba(0, 0, 0, 0.1);
    --radius-sm: 4px;
    --radius-md: 8px;
    --radius-lg: 12px;
  }
  
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  body {
    font-family: "Poppins", sans-serif;
    background-color: var(--background-color);
    color: var(--text-color);
    line-height: 1.6;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .page-container {
    width: 100%;
    max-width: 1200px;
    padding: 20px;
  }
  
  .form-container {
    background-color: var(--white);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-lg);
    overflow: hidden;
    width: 100%;
    max-width: 500px;
    margin: 0 auto;
    position: relative;
  }
  
  .form-header {
    padding: 30px 30px 20px;
    text-align: center;
    background: linear-gradient(135deg, var(--primary-color), var(--primary-dark));
    color: var(--white);
  }
  
  .logo {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 20px;
    font-weight: 600;
    font-size: 20px;
  }
  
  .logo-icon {
    width: 32px;
    height: 32px;
    background-color: var(--white);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-right: 10px;
  }
  
  .logo-svg {
    width: 20px;
    height: 20px;
    color: var(--primary-color);
  }
  
  h1 {
    font-size: 24px;
    font-weight: 600;
    margin-bottom: 8px;
  }
  
  .subtitle {
    font-size: 14px;
    opacity: 0.9;
    margin-bottom: 10px;
  }
  
  .alert-box {
    margin: 20px 30px 0;
    padding: 15px;
    background-color: var(--danger-light);
    border-radius: var(--radius-md);
    display: flex;
    align-items: flex-start;
    border-left: 4px solid var(--danger-color);
  }
  
  .alert-icon {
    width: 24px;
    height: 24px;
    color: var(--danger-color);
    margin-right: 12px;
    flex-shrink: 0;
  }
  
  .alert-content {
    flex: 1;
  }
  
  .alert-content h3 {
    font-size: 16px;
    color: var(--danger-dark);
    margin-bottom: 4px;
  }
  
  .alert-content p {
    font-size: 13px;
    color: var(--text-color);
  }
  
  .deletion-form {
    padding: 20px 30px 30px;
  }
  
  .form-group {
    margin-bottom: 24px;
  }
  
  label {
    display: block;
    font-size: 14px;
    font-weight: 500;
    margin-bottom: 8px;
    color: var(--text-color);
  }
  
  .input-container {
    position: relative;
  }
  
  .input-icon {
    position: absolute;
    left: 12px;
    top: 50%;
    transform: translateY(-50%);
    width: 20px;
    height: 20px;
    color: var(--text-light);
  }
  
  input {
    width: 100%;
    padding: 12px 12px 12px 44px;
    border: 1px solid var(--border-color);
    border-radius: var(--radius-md);
    font-size: 15px;
    transition: all 0.3s ease;
    background-color: var(--white);
    color: var(--text-color);
    font-family: "Poppins", sans-serif;
  }
  
  input:focus {
    outline: none;
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgba(0, 82, 204, 0.15);
  }
  
  input::placeholder {
    color: #aab;
  }
  
  .delete-button {
    width: 100%;
    padding: 14px 20px;
    background: linear-gradient(135deg, var(--danger-color), var(--danger-dark));
    color: var(--white);
    border: none;
    border-radius: var(--radius-md);
    font-size: 16px;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: var(--shadow-sm);
    margin-top: 10px;
  }
  
  .delete-button:hover {
    background: linear-gradient(135deg, var(--danger-dark), var(--danger-color));
    box-shadow: var(--shadow-md);
    transform: translateY(-1px);
  }
  
  .delete-button:active {
    transform: translateY(1px);
    box-shadow: var(--shadow-sm);
  }
  
  .button-icon {
    width: 18px;
    height: 18px;
    margin-right: 8px;
    color: var(--white);
  }
  
  .form-footer {
    padding: 15px 30px;
    background-color: var(--primary-light);
    text-align: center;
    font-size: 13px;
    color: var(--primary-dark);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  /* Responsive adjustments */
  @media (max-width: 576px) {
    .form-container {
      border-radius: 0;
      box-shadow: none;
    }
  
    .page-container {
      padding: 0;
    }
  
    .form-header {
      padding: 25px 20px 15px;
    }
  
    .deletion-form {
      padding: 20px;
    }
  
    .alert-box {
      margin: 20px 20px 0;
    }
  
    h1 {
      font-size: 22px;
    }
  }
  
  /* Animation for form elements */
  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(10px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  .alert-box {
    animation: fadeIn 0.4s ease-out forwards;
  }
  
  .form-group {
    animation: fadeIn 0.4s ease-out forwards;
  }
  
  .form-group:nth-child(1) {
    animation-delay: 0.1s;
  }
  
  .form-group:nth-child(2) {
    animation-delay: 0.2s;
  }
  
  .delete-button {
    animation: fadeIn 0.4s ease-out forwards;
    animation-delay: 0.3s;
  }
  
  /* Delete button pulse animation */
  @keyframes pulse {
    0% {
      box-shadow: 0 0 0 0 rgba(214, 48, 49, 0.4);
    }
    70% {
      box-shadow: 0 0 0 10px rgba(214, 48, 49, 0);
    }
    100% {
      box-shadow: 0 0 0 0 rgba(214, 48, 49, 0);
    }
  }
  
  .delete-button {
    animation: pulse 2s infinite;
  }
  
  .delete-button:hover {
    animation: none;
  }
  
```

> `public/script.js`

```js
document.getElementById("deleteButton").addEventListener("click", () => {

    const accountNumber = document.getElementById("accountNumber").value;
    const inkassoId = document.getElementById("inkassoId").value;
  

    const deleteData = { accountNumber, inkassoId };
  
      // küld el a szervernek a kérést és a bekért adatokat
  
      // kapd el a szerver válaszát
    
      // console logban jelenjen meg a szerver válasza: "Szerver válasza:" ...
      // alert formájában jelenjen ez meg: "Az inkasszó sikeresen eltávolítva."

  
      // hiba esetén: "Hiba történt:" ...
      // Hiba esetén jelenjen meg ez az alert: "Hiba történt a küldés során!"
  });
  
```

> `server.js`

```js
const express = require("express");
const fs = require("fs");
const path = require("path");

const app = express();
const PORT = 3003;

// JSON body parser
app.use(express.json());

// Statikus fájlok kiszolgálása a public mappából
app.use(express.static("public"));

// DELETE végpont a banki inkasszó törléséhez
// A törlés a megadott számlaszám és inkasszó azonosító alapján történik
app.delete("/api/inkasso", (req, res) => {
  try {
    // A törlendő adatok kinyerése: accountNumber és inkassoId
    const { accountNumber, inkassoId } = req.body;

    // A bank.json fájl aktuális tartalmának beolvasása
    const filePath = path.join(__dirname, "bank.json");
    const jsonData = fs.readFileSync(filePath, "utf-8");
    const dataObj = JSON.parse(jsonData);

    let accountFound = false;
    let inkassoDeleted = false;

    // Az accounts tömbben megkeressük a megfelelő számlát és eltávolítjuk a kívánt inkasszó rekordot
    dataObj.accounts = dataObj.accounts.map(account => {
      if (account.accountNumber === accountNumber) {
        accountFound = true;
        const initialCount = account.inkasszok.length;
        // A törlés: kiszűrjük a megadott inkasszó azonosítójú rekordot
        account.inkasszok = account.inkasszok.filter(inkasso => inkasso.id !== inkassoId);
        if (account.inkasszok.length < initialCount) {
          inkassoDeleted = true;
        }
      }
      return account;
    });

    // Ha nem található a számlaszám
    if (!accountFound) {
      return res.status(404).json({ status: "error", message: "Nincs ilyen számlaszám" });
    }

    // Ha a számlán nem volt ilyen inkasszó rekord
    if (!inkassoDeleted) {
      return res.status(404).json({ status: "error", message: "Nem található ilyen inkasszó rekord" });
    }

    // További lépés: eltávolítjuk azokat a számlákat, amelyekhez már nem tartozik inkasszó rekord
    dataObj.accounts = dataObj.accounts.filter(account => account.inkasszok.length > 0);

    // A frissített objektum visszaírása a bank.json fájlba
    fs.writeFileSync(filePath, JSON.stringify(dataObj, null, 2), "utf-8");

    // Visszaküldjük a sikeres törlésről szóló visszajelzést
    res.json({ status: "success", message: "Inkasszó törölve, üres számlák eltávolítva" });
  } catch (error) {
    console.error("Hiba az inkasszó törlésekor:", error);
    res.status(500).json({ status: "error", message: "Szerver hiba történt" });
  }
});

// Szerver indítása a megadott porton
app.listen(PORT, () => {
  console.log(`Szerver fut a http://localhost:${PORT} címen`);
});

```

> `bank.json`

```json
{
    "accounts": [
      {
        "customerName": "Kiss József",
        "accountNumber": "BANK0001 CUST0001 ACCT0001",
        "inkasszok": [
          { "id": "INK001", "description": "Havi díj levonása", "amount": 50 },
          { "id": "INK002", "description": "Hitelinkasszó", "amount": 150 }
        ]
      },
      {
        "customerName": "Németh Ágnes",
        "accountNumber": "BANK0002 CUST0002 ACCT0002",
        "inkasszok": [
          { "id": "INK003", "description": "Biztosítási díj", "amount": 70 }
        ]
      },
      {
        "customerName": "Tóth István",
        "accountNumber": "BANK0003 CUST0003 ACCT0003",
        "inkasszok": [
          { "id": "INK004", "description": "Szerviz költség", "amount": 120 }
        ]
      }
    ]
  }
  
```


### ❗TESZTELÉS❗

**Töröld az alábbi bejegyzést!**

**Számlaszám:** `BANK0002 CUST0002 ACCT0002`
**Inkasszó azonosító:** `INK003`

---

## ⚙️ szerver beállítása minden projektnél

> **Minden projektnél külön-külön létre kell hozni**
> **Az elkészült mappaszerkezet  és fájlok létrehozását követően**, nyisd meg a gyökérmappát terminálban (jobb katt > *Open in Terminal*), és futtasd az alábbi parancsokat:


### 1. Inicializálás

```bash
npm init -y
```

### 2. Express telepítése

```bash
npm install express
```

### 3. Szerver indítása

```bash
node server.js
```

## ❤️Segédanyag❤️

```js
fetch('URL', {
  method: '...',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(...)
})
.then(a => a.json())
.then(b => {})
.catch(c => {});
```

---

## ✅ Ellenőrzőlista a leadás előtt

- [ ] Helyes mappanév (pl. `kissbela/`)
- [ ] Mindhárom alkalmazás mappa létrehozva
- [ ] Minden app a leírt mappanevet, aleretet, console logot, filenevet tartalmazza,
- [ ] REST API működik (GET, POST, DELETE)
- [ ] Böngészőben futtathatóak az oldalak
- [ ] Gombnyomásra működnek a fetch hívások
- [ ] Változások elmentődnek a JSON fájlba
- [ ] Tesztek elvégezve a feladat leírás alapján.

---

## 📦 Leadás

- Tömörítsd az egész névvel ellátott mappát (`kissbela.zip`)
- Küldd be az instrukciók szerint a közös beadási mappába


