
## Character Types in C

There are `char`, `signed char`, and `unsigned char` as character types

The implementation defines `char` to have the same behavior as either `signed char` or `unsigned char`
- Check the `<limits.h>` file, if `CHAR_MIN` is `0`, it is unsigned, otherwise signed.

**All** char types are 1 byte, no issues with ordering bytes

## ASCII Encoding

ASCII is a codebook that maps bit patterns `0x00` through `0x7F` to *control characters* and *printable characters*.
- Range is known as the codespace
- Each pattern is called a code point
- ASCII encodes 128 values (MSB always 0)

Important codes:
- `Ox00` or `\0` for `NUL` (not to be confused with the `NULL` pointer, which is word size length), this is 2 bytes
- `0x20` for ' ' (whitespace)
- `0x7F` for `DEL`


![[ASCII_Codebook_Table.png]]

