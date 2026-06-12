# Visual Deck Editor Runtime Contract

The Visual Deck Editor is a built-in runtime capability for generated Frontend Slides decks.

This directory currently contains documentation only. It exists to make the editor's contract explicit: what deck structure it expects, what behavior it owns, and what boundaries maintainers should preserve. The editor implementation is still authored through the presentation template guidance in `html-template.md` and bundled inline into generated `index.html` files.

## Current Status

The editor is not a separate package or application.

What exists today:

- Generated decks include the editor UI and behavior inline.
- `html-template.md` defines the implementation requirements used when generating decks.
- This document defines the runtime contract and maintenance boundaries.
- The plugin copy keeps the same contract for installed Claude Code plugin users.

What this directory is not:

- It is not an npm package.
- It is not a source bundle.
- It is not a separate web app.
- It is not a claim that the editor can run on arbitrary HTML pages.

## Runtime Goals

- Work on generated fixed-stage HTML decks.
- Keep the final deck portable: root `index.html` plus relative local assets.
- Infer editable objects from normal slide DOM where possible.
- Treat explicit `data-editable*` attributes as optional hints, not hard requirements.
- It keeps editor-generated state temporary and removes editing chrome from saved/exported HTML.
- It avoids npm, backend services, hosted storage, user accounts, and framework lock-in.

## Current Role

- Bundled inline into generated Frontend Slides decks by default.
- Activated after draft generation through the edit toggle or `E` key.
- Edits text, media, visual boxes, simple shapes, font choices, layout, and entrance motion.
- Saves a clean, portable `index.html` with editor chrome and temporary detection markers removed.
- Works without npm, a framework, a backend, or a cloud account.

## Stable Contract

The editor should stay deck-neutral but not pretend to be a generic web page builder.

- Input: a fixed-stage HTML deck using `#deckStage` or `.deck-stage`, `.slide`, and 1920x1080 stage coordinates.
- Detection: infer editable text, media, SVG/canvas content, and shape-like boxes from ordinary DOM first.
- Hints: treat `data-editable`, `data-editable-media`, and `data-editable-box` as optional improvements, not requirements.
- Storage: derive browser draft keys from file identity rather than a deck-specific project name.
- Output: preserve the deck as a portable folder with root `index.html` and relative assets.

## Maintenance Rules

- Keep behavior aligned with `html-template.md`.
- Keep this root document and the plugin copy in sync.
- Do not describe `visual-editor/` as a complete source package while it only contains documentation.
- Do not broaden claims beyond the fixed-stage deck contract without implementation and verification.
- If editor implementation is later extracted into source files, place real runtime code here and update this document to describe the new layout.

## Out Of Scope For Now

- A general website/page builder.
- A cloud editing product with accounts or hosted storage.
- Arbitrary HTML page editing.
- Exact PowerPoint animation import. The editor can edit authored HTML entrance motion, but exact PPT animation fidelity belongs to the PPT extraction pipeline.
