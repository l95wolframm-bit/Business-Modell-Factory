# Handoff: Business Model Factory — Landing Page & Produkt-Tour

## Overview
Business Model Factory is a KI-gestütztes (AI-powered) tool that helps founders, solopreneurs and master's students **empirically validate a business model**. It combines automated market research (scientific papers, social media, GitHub, funding databases), an interactive Business Model Canvas, and an AI "stress-test" debate mode — specialized for the **German / DACH market**.

This bundle covers two marketing/product pages:
1. **`Business Model Factory.html`** — the public landing page (hero, problem, features, methodology, how-it-works, audiences, waitlist, footer).
2. **`Produkt-Tour.html`** — a product tour showing seven in-app screen mockups (Idee → Research → Markt & US-Transfer → Canvas + Stress-Test → Kalkulation → Fördermittel → Report).

Both share one design system and a dark/light theme.

## About the Design Files
The files in this bundle are **design references created in HTML** — prototypes that show the intended look, layout, copy and behavior. They are **not** production code to copy verbatim. The task is to **recreate these designs in the target codebase's environment** (React, Vue, Svelte, etc.) using its established components, routing and styling patterns. If no front-end environment exists yet, choose an appropriate framework (e.g. React + Vite, or Next.js) and implement there.

The in-app screens on the Produkt-Tour page are **static marketing mockups** of a future product UI — they illustrate what the real app should look like. When the actual application is built, these screens become real, data-driven views; here they are presentational only.

## Fidelity
**High-fidelity (hifi).** Final colors, typography, spacing, radii and shadows are all defined as tokens (see Design Tokens). Recreate the UI pixel-faithfully using the codebase's libraries. Copy (German) is final unless product decides otherwise.

---

## Global System

### Layout
- **Container widths:** standard `max-width: 960px`; wide `max-width: 1200px`. Horizontal padding `24px`. Centered with `margin-inline: auto`.
- **Section vertical rhythm:** `padding-block: clamp(56px, 8vw, 112–128px)`.
- **Spacing system:** all spacing is a multiple of **4px**.
- **Sticky nav** height `68px`, translucent background with `backdrop-filter: blur(14px)`; a bottom hairline border appears after the page is scrolled > 8px (`.scrolled`).
- **Responsive:** mobile-first, works from 375px. Nav links + nav CTA appear at `min-width: 880px`. In-app mockup sidebars hide at `max-width: 760px`; multi-column screen bodies collapse to one column at 760–980px breakpoints.
- **Reduced motion:** `@media (prefers-reduced-motion: reduce)` disables smooth scroll and all transitions; reveal elements show immediately.

### Reveal-on-scroll
Elements with class `.reveal` start `opacity: 0; translateY(16–18px)` and animate to visible via an IntersectionObserver (threshold ~0.06–0.12). A failsafe reveals anything already in viewport on load and on `window.load`. In the target app, use the framework's standard in-view animation (or none) — do **not** ship content that is permanently hidden if observers don't fire.

### Theme toggle
A button toggles `data-theme="dark"` on `<html>`. Initial theme follows `prefers-color-scheme`. **No localStorage is used** (by design). Sun icon shows in light mode, moon icon in dark.

---

## Design Tokens

### Colors — Light (default)
| Token | Hex / value | Use |
|---|---|---|
| `--bg` | `#f7f6f2` | page background (warm beige) |
| `--surface` | `#f9f8f5` | cards, panels |
| `--surface-2` | `#f1efe8` | insets, chips, tracks |
| `--text` | `#28251d` | primary text |
| `--text-muted` | `#7a7974` | secondary text |
| `--primary` | `#01696f` | teal accent, CTAs, links |
| `--primary-hover` | `#0c4e54` | CTA hover |
| `--on-primary` | `#f7f6f2` | text on teal |
| `--warn` | `#b4541f` | risk/low-confidence tags |
| `--border` | `oklch(from var(--text) l c h / 0.12)` | default borders (≈ rgba(40,37,29,.12)) |
| `--border-strong` | `oklch(from var(--text) l c h / 0.20)` | emphasized borders |
| `--hairline` | `oklch(from var(--text) l c h / 0.07)` | row dividers |

