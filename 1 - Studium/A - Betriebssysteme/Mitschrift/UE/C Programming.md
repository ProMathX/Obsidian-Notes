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

`int *const *p` `(int *const)(*p)`
(Mutable pointer to a constant pointer to an integer) declare p as pointer to const pointer to int
![[Pasted image 20261013151438.png]]

### Casting pointers

```C
int x = 2048 + 15;
char *y = (char*) &x;
printf("%#x\n",*y); //15 or 0xf
```

### struct 
![[Pasted image 20261013152526.png]]
Align the data accordign to the data size from big to lowest 

### pointers to struct 
![[Pasted image 20261013152848.png]]


### void pointers
trivial
### Singly Linked List
![[Pasted image 20261013152913.png]]

### Call by value
![[Pasted image 20261013153346.png]]

### Call by reference 
![[Pasted image 20261013153404.png]]


### Singly linked list: add to front (push)

```C 
#include <stdlib.h>

typedef struct node
{
	int data;
	struct node *next_node;
}node_t;


void push(node_ t **const head, const int value)
{
	node_t *rv = (node_t *)(malloc(sizeof(node_t)));
	rv->data = value;
	rv->next = *head;
}

```


Wobei diese variabte gelcih wäre
```C
#include <stdlib.h>
struct node 
{
    int data;
    struct node *next_node;
};


void push(struct node *(*const head), int value)
{
    struct node *new_node = (struct node*)(malloc(sizeof(struct node)));
    new_node->data = value;
    new_node->next_node = *head;
	*head = new_node;
}
```

![[Pasted image 20261013160906.png]]


### Singly  linked ist: pop
![[Pasted image 20261013160924.png]]
`node_t **head` weil head ein pointer zu einem node_t pointer ist also referenziert head immer auf ein node_t
### tagged unions
![[Pasted image 20261013161710.png]]

![[Pasted image 20261013163407.png]]


#### Links
- [[Learn Lean]]
https://ptgmedia.pearsoncmg.com/images/9780131774292/samplepages/0131774298.pdf

#### Tasks 
-[ ] singly linked list reimplemntieren (anschauen )