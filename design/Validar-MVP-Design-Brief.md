# Validar MVP — Design- & Build-Brief (für Claude / Claude Design)

> Diesen Brief komplett in eine Claude-Session einfügen. Er ist selbstständig –
> Claude braucht keinen weiteren Kontext, um den MVP als interaktives Tool zu entwerfen.

## Auftrag
Entwirf und baue den **Validar MVP** als interaktives, einseitiges Web-Tool (klickbarer Prototyp).
Liefere eine **vollständige, lauffähige Single-File-HTML** (HTML + CSS + Vanilla-JS, keine Build-Tools).
Mit **Mock-Daten**, aber so strukturiert, dass echte API-/LLM-Calls später leicht eingesetzt werden können.

## Produkt in einem Satz
Validar validiert eine Geschäftsidee empirisch: **Idee eingeben → automatische Recherche aus offenen Quellen → belegte Validierungs-Sektionen + Risiko-Score → Kurz-Report.** DACH-Fokus, Zielgruppe Gründer:innen/Solopreneure.

## MVP-Scope (bewusst klein – nicht erweitern)
**Drin:**
1. Idee-Eingabe + geführtes KI-Sparring (KI stellt 2–3 Rückfragen, Vorschlags-Chips)
2. Asynchrone Recherche auf **4 offenen Quellen**: OpenAlex, Crossref, kuratierte Förder-Liste (DACH), 1 Community-Quelle (Reddit/HN)
3. Validierung: **Marktbeleg**, **Differenzierung & Wettbewerb**, **Risk-Radar-Lite** (4 Kategorien)
4. Kurz-Report (Validierungs-Score, 3 Findings, Quellen) + **PDF-Export**

**Bewusst draußen (nicht bauen):** Buying Center, Hybrid-/Service-Kalkulation, Productized Service, Methoden-Bibliothek, Go/No-Go-Gate, DE/US-Trend-Versatz, Live-Förder-Matching, Multi-Agent, Auth/Workspaces.

