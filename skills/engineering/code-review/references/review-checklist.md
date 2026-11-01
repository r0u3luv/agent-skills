# Review Checklist

Use this only for higher-risk reviews.

## Correctness

- Does the implementation satisfy the stated behavior?
- Are edge cases handled explicitly?
- Are errors propagated or surfaced appropriately?

## Data and Compatibility

- Are migrations reversible or safely deployable?
- Are existing API contracts preserved?
- Are default values and null handling intentional?

## Security

- Are permissions checked at the right boundary?
- Are secrets excluded from logs and persisted artifacts?
- Are user-controlled inputs validated before sensitive operations?

## Tests

- Is there focused coverage for the changed behavior?
- Is there broader coverage for shared or cross-module behavior?
- Are failure cases tested where they matter?

