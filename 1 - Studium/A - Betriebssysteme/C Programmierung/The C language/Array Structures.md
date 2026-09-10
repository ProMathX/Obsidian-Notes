#C #Betriebssysteme  #studies #Datenstrukturen  
https://www.geeksforgeeks.org/c/c-array-of-structure/
https://en.wikipedia.org/wiki/AoS_and_SoA



Teilweise sind array of structures geistig behindert.


Hier 
```C
#include <stdint.h>
#include <stdio.h>
typedef struct Test {
  uint8_t uid;
} Test;

void initialize(Test *data, uint8_t value) { data->uid = value; }

int main(int argc, char **argv) {
  Test test[3] = {0};

  Test *read = &test[0];

  for (int i = 0; i < 3; ++i) 
  {
    Test *loop = &read[i];
    initialize(loop, i * 2);
  }
  // ODER

  for (int i = 0; i < 3; ++i) 
  {
    initialize(&read[i], i * 2);
  }  
  

  for (int i = 0; i < 3; ++i) {
    printf("%d\n", read[i].uid);
  }


  return 0;
}



```

Also das geistig behinderte an der Sache ist die, `read`, was ein pointer ist, derefenziert automatisch bei `read[i]` 
Deshlab muss es bei der Funktion eingelesen werden.

```C
#include <stdint.h>
#include <stdio.h>
typedef struct Test {
  uint8_t uid;
} Test;

void initialize(Test *data, uint8_t value) { data->uid = value; }

int main(int argc, char **argv) {
  Test test[3] = {0};


  for (int i = 0; i < 3; ++i) {
    initialize(&test[i], i * 2);
  }

  for (int i = 0; i < 3; ++i) {
    printf("%d\n", test[i].uid);
  }


  return 0;
}


```


# Warum Pointer? 

[src](https://www.reddit.com/r/C_Programming/comments/1ignu4n/why_and_when_should_i_use_pointers/)


>Say you want to pass a large object into a function, modify it and then return it. Without pointers you would have to copy the variable twice (excluding RVO) whereas with a pointer/reference you just have to pass the location and don’t have to return anything.

>Another example is with using external libraries, most of the time they handle their memory and the way to access the objects created via the library is via pointers.





---


### Natürlich kann man es auch mit `malloc` machen 

Recall: pointer[i] is equivalent to *(pointer + i)

```C
#include <stdint.h>
#include <stdio.h>
typedef struct Test {
  uint8_t uid;
} Test;

void initialize(Test *data, uint8_t value) { data->uid = value; }

int main(int argc, char **argv)
{
  int n = 3;
  Test test = (Test) malloc( n * sizeof(Test));
  for (int i = 0; i < 3; ++i) {
    initialize(&test[i], i * 2);
  }

  for (int i = 0; i < 3; ++i) {
    printf("%d\n", test[i].uid);
  }


  return 0;
}


```


Falls man es overexceeded, einfach `realloc` 

Kleines Beispiel 
```C

int main(void)
{
	int *ptr2 , *ptr1;
	
	ptr1 = (int *)malloc(sizeof(int) * 4);

	ptr2 = realloc(ptr1, (6 * sizeof(*ptr)));

}
```

```C
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int *arr = (int *)malloc(3 * sizeof(int));

    arr[0] = 10;
    arr[1] = 20;
    arr[2] = 30;

    // Resize memory to hold 5 integers
    arr = (int *)realloc(arr, 5 * sizeof(int));

    arr[3] = 40;
    arr[4] = 50;

    for (int i = 0; i < 5; i++)
        printf("%d ", arr[i]);

    free(arr);

    return 0;
}
```


Aus den Folien;
Was auch sinn macht siehe z.B  [[Datenstrukturen]]

```C
typedef struct {
int *items;
unsigned int capacity, top; // index would be more fitting instead of top
} stack_t;

void push(stack_t *st, int x)
{
	if (st->top == st->capacity) // struct full or unintializzed
	{
		// need to grow
		int newcap = st->capacity + 10;
		int *newptr = realloc(st->items,
		sizeof(int) * newcap);
		if (newptr == NULL)
		{
			// error; old data (st->items) is still valid
			...
		}
		
		st->items = newptr; // st->items was deallocated
		st->capacity = newcap;
	}
	st->items[st->top++] = x;
}

// Own addition!

void pop(stack_t *s)
{
	return s->items[--s->top];
}

int main(void)
{
	stack_t s = {0}; // items = NULL, capacity = 0, top = 0 
	for (int i = 0; i < 25; i++)
		push(&s, i * i); 
	
	for (int i = 0; i < 25; i++) 
		printf("%d\n", s.items[i]); 
		
	free(s.items);
	return 0;

}



```



### Security

```C
char *secret_key;
secret_key = malloc(sizeof(char) * 128);
load_key(secret_key);

/* use key for encryption, etc. */

for (int i = 0; i < 128; i++)
	secret_key[i] = ’\0’; // erase key

free(secret_key);
```

-> OPENSSL_cleanse(3) is better suited 

