# DESIGN.md – Cicor Procurement Tools Design System

## Überblick

Alle Procurement Tools folgen einem einheitlichen Dark-Theme-Design.
Die Tools sind standalone HTML-Dateien, die im Browser laufen.
Das Design soll professionell, übersichtlich und SAP-nah wirken,
ohne auf ein UI-Framework angewiesen zu sein.


## Farbpalette

### Hintergrund & Layout
| Element | Farbe | Hex |
|---------|-------|-----|
| Body-Gradient Start/End | Dunkelblau | #0f172a |
| Body-Gradient Mitte | Schieferblau | #1e293b |
| Card/Box Hintergrund | Schieferblau transparent | rgba(30,41,59,0.7) |
| Card Border | Grau transparent | rgba(148,163,184,0.15) |
| Card Border Hover | Indigo transparent | rgba(99,102,241,0.5) |
| Input-Felder Hintergrund | Dunkelblau | #0f172a |
| Input-Felder Border | Grau transparent | rgba(148,163,184,0.3) |

### Text
| Element | Farbe | Hex |
|---------|-------|-----|
| Primärtext | Hellgrau | #e2e8f0 |
| Titel (h1) | Fast-Weiss | #f8fafc |
| Subtitel/Labels | Silbergrau | #94a3b8 |
| Sekundärtext/Hints | Mittelgrau | #64748b |
| Footer | Dunkelgrau | #475569 |

### Akzentfarben (Kategorien)
| Kategorie | Farbe | Hex | Hintergrund (KPI) | Hintergrund (Excel-Zeile) |
|-----------|-------|-----|-------------------|--------------------------|
| Einsparung / Positiv | Grün | #10b981 | rgba(16,185,129,0.08) | #E2EFDA |
| Mehrkosten / Negativ | Rot | #f87171 | rgba(248,113,113,0.08) | #FCE4EC |
| Erstbeschaffung | Amber | #f59e0b | rgba(245,158,11,0.08) | #FFF3E0 |
| Neutral | Grau | #64748b | – | #F2F2F2 |
| Ignoriert/Warnung | Gelb | #fbbf24 | rgba(251,191,36,0.08) | #FFF8E1 |
| Netto/Primärakzent | Indigo | #6366f1 | rgba(99,102,241,0.08) | – |

