## MODIFIED Requirements

### Requirement: Dialog Action Buttons
The system SHALL support three button types: primary (outlined white — cancel), danger (red — destructive), and confirm (brand green — positive acknowledge). Buttons are arranged in a horizontal flex row. When the actions container has the `dialog__actions--single` modifier, the single button takes full width automatically.

#### Scenario: Danger action button
- **WHEN** a dialog has a danger action (e.g., delete)
- **THEN** the danger button SHALL be displayed with red background, fixed 186px width, white text

#### Scenario: Primary/cancel button
- **WHEN** a dialog has a cancel/secondary action
- **THEN** the primary button SHALL use white outlined style with flex:1 width

#### Scenario: Confirm button (new)
- **WHEN** a dialog uses `dialog__btn--confirm` button type
- **THEN** the button SHALL display with brand green background, white text, and flex:1 width

#### Scenario: Single-action layout
- **WHEN** `dialog__actions--single` class is added to the actions container
- **THEN** the single button inside SHALL expand to full width regardless of type
- **AND** the layout SHALL work correctly on both desktop and mobile

## ADDED Requirements

### Requirement: Dialog Single-Action Variant
The system SHALL support a single-action dialog variant where only one confirm button is shown, taking the full width of the actions row.

#### Scenario: Single confirm button
- **WHEN** a dialog is rendered with `dialog__actions--single` and one `dialog__btn--confirm` button
- **THEN** the button SHALL span the full width of the actions area
- **AND** clicking it SHALL fire the action callback and close the dialog

#### Scenario: Single-action on mobile
- **WHEN** a single-action dialog is displayed on mobile (≤ 767px)
- **THEN** the button SHALL remain full-width (consistent with desktop)
