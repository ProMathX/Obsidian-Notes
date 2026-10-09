---
topic: Introduction to C
date: 2026-03-16
course: OSUE
tags:
  - studies
  - Betriebssysteme
  - C
---
## VO

### History of C 
C is deeply embedded to UNIX
It is not portable to other systems

we will compile the system on gcc with -std=c99

C is:
- Imperative
- procedural: statements are grouped into procedures  
- statically typed: each variable has a type that does not change, functions have a return value
- compiled
- preprocessed

```C
#include <stdio.h>

int main(void)
{
	printf("Hello, C World\n");
	return 0;
}
```

### Introduction

```C
extern int k; //declared, but defined somewhere else
```
	^ used for libraries 

The scope of a vairable is the region of the code where the variable can be accessed 


```C
int x = 120;

int main(void)
{
	int x = 0;
	printf("Hello World\n");
		return x; // "0"
}
```

C99 `stdint` library


sizeof is an noperator
### Operator 
- Binary operator
- Unary OPerator 
- preincrement/postincrement
- ternary operators

>[!Truthifullness]
>In C 0 stands for false

short-cicuti evaluation: when e1 && e2 

1. evaluate e1
2. if e1 is false return 0
3. Otherwise, evaluate e2 and return its value

mirrored for e1 || e2 : e2 evaluted only if e1 is false

bitwise operators: trivial

implicit conversion. smallest numbers gets converted to the biggest number type of the other operator


### Functions
trivial 

### Global vs Local
- local variables mask global variables
- lcoal variables have a random value at defintion, unless intialized
- global variable are initialize dwith 0 by default

### Control Structures
trivial

https://homepages.cwi.nl/~storm/teaching/reader/Dijkstra68.pdf


### Keywords

again static [[Keywords]], defeiniert den Speicherbereich für den definierten integer i, und speichert diesen

## Offene Fragen 

This return value is used to indicated for the unix sstem, which state the program is,
- 0 success 
- 1 stdout 
- 2 stderr 




## Keywords




#### Links
- [[Learn Lean]]
