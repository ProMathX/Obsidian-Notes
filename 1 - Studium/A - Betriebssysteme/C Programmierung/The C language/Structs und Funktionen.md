#C
 #Datenstrukturen  
#studies 
#Betriebssysteme 

## Compound Literals


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
## Structs und Funktionen

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

## Typesafe Inheritance
Typesafe Inheritance
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