### Colors — Dark (`html[data-theme="dark"]`)
| Token | Value |
|---|---|
| `--bg` | `#1a1916` |
| `--surface` | `#222019` |
| `--surface-2` | `#2b2820` |
| `--text` | `#f0eee6` |
| `--text-muted` | `#a09d92` |
| `--primary` | `#3aa6ab` |
| `--primary-hover` | `#54bcc1` |
| `--on-primary` | `#11201f` |
| `--warn` | `#e0935f` |

Borders/hairlines are derived from `--text` via the same `oklch(from …)` alpha formulas, so they invert automatically.

### Typography
- **Display / headings:** `"Instrument Serif"` (Google Fonts), weight 400, used for all `h1/h2/h3` and any text ≥ 24px. `line-height: 1.04`, `letter-spacing: -0.01em`.
- **Body / UI:** `"Satoshi"` (Fontshare), weights 400/500/700.
- **Mono:** `ui-monospace, "SF Mono", Menlo, Consolas, monospace` — used for kickers, URL pills, code-ish labels, footnote citations.
- **Type scale (fluid, `clamp()`):**
  - Display: `clamp(2.5rem, …, 4.5rem)` (tour) / `clamp(2.75rem, …, 5rem)` (landing)
  - `.h2`: `clamp(1.85rem, …, 3rem)` to `clamp(2rem, …, 3.25rem)`
  - `.h3`: `clamp(1.4rem, …, 1.9–2rem)`
  - `.lede`: `clamp(1.125rem, …, 1.375rem)`, color `--text-muted`, max-width ~54–56ch
  - Body: `clamp(1rem, …, 1.0625rem)`
- Keep to 3–4 sizes per page. `text-wrap: pretty` where supported.

### Radii
`--r-sm: 8px`, `--r-md: 14px`, `--r-lg: 22px`; pills use `999px`. App windows use `18px`; in-app cells `9–10px`.

### Shadows (tone-matched to warm surface)
- `--shadow-sm`: `0 1px 2px rgba(40,37,29,.05), 0 1px 1px rgba(40,37,29,.04)`
- `--shadow-md`: `0 1px 2px rgba(40,37,29,.04), 0 10px 30px -12px rgba(40,37,29,.18)`
- `--shadow-lg`: `0 2px 4px rgba(40,37,29,.05), 0 30px 70px -28px rgba(40,37,29,.32)`
- Dark mode uses near-black rgba equivalents.

### Buttons
- `.btn` base: inline-flex, gap 8px, weight 500, padding `13px 22px` (lg: `15px 26px`), radius `999px`. Active state `translateY(1px)`.
- `.btn-primary`: bg `--primary`, text `--on-primary`, shadow-sm → on hover bg `--primary-hover` + shadow-md.
- `.btn-ghost`: text `--text`, `1px solid --border-strong`, bg `--surface` → hover border `--text`, bg `--surface-2`.
- Icons inside buttons are 18px Lucide-style strokes (`stroke-width: 2`).

### Tags / chips
- `.tag.ok` — teal text on `color-mix(primary 13%)` bg (success / "übertragbar" / "Hoch").
- `.tag.warn` — warn color on `color-mix(warn 14%)` bg (risk / "Niedrig").
- `.tag.neutral` — muted text, `surface-2` bg, border (neutral / "prüfen" / "Mittel").

### Icons
**Lucide** icon set (loaded via CDN `https://unpkg.com/lucide@latest`, then `lucide.createIcons()`). Most icons in the markup are inline SVGs drawn in the Lucide style (24×24 viewBox, `fill: none`, `stroke: currentColor`, `stroke-width: 2`). In the target app, use the real Lucide package (`lucide-react`, etc.) with matching names: search, arrow-right, check, sun, moon, lightbulb, layout-grid, bot, landmark, file-text, users, message-square, git-branch, bar-chart, euro, calendar, send, zap (bolt), etc.

---

## Page 1 — Landing (`Business Model Factory.html`)

Sections in order:

1. **Nav** — custom SVG logo (see Assets) + wordmark "Business Model Factory" (Instrument Serif 1.3rem). Links: Features, Methodik, **Tool ansehen** (→ `Produkt-Tour.html`), Preise. Right: theme toggle (40px circle) + "Early Access" primary button (→ `#waitlist`). Links/CTA appear ≥880px.

