# moduLive AR Vizualizace – Návod

## 📱 Co aplikace umí

- Přihlášení pro makléře (zabezpečeno přes Supabase)
- Výběr domu z galerie (6 modelů)
- AR zobrazení na Android i iOS zařízeních
- Ovládání: otáčení, změna velikosti

---

## 🚀 NASAZENÍ NA WEB

### Krok 1: Vytvoř účet na Supabase

1. Jdi na **https://supabase.com**
2. Klikni "Start your project" → přihlas se přes GitHub
3. Klikni "New Project"
4. Vyplň:
   - Name: `modulive-ar`
   - Database Password: vymysli silné heslo (ulož si ho!)
   - Region: Frankfurt (nejbližší)
5. Klikni "Create new project"
6. Počkej 1-2 minuty než se projekt vytvoří

### Krok 2: Získej API klíče

1. V Supabase dashboardu jdi do **Settings** (ozubené kolečko vlevo dole)
2. Klikni na **API**
3. Najdeš tam:
   - **Project URL** (např. `https://xxxxx.supabase.co`)
   - **anon public key** (dlouhý řetězec)
4. Obě hodnoty si zkopíruj

### Krok 3: Vlož API klíče do aplikace

1. Otevři soubor `index.html` v textovém editoru
2. Najdi řádky (cca řádek 340):
   ```javascript
   const SUPABASE_URL = 'YOUR_SUPABASE_URL';
   const SUPABASE_ANON_KEY = 'YOUR_SUPABASE_ANON_KEY';
   ```
3. Nahraď je svými hodnotami:
   ```javascript
   const SUPABASE_URL = 'https://xxxxx.supabase.co';
   const SUPABASE_ANON_KEY = 'tvuj_anon_key_zde';
   ```
4. Ulož soubor

### Krok 4: Nastav přihlašování v Supabase

1. V Supabase jdi do **Authentication** (vlevo)
2. Klikni na **Providers**
3. Ujisti se že **Email** je zapnutý
4. V sekci **Email Auth** vypni "Confirm email" (pro jednoduchost)

### Krok 5: Přidej prvního uživatele

1. V Supabase jdi do **Authentication** → **Users**
2. Klikni "Add user" → "Create new user"
3. Vyplň:
   - Email: `makler1@modulive.local` (nebo jakýkoliv jiný)
   - Password: heslo pro makléře
4. Klikni "Create user"
5. Opakuj pro další makléře

**Poznámka:** Email nemusí být skutečný – slouží jako uživatelské jméno.

### Krok 6: Nahraj na GitHub

1. Jdi na **https://github.com** (vytvoř účet pokud nemáš)
2. Klikni "+" → "New repository"
3. Pojmenuj: `modulive-ar`
4. Nech "Public" nebo vyber "Private"
5. Klikni "Create repository"
6. Nahraj všechny soubory ze složky `ar-modulive`:
   - Klikni "uploading an existing file"
   - Přetáhni soubory (index.html, models/)
   - Klikni "Commit changes"

### Krok 7: Nasaď na Render

1. Jdi na **https://render.com** (přihlas se přes GitHub)
2. Klikni "New" → "Static Site"
3. Propoj svůj GitHub repozitář `modulive-ar`
4. Vyplň:
   - Name: `modulive-ar`
   - Build Command: nech prázdné
   - Publish Directory: `.`
5. Klikni "Create Static Site"
6. Za pár minut dostaneš odkaz (např. `https://modulive-ar.onrender.com`)

### Krok 8: Vlastní doména (volitelné)

1. V Render jdi do nastavení tvého webu
2. Klikni "Custom Domains"
3. Přidej svou doménu (např. `ar.modulive.cz`)
4. Render ti ukáže DNS záznamy – nastav je u svého registrátora

---

## 👥 SPRÁVA UŽIVATELŮ

### Přidání nového makléře

1. Jdi do Supabase → Authentication → Users
2. Klikni "Add user" → "Create new user"
3. Zadej email (např. `novak@modulive.local`) a heslo
4. Hotovo – makléř se může přihlásit

### Smazání makléře

1. Jdi do Supabase → Authentication → Users
2. Najdi uživatele
3. Klikni na tři tečky → "Delete user"

### Změna hesla

1. Jdi do Supabase → Authentication → Users
2. Najdi uživatele
3. Klikni na tři tečky → "Send password recovery"
   (nebo smaž a vytvoř znovu s novým heslem)

---

## 🏠 PŘIDÁNÍ 3D MODELŮ

### Co potřebuješ od projektanta

**Pro Android:** soubory `.glb` (GLB/GLTF formát)
**Pro iOS:** soubory `.usdz` (Apple formát)

Každý dům potřebuje oba formáty pro plnou kompatibilitu.

### Jak přidat modely

1. Přejmenuj soubory:
   - `house1.glb`, `house1.usdz`
   - `house2.glb`, `house2.usdz`
   - atd.

2. Nahraj do složky `models/` na GitHubu:
   - Jdi do repozitáře
   - Otevři složku `models`
   - Klikni "Add file" → "Upload files"
   - Přetáhni soubory
   - Klikni "Commit changes"

3. Render automaticky aktualizuje web (1-2 minuty)

### Úprava názvů domů

V souboru `index.html` najdi sekci `const houses = [` a uprav:

```javascript
{
    id: 1,
    name: "Dům Marian",        // ← název domu
    area: "120 m²",            // ← plocha
    rooms: "4+1",              // ← dispozice
    modelGLB: "models/house1.glb",
    modelUSDZ: "models/house1.usdz",
    thumbnail: null
},
```

---

## ⚠️ PODPOROVANÁ ZAŘÍZENÍ

| Zařízení | Prohlížeč | Podpora |
|----------|-----------|---------|
| Android telefon | Chrome | ✅ Plná (WebXR) |
| iPhone | Safari | ✅ Plná (AR Quick Look) |
| iPad | Safari | ✅ Plná (AR Quick Look) |
| Desktop | Jakýkoliv | ⚠️ Pouze galerie, ne AR |

---

## 🔧 ŘEŠENÍ PROBLÉMŮ

### "Nesprávné přihlašovací údaje"
- Zkontroluj, že uživatel existuje v Supabase
- Zkontroluj správnost hesla
- Zkontroluj že v index.html jsou správné API klíče

### AR nefunguje na Android
- Musíš používat Chrome
- Telefon musí podporovat ARCore
- Musíš povolit přístup ke kameře

### AR nefunguje na iOS
- Potřebuješ soubory .usdz
- Safari musí být aktuální verze

### Model se nezobrazuje
- Zkontroluj že soubor existuje v models/
- Zkontroluj název souboru (malá/velká písmena)
- Zkus model otevřít na https://gltf-viewer.donmccurdy.com

---

## 📞 STRUKTURA PROJEKTU

```
ar-modulive/
├── index.html          # Hlavní aplikace
├── NAVOD.md           # Tento návod
└── models/
    ├── README.md      # Info o modelech
    ├── house1.glb     # Model pro Android
    ├── house1.usdz    # Model pro iOS
    └── ...
```

---

*© 2026 moduLive*
