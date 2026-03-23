# Task Dashboard

## Kde dashboard spravovat

- Otevri `task-dashboard.html` v Cursoru.
- Cokoli upravis a ulozis (`Ctrl+S`), projevi se po obnove stranky v prohlizeci (`F5`).
- Data ukolu se ukladaji lokalne v prohlizeci (`localStorage`), ne do souboru automaticky.

## Jak naplnit dashboard ukoly

- V hornim formulari vypln:
  - nazev ukolu
  - prioritu
  - stav
  - termin
- Klikni na `Pridat ukol`.
- U Kanban pohledu muzes ukol pretahnout mezi sloupci.

## Jak udelat zalohu do CSV

- Klikni na `Export CSV`.
- Soubor se stahne do slozky Downloads (nebo podle nastaveni prohlizece).
- Obnoveni zalohy: `Import CSV` a vyber soubor.

## GitHub Pages (publikace webu)

1. Vytvor novy prazdny repozitar na GitHubu.
2. V terminalu na plose spust:

```bash
git init
git add "task-dashboard.html" "index.html" "README-task-dashboard.md"
git commit -m "Add task dashboard"
git branch -M main
git remote add origin <TVUJ_GITHUB_REPO_URL>
git push -u origin main
```

3. Na GitHubu:
   - `Settings` -> `Pages`
   - `Source`: `Deploy from a branch`
   - Branch: `main`, folder: `/ (root)`
   - `Save`

4. URL bude ve tvaru:
   - `https://<username>.github.io/<repo>/`

## Poznamka k ulozeni dat

- Na GitHub Pages se ukoly porad ukladaji jen v prohlizeci daneho zarizeni.
- Pro prenos mezi zarizenimi pouzij vzdy `Export CSV` a pak `Import CSV`.
