#C
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
Weil es kaum einheitlich ist, je nach Terminal konfiguration kann es rumspacken

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


![[Pasted image 20260711111646.png]]

----
In C: 0 is false, everything else is true (even -1)

----

#### goto 

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
### Macros
Das ist smart
```C
#define NRELEMENTS(a) (sizeof(a) / sizeof(a[0]))

```


----

Pointers

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
	*pin = (int *) pv; int *) /* is necessary in C ++ ,
							   * but not mandatory in C */
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






---
## Datatypes

struct Dataset 










