# JR Ticket Order Form Generator

A browser-based tool for [Cocolo Travel](https://cocolo-travel.com) to generate JR seat reservation order forms (PDF) for multiple customers in one session.

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
Jour N YYYY-MM-DD Depart de [Station] à HH:MM Arrivée à HH:MM à [Station]
```

Example:

```text
Jour 6 2026-05-09 Depart de Shinjuku à 09:30 Arrivée à 11:28 à Kawaguchiko
Jour 7 2026-05-10 Depart de Kawaguchiko à 08:23 Arrivée à 09:10 à Otsuki
```

Stations not found in the built-in list are flagged with a warning but still included in the form.

## Dependencies (CDN, no install needed)

| Library | Version | Purpose |
| --- | --- | --- |
| [jsPDF](https://github.com/parallax/jsPDF) | 2.5.1 | PDF generation |
| [html2canvas](https://html2canvas.hertzen.com) | 1.4.1 | Form rendering to canvas |

## Browser support

Any modern browser with `localStorage` and Canvas support (Chrome, Firefox, Edge, Safari).