2. **Hero** — left-aligned. Badge pill ("Early Access · DACH-Markt · Q3 2026" with pulsing teal dot). H1 (display): *"Vom Markt. Von Daten. Von Wissenschaft. Nicht von Bauchgefühl."* (second sentence in `--text-muted`). Lede (1 sentence). Two CTAs: "Jetzt Early Access sichern" (primary) + "Demo ansehen" (ghost → `Produkt-Tour.html`). Small note row with check icon. **Proof strip:** 4-column stat grid (serif numbers + muted labels), top hairline border.

3. **Problem** — eyebrow + serif headline. **Asymmetric 2+1 grid** (NOT 3 equal columns): one tall wide card on the left spanning 2 rows (huge serif stat "42%" in teal + heading + paragraph + source line pinned to bottom), two stacked cards on the right ("11 h", "0"). Cards: surface bg, border, radius-lg, hover lift `translateY(-3px)` + shadow-md.

4. **Feature showcase** — 4 alternating rows (`.feature-row`, every other `.reverse`), 2-col at ≥860px (copy / visual). Each: serif index ("01"–"04") with trailing rule, h3, paragraph, tag pills. The **visual** side is a CSS-built mini UI mock (not an image):
   - 01 Research Engine — source rows (SSRN, OpenAlex, Reddit, GitHub, Hugging Face) with check/spinner + "live" pulse.
   - 02 DE/US Trend — horizontal axis with two pins (US earlier, DACH later) + "+14 Monate" gap pill.
   - 03 Canvas + Stress-Test — 3-col mini canvas grid (one active cell) + AI "Gegenfrage" chat bubble.
   - 04 Fördermittel — program rows (EXIST, EIC, Distr@l, go-digital) with match-% bars.

5. **Methodik** — `--surface` band with top/bottom borders. Two columns: left copy + a left-bordered citation block (Haaker, Bouwman, Janssen & de Reuver 2017 — Business Model Stress Testing). Right: 3 method items (icon tile + title + text): Design Science Research, Szenario-basiertes Stress Testing, Evidenz vor Meinung.

6. **Wie es funktioniert** — vertical numbered **timeline** (a 2px gradient line connects circular serif step numbers 1–4). Steps: Idee eingeben → Research läuft automatisch → Canvas interaktiv ausfüllen & debattieren → Report + Förder-Matching. Each step has a small teal "step-tag" pill.

7. **Für wen** — eyebrow + headline, then 3 audience cards (icon tile, uppercase role label, serif heading, paragraph, check-list). Roles: KI-Gründer / Masteranden & Forschende / Legal-Tech-Berater.

8. **Early Access Waitlist** (`#waitlist`) — large rounded card (shadow-lg), 2-col at ≥820px. Left: eyebrow + headline + lede + two serif stats ("1.240+", "Q3 2026"). Right: email form — pill-shaped field (mail icon + input) with teal focus ring, primary submit button, lock-icon fine print. On submit: client-side email validation; on success the form hides and a teal success panel ("Danke – du stehst auf der Liste…") shows. No storage, no backend (wire to real API in production).

9. **Footer** — logo + tagline, Produkt + Ressourcen link columns (external links open in new tab with `rel="noopener noreferrer"`), bottom bar with copyright + legal links.

---

## Page 2 — Produkt-Tour (`Produkt-Tour.html`)

Shares the nav/footer/theme system. Hero: badge with German-flag chip, H1 *"Ein Blick ins Tool."*, lede, CTAs, a **legend** row, and an **"engines" strip** of chips communicating the multi-model orchestration: **Perplexity** (Recherche & US-Scan) · **Claude** (Pitch & Design) · **BMF-Modell** (Canvas & Stress-Test).

