#C

# Disclaimer

Für das Erstellen meiner C Erkentniss wurde keine KI verwendet

![[Pasted image 20260714193033.png]]

Für das Lernen und der Zusammenfassung

- [Youtube Playlist von einem Franzosen 10/10 ](https://youtube.com/playlist?list=PL71Y0EmrppR0KyZvQWj63040UEzKQU7n8&si=MBRaZZBmamGU9Ox7)
- K&R The C Programming Language 2nd Edition

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

(mit typedef definierte alias)
`uint8_t`, `int8_t`, `int32_t`,`uint32_t`, `int64_t`, `uint64_t`

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

----
### In C: 0 is false, everything else is true (even -1)

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
Das ist smart
```C
#define NRELEMENTS(a) (sizeof(a) / sizeof(a[0]))

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
	/* Vice versa*/
	
	


}
```

```C

#include <stdio.h>

int main(void)
{
    int a = 3;

    void *p = &a;

    printf("%p\n", p);
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

char const *cp = &c; /* same as const char * cp */

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
		printf("found a %s at %p\n",p,&p);
	}
	return 0;
}



```

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
	int (*f)(int, int) = f 
	
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



---
# Datenstrukturen

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
struct account_node = &user1;

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
