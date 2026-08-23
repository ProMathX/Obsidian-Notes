#C
#studies 
#Betriebssysteme 


sizeof retourniert die die byte größe des jeweiligen datentypes.

Wozu? Speicherallokierung

```C
#define ARRAY_LENGTH(a) (sizeof(a)/sizeof(a[0]))

int main(void)
{
	int a = 3;
	int xr[] = malloc(sizeof(int) * ARRAY_LENGTH(a)) /*schlecher Code nur als Beispiel*/
}

```

#### size_t & ssize_t
`size_t = variable_name;` (fixed size) 
	ist seit C99 ein unsigned int mit (mind.) 4 bytes 
`ssize_t = variable_name` (variable size)

Gibt die größe der Varibale in bytes an(`sizeof`). 

[src](https://www.geeksforgeeks.org/c/size_t-data-type-c-language/)
```C
// Here argument of 'n' refers to maximum
//blocks that can be allocated which
//is guaranteed to be non-negative.
void* malloc(size_t n);

// While copying 'n' bytes from 's2' to 's1'
// n must be non-negative integer.
void* memcpy(void* s1, void const* s2, size_t n);

// strlen() uses size_t because the length
//of any string will always be at least 0.
size_t strlen(char const* s);

```


>[!Merke]
>size_t oder ssize_t ist für die Speicherallokierung da, um zugriff auf diesen Dateientyp zu haben, muss der jeweilige Zugriff vom gleichen Datentyp sein, siehe dynamische Arrays





