# Task Dashboard – CLAUDE.md

Projektová dokumentace pro Claude Code. Shrnutí všeho důležitého pro případ, že se sem vrátíš.

---

## Co je tento projekt

Jednoduchý osobní task-dashboard v jednom HTML souboru (`task-dashboard.html`).
Běží jako statická stránka na GitHub Pages:
**https://danielavokalova.github.io/task-dashboard/task-dashboard.html**

---

## Technologie

- Čisté HTML + CSS + JavaScript (žádný build krok, žádné závislosti)
- Chart.js (sloupcový/kruhový graf statistik) – CDN
- Supabase JS SDK – CDN (volitelný cloud sync)
- GitHub Gist API – záloha dat (fetch, bez knihoven)

---

## Struktura

```
task-dashboard.html   – hlavní soubor, vše v jednom
index.html            – přesměrování na task-dashboard.html
README.md             – základní popis repozitáře
README-task-dashboard.md – uživatelská dokumentace (česky)
CLAUDE.md             – tento soubor, pro Claude Code
```

---

## Jak data fungují

Úkoly se ukládají do `localStorage` prohlížeče pod klíčem `taskDashboardDataV2`.
Po každé změně se spustí:
1. `saveTasks()` → localStorage
2. `scheduleCloudSync()` → Supabase (pokud připojeno)
3. `scheduleGistBackup()` → GitHub Gist (pokud token uložen)

---

## GitHub Gist záloha – jak funguje

### Nastavení (jednorázové)
Token a Gist ID se předají přes URL hash – **nikdy nejsou uloženy ve zdrojovém kódu**:

```
https://danielavokalova.github.io/task-dashboard/task-dashboard.html#gist_token=<TOKEN>&gist_id=<GIST_ID>
```

Při prvním načtení stránka:
1. Přečte hash z URL
2. Uloží token + gist_id do `localStorage` (klíč `taskDashboardGistConfigV1`)
3. Smaže hash z URL (token není vidět v historii)

### Automatická záloha
- Po každé úpravě úkolu se do **2 sekund** pošle záloha na Gist (debounce)
- Gist je privátní, obsahuje soubor `tasks.json` se všemi úkoly + extras + časové razítko

### Obnova po výpadku
- Pokud je `localStorage` prázdný a token je uložen → data se automaticky obnoví z Gistu bez jakéhokoli klikání

### Kde jsou přihlašovací údaje Daniely
- Gist ID: `72e0ce64b565cb8b748722304953ce0e`
- Token: uložen pouze v `localStorage` prohlížeče (nikdy v kódu)
- Token má oprávnění pouze `gist` (minimální přístup)
- Pokud token expiruje nebo zmizí: vygenerovat nový na github.com → Settings → Developer settings → Personal access tokens → Tokens (classic) → scope: `gist`
- Pak otevřít setup URL výše s novým tokenem

---

## Supabase cloud sync (volitelný)

V dashboardu je tlačítko **Cloud připojení**. Pokud bude potřeba plný real-time sync mezi zařízeními, viz `README-task-dashboard.md` pro SQL setup v Supabase.

Aktuálně: **nepřipojeno** (stačí Gist záloha).

---

## Git workflow

Vývojová větev: `claude/fix-dashboard-sync-backup-Dur6i`
Produkce: `main` → automaticky nasazeno přes GitHub Pages

```bash
# Úpravy vždy commitovat a pushnout:
git add task-dashboard.html
git commit -m "Popis změny"
git push origin main
```

---

## Důležité poznámky

- **Neukládej token do zdrojového kódu** – GitHub Push Protection to zablokuje
- Soubor je velký (~96 KB) – při čtení přes API použij chunking
- `localStorage` je vázán na origin – `file://` a `https://` jsou různé origin
- GitHub Pages se aktualizuje do ~2–5 minut po pushnutí na main
