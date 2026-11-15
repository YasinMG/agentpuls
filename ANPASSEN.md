# AgentPulse anpassen – was steht wo?

Die Seite besteht aus 4 Dateien. Auf GitHub: Datei öffnen → Stift-Symbol (Edit) → ändern → **Commit changes**.
Vercel baut danach automatisch neu (ca. 30 Sekunden).

```
index.html        Gerüst: Kopfzeile, Menü links, Tab-Leiste unten (Handy)
css/style.css     Design: Farben, Rundungen, Abstände, Handy-Layout
js/data.js        INHALTE: alle Texte, Zahlen, Agenten, Verbindungen, Tour
js/app.js         Logik: baut die Seiten (nur ändern, wenn nötig)
```

Tipp: In jeder Datei steht oben ein Inhaltsverzeichnis. Mit **Strg+F** nach der Nummer suchen
(z. B. `== 1.` in style.css oder `2. DIE SIEBEN` in data.js).

---

## Häufige Änderungen

| Was möchten Sie ändern? | Datei | Wo genau |
|---|---|---|
| **Firmenname / Produktname** | `js/data.js` | Abschnitt **1. FIRMA & MARKE** → `produkt`, `firma`, `bereich` |
| **Akzentfarbe** (Buttons, aktive Tabs, Linie) | `css/style.css` | Abschnitt **== 1.** → `--acc` (und `--acc-ink` für Text) |
| **Hintergrund / Kachelfarbe** | `css/style.css` | **== 1.** → `--bg`, `--tile` (hell) und im Block `prefers-color-scheme:dark` + `[data-theme="dark"]` (dunkel) |
| **Grün / Orange / Rot** der Status | `css/style.css` | **== 1.** → `--ok`, `--warn`, `--bad` (+ jeweils `-ink`, `-bg`) |
| **Rundung der Kacheln** | `css/style.css` | **== 1.** → `--radius` (Desktop) und **== 13.** → `--radius` (Handy) |
| **Abstand zwischen Kacheln** | `css/style.css` | **== 1.** → `--gap` |
| **Score-Kachel (lila Verlauf)** | `css/style.css` | **== 6.** → `.hero{… background:linear-gradient(…)}` |
| **Die 7 Dimensionen** (Namen, Punkte) | `js/data.js` | **2. DIE SIEBEN DIMENSIONEN** |
| **Agenten** (Name, Kanal, Kennzahlen) | `js/data.js` | **3. AGENTEN** |
| **Frühwarnungen** | `js/data.js` | **4. FRÜHWARNUNGEN** |
| **Technische KPIs** | `js/data.js` | **5. TECHNISCHE KENNZAHLEN** |
| **Vorher/Nachher-Tabelle, ROI-Startwerte** | `js/data.js` | **6. GESCHÄFTSKENNZAHLEN** und `AP.roi` |
| **Erklärtexte hinter dem „?“** | `js/data.js` | **7. ERKLÄRUNGEN** |
| **Welche App zu welchem Agenten gehört** | `js/data.js` | **8. VERBINDUNGEN** → `AP.agentConn` |
| **Felder & Hilfetexte der Verbindungen** | `js/data.js` | **8.** → `AP.connectors` |
| **Kundennamen & Fragen im Live-Strom** | `js/data.js` | **9. LIVE-SIMULATOR** |
| **Texte der geführten Tour** | `js/data.js` | **10. GEFÜHRTE TOUR** |
| **Menüpunkte links (Desktop)** | `index.html` | Block `<nav class="side">` |
| **Tabs unten (Handy)** | `index.html` | Block `<nav class="tabbar">` (max. 5 Einträge) |
| **Einträge im „Mehr“-Menü (Handy)** | `js/app.js` | Funktion `showMore()` (Abschnitt `## 7.`) |
| **Überschriften & Untertitel der Seiten** | `js/app.js` | Abschnitt `## 6.` → jeweils `head('Titel', 'Untertitel' …)` |
| **Start-Zeitraum (30 Tage) / Live an/aus** | `js/app.js` | Abschnitt `## 2.` → `range: 30`, `live: true` |
| **Zahlenformat bei [7, 30, 90] Tagen** | `js/data.js` | Werte in eckigen Klammern: `[7 Tage, 30 Tage, 90 Tage]` |

---

## Handy-Layout

Alles im Abschnitt **== 13. RESPONSIVE** in `css/style.css`:

- **unter 1024 px** (Tablet & Handy): Seitenleiste verschwindet, die Tab-Leiste unten erscheint.
- **unter 820 px** (Handy): Kacheln 2-spaltig, Tabellen werden zu Karten, Detail-Fenster wird ein Bottom-Sheet (nach unten wischen schließt es).

Grenzen ändern: die Zahlen in `@media (max-width:1023px)` und `@media (max-width:819px)` anpassen.

Tabellen-Beschriftungen auf dem Handy (z. B. „Kanal“, „Erfolgsrate“) kommen aus `data-label="…"` in `js/app.js`.

---

## Hell- und Dunkelmodus

- Automatisch nach Einstellung des Handys/Computers.
- Mond/Sonne oben rechts schaltet manuell um (wird im Browser gemerkt).
- Dunkle Farben: `css/style.css`, Abschnitt **== 1.**, die beiden Blöcke mit `--bg:#000`.

---

## Wichtig

- Alle Zahlen sind **Demo-Daten**. Es gibt keine echten KI-Agenten und keine echten API-Aufrufe.
- Bei „Verbindungen“ wird nur das **Format** der Eingaben geprüft. Keine echten Schlüssel eingeben.
- Vor öffentlichem Einsatz in Deutschland: Impressum und Datenschutzerklärung verlinken.
