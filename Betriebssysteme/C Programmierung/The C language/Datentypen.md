#C
#studies 
#Betriebssysteme 

![[Pasted image 20260711111646.png]]

(mit typedef definierte alias, fixed integers)
`uint8_t`, `int8_t`, `int32_t`,`uint32_t`, `int64_t`, `uint64_t`
![[Pasted image 20260716194945.png]]

[src](https://en.cppreference.com/cpp/types/integer)

| Chartacter    | Type    | Output format                              |
| ------------- | ------- | ------------------------------------------ |
| C, c          | int     | a single-byte character                    |
| d             | int     | Signed decimal integer.                    |
| i             | int     | Signed decimal integer.                    |
| o             | int     | Unsigned octal integer.                    |
| u             | int     | Unsigned decimal integer.                  |
| X, x          | int     | Unsigned hexadecimal integer               |
| E, e, f, G, g | double  | Signed value; form [–]d.dddd e [-]dd[d]    |
| p             | Pointer | Prints the address of the argument in hex. |
| S, s          | String  | specifies a single-byte–character string.  |
|               |         |                                            |

```C
#include <stdio.h>

int main()
{

    // Use sizeof() to know size of the data types
    printf("The size of int: %d\n", sizeof(int));
    printf("The size of char: %d\n", sizeof(char));
    printf("The size of float: %d\n", sizeof(float));
    printf("The size of double: %d", sizeof(double));

    return 0;
}

```

<br>
----
### In C: 0 is false, everything else is true (even -1)


Fun Fact 


`int foo$bar$ = 3;` ist gültig!


<br>