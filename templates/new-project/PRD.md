# QuickQuote — Product Requirements Document

**Status:** Draft
**Date:** 2025-11-14

---

## Problem

Field sales reps spend 20-40 minutes manually building material estimates in
spreadsheets for every customer quote. This causes delays at the appointment,
errors from mental math, and lost deals when customers want a number on the spot.

---

## User

Solo field sales rep. Not technical. Works from a phone or tablet at job sites.
Needs to produce a quote in front of a customer in under 5 minutes.

---

## Solution

A local-first mobile-friendly web app where the rep inputs job parameters
(linear feet, material type, gate count) and gets an instant itemized quote
with materials, labor, and total. Quote can be printed or exported as PDF.

---

## Success Criteria

1. A rep can produce a complete itemized quote in under 5 minutes from scratch.
2. The quote calculates materials automatically from linear footage inputs.
3. Output can be saved as PDF or printed directly from the browser.
4. No login required — runs locally in the browser, no server dependency.

---

## Scope

### In Scope
- Material quantity calculator (linear feet → item counts)
- Labor cost calculator with configurable rate
- Itemized quote output with line items and total
- PDF export / print view
- Configurable price list (stored locally)

### Out of Scope
- User accounts or cloud sync
- CRM integration
- Mobile app (native iOS/Android)
- Multi-user or team features
- Invoice generation or payment processing

---

## Key Decisions

- Local-first: no backend, no login, no server. Runs entirely in the browser.
- Price list stored in localStorage for persistence between sessions.
- PDF export via browser print dialog — no external library needed for v1.

---

## Open Questions

None — ready to build.