### The reusable in-app "window" shell
Each tour step renders a fake app window:
- **`.win`** — radius 18px, border, `--shadow-lg`, overflow hidden.
- **`.win-bar`** — `--surface-2` top bar: three 11px traffic-light dots + a centered mono URL pill (`app.businessmodelfactory.de/<page>`).
- **`.app`** — grid `206px | 1fr` (sidebar | main); collapses to 1 column < 760px (sidebar hidden).
- **`.app-side`** — left nav: "BMF" brand, "PROJEKT" group label, 7 nav items (Idee, Research [badge 218], Markt & Wettbewerb, Canvas, Kalkulation, Fördermittel [badge 6], Report), and a user footer (avatar "MK", "M. Krüger · Pro · DACH"). The active item gets `color-mix(primary 11%)` bg + teal icon. **Implementation note:** in the prototype the sidebar is cloned from a `<template id="sidebarTpl">` into each window via JS, and the active item is set from each `.app-side[data-active]`. In a real app this is just one persistent sidebar component with an `active` route.
- **`.app-top`** — breadcrumb (bold current view) on the left; right side shows context badges: a market badge (German-flag chip + "Deutschland"/"DACH"/"DE · EU"), an **engine badge** (bolt icon + "Perplexity"/"Claude"), and status `.tag`s.
- **`.app-body`** — the screen content.

### The 7 screens
1. **Idee (Twitter-Pitch)** — centered card with mono prompt, the one-sentence idea (Legal-Tech / DSGVO contract-checking for small German law firms) + blinking caret, char count. Below: "Automatisch erkannt" detect panel with chips (Branche, Zielgruppe, Region: Deutschland (DACH), Modell, Rechtsform-Tendenz UG/GmbH). Primary "Research starten" button.
2. **Research Engine** — 2-col: left sources panel (SSRN, OpenAlex, **Destatis**, **DPMA**, Reddit r/jura with checks; GitHub, Hugging Face pending/spinner) + "218 Treffer"; right "Erkenntnisse" finding cards, each with a claim, supporting text, and mono source citation chips. Engine badge: **Perplexity**.
3. **Markt, US-Signale & Wettbewerb** — grid: market-size card (TAM/SAM/SOM stacked bars in € with descending teal opacity + note) and the DE/US trend-offset axis (+14 Monate); a competitor-positioning card (rows with letter tiles + "Lücke:" tags, ending in "Deine Position · Freiraum"); and a **full-width US-card** ("US-Markt · Voraus-Signale", Perplexity badge) with US-flag signal rows (übertragbar/prüfen) + an **"Empfehlung der KI"** recommendation box (teal-tinted) that proactively proposes which US patterns to bring to DACH. This is the "tool thinks for itself / brings US trends to Germany" behavior.
4. **Canvas + KI-Stress-Test** — left: full 9-block **Business Model Canvas** (German labels: Schlüsselpartner, Aktivitäten, Ressourcen, Nutzenversprechen [active/teal], Beziehungen, Kanäle, Kundensegmente, Kostenstruktur, Einnahmequellen). Two blocks carry a small warn dot ("Annahme ungeprüft"). Right: **stress-test chat** panel — scenario label, alternating AI/user messages (AI poses Gegenfragen), a "Annahme-Risiko: Mittel" warn tag, and a disabled input row with send button. Canvas grid: 5 cols (cost spans 3, revenue spans 2); collapses to 2 cols < 560px.
5. **Kalkulation (NEW)** — assumption-based business case. Left: "Annahmen · anpassbar" list — 6 rows, each `label (+ sublabel) | serif value | confidence tag` (Preis €49, variable Kosten €4,80, Fixkosten €28.000, CAC €180, Conversion 6 %, zahlende Nutzer Monat 12 = 720). A teal "KI-Vorschlag" note (compares price to US median, suggests a hybrid tariff). Right: two result cards — "Ergebnis · pro Monat" (Deckungsbeitrag/Nutzer €44,20, Fixkosten, Umsatz, and a centered break-even callout "Monat 16 · ~634 zahlende Nutzer") and "Kapital & Runway" (Kapitalbedarf €410k, Runway 22 Mon., Puffer +6 Mon.). **All outputs derive from the assumptions** — in production these are live formulas:
   - Deckungsbeitrag/Nutzer = Preis − variable Kosten (49 − 4,80 = 44,20)
   - Break-even Nutzer = Fixkosten ÷ Deckungsbeitrag (28.000 ÷ 44,20 ≈ 634)
   - Umsatz Monat 12 = Preis × zahlende Nutzer (49 × 720 = 35.280)
