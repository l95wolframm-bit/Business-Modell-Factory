# Business Model Factory

KI-gestütztes Tool, mit dem Gründer:innen, Solopreneure und Master-Studierende ein
Geschäftsmodell **empirisch validieren**. Es kombiniert automatisierte Marktrecherche
(wissenschaftliche Paper, Social Media, GitHub, Förderdatenbanken), ein interaktives
Business Model Canvas und einen KI-gestützten „Stress-Test"-Debattenmodus —
spezialisiert auf den **deutschen / DACH-Markt**.

## Status

Aktuell enthält das Repo den **Design-Handoff**: zwei hochauflösende HTML-Prototypen
(Landing Page + Produkt-Tour) plus die vollständige Design-Dokumentation. Die
eigentliche Anwendung ist noch nicht implementiert.

## Projektstruktur

```
.
├── design/                       # Design-Handoff (Referenz, nicht produktiv)
│   ├── HANDOFF.md                # Vollständige Design-Doku: Tokens, Layout, Komponenten
│   ├── Business Model Factory.html   # Landing-Page-Prototyp
│   └── Produkt-Tour.html             # Produkt-Tour mit 7 In-App-Screen-Mockups
└── README.md
```

## Design-Prototypen ansehen

Die HTML-Dateien sind eigenständig und verlinken sich gegenseitig. Im Browser öffnen:

```bash
open "design/Business Model Factory.html"
```

Oder über einen lokalen Server (empfohlen, damit relative Links sauber funktionieren):

```bash
cd design && python3 -m http.server 8000
# → http://localhost:8000/Business%20Model%20Factory.html
```

## Nächste Schritte

Laut [`design/HANDOFF.md`](design/HANDOFF.md) sollen die Designs in einem echten
Frontend-Stack nachgebaut werden (Empfehlung: React + Vite oder Next.js). Die
In-App-Screens der Produkt-Tour sind reine Marketing-Mockups und werden später zu
datengetriebenen Views.

- [ ] Frontend-Stack scaffolden (React + Vite + TS)
- [ ] Design-Tokens aus `HANDOFF.md` übernehmen (Farben, Typografie, Spacing)
- [ ] Landing Page als Komponenten umsetzen
- [ ] Produkt-Tour umsetzen
