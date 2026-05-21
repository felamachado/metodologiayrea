# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Static HTML educational site for students of **Metodología de la Educación a Distancia** and **Recursos Educativos Abiertos** at the Uruguayan Profesorado de Informática. This is a standard web project — unlike the Schoology pages in the parent directory, there are no LMS constraints here: external CSS files, CSS Grid, Flexbox, and JavaScript are all fine.

## Structure and conventions

- `index.html` — main page with content listing; update it whenever a new page is added
- Additional pages: `lowercase-con-guiones.html` naming convention
- `styles.css` — shared stylesheet for all pages (centralized, not inline)
- `images/` — all image assets

Each page must have exactly one `<h1>` and include a navigation link back to `index.html`.

## Design system

| Token | Value |
|-------|-------|
| Primary | `#1a237e` (dark educational blue) |
| Accent | `#e65100` (amber, calls to action) |
| Background | `#fafafa` |

Target audience is teachers in formation — keep the aesthetic **minimal, modern, and professional**.

## Context

This sub-project lives inside the same git repo as the Schoology ethics page (`../index.html`, `../modern-inner.html`). Those files use table-based inline styles to survive Schoology's CSS stripper — do not apply those constraints here.
