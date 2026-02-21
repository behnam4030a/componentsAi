# Change: Add Dialog Component

## Why
The UI kit needs a confirmation dialog for destructive/important actions (delete, status change, etc.). This is a centered overlay dialog that requires explicit user confirmation before proceeding, preventing accidental data loss.

## What Changes
- Add new `components/dialog/` directory with CSS, JS, and demo HTML
- Dialog overlays full page with semi-transparent backdrop
- Desktop: dialog slides up from bottom to center of page
- Mobile (<768px): dialog acts as a Bottom Sheet, slides up from bottom to a limited height
- Close via: X button, action buttons, or clicking outside (backdrop)
- Clicking outside = cancel (no action taken, dialog closes silently)
- Supports danger (red) and primary (green) action buttons
- JS API: `Dialog.open(id)`, `Dialog.close(id)`, `Dialog.closeAll()`

## Impact
- Affected specs: `dialog` (new capability)
- Affected code:
  - `components/dialog/dialog.css` (new)
  - `components/dialog/dialog.js` (new)
  - `components/dialog/index.html` (new demo)
  - `components/dialog/tokens.json` (already created)
  - `index.html` (root — link new CSS/JS)
