## What is Unicode?

Significant expansion of original ASCII codebook to include more scripts and also emojis
- As of February 12, 2024, Unicode supports 149,813 characters

In `C`, there is no native encoding of Unicode, so it uses the underlying [[Characters.md|character]] data type.

Completely backwards compatible with [[Characters.md#ASCII Encoding|ASCII]]

## UTF-8 Encoding

"**8** bit **U**nicode **T**ransformation **F**ormat"

Uses a variable length character encoding, using 1, 2, 3, or 4 bytes