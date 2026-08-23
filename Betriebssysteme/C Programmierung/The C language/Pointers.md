#C
#studies 
#Betriebssysteme 


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



