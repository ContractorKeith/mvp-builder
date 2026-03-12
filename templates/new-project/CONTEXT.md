# QuickQuote

## What this is
Field sales reps waste 20-40 minutes per appointment manually building material
estimates in spreadsheets. QuickQuote is a local-first browser app where a rep
enters job parameters and gets an instant itemized quote with materials, labor,
and total — no login, no server, no setup.

## User
Solo field sales rep. Works from phone or tablet at job sites. Not technical.
Needs a quote in front of a customer in under 5 minutes.

## Stack
- **Language:** Vanilla JavaScript, HTML, CSS — no build step
- **Architecture:** Single-page local app, no backend
- **Data:** localStorage for price list persistence
- **Key deps:** None
- **Deploy:** Open index.html directly, or static host

## Structure
```
/
├── index.html       ← entire app lives here
├── style.css        ← layout + print stylesheet
├── calculator.js    ← material + labor calculation logic
└── storage.js       ← localStorage read/write helpers
```

## Conventions
- No frameworks, no build tools
- All business logic in calculator.js, not inline in HTML
- localStorage keys prefixed with `qq_` (e.g., `qq_pricelist`)
- Print styles in a `@media print` block at bottom of style.css

## Do NOT
- Add a backend or login system
- Add npm dependencies
- Implement CRM integration
- Build native mobile app features
- Add multi-user or cloud sync

## Current State
Sprint 1 in progress. Calculator logic complete. Print stylesheet and
localStorage UI are next.

## Success Criteria
1. Complete quote produced in under 5 minutes
2. Materials auto-calculated from linear footage
3. Output printable as PDF via browser
4. No login required
