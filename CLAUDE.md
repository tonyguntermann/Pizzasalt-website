# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file static landing page for PizzaSalt (pizzasalt.com) — a pre-launch "coming soon" site for artisan pizza finishing salts. Everything lives in `index.html`: HTML structure, all CSS (inline `<style>`), and JavaScript (inline `<script>`).

No build system, no dependencies, no package manager. Open `index.html` directly in a browser to preview.

## Architecture

**Single file: `index.html`**

Page sections (top to bottom):
1. **Hero** — full-viewport with diagonal red panel, left-side brand copy, right-side signup card
2. **Ticker** — gold scrolling marquee strip
3. **Flavors** — dark background grid of 6 flavor cards
4. **How It Works** — tan background, 4-step process
5. **Manifesto** — red background pull quote
6. **Footer** — dark footer with logo

**CSS design tokens** (`:root` CSS variables):
- `--red` `--cream` `--tan` `--char` `--gold` `--smoke`

**Fonts** (Google Fonts): `Bebas Neue` (headings/display), `DM Serif Display` (card headings), `DM Sans` (body)

**JavaScript** (bottom of file, inline `<script>`):
- `animateCounter()` — counts up to a hardcoded placeholder (`target = 47`); replace with real data
- `handleSignup()` — validates email, collects form data, POSTs to `https://n8n.pizzasalt.com/webhook/pizzasalt-signup`, then shows success state
- IntersectionObserver — fade-in animation for `.flavor-card` and `.step` elements

## Key Integration Points

- **Signup webhook**: `https://n8n.pizzasalt.com/webhook/pizzasalt-signup` — receives `{ name, email, flavors, pizzaType }` as JSON POST
- **Sign-up counter**: The `47` in `animateCounter()` is a hardcoded placeholder; it should eventually be replaced with a live count from the backend
- **Responsive breakpoint**: `820px` — below this, the diagonal red hero panel hides and the two-column hero layout collapses to single column
