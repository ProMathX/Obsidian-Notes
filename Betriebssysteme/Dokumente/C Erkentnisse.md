#C
# Disclaimer

Für das Erstellen meiner C Erkentniss wurde keine KI verwendet

![[Pasted image 20260714193033.png]]

Für das Lernen und der Zusammenfassung
- [Youtube Playlist von einem Franzosen 10/10 ](https://youtube.com/playlist?list=PL71Y0EmrppR0KyZvQWj63040UEzKQU7n8&si=MBRaZZBmamGU9Ox7)
- K&R The C Programming Language 2nd Edition
- https://beej.us/guide/bgc/html/index-wide.html
verwendet
# Grundlage
Erstens
Generell input reading von einer Text-Datei 

```c
#include <stdio.h>

int main()
{
	FILE *f = fopen("text.txt","r");
	int c;
	while((c = getchar()) != EOF)
	{
		putchar(c)
	}
	f = NULL;
	return 0;
}
```

Wenn man einen character input hat und man eine Zahl haben will daraus, dann gilt 

'0' = 48
'1' = 49
'2' = 50
'3' = 51
...
'9' = 57

```c
#include <stdio.h> /* count digits, white space, others */

main()
{
    int c, i, nwhite, nother;
    int ndigit[10];

    nwhite = nother = 0;
    for (i = 0; i < 10; ++i)
        ndigit[i] = 0;

    while ((c = getchar()) != EOF)
        if (c >= '0' && c <= '9')
            ++ndigit[c-'0'];
        else if (c == ' ' || c == '\n' || c == '\t')
            ++nwhite;
        else
            ++nother;

    printf("digits =");
    for (i = 0; i < 10; ++i)
        printf(" %d", ndigit[i]);
    printf(", white space = %d, other = %d\n", nwhite, nother);
}
```


Das heißt bei 
```C
++ndigit[c-'0']
```

Wird mit 
```c
c = '7' <==> c = 55

-> ++ndigit[55-48] -> ++ndigit[7]
```

Bruder K&R einfach Genien 

Wenn ich bei dem Array dann ++ndigit[7] habe, habe ich dann, weil ich das Array davor mit
0er initalisiert habe, counte ich eine +1 auf diese Stelle und weiß, wieviele 7er es gibt.
### Graphen oder Diagramme vermeiden
Weil es kaum einheitlich ist, je nach Terminal konfiguration kann es rumspacken.
Ansonten Graphics Libraries verwenden wie SDL


### User Input 

Beispiel 
```C
FILE *input_file = NULL;
    if (argc == 2)
        input_file = fopen(argv[1], "r");
    else
        input_file = stdin;

    /* FILE* output_file = fopen(asm_filename, "w"); */
    FILE *output_file = stdout;
```


---
# Dokumentation

Dokumenation erfolgt mit Doxygen

`doxygen -g` im Projekt-Folder
Dann entsteht eine Doxyfile

Dann die Doxyfile editieren

```Doxyfile
PROJECT_NAME           = "Hello World Program"
OUTPUT_DIRECTORY       = docs
INPUT                  = .
RECURSIVE              = YES
EXTRACT_STATIC         = YES
GENERATE_LATEX         = NO

```

Dann 
`doxygen Doxyfile`

es kreiert dann ein docs/html in projekt verzeichnis 


dann 
`xdg-open doc/html/index.html`

---
24. Avoid side effects with && and ||, e.g., write if(b != 0) c = a/b; instead of if(b != 0 && c = a/b).
25. Each switch block must contain a default case. If the case is not reachable, write assert(0) to this case (defensive programmin

----

# Datentypen


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
----
#  goto 

```C
#include <stdio.h>

int main() {
    int n = 0;  

    // If the number is zero, jump to
  	// jump_here label
    if (n == 0)
        goto jump_here;

    // This will be skipped
    printf("You entered: %d\n", n);

jump_here:
    printf("Exiting the program.\n");
    return 0;
}
```

---

Da alles einen Rückgabewert in C hat, um die Rückgabewerte explizit zu ignorieren 
(void) foo();
verwenden 
bspw.
`(void) prinf("Hello\n")`

<br>

----
# Conditional Replacements
#### Die einzelnen Direktiven

| Direktive         | Bedeutung                                                                             |
| ----------------- | ------------------------------------------------------------------------------------- |
| `` #ifdef NAME `` | ``Prüft: **Ist `NAME` definiert?** (egal welchen Wert es hat)``                       |
| `#ifndef NAME`    | ``Prüft: **Ist `NAME` NICHT definiert?** (das Gegenteil von `#ifdef`)``               |
| `#if AUSDRUCK`    | `Prüft einen **konstanten Ausdruck** (z. B. Vergleich, Rechnung)`                     |
| `#elif AUSDRUCK`  | `"else if" — weitere Bedingung, falls die vorherige falsch war`                       |
| `#else`           | `Wird ausgeführt, falls keine vorherige Bedingung zutraf`                             |
| `` #endif ``      | ``**Pflicht** am Ende jedes `#if`/`#ifdef`/`#ifndef`-Blocks — schließt den Block ab`` |

 Beispiel 1: Plattformabhängiger Code für libraries 
```C
#ifdef WIN32
#include <windows.h>
#else
#include <unistd.h>
#endif

```

Beispiel 2: den Debugger ein und ausschalten innerhalb vom Code

```C
#if DEBUG >= 2
printf("debug, debug\n");
#endif
```

Zum Nutzen:
`gcc -DDEBUG=2 main.c -o main`


Anderes Beispiel 

```C
#include<stdio.h>
#define DEBUG 1

int main() {
	int a=2, b=3, ergebnis;
	ergebnis = (2*a) + (2*b);

	#if DEBUG >= 1
	printf("* Debug: ergebnis = (2*%d) + (2*%d);\n", a, b);
	#endif	

	#if DEBUG >= 2
	printf("* Debug: a=%d, b=%d, ergebnis=%d\n", a, b, ergebnis);
	#endif	

	printf("Das Ergebnis ist %d\n", ergebnis);
	return 0;
}

```

ist aber äquivalent zu
`gcc -DDEBUG=2 main.c -o main`

```C
#include <stdio.h>
int main() {
#if DEBUG == 1
  printf("DEBUG 1 DEBUG 1\n");
#endif

#if DEBUG == 2
  printf("DEBUG 2 DEBUG 2\n");
#endif
  return 0;
}

```

Output 
`DEBUG 2 DEBUG 2`

----
#  Macros
Das ist smart aber man sollte es bedacht nutzen
```C
#define NRELEMENTS(a) (sizeof(a) / sizeof(a[0]))

```


Multi-Line Macros
```C
#define SUM_BETWEEN(start, end){         \
	int sum = 0;                         \
	for(int i = (start); i < (end); i++) \
		sum += i;                        \
	printf("%d\n",sum);                  \
}

int  main(void)
{
	int sum = 20; /*Deshalb die klammern!, ansonsten compiler error*/
	SUM_BETWEEN(2,8) /* Weil printf in der Macro scho ein ; hat wird hier nicht benötigt*/
	
	return 0;

}


```

Es gehen auch Präfixe mit Macros.
Vorteil: Zum Generieren von Macros
```C
#define PREFIX(var_name) new_##var_name

#define GENERIC_ADD(type)  \
	type add_##type(type x, type y) \
	{ \
	   return ((x)+(y))\
	}\ 								

GENERIC_ADD(int)

GENERIC_ADD(float)

GENERIC_ADD(long)

int main(void)
{
	int PREFIX(foo) = 123;
	printf("%d\n",new_foo); /*123*/
	printf("%d\n",add_int(1,1)); /*2*/
	printf("%.2f\n",add_float(1.0,1.0)); /*2.0*/
	printf("%ld\n",add_long(1L,1L)); /*2L*/
	return 0;
}

```

```C
#define PRINT_LOOP(iterations, ...){\
	for(int i = 0; i < (iterations); i++) \
		printf(__VA_ARGS__); \
} \


int main(void)
{
	PRINT_LOOP(3,"hello %d %s\n",32,"bar");
}

```

----
# Pointers

generell passt, aber Achtung

```C
int main()
{
	int arr[] = {0,1,2,3,4}
	int *p = &arr[0]; /* p points to 0*/
	*p += 23 /* *p is now 23 */
	p++; /*p shows to the next obejct in the array*/
}
```

Wenn ein pointer eines anderen datentyps auf einen anderen pointer eines anderen datentypes zeigt 

bsp
```C

void *pv;
int *pin;
int a;

void foo()
{
	*pv = &a; /* ok but warning*/
	*pin = (int *) pv;  /* is necessary in C ++ ,
							   * but not mandatory in C */

}
```

```C

#include <stdio.h>

int main(void)
{
    int a = 3;

    void *p = &a;

    printf("%p\n", p);  /* 0x7fff27b7f8cc*/
    printf("%d\n", *p); /* ERROR: der Compiler weiß nicht konkret auf was der pointer eigentlich zeigt (dereferenz)*/
    printf("%d\n", *(int *)p) /* der Pointer wird in ein int pointer gecastet dann dereferenziert*/ 
}


```


Wozu? 

Für generische Funktionen

#### Pointer und Const

```C
char c;
char *const cp = &c
/* The value to which cp points to can be changed ,
* however , the pointer can ’t be changed
*/

const char *cp = &c;
/* The value to which cp points to can ’t be changed ,
* however , the pointer can be changed
*/

char const *cp = &c; /* same as const char *cp */

const char *const cp = &c;
/* The value to which cp points to can ’t be changed ,
* the pointer can ’t be changed either
*/

```


#### Return Values und Pointers

```C
char *first_b (const char *a)
{
	for(int i = 0; i < strlen(a); i++)
	{
		if(a[i] == 'b') return &a[i];
	}

	return NULL;
}


int main(void)
{
	char *s1 = "foobar";
	char *s2 = "foo";
	char *p = first_b(s1);
	if(p != NULL)
	{
		printf("found a %s at %p\n",&p,p); //bar
	}
	return 0;
}



```


### Index & Pointers
Wenn man eine referenz zwischen zwei Objekten haben will, benötigt man einen Pointer.
Macht nur Sinn, wenn alle User in einem zentralen Array liegen.

```C
User john = (User)
{
	.name = John,
	.friend = &sarah;
};
```

```C
User sarah = (User)
{
	.name = Sarah,
	.friend = NULL;
};


```

Was wenn der Speicher sich bei sarah ändert? 
--> Dangling Pointer bei john 

Fix:

Wenn unser User struct so definiert ist:

Natürlich unter der vorbedingung 

```C
typedef struct string
{
	char *s1;
	int length;

}String;


```

```C
typedef struct
{
	String name;
	User *friend;
} User; 
```
--> Dann speichern wir statt den Pointer zum einem anderen Struct, den Index

```C

typedef struct
{
	String name;
	int32_t friendIndex;
} User;


```

Dann wird

```C
User john = (User)
{
	.name = John,
	.friend = &sarah;
};
```

zu 
```C
User john = (User)
{
	.name = John,
	.friend = 27;
};
```

konkretes Beispiel 

```C
#define MAX_USERS 100

typedef struct {
    char name[32];
    int32_t friendIndex;  // -1 = kein Freund
} User;

User users[MAX_USERS];
int32_t userCount = 0;

int32_t addUser(const char *name, int32_t friendIndex) {
    User *u = &users[userCount];
    strncpy(u->name, name, sizeof(u->name) - 1);
    u->friendIndex = friendIndex;
    return userCount++;   // gibt den Index des neuen Users zurück
}

int main(void) {
    int32_t sarahIdx = addUser("Sarah", -1);
    int32_t johnIdx  = addUser("John", sarahIdx); // John zeigt per Index auf Sarah

    // Zugriff: statt john.friend->name schreibst du:
    User *john = &users[johnIdx];
    User *johnsFriend = &users[john->friendIndex];
    printf("Johns Freund heißt %s\n", johnsFriend->name);

    return 0;
}

```


#### Double pointer

Von geeksforgeeks:
>[!Quote]
>A double pointer in C is a pointer that stores the address of another pointer


```C
int main(void)
{
	int var = 10;
	int *p = &var;
	int **pp = &p;

	printf("var: %d\n", var);     
	printf("*ptr1: %d\n", *ptr1);     
	printf("**ptr2: %d", **ptr2);     
	return 0;

}
```



Für was? Dynamic 2d array.

Beispiel.:

```C
int main(void)
{
    int m, n;
    m = 4;
    n = 3;

    int **arr = malloc((m) * sizeof(int *));

    for (int i = 0; i < m; i++)
    {
        arr[i] = (int *)malloc((n) * sizeof(int));
    }

    for (int i = 0; i < m; i++)
    {
        free(arr[i]);
    }
    free(arr);

}
```




<br>
---
# Keywords

`static` -> allows a variable to keep its value after a function ends
Bsp 
```C
int add(int myNumber) {  
  static int total = 0;  
  total += myNumber;  
  return total;  
}  
  
int main() {  
  printf("%d\n", add(5));  
  printf("%d\n", add(2));  
  printf("%d\n", add(4));  
  printf("%d\n", add(9));  
  return 0;  
}


```

`typedef` -> Defines a custom data type
```C

#include <stdio.h>  
  
typedef float Temperature;  
  
int main() {  
  Temperature today = 25.5;  
  Temperature tomorrow = 18.6;  
  
  printf("Today: %.1f C\n", today);  
  printf("Tomorrow: %.1f C\n", tomorrow);  
  
  return 0;  
}


```

```C
#include <stdio.h>  
  
// Without typedef:  
struct Car {  
  char brand[30];  
  int year;  
};  
  
// With typedef:  
typedef struct {  
  char brand[30];  
  int year;  
} Car;  
  
int main() {  
  struct Car car1 = {"BMW", 1999}; // needs "struct"  
  Car car2 = {"Ford", 1969}; // shorter with typedef  
  
  printf("%s %d\n", car1.brand, car1.year);  
  printf("%s %d\n", car2.brand, car2.year);  
  return 0;  
}

```

---

`goto` -> Jumps to a line of code specified by a label
```C
#include <stdio.h>

int main() {
    int n = 0;  

    // If the number is zero, jump to
  	// jump_here label
    if (n == 0)
        goto jump_here;

    // This will be skipped
    printf("You entered: %d\n", n);

jump_here:
    printf("Exiting the program.\n");
    return 0;
}

```


<br>
---

# Function Pointers

Man kann eine Funktion definieren und diese dann als Pointer accessen, hat baer einer beschissene Syntax. 

```C


int foo(int x, int y)
{
	return x+y;
}

int main(void)
{
	int (*f)(int, int) = foo
	
	printf("%d", f(3,4)) /*returns 7*/

	return 0;
}




```

Gleiches gilt auch wenn man eine Funktion hat und in die Funktion eine andere funktion einpackt

```C


int foo(int x, int y)
{
	return x+y;
}

bool p(int x)
{
	return x%2 == 0;
}

void print_f(int xs[10], bool (*predicate)(int))
{
	for(int i = 0; i < 10;i++)
	{
		if(predicate(xs[i]))
		{
			printf("%d\n", xs[i]);
		}
	}

}

int main(void)
{
	int xs[]= {1,2,3,4,5,6};
	int (*f)(int, int) = f 
	
	printf("%d", f(3,4)) /*returns 7*/

	return 0;
}

```

Damit es lesbarer wird 

```C

#typedef int(* my_function)(int,int)
int foo(int x, int y)
{
	return x+y;
}

bool p(int x)
{
	return x%2 == 0;
}

void print_f(int xs[10], bool (*predicate)(int))
{
	for(int i = 0; i < 10;i++)
	{
		if(predicate(xs[i]))
		{
			printf("%d\n", xs[i]);
		}
	}

}

int main(void)
{
	int xs[]= {1,2,3,4,5,6};
	//int (*f)(int, int) = f 
	my_function f = foo;
	
	printf("%d", f(3,4)) /*returns 7*/

	return 0;
}

```

---
# Bit Flags High IQ move

Wenn du in C eine Funktion hast 

`void foo(int x, bool a, bool b, bool c);`

Dann muss man ja 3 Variablen festlegen  oder hinenschreiben.

Es gibt aber einen Umweg, in dem man Binär rechnet.


```C
#include <stdio.h>
#include <sys/types.h>

/* Bitwise Flags: */
/*Option 1:*/
// typedef unsigned int t_flag;
// #define FLAG_A (1 << 0) // 001
// #define FLAG_B (1 << 1) // 010
// #define FLAG_C (1 << 2) // 100

/*Option 2: */
typedef enum
{
    FLAG_A = (1 << 0), // 001

    FLAG_B = (1 << 1), // 010

    FLAG_C = (1 << 2) // 100

} t_flag;

int foo(int a, t_flag flag)
{
    if (flag & FLAG_A)
    {
        a += a;
        /*Unsetting FLAG_A*/
        flag &= ~FLAG_A; // 001 ^ 110 = 000
    }
    if (flag & FLAG_B)
    {
        a *= a;
        flag &= ~FLAG_B;
    }
    if (flag & FLAG_C)
    {
        a = ~a;
        flag &= ~FLAG_C;
    }

    return a;
}

int main(void)
{

    printf("%d\n", foo(1234, 0));
    printf("%d\n", foo(1234, FLAG_A));
    printf("%d\n", foo(1234, (FLAG_B | FLAG_C)));
    /*
       Im Binären ist in diesem Fall, wenn ich
       B v C <=> 010 v 100 => 110
       Die Felder von B und C sind belegt
       -> Somit FLAG_B und FLAG_C ist true
    */

    return 0;
}

```


----
# sizeof


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


----

# Strings

String literal 

`char *literal = "Hello World";` --> Nicht modifizierbar
`char array[] = "Hello World";` --> Modifizierbar

Somit:
`array[0] = '#'` -> Funktioniert
`literal[0] = '#'` -> segfault!

Man literal aber mit strdup() modifizieren

```C
#include <stdio.h>
#include <string.h>

int main(void)
{
    char *literal = "Hello World!";
    char array[] = "Hello World";

    array[0] = '#';

    char *s = strdup(literal);

    s[0] = '#';

    printf("%s\n", s);
    printf("%s\n", array);
    return 0;
}
```

#### Split String

https://www.youtube.com/watch?v=Uv0-vitgez0&list=PL71Y0EmrppR0KyZvQWj63040UEzKQU7n8&index=19

https://gist.github.com/cacharle/fe5c88acc539ed9347186f69f05ead83

oder verwende strtok (kann nicht bei ,,, kein \b setzen),strsep (kann dann ein \b setzen)

siehe manpages dementsprechend



---
# Datenstrukturen
### Arrays

Es gibt Gott weiß viele möglichkeiten ein beschissenes Array in C aufzusetzen.

#### Variante 1
```C
int array[your_length] ={....}
```

#### Variante 2
```C
int *array = (int*) malloc(sizeof(int)*your_length);

free(array);
```

### 2D-Arrays
#### Variante 1
```C
int array[m][n] = {{..},...,{...}}
```

#### Variante 2
```C
int **matrix = (int**) malloc(sizeof(int)*m*n)

free(matrix);
```


Falls man es in eine Funktion passen will zB.:

```C 
#include <math.h>
#include <stdio.h>
#include <stdlib.h>

int **matrixTranspose(int **matrix, int m, int n) {

  if (matrix == NULL) {
    fprintf(stderr, "Error: given array is empty!");
    return NULL;
  }

  int **data = (int **)malloc(sizeof(int *) * n);
  for (int i = 0; i < n; i++) {
    data[i] = (int *)malloc(sizeof(int) * m);
  }

  for (int i = 0; i < m; i++) {
    for (int j = 0; j < n; j++) {
      data[j][i] = matrix[i][j];
    }
  }

  return data;
}

int main(int argc, char **argv) {

  int m, n;
  m = 2;
  n = 4;
  int **matrix = (int **)malloc(sizeof(int *) * m);
  for (int i = 0; i < m; i++) {
    matrix[i] = (int *)malloc(sizeof(int) * n);
  }

  int values[2][4] = {{1, 1, 1, 1}, {2, 2, 2, 2}};

  for (int i = 0; i < m; i++) {
    for (int j = 0; j < n; j++) {
      matrix[i][j] = values[i][j];
    }
  }

  int **output = matrixTranspose(matrix, m, n);

  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      printf("%d ", output[i][j]);
    }
    printf("\n");
  }

  for (int i = 0; i < m; i++) {

    free(matrix[i]);
  }

  for (int i = 0; i < n; i++) {

    free(output[i]);
  }

  free(matrix);
  free(output);
}

```

### Dynamic Arrays

#### Approach 1 
```C
typedef struct 
{
	size_t length;
	size_t capacity;
	size_t item_size;
	void *item

}Array;

//Returns a struct1
Array array_init(size_t item_size,size_t initial_capacity)
{
	return(Array){
		.capacity = initial_capacity,
		.item_size=item_size,
		.items = malloc(initial_capacity * item_size),
	};

}

```

#### Approach Tsoding

![[Pasted image 20260721163341.png]]

```C
#include <stddef.h>
#include <stdio.h>
#include <stdlib.h>
typedef struct
{
    int *item;
    size_t index; //wegen Memory
    size_t capacity; // wegen Memory
} Array;

int main(void)
{
    Array xs = {0}; /* Initialize the Array*/

    for (int i = 0; i < 10; i++)
    {
        if (xs.capacity <= xs.index) // bound check
        {
            if (xs.capacity == 0) //per default:initialised with 0
            {
                xs.capacity = 256;
            }
            else
            {
                xs.capacity *= 2;
            }
            xs.item = realloc(xs.item, xs.capacity * sizeof(*xs.item)); //sizeof(int)
        }
        xs.item[xs.index++] = i;
    }

    for (size_t i = 0; i < xs.index; i++)
    {
        printf("%d\n", xs.item[i]);
    }

    return 0;
}
```

```C
#include <stddef.h>
#include <stdio.h>
#include <stdlib.h>
typedef struct
{
    int *item;
    size_t index;
    size_t capacity;
} Array;

#define add_array(xs,s) \
do{\
        if (xs.capacity <= xs.index)\
        {\
            if (xs.capacity == 0)\
                xs.capacity = 256;\
            else\
                xs.capacity *= 2;\
            xs.item = realloc(xs.item, xs.capacity * sizeof(*xs.item));\
        }\
        xs.item[xs.index++] = i;\
}while(0)\


int main(void)
{
    Array xs = {0};

    for (int i = 0; i < 10; i++)
    {
	    add_array(xs,i);
    }

    for (size_t i = 0; i < xs.index; i++)
    {
        printf("%d\n", xs.item[i]);
    }

    return 0;
}
```

I love Tsodings big and meaty brain.

### Arrays & Strings Bound Checkings
An sich klar, aber es gibt kniffe 

```C

#define ARRAY_LENGTH(a) (sizeof(a)/sizeof(a[0]))

typedef struct Int32Array
{
	int32_t *items;
	int32_t  length;
	int32_t  capacity 
};

int Int32Array_Get(Int32Array array[], int32_t index)
{
	if(index >= 0 && index < array.length)
	{
		return array.items[index];
		
	}
	fprintf(stderr, "Array OutOfBounds\n")
	return 0;

	
}

void foo(Int32Array array)
{
	for(int i = 0; i <= array.length; i++) // <= ! Bound Chechking nötig
	{
		int item = Int32Aray_Get(array,i);
		
	}

}


int main(void)
{
	Int32Array array = {};
	

}



```


```C
typedef struct
{
	char *chars;
	int32_t length;
}String;

void PrintChars(String string)
{
	for(int i = 0; i < string.length; i++)
	{
		printf("%c", string.chars[i]);
	}

}


```
--> Vorteil String splicing!


#### VLA (Variable Length Array)

via malloc
 *DONT USE THEM* :LiFileExclamationPoint:  You can corrupt it!
 
```C

int main(void)
{
	int *xs = malloc(sizeof(int)*128);

	for(int i = 0; i < 128, i++)
	{
		xs[i] = i*i;
	}

	for(int i = 0; i < 128, i++)
	{
		printf("%d\N",x[i]);
	}

	free(xs);
	xs = NULL;
	return 0;

}
```


### Structs

Jedem Wert wird im Speicher es fix allokiert, sprich die variablen haben eine fixe Speicheradresse


```C
/*Tagged Struct*/
struct account {
  char username[32];
  char password[32];
  unsigned int uid;
};

/*Untagged structs*/
struct account
{
	...
	
}user1,user2;

/*Mixed:*/
struct account
{
	...
}user1,user2;


int main(void) {
  struct account user1 = {"Alice", "4lic3", 1};
  
  struct account user2 = {"Bob", "b5b", user1.uid + 1};
  
  /*Since C99*/
  struct account user1 = {.uid = 1, .username = "Alice", .password = "4lic3"}
}

```


##### Pointers and structs 

```C
struct account 
{
	char username[32];
	char password[32];
	unsigned int uid;
};

void foo(void)
{
	struct account user1 = {"Alice", "4lic3", 1};
	struct account *p = &user1;
	
	p->uid;
}

```

```C
#include <stdio.h>

// a larger struct which may carry a lot of data
struct Student {
    char name[50];
    unsigned int id;
    unsigned int semester;
    float gpa;
};

// passing by value
void print_student(struct Student s) {
    printf("Name: %s, ID: %d, in semester %d, with GPA: %.2f\n", s.name, s.id, s.semester, s.gpa);
}

// passing by pointer
void print_student(struct Student* s) {
    printf("Name: %s, ID: %d, in semester %d, with GPA: %.2f\n", s->name, s->id, s->semester, s->gpa);
}


```

Von [wikipedia](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#Pointers)
```C
struct Point p = { 3, 7 };
int x = p.x /* x = 3 */;
p.x = 10;
struct Point* pp = &p;
x = pp->x; /*x =  10*/
pp->x = 8; /* p.x = 8*/
```

##### Anonyme structs und arrays 

```C
#include <stdio.h>
struct Vector
{
    int x;
    int y;
};

int scalar(int s, struct Vector v)
{

    return s * v.x + s * v.y;
}

int array_sum(int length, int array[])
{
    int sum = 0;

    for (int i = 0; i < length; i++)
    {
        sum += i;
    }
    return sum;
}

int main(void)
{
    /*Wie in Java*/
    printf("%d\n", scalar(4, (struct Vector){5, 3}));
    printf("%d\n", array_sum(5, (int[]){1, 2, 3, 4, 5}));
}
```

```java
public class Test  
{  
    public static void main(String[] args)  
    {  
        System.out.println(scalar(3,(new Vector(2,3))));  
    }  
  
      
    private static class Vector  
    {  
        int x,y;  
          
        Vector(int x, int y)  
        {  
            this.x = x;  
            this.y =y;  
        }  
  
    }  
  
  
    private static int scalar(int s, Vector v)  
    {  
        return s*v.x+s*v.y;   
    }  
}
```


##### Singly Linked List
Die Knoten sind mit Pointern referenziert

```C
struct account_node
{
	char username[32];
	char password[32];
	unsigned int uid;
	struct account_node *next;

}; 

struct account_node user1,user2;
struct *account_node = &user1;

user1.next = &user2;
user2.next = NULL;

struct account_node *p = head;

while(p != NULL)
{
	p = p -> next
} 


```





-----
### Union

```C
union number 
{
	char c_number; // 1byte
	short s_number; // 2 bytes 
};

/* Zugriff auf union*/
union number i;
i.c_number = 0x42;
i.s_number = 0x6548;

```

### Struct vs Union

[reddit](https://old.reddit.com/r/learnprogramming/comments/gly5wr/c_is_it_better_to_use_struct_or_union_when_should/)

Within a union all the members share the same memory, so setting one member affects all the members. This _can_ be used to save memory, but it means you can only use one of the members at a time, and using one invalidates the others. Generally, this isn’t very desirable and can lead to all sorts of bugs.

```C
union {

int a;

int b; }
```

If I change a, the b also changes.

We’re way past the days of counting memory, so unions nowadays are often reserved for dealing with some very specific low-level data packing problems. General rule of thumb is, don’t use them unless you really know you need to use them.

#### Union und Pointer
```C
union val
{
	int *a;
	int *b;
};

int a = 3;
int *p = &a;

t.a = p;
printf("%d\n",*t.a);

```

Es gibt Millionenmöglichkeiten, es zu machen,

man kann auch sagen union hat kein pointer sondern nromale int, dementesprechen dann t.a = \*p;

----
### Enumeration

```C
/*Generelle Struktur*/
enum [TYPENAME]
{
	IDENTIFIER [ = VALUE] [, IDENTIFIER] [ = VALUE]*
};

/* Zugriff*/
enum boolean 
{
	FALSE = 0,
	TRUE
};

enum account 
{
	PREMIUM = 1,
	STANDARD = 2,
	BUSINESS = 4,
	FREE = 3
};


void foo(void)
{
	enum account account1;
	account1 = BUSINESS;
	
}


```

----
### Typedef

```C

/* stdint . h */
...
typedef signed char int8_t ;
typedef unsigned char uint8_t ;
typedef signed int int16_t ;
typedef unsigned int uint16_t ;
...
# include < stdint .h >
...
uint8_t i ;
for ( i = 0; i < 10; ++ i )
printf ( " % u \ n " , i );
...



```


```C
struct account 
{
	char username[32];
	char password[32];
	unsigned int uid;

};
typedef struct account account_t;

typedef struct account 
{
	char username[32];
	char password[32];
	unsigned int uid;

} account_t;

...

void foo(void)
{
	account_t user1 = {"alice","4l1c3",41};

}



```

---
Bisschen hervorgegriffen:

### Lookup Table 

```C
#include <stdio.h>

static const char case_convert_lookup[] = {['a'] = 'A',

                                           ['b'] = 'B',

                                           ['c'] = 'C'

};

int main(void)
{
    printf("%c\n", case_convert_lookup['a']);
}


```


*Achtung: Die Indizes sollten nicht so groß sein*

### Tagged Union (Nesting)
Wozu? Dynamisches Schreiben in C
```C
#include <stdbool.h>
#include <stdio.h>

enum tag
{
    TAG_BOOL,
    TAG_INT,
    TAG_FLOAT
};

struct dynamic
{
    enum tag tag;

    union {
        bool b;
        int i;
        float f;
    } value;
};

int main(void)
{

    struct dynamic d;

    d.tag = TAG_FLOAT;

    float p = d.value.f = 2.31;

    printf("%.2f\n", p);
}



```

### Bitfields
Wannn? Wenn du Binärdaten parst, BMP, TCP/IP, ICMP
Sehr wichtig
Beispiel
```C
#include <stdbool.h>

struct foo
{
    int first : 4; //verbraucht 4 bytes 
    int second : 4; //verbraucht 4 bytes 
    int alone : 1; //verbraucht 1 byte 
    int last : 7; //verbraucht 7 bytes 
};

int main(void)
{

    struct foo f;

    f.first = 2;
    f.second = 2;
    f.alone = 0;


    /* parse the data into foo*/

    int *fd = open(...);
    read(fd, f, sizeof(f));
}


```

----


### Linked Lists
https://www.learn-c.org/en/Linked_lists

```C

typedef struct Node
{
    int *data;
    int capacity;
    struct Node *next;
} Node;

int main(void)
{
    // Main node
    Node *n = NULL;
    n = (Node *)malloc(sizeof(Node));
    n->capacity = 10;
    n->data = arrayInitializer(n->capacity);
    n->next = NULL;

    // Second Node
    Node *m = NULL;
    m = (Node *)malloc(sizeof(Node));
    m->capacity = 12;
    m->data = arrayInitializer(m->capacity);
    
    // Linking
    n->next = m;
    
}


```

# Man pages 
Um alle möglichen EInträge zu sehen

`man -f PAGE_NAME`

ZB. 
`man -f open`
liefert 

```bash
$~ man -f open
open (2)             - open and possibly create a file
open (3p)            - open file
open (3perl)         - perl pragma to set default PerlIO layers for input and output
open (n)             - Open a file-based or command pipeline channel
```

Um es zu öffnen:
´man 2 open´

#### Suchen 
`man -k keyword`
`apropos keyword`

# Source Files und Programmstruktur

### Header Files

- Contains prototypes and constants
- Contaions *no* definitions of functions 
- use `#include`
	- `#include <account.h> searches in library path`
	- `#include "account.h" searches in local folder`


```C
/* account.h */
# ifndef ACCOUNT_H /* include guard */
# define ACCOUNT_H

typedef struct { ... } account_t ;

void acc_init ( account_t *);
void acc_set_password ( account_t * , const char *);
# endif /* ACCOUNT_H */
```



In `account.c`
```C
# include " account.h "
void acc_init ( account_t * account )
{
/* do stuff here to initialize
* the account ( check dublicates .
* constraints etc .) */
/* assign uid if done correctly */
}
void acc_set_password ( account_t * account ,const char * pw )
{
/* set password for account */
}

int main ( void )
{
	account_t account ;
	account.username = " alice " ;
	account.password = " 4 l1c3 " ;
	acc_init (& account );
	acc_set_password (& account , " n3wl1c3 " );
	return 0;
}

```

```bash 
$~ gcc -c account.c
$~ gcc -c prog.c
$~ gcc -o prog prog.o account.o
```


[BeeJee](https://beej.us/guide/bgc/html/index-wide.html#multifile-projects)


### ASan
Address Sanitazation 
`clang -fsanitize=address`

--> Nur im Test-branch o.Ä nutzen



# Funktionen

relativ trivial, aber funktionen können auch n variablen annehmen
`void foo(int a, ...)`

Es kann alles mögliche retourniewrt werden,
es geht auch ein Struct


### Pointer as Parameter

```C
void minMaxArray(int *array, int n, int *min, int *max);

typedef struct
{

    int *data;
    int length;

} Array;

int main(void)
{
    Array xs = {0};
    xs.data = arrayInitializer(10);
    int x = 10;
    int *myarray = arrayInitializer(x);

    int lo, hi;
    minMaxArray(xs.data, 10, &lo, &hi);
    printf("%d %d", lo,hi);
}

void minMaxArray(int *arr, int n, int *min, int *max)
{
    *max = *min = arr[0];
    for (int i = 1; i < n; i++)
    {
        if (arr[i] < *min)
            *min = arr[i];
        if (arr[i] > *max)
            *max = arr[i];
    }
}


```



### Pointerfunctions 
```C
int *arrayInitializer(int n);

int main(void)
{
	int size = 10;
    int *myarray = arrayInitializer(size);
}

int *arrayInitializer(int n)
{
    return (int*)malloc(sizeof(int) * n);
}
```


# Error Handling

Angenommen test.c gibt es nicht wir bekommen dann ein SIGABRT durch den assert
```C
int main(void)
{
	FILE *f = fopen("test.c","r");
	assert(f != NULL);
	int c;
	while ((c = fgetc(f)) != EOF)
	{
		fputc(c,f);
	}

	return 0;
}
```


die Standardbibliothek errno.h fixt es:
```C
#include <errno.h>
int main(void)
{
	FILE *f = fopen("test.c","r");

	if(f == NULL)
	{
		printf("%d\n",errno);
		perror(NULL); // perror("ERROR:\t")
		return 1;
	}

	int c;
	while ((c = fgetc(f)) != EOF)
	{
		fputc(c,f);
	}

	return 0;
}
```

um die Standarderrorliste zu sehen:
`errno --list`

Mit `perror` wird der System error mitgeprintet siehe man page.

Anhand des Integer Wertes von errno.


Ohne perror
```C
#include <errno.h>
int main(void)
{
	FILE *f = fopen("test.c","r");

	if(f == NULL)
	{
		printf("%d: %s\n",errno,sterror(errno));
		return 1;
	}

	int c;
	while ((c = fgetc(f)) != EOF)
	{
		fputc(c,f);
	}

	return 0;
}
```



# Regex

Die Bibliothek <regex.h> hinzufügen und dann manpages lesen


```C
int main(void)
{
	regex_t preg;
	assert(regcomp(&preg,"ab*", REG_EXTENDED) == 0); // for amore detailed error see Error Handling, keyword perror
	
	assert(regcomp(&preg,"(ab*)(ac+)", REG_EXTENDED) == 0);	
		
	int result = regexec(&preg, "cbbbb",0,NULL,0);
	if(result == 0)
		printf("match")
	else if(result == REG_NOMATCH)
		printf("no match");
	
	regfree(&preg);
	return 0;
}
```



### Regex Arrays
siehe für .rm_so und rm_eo man regex.h (benötigt die posix programmers manual)

```C
	regex_t preg;	
	assert(regcomp(&preg,"(ab*)(cd*)", REG_EXTENDED) == 0);	
	const size_t nmatch = 10;
	regmatch_t pmatch[nmatch+1];
	char *s = "abbcdddddd";
	int result = regexc(&preg,s,nmatch,pmatch,0);
	
	if(result == 0)
	{
		printf("match\n");
		
		for(size_t i = 0; pmatch[i].rm_so != -1 && i < nmatch;i++)
		{
			char buff[256] = {0};
			strncpy(buf,s+pmatch[i].rm_so, pmatch[i].rm_so-pmatch[i].rm_eo);
			printf("start %d, end: %d: %s\n",pmatch[i].rm_so,pmatch[i].rm_eo,buf);
		
		}
		
	}
	else if(result == REG_NOMATCH)
		printf("no match\n");
	
	regfree(&preg);
	return 0;

```

### Regex Error Handling
```C
int main(void)
{
	regex_t preg;
	int errorcode = regcomp(&preg, "ab***", 0);
	
	if(errorcode != 0)
	{
		const size_t buff_size = 129;
		char errbuf[buff_size+1];		
		regerror(errorcode,&preg,errbuf,buff_size);
		printf("regex error: '%s': '%s'\n","ab***",errbuf);
		
	}
	
	regfree(&preg);
	return 0;
}
```

# Compound Literals

Ich bin dem zufällig gestoßen, ich habe mich mit structs und pointers und anderem Zeiug herumgespielt

Und dann bin ich diesem Prinzip in C zugestoßen, [Compound literals](https://en.cppreference.com/c/language/compound_literal), ich hätte nie
gedacht, dass es sowas geben würde. (Es geht bei structs, unions und arrays sogar wtf)

Es hängt auch etwas mit anonymen structs ab.

Also zum Beispiel:
```C

typedef struct
{
    char *s1;
    size_t length;
} String;

typedef struct
{
    uint16_t pid;
    String pName;
} Person;

void personNameSetter(Person *p)
{
    p->pName = (String){"Cihat"};
}

int main(void)
{
    Person *pP = (Person *)malloc(sizeof(Person));
}

```

Der Grund warum man das "Casten" muss in ein String struct, was ja von der Idee ja insane ist, weil ein struct ja eine Struktur ist und nicht ein Datentyp.


ohne compound literals
```C
typedef struct
{
    char *s1;
    size_t length;
} String;

typedef struct
{
    uint16_t pid;
    String pName;
} Person;

void personNameSetter(Person *p)
{
    p->pName.s1 = "Cihat";
    p->pName.length = strlen("Cihat");
}

int main(void)
{
    Person *pP = (Person *)malloc(sizeof(Person));
}
```

oder 
```C

typedef struct
{
    char *s1;
    size_t length;
} String;

typedef struct
{
    uint16_t pid;
    String pName;
} Person;

void personNameSetter(Person *p,String name)
{
    p->pName = name;
}

int main(void)
{
    Person *pP = (Person *)malloc(sizeof(Person));
}

```





# Structs und Funktionen 

Ich bin, wtf junge
```C

typedef struct{
	char *name;
	uint8_t name_lenght
}String;


Person callPerson(uint16_t pid, String name)
{
	/* gültiger C code btw*/
    //return (Person){.pid = 1, .pName = (String){"Cihat"}};

    Person p;
    p.pid = 1;
    p.pName.s1 = "Cihat";
    p.pName.length = strlen(p.pName.s1);
    return p;
}

int main(void)
{
    Person (*f)(uint16_t,String) = callPerson;
	
	Person p = f(2,(String){"Cihat"});
	
	printf("%d\n%s\n",p.pid,p.pName.s1);
	
}
```






# Typesafe Inheritance
[src](http://www.deleveld.dds.nl/inherit.htm)

### The good:  

- For most things you dont have to do any casting at all.  This is very unusual for inheritence schemes in C.
- Memory layout and efficiency is probably quite similar to what you would get using classes in C++.
- Hidden base classes (like private derivation in C++) are possible.

### The bad:  

- The class declarations are verbose and brittle and there remains the possibility for subtle problems if you dont follow some reasonably simple conventions:
- 1. The base class must come first in the declaration.
    2. If you initialise from static data then the base class you want to initialse must come first in the base class union.
    3. There is no compiler warning when trying to derive from incompatible classes.
- Without wrapper macros the source code can be a bit hard to follow

### The ugly:  

- If data is initialized statically then multiple `{{ ... }}` are necessary and this is ugly.

Douglas Eleveld  
deleveld@dds.nl
----


```C
/* Typesafe inheritance in C  
  
Doug Eleveld (deleveld@dds.nl)  
  
The inheritance tree in this example like this:  
  
   ANIMAL  
    | weight  
    | name  
    |  
    +- INSECT  
    |     exoskeleton  
    |  
    +- MAMMAL  
        | fur  
        |  
        +- MONKEY  
        |     tail  
        |  
        +- HUMAN          <-- MAMMAL is hidden base class  
              thumb  
  
   This has written using DJGPP.  
*/  
  
#include <stdlib.h>  
#include <stdio.h>  
  
/* An animal --------------------------------------------------------------*/  
typedef struct ANIMAL_DATA {  
    int weight;  
    const char * name;  
} ANIMAL_DATA;  
  
typedef struct ANIMAL {  
    union {  
        ANIMAL_DATA animal;  
    } base;  
} ANIMAL;  
  
/* This macro perfoms like a typesafe cast */  
#define GETANIMAL(self) (&(self)->base.animal)  
  
/* Accessor macros (syntactic-sugar) */  
#define weight(self)    (GETANIMAL(self)->weight)  
#define name(self)      (GETANIMAL(self)->name)  
  
/* An insect is an animal -------------------------------------------------*/  
typedef struct INSECT_DATA {  
    union {  
        ANIMAL_DATA animal;  
    } base;  
    int exoskeleton;  
} INSECT_DATA;  
  
typedef struct INSECT {  
    union {  
        INSECT_DATA insect;  
        ANIMAL_DATA animal;  
    } base;  
} INSECT;  
  
#define GETINSECT(self)   (&(self)->base.insect)  
#define exoskeleton(self) (GETINSECT(self)->exoskeleton)  
  
/* An mammal is also an animal --------------------------------------------*/  
typedef struct MAMMAL_DATA {  
    union {  
        ANIMAL_DATA animal;  
    } base;  
    int fur;  
} MAMMAL_DATA;  
  
typedef struct MAMMAL {  
    union {  
        MAMMAL_DATA mammal;  
        ANIMAL_DATA animal;  
    } base;  
} MAMMAL;  
  
#define GETMAMMAL(self) (&(self)->base.mammal)  
#define fur(self)       (GETMAMMAL(self)->fur)  
  
/* An monkey is a mammal with a tail --------------------------------------*/  
typedef struct MONKEY_DATA {  
    union {  
        MAMMAL mammal;  
        ANIMAL animal;  
    } base;  
  
    int tail;  
} MONKEY_DATA;  
  
typedef struct MONKEY {  
    union {  
        MONKEY_DATA monkey;  
        MAMMAL_DATA mammal;  
        ANIMAL_DATA animal;  
    } base;  
} MONKEY;  
  
#define GETMONKEY(self) (&(self)->base.monkey)  
#define tail(self)      (GETMONKEY(self)->tail)  
  
/* An human is a mammal with a opposable thumb ----------------------------*/  
typedef struct HUMAN_DATA {  
    union {  
        MAMMAL mammal;  
        ANIMAL animal;  
    } base;  
    int thumb;  
} HUMAN_DATA;  
  
typedef struct HUMAN {  
    union {  
        HUMAN_DATA human;  
        /* MAMMAL_DATA mammal; Conversion to MAMMAL_DATA is hidden  
                               So this is a private base class */  
        ANIMAL_DATA animal;  
    } base;  
} HUMAN;  
  
#define GETHUMAN(self) (&(self)->base.human)  
#define thumb(self)    (GETHUMAN(self)->thumb)  
  
/* Trying out inheritance in C ------------------------------------------- */  
int main(void)  
{  
    ANIMAL unknown;  
    INSECT beetle;  
    MAMMAL beaver;  
    MONKEY george;  
    HUMAN programmer;  
      
    /* A generic animal */  
    weight(&unknown) = 1;  
    name(&unknown) = "unknown";  
  
    /* A beetle with a thick exoskeleton */  
    weight(&beetle) = 1;  
    name(&beetle) = "Herbie";  
    exoskeleton(&beetle) = 100;  
  
    /* A furry beaver */  
    weight(&beaver) = 10;  
    name(&beaver) = "Barry";  
    fur(&beaver) = 5;  
      
    /* The monkey has a long tail */  
    weight(&george) = 10;  
    name(&george) = "George";  
    fur(&george) = 1;  
    tail(&george) = 10;  
  
    /* Programmers are humans */  
    weight(&programmer) = 150;  
    name(&programmer) = "Steve";  
/*    fur(&programmer) = 1;   ERROR: No public access to MAMMAL base class */  
    thumb(&programmer) = 2;  
  
    /* Animals have weight */  
    printf("\n\n");  
    printf("%s animal has weight %i\n\n", name(&unknown), weight(&unknown));  
  
    /* Beetles have weight and exoskeleton */  
    printf("%s the beetle has weight %i\n", name(&beetle), weight(&beetle));  
    printf("%s the beetle has exoskeleton %i\n\n", name(&beetle), exoskeleton(&beetle));  
  
    /* Mammals have weight and fur */  
    printf("%s the beaver has weight %i\n", name(&beaver), weight(&beaver));  
    printf("%s the beaver has fur %i\n\n", name(&beaver), fur(&beaver));  
  
    /* Monkeys have weight, fur and tails */  
    printf("%s the monkey has weight %i\n", name(&george), weight(&george));  
    printf("%s the monkey has fur %i\n", name(&george), fur(&george));  
    printf("%s the monkey has tail %i\n\n", name(&george), tail(&george));  
  
    /* Humans have weight and thumbs */  
    printf("%s the programmer has weight %i\n", name(&programmer), weight(&programmer));  
    printf("%s the programmer has thumb %i\n\n", name(&programmer), thumb(&programmer));  
  
    /* Accessing a hidden base class gets a compile time error */  
    /*fur(&programmer);          ERROR */  
  
    /* The wrong function gets a compile-time error */  
    /*tail(&programmer);         ERROR */  
    /*exoskeleton(&programmer);  ERROR */  
    /*exoskeleton(&george);      ERROR */  
  
    return 0;  
}

```
## Output:

unknown animal has weight 1  
  
Herbie the beetle has weight 1  
Herbie the beetle has exoskeleton 100  
  
Barry the beaver has weight 10  
Barry the beaver has fur 5  
  
George the monkey has weight 10  
George the monkey has fur 1  
George the monkey has tail 10  
  
Steve the programmer has weight 150  
Steve the programmer has thumb 2