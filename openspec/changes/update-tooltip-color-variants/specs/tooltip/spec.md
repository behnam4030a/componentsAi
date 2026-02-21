## ADDED Requirements

### Requirement: Color Variants
The tooltip component SHALL support 7 color variants via the `data-tooltip-variant` attribute and corresponding CSS modifier classes. Each variant MUST override the bubble background, text color, and arrow color.

Supported variants: `primary`, `secondary`, `success`, `danger`, `warning`, `info`, `dark`.

| Variant | BG | Text | Arrow |
|---------|-----|------|-------|
| default | #364455 | #ffffff | #364455 |
| primary | #7160e8 | #ffffff | #7160e8 |
| secondary | #7b7c7d | #ffffff | #7b7c7d |
| success | #54b054 | #ffffff | #54b054 |
| danger | #cc2635 | #ffffff | #cc2635 |
| warning | #f98845 | #ffffff | #f98845 |
| info | #3595de | #ffffff | #3595de |
| dark | #000000 | #ffffff | #000000 |

#### Scenario: Variant applied via HTML attribute
- **WHEN** a tooltip element has `data-tooltip-variant="primary"`
- **THEN** the tooltip bubble and arrow MUST render with background color #7160e8

#### Scenario: Variant applied via JavaScript
- **WHEN** `setVariant("danger")` is called on a tooltip instance
- **THEN** the tooltip MUST update to use the danger color (#cc2635)

#### Scenario: Default when no variant specified
- **WHEN** no `data-tooltip-variant` attribute is present
- **THEN** the tooltip MUST use the default color (#364455)

#### Scenario: Variant cleanup on destroy
- **WHEN** `destroy()` is called on a tooltip with a variant
- **THEN** the variant modifier class MUST be removed from the element
