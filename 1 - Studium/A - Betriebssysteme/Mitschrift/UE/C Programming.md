---
topic: C Programming
date: 2026-03-16
course: OSUE
tags:
  - studies
  - Betriebssysteme
  - C
---
# VO

### Pointers to const and const pointers
`const int *p` pointer to a constant integer
	- Integer value cannot be changed via p 
	- p can be changed to point another integer (even not const)
	
`int *const p` a constant pointer to an integer 
- The integer value can be changed via p 
- p cannot be cahnged to point another address

`int *const *p`
(Mutable pointer to a constant pointer to an integer)
![[Pasted image 20261013151438.png]]

### Casting pointers

```C
int x = 2048 + 15;
char *y = (char*) &x;
printf("%#x\n",*y); //
```

#### Links
- [[Learn Lean]]
