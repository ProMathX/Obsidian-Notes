Ist direkt aus dem K&R uebernommen 



Pointer subtraction is also valid: if p and q point to elements of the same array, and p<q, then q-p+1 is the number of elements from p to q inclusive. This fact can be used to write yet another version of strlen: 
```C
int strlen(char *s)
{
  char *p = s;
  while (*p != '\0') 
	  p++; 
  return p - s;
} 

```


> In its declaration, p is initialized to s, that is, to point to the first character of the string. In the while loop, each character in turn is examined until the '\0' at the end is seen. Because p points to characters, p++ advances p to the next character each time, and p-s gives the number of characters advanced over, that is, the string length. (The number of characters in the string could be too large to store in an int. The header <stddef.h> defines a type ptrdiff_t that is large enough to hold the signed difference of two pointer values. If we were being cautious, however, we would use size_t for the return value of strlen, to match the standard library version. size_t is the unsigned integer type returned by the sizeof operator.

[[C Programming Language.pdf#page=93&selection=2,0,64,9|C Programming Language, page 93]]

Remember unary operators like * and ++ associate right to left.

Page 89:

The correspondence between indexing and pointer arithmetic is very close.

By definition, the value of a variable or expression of type array is the
address of element zero of the array. Thus after the assignment

```c
pa = &a[0];
```

`pa` and `a` have identical values. Since the name of an array is a synonym
for the location of the initial element, the assignment `pa = &a[0]` can
also be written as

```c
pa = a;
```

Rather more surprising, at first sight, is the fact that a reference to
`a[i]` can also be written as `*(a+i)`. In evaluating `a[i]`, C converts it
to `*(a+i)` immediately; the two forms are equivalent.

Applying the operator `&` to both parts of this equivalence, it follows
that `&a[i]` and `a+i` are also identical: `a+i` is the address of the
*i*-th element beyond `a`.

As the other side of this coin, if `pa` is a pointer, expressions might use
it with a subscript; `pa[i]` is identical to `*(pa+i)`. In short, an
array-and-index expression is equivalent to one written as a pointer and
offset.

### One key difference

There is one difference between an array name and a pointer that must be
kept in mind:

- A **pointer** is a variable, so `pa = a` and `pa++` are legal.
- An **array name** is *not* a variable; constructions like `a = pa` and
  `a++` are illegal.

When an array name is passed to a function, what is passed is the location
of the initial element. Within the called function, this argument is a
local variable, and so an array name parameter is a pointer — that is, a
variable containing an address.

We can use this fact to write another version of `strlen`, which computes
the length of a string.




![[Pasted image 20260902122702.png]]
## The Core Idea

If `p` is a pointer to some element of an array, `p++` increments `p` to
point to the next element, and `p += i` increments it to point `i`
elements beyond where it currently points. These are the simplest forms
of pointer, or address, arithmetic.

C is consistent and regular in its approach to address arithmetic. The
integration of pointers, arrays, and address arithmetic is one of the
strengths of the language: arithmetic on a pointer is automatically
scaled by the size of the type it points to. Adding `1` to an `int *`
advances it by `sizeof(int)` bytes, not one byte, which is what allows
the same pointer-walking code to work regardless of the element type.

---

## Worked Example: A Rudimentary Storage Allocator

K&R illustrates address arithmetic with a minimal allocator consisting of
two routines: `alloc(n)`, which returns a pointer to `n` consecutive
character positions, and `afree(p)`, which releases storage so it can be
reused. The routines are "rudimentary" because calls to `afree` must be
made in the opposite order to the calls made on `alloc` — the storage is
managed as a stack, last-in first-out.

```c
#define ALLOCSIZE 10000 /* size of available space */

static char allocbuf[ALLOCSIZE]; /* storage for alloc */
static char *allocp = allocbuf;  /* next free position */

char *alloc(int n)    /* return pointer to n characters */
{
    if (allocbuf + ALLOCSIZE - allocp >= n) { /* it fits */
        allocp += n;
        return allocp - n;   /* old p */
    } else                   /* not enough room */
        return 0;
}

void afree(char *p)   /* free storage pointed to by p */
{
    if (p >= allocbuf && p < allocbuf + ALLOCSIZE)
        allocp = p;
}
```

`allocp` points to the next free element. When `alloc` is asked for `n`
characters, it checks whether there is enough room left in `allocbuf`. If
so, it returns the current value of `allocp` and then advances it by
`n`. If there is no room, it returns zero.

`static char *allocp = allocbuf;` initializes `allocp` to point to the
beginning of `allocbuf`. This could equally be written as
`static char *allocp = &allocbuf[0];`, since the array name is the
address of the zeroth element.

Because C guarantees that zero is never a valid address for data, a
return value of zero can be used to signal an abnormal event — in this
case, no space left. `NULL` is often used in place of the literal zero,
as a mnemonic to indicate that this is a special pointer value.

---

## Comparing Pointers

If `p` and `q` point to elements of the same array, relations such as
`==`, `!=`, `<`, `>=` work as expected. For example, `p < q` is true if
`p` points to an earlier element of the array than `q` does. Any pointer
can be meaningfully compared for equality or inequality with zero.

The behavior is undefined for arithmetic or comparisons involving
pointers that do not point to members of the same array. The one
exception is that the address of the first element past the end of an
array may be used in pointer arithmetic.

---

## Adding an Integer to a Pointer

The construction `p + n` means the address of the *n*-th object beyond
the one `p` currently points to. This holds regardless of the type of
object `p` points to; `n` is scaled according to the size of that type.
If an `int` is four bytes, for example, `n` is scaled by four.

---

## Subtracting Two Pointers

Pointer subtraction is also valid: if `p` and `q` point to elements of
the same array and `p < q`, then `q - p + 1` is the number of elements
from `p` to `q` inclusive.

This fact can be used to write another version of `strlen`:

```c
int strlen(char *s)
{
    char *p = s;

    while (*p != '\0')
        p++;
    return p - s;
}
```

`p` is initialized to `s`, pointing to the first character of the
string. In the loop, each character is examined in turn until the `'\0'`
at the end is found. Since `p` points to characters, `p++` advances it
to the next character each time, and `p - s` gives the number of
characters advanced over — that is, the string length.

The number of characters in a string could in principle be too large to
store in an `int`. The header `<stddef.h>` defines a type `ptrdiff_t`,
large enough to hold the signed difference of two pointer values. A more
cautious version would use `size_t` for the return value, matching the
standard library, since `size_t` is the unsigned integer type returned
by `sizeof`.

Pointer arithmetic is consistent across types: if `p` were a pointer to
`float` instead of `char`, `p++` would advance to the next `float`. An
allocator that manages floats instead of characters could be written
merely by changing `char` to `float` throughout `alloc` and `afree`. All
pointer manipulations automatically take into account the size of the
objects pointed to.

---

## Legal and Illegal Pointer Operations

The valid pointer operations are:

- Assignment of pointers of the same type
- Adding or subtracting a pointer and an integer
- Subtracting or comparing two pointers to members of the same array
- Assigning or comparing a pointer to zero

All other pointer arithmetic is illegal. It is not legal to add two
pointers, or to multiply, divide, shift, or mask them, or to add `float`
or `double` to them, or, except for `void *`, to assign a pointer of one
type to a pointer of another type without a cast.

