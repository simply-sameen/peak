# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev       # Vite dev server (localhost:5173)
npm run build     # Production build → dist/
npm run preview   # Preview the dist/ build locally
```

## Stack

Vanilla HTML + CSS + JS. Single file: `index.html`. No framework, no component system, no TypeScript. Vite is used only as a dev server and bundler — there is no JSX, no imports, no modules.

## Architecture

Everything lives in `index.html`:
- **CSS** — inline `<style>` block with CSS custom properties for all design tokens
- **HTML** — `.page` container → nav → `.hero-body` → `.know-group` → `.waitlist-section` → `.footer-wrap`
- **JS** — inline `<script>` IIFE at the bottom; handles the waitlist form with a direct `fetch()` to Supabase REST

The Supabase URL and anon key are hardcoded in the script block (not imported from `.env`). The `.env` file exists but is not consumed by the page — do not refactor to use `import.meta.env` unless the build pipeline changes.

Supabase table: `waitlist`, column: `email`. Success = HTTP 201. Duplicate = 409 or `body.code === '23505'`.

## Design System

- **Font**: DM Sans (all weights via Google Fonts). DM Mono is not currently in use.
- **Tokens** (CSS custom properties in `:root`): `--bg`, `--text`, `--accent`, `--btn-bg`, `--btn-text`, `--input-bg`, `--divider`, `--muted`
- **Figma file**: `jUzPzZYNoxPVjFpJ0kMzPL` ("Simply"), canvas node `1307:17` ("Fend landing")

## Breakpoints

Three exact breakpoints from Figma — do not add others:

| Breakpoint | Viewport | `.page` container | Top/bottom padding |
|---|---|---|---|
| Desktop (default) | 1440px | `max-width: 1085px` | 85px |
| Tablet | `≤ 1024px` | `max-width: 839px` | 57px |
| Mobile | `≤ 576px` | `max-width: 576px; padding: 57px 28px` | 57px |

Vertical gap between every section at every breakpoint: **200px**.

## Figma Workflow

- Call `get_design_context` before writing any code for a section
- Call `get_variable_defs` to pull exact token values — do not estimate
- `get_variable_defs` requires a layer selected in the Figma desktop app; if it fails, use `get_metadata` to find node IDs and `get_screenshot` at high resolution to extract values visually
- All spacing and sizing values must come exactly from Figma — if a value is unclear, ask
