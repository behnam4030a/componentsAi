## ADDED Requirements

### Requirement: Dialog Overlay
The system SHALL display a semi-transparent overlay covering the entire page when a dialog is opened.

#### Scenario: Overlay appears on open
- **WHEN** `Dialog.open(id)` is called
- **THEN** a full-page overlay with semi-transparent background is shown
- **AND** the overlay fades in with animation

#### Scenario: Overlay click closes dialog
- **WHEN** the user clicks on the overlay (outside the dialog box)
- **THEN** the dialog SHALL close without triggering any action callback
- **AND** this acts as a cancel/dismiss operation

### Requirement: Dialog Container
The system SHALL render a dialog box (434px wide, 8px border-radius, 16px padding, white background) centered on the overlay.

#### Scenario: Dialog structure
- **WHEN** a dialog is displayed
- **THEN** it SHALL contain a header (close icon + title), description text, and an actions row with buttons

#### Scenario: Dialog slide-up animation
- **WHEN** the dialog opens
- **THEN** the dialog box SHALL animate from the bottom of the page upward to the center of the viewport

### Requirement: Dialog Close Mechanisms
The system SHALL support closing the dialog via X button, action buttons, overlay click, or Escape key.

#### Scenario: Close via X button
- **WHEN** the user clicks the close (X) icon in the dialog header
- **THEN** the dialog SHALL close without triggering any action

#### Scenario: Close via Escape key
- **WHEN** the user presses the Escape key while a dialog is open
- **THEN** the dialog SHALL close without triggering any action

#### Scenario: Close via action button
- **WHEN** the user clicks any action button (primary or danger)
- **THEN** the dialog SHALL close
- **AND** the corresponding action callback SHALL fire

### Requirement: Dialog Action Buttons
The system SHALL support two button types: primary (brand green #26a88c) and danger (red #c50f1f).

#### Scenario: Danger action button
- **WHEN** a dialog has a danger action (e.g., delete)
- **THEN** the danger button SHALL be displayed with red background (#c50f1f), fixed 186px width, white text

#### Scenario: Primary/cancel button
- **WHEN** a dialog has a cancel/secondary action
- **THEN** the primary button SHALL use brand green (#26a88c) background with flex:1 width

### Requirement: Dialog JavaScript API
The system SHALL expose a global `Dialog` object with `open`, `close`, and `closeAll` methods.

#### Scenario: Open dialog by ID
- **WHEN** `Dialog.open('my-dialog')` is called
- **THEN** the dialog element with `id="my-dialog"` SHALL be displayed with overlay and animation

#### Scenario: Close dialog by ID
- **WHEN** `Dialog.close('my-dialog')` is called
- **THEN** the dialog SHALL animate out and the overlay SHALL be removed

#### Scenario: Close all dialogs
- **WHEN** `Dialog.closeAll()` is called
- **THEN** all open dialogs SHALL be closed

### Requirement: Dialog Mobile Responsive
The system SHALL display the dialog as a Bottom Sheet on mobile viewports (max-width: 768px).

#### Scenario: Mobile Bottom Sheet behavior
- **WHEN** the viewport width is 768px or less
- **AND** a dialog is opened
- **THEN** the dialog SHALL slide up from the bottom of the screen
- **AND** remain anchored to the bottom (not centered)
- **AND** have full width with small inset margins

### Requirement: Dialog Body Scroll Lock
The system SHALL prevent background page scrolling while a dialog is open.

#### Scenario: Scroll lock on open
- **WHEN** a dialog is opened
- **THEN** the body element SHALL not be scrollable

#### Scenario: Scroll unlock on close
- **WHEN** all dialogs are closed
- **THEN** the body scroll SHALL be restored
