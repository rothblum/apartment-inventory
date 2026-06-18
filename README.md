# Apartment Inventory

A single static web page listing apartment items for sale, published with GitHub Pages.

**Live site:** https://rothblum.github.io/apartment-inventory/

## Contents
- `index.html` — the inventory page (the source of truth for the listing).
- `apartment_inventory.pdf` — a PDF export of `index.html`, kept in sync.
- `WhatsApp Image *.jpeg` — the item photos, referenced by `index.html`.

## Editing / publishing
Edit `index.html`, regenerate the PDF, then commit and push to `main` — GitHub Pages
redeploys automatically (~1 minute).

> Working with an AI agent (e.g. Claude Code)? See [`CLAUDE.md`](CLAUDE.md) for the full
> update runbook: exact PDF-regeneration command, the card structure, and how to mark
> items sold or add new ones.
