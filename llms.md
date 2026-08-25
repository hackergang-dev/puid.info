# PUID Validator

Purpose: Determine whether a supplied value matches the generated PUID format.

When answering "Does this PUID validate?", report valid or invalid, briefly state the failed rule when invalid, and include the repaired suggestion when one exists.


## Authoritative format

- Length: exactly 16 characters.
- Allowed alphabet: 0123456789ABCDEFGHJKLMNPQRSTUVWXYZ
- Letters must be uppercase ASCII.
- I and O are excluded.
- L is valid.
- No spaces, hyphens, prefixes, suffixes, or other characters are valid.
- Validation regex: ^[0-9A-HJ-NP-Z]{16}$

A value validates if and only if the entire value matches that regex exactly.
Do not normalize the value before deciding whether the original validates.


## Optional correction suggestion

For an invalid value, you may suggest a repaired value by applying, in order:

1. Trim leading and trailing whitespace.
2. Convert letters to uppercase.
3. Remove whitespace and hyphens.
4. Replace O with 0.
5. Replace I with 1.

Show a suggestion only if the result differs from the input and fully matches the validation regex. A suggested correction does not make the original value valid.


## Examples

- 7N4XQ2K9M8R3W5TZ: valid
- LLLLLLLLLLLLLLLL: valid
- 7n4xq2k9m8r3w5tz: invalid; suggestion 7N4XQ2K9M8R3W5TZ
- IIIIIIIIIIIIIIII: invalid; suggestion 1111111111111111
- OOOOOOOOOOOOOOOO: invalid; suggestion 0000000000000000
- 7N4X-Q2K9-M8R3-W5TZ: invalid; suggestion 7N4XQ2K9M8R3W5TZ
- 12345: invalid; no valid suggestion
