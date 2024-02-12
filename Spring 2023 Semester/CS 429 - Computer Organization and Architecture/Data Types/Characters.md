
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
- `Ox00` or `\0` for `NUL` (not to be confused with the `NULL` pointer, which is word size length), this is 1 byte
- `0x20` for ' ' (whitespace)
- `0x7F` for `DEL`

### Codebook

![[ASCII_Codebook_Table.png]]

## Operations on Characters

Characters are literally just [[Manipulating Integer Representations|integer types]], so you can perform arithmetic operations on them.

### Example: `atoi()`

`atoi()` is part of the standard C library, and provides a way of converting ASCII to Integer (hence the a-to-i name).

`atoi("429")` would return `429`

```c
int atoi(const char[s]) { // const tells us the parameter array cannot change
	int retval = 0;
	for(int i = 0; s[i] != '\0'; i++) {
		retval *= 10;
		retval += s[i]-'0';
	}
	return retval;
}
```








## Other representations

There are other representations for characters as well, namely [[Unicode]].