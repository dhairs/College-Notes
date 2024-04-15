## Definition

Pointer arithmetic allows us to do literal mathematical operations with pointer addresses, which allows us to do very interesting things.

This is very important when working with [[Arrays|Arrays]], but is used outside of that as well.

## How it works

When you have a pointer `T *p` where `T` is the type and `int i`

`p + i` has the effect:
- `TYPE(p+i) =` pointer-to-**T**
- `VAL(p+i) = VAL(p) + SIZE(T) * VAL(i)`

So basically, the language moves the pointer `i` **elements** of type `T` over. So for an `int` type, we'd be moving over `4` bytes every time we do `+ 1` on the pointer to the `int`.

In terms of [[Arrays|Arrays]], `s* = 'h'` is equivalent to `s[0] = 'h'`

So, `*(s+2) = *(s+4)` is the same as `s[2] = s[4]`

## Arithmetic with Casted Pointers

Recall [[Pointers#Casting Pointers|Casting Pointers]] changes purely the type, not value. We can use this to our advantage.

So, given `char s[8] = "Hello!\n;`
- The expression `(int *)s + 7` has type pointer to `int` and so the value is `ADDR(s) + SIZE(int) * 7` (in this case, that turns out to be `ADDR(s)+28`)
- The expression `(int *)(s + 7)` has type pointer to `int` and so the value is `ADDR(s) + SIZE(char) * 7` (in this case, that turns out to be `ADDR(s) + 7`)
- The statement `int x = *((int *) s);` will interpret the four bytes starting at address `s` as an `int` and set `x` equal to this value
	- It will just copy these four bytes over
	- The resulting value of `x` depends on the endianness of the machine
