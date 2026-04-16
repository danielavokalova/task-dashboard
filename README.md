# Task Dashboard – Daniela Vokálová

Osobní task-dashboard v jednom HTML souboru. Kanban + seznam, statistiky, automatická záloha na GitHub.

## Kde ho najdeš

**https://danielavokalova.github.io/task-dashboard/task-dashboard.html**

## Co umí

- Kanban board (K vyřízení / Rozpracované / Dokončené)
- Filtrování, řazení, vyhledávání
- Priority, termíny, produkty, typy požadavků
- Statistiky a grafy
- Export/Import CSV
- Automatická záloha na GitHub Gist po každé změně
- Obnova dat po výpadku proudu nebo restartu prohlížeče

## Záloha dat

Po výpadku (vypnutí PC, reset prohlížeče) se data obnoví automaticky z GitHubu.

Pokud záloha přestane fungovat (expirovaný token), vygeneruj nový na:
**github.com → Settings → Developer settings → Personal access tokens → Tokens (classic)**
→ scope: `gist` → pak otevři setup URL (viz CLAUDE.md).

## Technické detaily

Viz `CLAUDE.md` – dokumentace pro vývojáře / Claude Code.