## User-Flow
Single-Page, vertikaler Flow ODER 4-Schritt-Wizard (deine Wahl – Wizard bevorzugt für „Tool"-Gefühl).
**Idee & Sparring → Research (async) → Validierung → Report.** Oben ein „MVP · Phase 1"-Badge. Reset-Button („Neuer Lauf“) startet den Flow neu.

## Modul-Specs (mit Zuständen)
**1 · Idee & KI-Sparring**
- Textarea für die Idee (Platzhalter, Zeichenzähler).
- Nach Eingabe stellt die „KI“ **nacheinander 2–3 Rückfragen** (Chat-artig: KI-Frage links, Antwort rechts), je mit **Vorschlags-Chips** zum Antippen.
- Auto-erkannte Tags: Branche · Zielgruppe · Region.
- Zustände: *leer → Eingabe → Sparring-Dialog → fertig.*

**2 · Research (4 offene Quellen)**
- 4 Quellen-Zeilen mit Icon, Name, Kurzinfo, **Status-Tag** (wartet / läuft / belegt) + Trefferzahl.
- **Asynchron**: Status läuft nacheinander durch (per Timer simulieren), Teilergebnisse erscheinen sofort. Kein blockierender Spinner.
- Hinweiszeile: „Recherche läuft als Hintergrund-Job (~60–90 s).“
- Zustände je Quelle: *pending / running / done / error.*

**3 · Validierung (3 Sektionen)**
- **Marktbeleg** und **Differenzierung & Wettbewerb**: je 1–2 Sätze mit Quellen-Hochzahlen (¹·²).
- **Risk-Radar-Lite**: 4 Kategorien (**Markt, Wettbewerb, Regulierung, Finanzen**), je Score 0–10 + Balken + farbiger Punkt (grün = niedrig, bernstein = mittel, magenta = hoch). Subtil, kein Rot-Alarm.

**4 · Kurz-Report**
- Gesamt-**Validierungs-Score /100** (groß, Serif).
- 3 Kern-Findings (Häkchen-Liste).
- Quellen-Zeile (mono).
- Buttons: **Report als PDF** (mit `window.print()` + Print-CSS) · **Neuer Lauf**.

## Interaktion & Zustände
- Async via `setTimeout` simulieren; Flow soll **echt wirken**.
- Skeleton/Status statt langer Spinner; `prefers-reduced-motion` respektieren.
- Leerer/Fehler-Zustand je Quelle vorsehen.
- Theme-Toggle (Initial aus `prefers-color-scheme`, **kein** localStorage).

## Design-System „Editorial Precision“ (verbindlich)
**Schrift:** `Instrument Serif` (Display/Headlines ≥20px) · `Inter` (UI/Body) · `JetBrains Mono` (Eyebrows, Labels, Zahlen). Google-Fonts-CDN.
**Stil:** sachlich/präzise (Linear-/Stripe-Anmutung). Flache, **hairline-gerahmte** Karten; kleine Radien (8–14px); Mono-Eyebrows mit kurzer Leitlinie; tabellarische Mono-Ziffern; links-ausgerichtet; **eine** Akzentfarbe.
**Verboten:** Glasmorphismus, Gradients, Lila/Blau-Schemes, bunte Icon-Kreise, zentrierter Default-Text, dekorative Blobs.
**Icons:** schlanke Stroke-SVGs (Lucide-Stil), `currentColor`.

**Farb-Tokens — Light:**
```
--bg:#fbfbf9; --surface:#ffffff; --surface-2:#f4f3ef;
--ink:#16150f; --muted:#6b6a63; --faint:#a4a39b;
--line:rgba(22,21,15,.11); --line-strong:rgba(22,21,15,.18);
--accent:#0a5d62; --accent-ink:#084a4e; --on-accent:#ffffff;
--ok:#3f8f4f; --warn:#8a5a1c; --high:#ad4385;
```
**Farb-Tokens — Dark (`html[data-theme="dark"]`):**
```
--bg:#0c0c0b; --surface:#141413; --surface-2:#1b1b19;
--ink:#ededea; --muted:#92918a; --faint:#5c5b55;
--line:rgba(255,255,255,.10); --line-strong:rgba(255,255,255,.17);
--accent:#54b8b2; --accent-ink:#6fcac4; --on-accent:#08110f;
--ok:#6daa45; --warn:#c08a52; --high:#d163a7;
```

**Logo (Radar-Mark, currentColor, in 24–34px nutzbar):**
```html
<svg viewBox="0 0 32 32" fill="none" aria-hidden="true">
  <rect x="2.25" y="2.25" width="27.5" height="27.5" rx="6.5" stroke="currentColor" stroke-width="2"/>
  <circle cx="16" cy="16.2" r="9.4" stroke="currentColor" stroke-width="1.5" opacity="0.5"/>
  <circle cx="16" cy="16.2" r="5" stroke="currentColor" stroke-width="1.5" opacity="0.85"/>
  <path d="M16 16.2 L24.3 10.8" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"/>
  <circle cx="21.6" cy="12.2" r="1.7" fill="currentColor"/>
  <circle cx="16" cy="16.2" r="2" fill="currentColor"/>
</svg>
```

## Tech-Vorgaben
- Eine `.html`, alles inline. Responsiv ab **360px**. WCAG-AA-Kontraste.
- Vanilla-JS (kein Framework nötig). Falls Framework gewünscht: React + Vite, gleicher Look.
- **Klare, austauschbare Mock-Funktionen**, damit echte Integrationen später nur diese ersetzen:
  - `getSparringQuestions(idea)` → Liste von Rückfragen + Vorschlags-Chips
  - `runResearch(sources)` → async, liefert je Quelle Status + Trefferzahl + Belege
  - `computeRiskLite(findings)` → 4 Kategorie-Scores
  - `buildReport(state)` → Gesamt-Score, Findings, Quellen
- Beispiel-Inhalt (Legal-Tech-Idee): „KI-Plattform, die kleinen Kanzleien hilft, Mandantenverträge automatisch auf DSGVO-Konformität zu prüfen.“

## Architektur-Hinweis (für die spätere Echt-Version, nicht im Prototyp bauen)
Frontend (statisch) → schlankes Backend (FastAPI/Express + Postgres) → Job-Queue (Research async) → **1 LLM** (Claude) + 4 Quellen mit Caching. Observability & Token-/Latenz-Budget von Tag 1.

## Output-Erwartung
Eine vollständige Single-File-HTML, die ich im Browser öffnen und durchklicken kann (Idee eingeben → Sparring → Research läuft → Validierung → Report → PDF). JS-Flow kommentiert und an den o. g. Funktionsgrenzen sauber trennbar.
