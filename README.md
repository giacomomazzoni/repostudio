# RepoStudio

Sito marketing e blog report per RepoStudio — servizio italiano di ricerche AI per PMI e professionisti.

**Stack:** Astro 4 · CSS vanilla · deploy su Cloudflare Pages

---

## Setup locale

```bash
npm install
npm run dev      # dev server su http://localhost:4321
npm run build    # build in /dist
npm run preview  # preview build locale
```

---

## Aggiungere un nuovo report

1. Crea un file `.md` in `src/pages/report/`, es. `mio-report.md`
2. Copia il frontmatter da un report esistente e adattalo:

```yaml
---
layout: ../../layouts/Report.astro
title: "Titolo del report"
description: "Descrizione breve per SEO e card."
date: "2026-11-01"
category: "Brief Immobiliare"
zona: "Genova"
slug: "mio-report"
published: true
keyNumbers:
  - num: "+3,2%"
    label: "Descrizione del numero"
  - num: "1.500 €/m²"
    label: "Altra metrica"
  - num: "2,5%"
    label: "Terza metrica"
---
```

3. Scrivi il corpo del report in Markdown
4. Per i callout, usa le classi HTML inline:
   - `<div class="callout-warn">...</div>` — avviso giallo
   - `<div class="callout-info">...</div>` — info viola chiaro

Il report compare automaticamente nella griglia di `/report/`.

Per nascondere un draft senza eliminarlo: `published: false`

---

## Deploy su Cloudflare Pages

1. Connetti il repo GitHub a Cloudflare Pages
2. Impostazioni build:
   - **Build command:** `npm run build`
   - **Build output directory:** `dist`
   - **Node version:** 18+
3. Nessuna variabile d'ambiente richiesta

---

## Aggiornare SLOTS ogni lunedì

In `src/pages/index.astro`, riga 5:

```js
const SLOTS = 4;  // ← aggiorna questo numero ogni lunedì
```

Il numero appare nel banner top, nella hero e nella scarcity box. Basta aggiornare questo valore e fare deploy.

---

## Sostituire il link del form

Cerca `YOUR_FORM_LINK_HERE` in:

- `src/layouts/Base.astro` (usato in nav e banner)
- `src/layouts/Report.astro` (CTA inline e footer)
- `src/pages/index.astro` (tutti i bottoni CTA)
- `src/pages/report/index.astro` (CTA banner)

Sostituisci con il link al tuo form (Typeform, Tally, Google Forms, ecc.).

---

## Struttura progetto

```
src/
  layouts/
    Base.astro        ← nav, footer, SEO head
    Report.astro      ← layout pagine report
  pages/
    index.astro       ← landing page
    report/
      index.astro     ← griglia report
      *.md            ← singoli report
  styles/
    global.css        ← variabili CSS e stili globali
public/
  favicon.svg
```
