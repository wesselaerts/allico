# MCX Quiz Trainer — Setup & Deployment

Single-file HTML quiz app voor je ARM Cortex-M tentamen (HAN), met geïntegreerde datasheet PDF, AI grading, en cross-device sync via export/import.

## Bestanden

- `index.html` — de hele quiz app (~200 KB, logo en favicon zijn ingebakken)
- `MCXAP64M96FS3RM.pdf` — MCX A153 Reference Manual (~16 MB)
- `README.md` — dit bestand
- `mcx_logo.svg` / `mcx_logo_*.png` — optioneel, logo bestanden (al embedded in `index.html`)

---

## Lokaal gebruiken op je laptop

1. Zet `index.html` en `MCXAP64M96FS3RM.pdf` in dezelfde map.
2. Dubbelklik `index.html` — opent in je browser.
3. Klik op de groene 📄-knop rechtsonder → klik "Selecteer datasheet PDF" → kies `MCXAP64M96FS3RM.pdf` uit dezelfde map.
4. De PDF wordt in IndexedDB van je browser bewaard — volgende sessies hoef je hem niet meer te selecteren.

**Let op:** wanneer je het HTML-bestand lokaal opent via `file://`, blokkeren browsers vaak `fetch()` van relatieve URLs. Daarom werkt auto-load lokaal niet en moet je de PDF de eerste keer handmatig selecteren. Bij GitHub Pages (zie onder) gebeurt dat automatisch.

---

## Op je iPhone gebruiken (via GitHub Pages)

GitHub Pages is gratis statische hosting. Je krijgt een publieke URL die op elk apparaat werkt.

### Stappen:

1. **Maak een GitHub account** (als je er nog geen hebt) op github.com.
2. **Maak een nieuwe repository** — klik "+" rechtsboven → "New repository":
   - Naam: bijvoorbeeld `mcx-quiz`
   - Public ✅ (private vereist een betaalde Pro plan)
   - "Add a README" mag je aanvinken (we overschrijven dat).
   - Klik "Create repository".
3. **Upload de bestanden**:
   - Klik op "Add file" → "Upload files".
   - Sleep `index.html`, `MCXAP64M96FS3RM.pdf` (en optioneel deze README + logo's) erin.
   - Klik onderaan "Commit changes".
4. **Zet GitHub Pages aan**:
   - Ga naar Settings (tabblad bovenaan je repo) → Pages (linker menu).
   - Bij "Source" kies "Deploy from a branch".
   - Bij "Branch" kies `main` en map `/ (root)`.
   - Klik Save.
5. **Wacht ~30 seconden**, ververs de Pages instellingen-pagina. Je krijgt een URL te zien zoals:
   ```
   https://JOUW-USERNAME.github.io/mcx-quiz/
   ```
   Geen `index.html` op het eind nodig — GitHub Pages serveert hem automatisch.
6. **Open die URL** op je iPhone in Safari. De PDF wordt automatisch geladen (eerste keer ~10 sec, daarna gecached in IndexedDB).
7. **Voeg toe aan beginscherm**: in Safari klik op het deel-icoontje (vierkant met pijl omhoog) → "Voeg toe aan beginscherm". Nu heb je een app-icoontje met het MCX logo, en de app draait full-screen zonder Safari UI.

### iPhone tips
- Het PDF panel wordt full-screen op kleine schermen.
- De API key invullen werkt hetzelfde als op laptop — wordt in iPhone Safari's localStorage opgeslagen.
- Werkt ook offline na de eerste keer laden (zolang Safari de cache niet flusht).

---

## Stats syncen tussen laptop en iPhone (handmatig)

Localstorage is per apparaat, dus scores syncen niet automatisch. Dit is een eenvoudige workaround:

1. Op laptop: Dashboard → **Exporteer stats** → krijg een JSON bestand.
2. Stuur het bestand naar je iPhone via AirDrop, e-mail, of cloudopslag.
3. Op iPhone: Dashboard → **Importeer stats** → kies het JSON bestand → bevestig.

Doe dit een paar keer per week om je voortgang in sync te houden. (Echte automatische sync zou een backend-server vereisen — kan later toegevoegd worden met bv. Firebase of Supabase.)

---

## AI Settings (eenmalig)

Voor "Laat Claude beoordelen" en "Stel een vraag aan Claude":

1. Ga naar console.anthropic.com → maak een API key (begint met `sk-ant-`).
2. In de app: Dashboard → ⚙ AI Settings → plak je key → kies model (Haiku 4.5 is goedkoop en snel genoeg) → Opslaan.
3. Doe dit zowel op laptop als op iPhone (de key wordt per apparaat in localStorage opgeslagen).

Kosten met Haiku 4.5: paar tienden van een cent per beoordeling. Een hele examen-sessie kost een paar cent.

---

## Privacy & security

- API key: lokaal in je browser's `localStorage`, niet geüpload naar GitHub of waar dan ook. Wel zichtbaar voor iemand met fysieke browser-toegang via DevTools.
- Stats: lokaal in `localStorage`.
- PDF: lokaal in `IndexedDB`.
- Niets van dit alles staat in de bestanden die op GitHub komen — die zijn statisch en bevatten geen persoonlijke data.

Veel succes met je tentamen!
