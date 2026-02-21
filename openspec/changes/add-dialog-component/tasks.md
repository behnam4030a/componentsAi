## 1. Setup
- [ ] 1.1 Create `components/dialog/` directory structure
- [ ] 1.2 Confirm `tokens.json` values match Figma design

## 2. CSS Implementation
- [ ] 2.1 Define CSS custom properties from design tokens
- [ ] 2.2 Implement overlay (full-page backdrop with semi-transparent gradient)
- [ ] 2.3 Implement dialog container (white box, 434px width, 8px radius, 16px padding)
- [ ] 2.4 Implement header section (close icon + title)
- [ ] 2.5 Implement description section (secondary text with padding)
- [ ] 2.6 Implement actions section (primary + danger buttons, 24px gap)
- [ ] 2.7 Implement primary button styles (brand green #26a88c, inner shadow)
- [ ] 2.8 Implement danger button styles (red #c50f1f, fixed 186px width)
- [ ] 2.9 Add slide-up animation (dialog enters from bottom to center)
- [ ] 2.10 Add overlay fade-in animation
- [ ] 2.11 Implement mobile responsive (<768px) — Bottom Sheet behavior (slide up from bottom, limited height)

## 3. JavaScript Implementation
- [ ] 3.1 IIFE structure with auto-init on DOMContentLoaded
- [ ] 3.2 `Dialog.open(id)` — show overlay + animate dialog in
- [ ] 3.3 `Dialog.close(id)` — animate out + remove overlay
- [ ] 3.4 `Dialog.closeAll()` — close all open dialogs
- [ ] 3.5 Close on overlay (backdrop) click — acts as cancel
- [ ] 3.6 Close on X button click
- [ ] 3.7 Close on Escape key press
- [ ] 3.8 Callback support: `Dialog.onClose(id, fn)`, `Dialog.onAction(id, fn)`
- [ ] 3.9 Prevent body scroll when dialog is open

## 4. Demo Page
- [ ] 4.1 Create `components/dialog/index.html` with demo scenarios
- [ ] 4.2 Demo: delete confirmation (danger button)
- [ ] 4.3 Demo: general confirmation (primary button)
- [ ] 4.4 Demo: API test buttons

## 5. Integration
- [ ] 5.1 Link dialog CSS/JS in root `index.html`
