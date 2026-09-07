# Swiss Calendar Creator

Parametric calendar generator in the **International Typographic Style** (Swiss design): strict grid, flush-left sans-serif, hairline rules, generous white space, one accent ink.

Available as a **web app** and an **Affinity (by Canva) script** — same drawing engine, two environments.

**[→ Open web app](https://3dvic.com/apps/swiss-calendar-creator/)** · **[Article & context](https://3dvic.com/work/swiss-calendar-creator)**

Third tool in the *Swiss ___* family, alongside [Swiss Grid Explorer](https://github.com/vicc3d/swiss-grid-explorer).

---

## Platforms

| Platform | File | Requires |
|---|---|---|
| Web | `web-app/index.html` | Any browser — no install, no build |
| Affinity | `affinity-script/swiss_calendar_creator.js` | Affinity (April 2026+) with MCP |

**Current versions:** Web app `v1.0` · Affinity script `v1.0`

---

## Views

| View | What it draws |
|---|---|
| **Year** | 12 mini-months in a 4 × 3 grid |
| **Month** | The month grid, optional week-number column (ISO 8601 or "from 1"), dimmed adjacent-month days |
| **Week** | 7 columns with the date range and week number |
| **Day** | A single day with hour slots; the layout adapts to the canvas proportion — landscape puts the date on the left and the hours on the right, portrait stacks everything |

---

## Web App

Open `web-app/index.html` in any browser. No dependencies, no build step, no server.

- Live SVG preview
- 11 document formats (A2–A5, US Letter/Tabloid, poster, square, 16:9, 9:16, screen) + custom size, 5 units
- Editable title / subtitle (auto-generated when left empty)
- Week starts Monday or Sunday · ISO 8601 or "from 1" week numbering
- Toggle: weekday header, grid rules, vertical lines, adjacent months, week numbers, bold weekends, accent bar, "mark today"
- Day-view agenda: hour range, 12 h / 24 h labels
- **Per-country national holidays** — UY, AR, CL, CO, MX, PE, ES, US — with Easter and other movable feasts computed. Approximate; editable
- **Per-date notes** you add yourself, optionally highlighted as holidays
- Style: typeface, ink / accent / rule / dimmed / paper colors
- Export **SVG** with named layer groups (Illustrator / Affinity / Inkscape), or **PNG** to share (2× for px formats, 150 dpi for physical ones)
- Import / export settings as JSON
- Bilingual (ES / EN) — interface *and* calendar content

No PDF — deliberately, to keep the same zero-dependency footprint as *Swiss Grid Explorer*. The PNG is rasterised through a `<canvas>`, still no libraries.

---

## Affinity Script

`affinity-script/swiss_calendar_creator.js` — a single bilingual file (EN + ES), no dependencies. Carries the JSDoc header the **Affinity Script Manager** reads (`name` / `description` / `version` / `author` / `license`).

**Install:** open Affinity (Designer, Publisher or Photo, April 2026+), enable MCP in **Settings → AI / MCP**, and either add the file through the Script Manager or ask your AI assistant to push it via `save_script_to_library`. Library scripts appear after an Affinity restart.

**Use:** select an **artboard** (the calendar fills it) or a **rectangle / frame inside one** (the calendar fills that box), then run the script. Pick the language, then the view and settings. The result lands in one container layer named e.g. `Calendar · Month 2026 · September`.

The dialog has two columns of collapsible sections: view + date + agenda on the left, elements + style on the right. Every control has a tooltip on its label.

---

## One engine, two platforms

The four view functions — `drawYear`, `drawMonth`, `drawWeek`, `drawDay` — take an area `{x, y, w, h}` and a config object, and every mark is one of five primitives: `rect`, `rule`, `vrule`, `text`, `richText`. The date math (`daysInMonth`, `columnOf`, `isoWeek`, `sameDay`) and the ISO / "from 1" week numbering are identical on both platforms.

Porting to the web meant reimplementing the five primitives over `<rect>` / `<text>` instead of Affinity nodes. The Year and Month layouts are unchanged. Week and Day were reworked to **fill the canvas at any proportion** — on the web the user only controls the sheet, not a selection box, so the week becomes 7 full-height columns and the day fills its empty zone with writing lines instead of leaving it blank.

---

## SVG Output

```xml
<svg xmlns="http://www.w3.org/2000/svg"
     xmlns:inkscape="http://www.inkscape.org/namespaces/inkscape"
     width="210mm" height="297mm" viewBox="0 0 210 297">
  <g class="paper"    inkscape:groupmode="layer" inkscape:label="Paper">…</g>
  <g class="calendar" inkscape:groupmode="layer" inkscape:label="Calendar">…</g>
</svg>
```

---

## Repository Structure

```
swiss-calendar-creator/
├── README.md
├── LICENSE
├── web-app/
│   └── index.html                 ← Web app (v1.0)
└── affinity-script/
    └── swiss_calendar_creator.js  ← Affinity script (v1.0)
```

---

## Credits

**Concept, UX/UI & Design** — [Victor Crespo](https://3dvic.com)

Bundled holiday lists are national and approximate — always check them against current legislation.

Released under the [MIT License](LICENSE).