6. **Fördermittel-Matching** — filter row (Bundesland: Hessen, Phase: Pre-Seed, Typ) + program list with match-% bars, € amounts, deadlines, region (EXIST-Gründerstipendium 94% expanded with "Warum es passt" / "Nächster Schritt", EIC Accelerator 81%, HTGF 73%, Distr@l 67%, INVEST 61%). Market badge "DE · EU".
7. **Report** — left: document mock ("Differenzierungs-Report") with header (title, date, "belegt durch 218 Quellen") + a serif Validierungs-Score "78/100"; numbered sections 01–06 (incl. **06 Pitch & Marketing — "mit Claude"**) with superscript footnote refs; a mono footnote line. Right: "Auf einen Blick" stat card (Score, belastbare Annahmen 7/9, Quellen, Förder-Matches, SOM, Break-even Monat 16) + "Export" card (PDF primary, Pitch-Deck-Gerüst ghost, "erzeugt mit Claude" note). Engine badge: **Claude**.

Closing CTA section + footer.

---

## Interactions & Behavior
- **Theme toggle:** flips `data-theme` on `<html>`; CSS variables do the rest. Sun/moon icon swap via `[data-theme]` selectors.
- **Smooth in-page scroll** to anchors; `scroll-padding-top` accounts for the sticky nav.
- **Nav border** appears on scroll (`.scrolled`).
- **Reveal animations** as described (gate on in-view; respect reduced-motion).
- **Waitlist form:** preventDefault → regex email check → on fail, focus + red border; on success, hide form + show success panel. Replace with a real POST in production.
- **Cross-page links:** landing ↔ tour via relative hrefs (`Produkt-Tour.html`, `Business Model Factory.html#…`). In a SPA these become routes (`/`, `/tour`, hash/section anchors).
- **External links:** `target="_blank" rel="noopener noreferrer"`.
- **Pulse/spinner micro-animations** on "live"/pending states (decorative; safe to simplify).

## State Management
Minimal — these are presentational pages. For a real implementation:
- `theme: 'light' | 'dark'` (init from `prefers-color-scheme`).
- Waitlist: `email`, `status: idle | invalid | submitting | success`.
- The in-app screens, when built for real, need: project/idea input, async research job + results, market metrics, canvas block values + assumption objects (value + confidence + source), stress-test conversation, **calculation inputs → derived outputs (pure functions)**, funding matches, and the generated report. In THIS bundle all of that is static mock content.

## Accessibility
- Targets WCAG AA contrast for text on surfaces in both themes. Verify any new combinations.
- Buttons/toggles have `aria-label`s; nav uses `<nav aria-label>`; success panel uses `role="status"`.
- Hit targets ≥ 40–44px. Honor `prefers-reduced-motion`.

## Assets
- **Logo:** custom inline SVG (no external file). A rounded-square "canvas" frame with internal grid lines (a vertical divider + a horizontal divider creating a canvas/grid reference), a geometric stroked **"B"** on the left, and three filled dots down the right column. Monochrome via `currentColor` (so it adapts to light/dark and accent). Provided at 30px (nav) and scales to any size; works at 24px and 200px. Recreate as a single SVG component.
- **Flag chips:** the German flag (hero/market badges) and US flag (US-signal rows) are tiny CSS gradient rectangles, not images — reproduce as small SVGs or CSS in the target app.
- **Fonts:** Instrument Serif (Google Fonts), Satoshi (Fontshare). Load via the codebase's font pipeline.
- **Icons:** Lucide (use the real package).
- No photographic/raster imagery is used; product "screenshots" are CSS/HTML mockups.

## Files
- `Business Model Factory.html` — landing page (self-contained: inline CSS + JS, CDN fonts + Lucide).
- `Produkt-Tour.html` — product tour with the 7 in-app mockups (self-contained).
- `README.md` — this document.

Both HTML files are single-file references; all CSS is in a `<style>` block in `<head>` and all JS in a `<script>` at the end. Open them in a browser to inspect exact spacing, hover states and the dark theme while implementing.
