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



