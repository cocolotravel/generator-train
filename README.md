# JR Ticket Order Form Generator

A browser-based tool for [COCOLO Travel](https://cocolo-travel.com) to generate JR seat reservation order forms (PDF) for multiple customers in one session.

The UI follows the COCOLO Travel design system — Washi/Millennium Washi surfaces, Sumi text, a Kin accent, Roslindale for the title, Inter for the interface — while the generated order form itself keeps the plain black-and-white layout expected by JR staff.

## Features

- **Multi-customer support** — manage several customers simultaneously via tabs
- **Train data parsing** — paste itinerary lines and parse them automatically into structured legs
- **Live PDF preview** — see the formatted reservation form before downloading
- **Batch PDF export** — download PDFs for all customers at once
- **Session persistence** — data is saved to `localStorage` so it survives page refreshes
- **Station translation** — converts English station names to Japanese automatically

## Usage

1. Open `index.html` in any modern browser (no server required)
2. Click **＋** to add a customer and enter their name
3. Paste their itinerary into the **Train Data** textarea using the format below
4. Click **▶ Parse trains** to generate the form preview
5. Click **⬇ Download PDF** to save the form, or **⬇ Download All PDFs** to export every customer at once

### Input format

Each line must follow this pattern:

```text
Jour N YYYY-MM-DD Depart de [Station] à HH:MM Arrivée à HH:MM à [Station] avec [Line] sur [Train]
```

The `avec [Line] sur [Train]` suffix is optional. When present:

- Lines marked `avec JR` are kept; the train name/number (e.g. `Kodama 813`) is written into the **TRAIN NAME AND NUMBER** column.
- Lines with any other operator (e.g. `avec Tozan`) are filtered out — this form covers JR tickets only.
- Lines with no `avec` suffix are always included with the train column left blank.

Example:

```text
Jour 6 2026-04-27 Depart de Tokyo à 09:27 Arrivée à 10:00 à Odawara avec JR sur Kodama 813
Jour 6 2026-04-27 Depart de Odawara à 10:07 Arrivée à 10:22 à Hakone-Yumoto avec Tozan
Jour 7 2026-04-28 Depart de Hakone-Yumoto à 09:24 Arrivée à 09:38 à Odawara avec Tozan
Jour 7 2026-04-28 Depart de Odawara à 10:11 Arrivée à 12:12 à Kyoto avec JR sur Hikari 637
```

In the example above, the two `avec Tozan` legs are filtered out and only the two JR legs appear in the form.

Stations not found in the built-in list are flagged with a warning but still included in the form.

## Dependencies (CDN, no install needed)

| Library | Version | Purpose |
| --- | --- | --- |
| [jsPDF](https://github.com/parallax/jsPDF) | 2.5.1 | PDF generation |
| [html2canvas](https://html2canvas.hertzen.com) | 1.4.1 | Form rendering to canvas |

Fonts (Inter from Google Fonts, Roslindale from `assets.cocolotravel.com`) and the COCOLO cloud logo (bundled under `assets/logos/`) are the only brand-specific assets — everything else is self-contained in `index.html`.

## Browser support

Any modern browser with `localStorage` and Canvas support (Chrome, Firefox, Edge, Safari).