### Buttons
| Element | Farbe/Gradient |
|---------|---------------|
| Primär-Button (aktiv) | linear-gradient(135deg, #6366f1, #8b5cf6) |
| Primär-Button (inaktiv) | #334155 mit Text #64748b |
| Download-Button | Border #10b981, Background rgba(16,185,129,0.1) |
| Hover-Effekt | filter: brightness(1.1) bzw. Background-Aufhellung |

### Upload-Felder
| Zustand | Hintergrund | Border |
|---------|------------|--------|
| Leer | rgba(30,41,59,0.7) | rgba(148,163,184,0.15) |
| Hover | – | rgba(99,102,241,0.5) |
| Geladen (done) | rgba(16,185,129,0.08) | rgba(16,185,129,0.3) |
| Titel nach Upload | #10b981 |


## Typografie

| Element | Font | Grösse | Gewicht | Sonstiges |
|---------|------|--------|---------|-----------|
| Body | Segoe UI, Helvetica Neue, Arial | – | – | – |
| h1 Titel | – | 1.75rem | 700 | letter-spacing: -0.02em |
| Subtitel | – | 0.9rem | 400 | italic, Farbe #94a3b8 |
| Config-Label | – | 0.8rem | 600 | uppercase, letter-spacing: 0.05em |
| KPI-Wert | – | 1.2rem | 700 | font-variant-numeric: tabular-nums |
| KPI-Label | – | 0.73rem | 400 | uppercase |
| Tabellen-Header | – | 0.8rem | 600 | – |
| Tabellen-Daten | – | 0.8rem | 400 | tabular-nums |
| Badge | – | 0.75rem | 500 | border-radius: 99px |
| Footer | – | 0.75rem | 400 | – |

### Excel-Typografie
Alle Excel-Zellen verwenden **Arial** als Schriftart:
| Element | Grösse | Gewicht |
|---------|--------|---------|
| Report-Titel | 16pt | Bold |
| Subtitel | 10pt | Italic |
| Zusammenfassung Daten | 11pt | Normal |
| Netto-Effekt | 12pt | Bold |
| Tabellen-Header | 10pt | Bold, Weiss |
| Tabellen-Daten | 10pt | Normal |
| Methodik-Text | 9pt | Normal, Grau |


## Komponenten

### Card / Box
```css
background: rgba(30,41,59,0.7);
border-radius: 12px;
padding: 1.5rem;
border: 1px solid rgba(148,163,184,0.15);
margin-bottom: 1.5rem;
```

### Accordion (einklappbare Sektion)
- Header: Card-Stil mit `cursor: pointer`, `user-select: none`
- Geöffnet: Header border-radius nur oben (12px 12px 0 0)
- Body: border-top: none, border-radius nur unten (0 0 12px 12px)
- Pfeil: ▼ mit `transform: rotate(180deg)` bei geöffnet
- Transition: 0.25s auf transform

### KPI-Kachel
```css
border-radius: 10px;
padding: 1rem;
text-align: center;
border: 1px solid [Akzentfarbe mit 0.15 Opacity];
background: [Akzentfarbe mit 0.08 Opacity];
```
Grid: 3 Spalten (Standard), 4 Spalten wenn Erstbeschaffung aktiv.

### Upload-Box
```css
border-radius: 12px;
padding: 1.25rem;
text-align: center;
cursor: pointer;
transition: all 0.2s;
position: relative; /* für "optional" Badge */
```
Grid: 3 Spalten gleichmässig.
Icon wechselt von 📄 zu ✓ nach Upload.
Dateiname + Zeilenanzahl als kleine Info-Pill darunter.

### Tabellen
```css
width: 100%;
border-collapse: collapse;
font-size: 0.8rem;
```
- Header: text-align: right, border-bottom 1px
- Daten: text-align: right, font-variant-numeric: tabular-nums
- Wertespalten haben spezifische CSS-Klassen: `.sav` (grün), `.cost` (rot), `.erst` (amber)

### Error-Box
```css
background: rgba(239,68,68,0.1);
border: 1px solid rgba(239,68,68,0.3);
border-radius: 10px;
padding: 1rem;
color: #fca5a5;
```

### Checkbox
```css
accent-color: #f59e0b;
width: 18px;
height: 18px;
```
Label: 0.88rem, normaler Text. Hint daneben: 0.75rem, #94a3b8.


## Excel-Farbschema

### Sheet-Header (erste Zeile)
| Sheet | Hintergrundfarbe | Hex |
|-------|-----------------|-----|
| Zusammenfassung / Detail | Dunkelblau | #2F5496 |
| Top 20 Einsparungen | Dunkelgrün | #375623 |
| Top 20 Mehrkosten | Dunkelrot | #953735 |
| Top 20 Erstbeschaffungen | Dunkel-Amber | #BF8F00 |
| Ignorierte WE | Dunkelgrau | #616161 |

Schrift in Headern immer Weiss (#FFFFFF), zentriert, Textumbruch aktiv.

### Zeilenfarben Detail-Sheet
| Kategorie | Hintergrund | Hex |
|-----------|------------|-----|
| Einsparung | Hellgrün | #E2EFDA |
| Mehrkosten | Hellrot | #FCE4EC |
| Erstbeschaffung | Hell-Orange | #FFF3E0 |
| Neutral | Hellgrau | #F2F2F2 |
| Ignoriert | Hell-Gelb | #FFF8E1 (Text: #8B6914) |

### Zebrastreifen Top-Sheets
| Sheet | Gerade Zeilen | Ungerade Zeilen |
|-------|--------------|----------------|
| Einsparungen | #F5FBF2 | #FFFFFF |
| Mehrkosten | #FFF5F5 | #FFFFFF |
| Erstbeschaffungen | #FFF8E1 | #FFFFFF |
| Ignorierte | #F5F5F5 | #FFFFFF |

### Zusammenfassung
- Einsparungszeile: Hintergrund #E2EFDA
- Mehrkostenzeile: Hintergrund #FCE4EC
- Erstbeschaffungszeile: Hintergrund #FFF3E0
- Netto-Effekt: Schrift #2F5496, Bold 12pt, unterer Rand medium #2F5496

### Zahlenformate
| Typ | Format |
|-----|--------|
| Stückpreise | #,##0.0000 |
| Einsparung/Mehrkosten | #,##0.00 |
| Mengen | #,##0 |
| Prozent (Anteil) | 0.0% |


## Layout & Responsive

### Desktop (Default)
- Container: max-width 960px, zentriert
- Upload-Grid: 3 Spalten
- KPI-Grid: 3 Spalten (4 bei Erstbeschaffung)
- Padding: 2rem body

### Mobile (max-width: 700px)
- Upload-Grid: 1 Spalte
- Config-Bar: Column statt Row
- KPI-Grid: 2 Spalten
- Option-Bar: Column statt Row


## Allgemeine Prinzipien

1. **Dark Theme durchgehend** – Kein Light Mode, konsistente dunkle Oberfläche
2. **Farben = Bedeutung** – Grün ist immer positiv, Rot immer negativ, Amber immer Sonderfälle
3. **Transparenz statt Opazität** – Hintergründe nutzen rgba() für Tiefenwirkung
4. **Minimale Animationen** – Nur Hover-Effekte (0.2s) und Accordion-Pfeil (0.25s)
5. **Zahlen immer tabular-nums** – Für saubere Spaltenausrichtung
6. **Excel = Browser-Pendant** – Gleiche Farblogik im Excel wie im Tool
7. **Keine Frameworks** – Reines CSS, kein Tailwind, kein Bootstrap
8. **Keine externen Fonts** – System-Fonts (Segoe UI) im Browser, Arial im Excel
9. **Self-contained** – Einzige externe Abhängigkeit ist die xlsx-js-style CDN
10. **Accessible Labels** – Config-Labels uppercase mit letter-spacing für Lesbarkeit
