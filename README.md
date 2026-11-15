# AgentPulse – Klick-Demo: Monitoring von KI-Agenten im Kundenservice

Statische Webseite (HTML, CSS, JavaScript). Kein Server, keine Datenbank, kein Build nötig.
Alle Zahlen sind Demo-Daten – es gibt keine echten KI-Agenten und keine externen API-Aufrufe.

```
index.html        Gerüst (Kopfzeile, Menü, Tab-Leiste Handy)
css/style.css     Design & Handy-Layout
js/data.js        Alle Inhalte & Zahlen
js/app.js         Logik
ANPASSEN.md       Was ändere ich wo? (Farben, Texte, Agenten, Menü …)
```

## Lokal ansehen
`index.html` per Doppelklick öffnen – oder `python -m http.server 8080` und http://localhost:8080 aufrufen.

## Auf GitHub + Vercel aktualisieren
Neue Dateien ins Repository legen und pushen:

```bash
git add .
git commit -m "Neues Design + Handy-Version"
git push
```

Vercel veröffentlicht automatisch neu. Vercel-Einstellungen: Framework Preset **Other**, Build Command leer, Output Directory `./`.

Die alte Datei-Struktur (Ordner `fonts/`) wird nicht mehr gebraucht und kann gelöscht werden:
`git rm -r fonts` vor dem Commit.

## Andere Hosting-Wege
- **Netlify:** Ordner auf https://app.netlify.com/drop ziehen.
- **Eigener Server:** `docker compose up -d --build` → läuft auf Port 8080.
- **Azure Static Web Apps:** `staticwebapp.config.json` ist dabei.

## Vor öffentlichem Einsatz in Deutschland
Impressum und Datenschutzerklärung verlinken. Die Seite setzt keine Cookies und lädt keine externen Schriften;
im localStorage stehen nur: Tour gesehen, Hell/Dunkel, Verbindungsstatus (ohne Schlüssel).
