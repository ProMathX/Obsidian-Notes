#C
#studies 
#Betriebssysteme
## String literal 

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



## Bitfields
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




## Datenstrukturen

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


### Singly Linked Lists
https://www.learn-c.org/en/Linked_lists
https://en.wikipedia.org/wiki/Linked_list
https://www.youtube.com/watch?v=_jQhALI4ujg
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

#### Anmerkung zum Double Pointer

Von C-learn.org

> [!cite]
> To add to the beginning of the list, we will need to do the following:
> 
>     Create a new item and set its value
>     Link the new item to point to the head of the list
>     Set the head of the list to be our new item
> 
> This will effectively create a new head to the list with a new value, and keep the rest of the list linked to it.
> 
> Since we use a function to do this operation, we want to be able to modify the head variable. To do this, we must pass a pointer to the pointer variable (a double pointer) so we will be able to modify the pointer itself.


```C
void push(node_t ** head, int val) {
    node_t * new_node;
    new_node = (node_t *) malloc(sizeof(node_t));

    new_node->val = val;
    new_node->next = *head;
    *head = new_node;
}

```

Der Grund warum man hier einen Double Pointer verwendet ist, soweit ich das verstanden
habe, dass man die Referenz des Pointer ändert und nicht auf das was der Pointer zeigt.


mit meiner eigenen Implemention
[] muss noch Daten abspeichern/ändern
```C
#include <assert.h>
#include <errno.h>
#include <iso646.h>
#include <stddef.h>
#include <stdio.h>
#include <stdlib.h>
#include <strings.h>
typedef struct node {
  int val;
  struct node *next;
} node_t;

node_t *createNode(int data) {
  node_t *rv = (node_t *)malloc(sizeof(node_t));

  if (rv == NULL)
    fprintf(stderr, "Error allocating memory");

  rv->val = data;
  rv->next = NULL;
  return rv;
}
void inserAtLast(node_t *head, int data) {
  node_t *current = head;
  while (current->next != NULL) {
    current = current->next;
  }

  current->next = createNode(data);
}

void inserAtFirst(node_t **head, int data) {
  node_t *newNode = createNode(data);

  newNode->next = *head;

  *head = newNode;
}

void popAtFirst(node_t **head) {
  if (*head == NULL) {
    fprintf(stderr, "Error");
  }

  node_t *tmp = (*head)->next;
  free(*head);
  *head = tmp;
}

void popAtLast(node_t *head) {
  node_t *current = head;
  while (current->next->next != NULL) {
    current = current->next;
  }
  free(current->next);
  current->next = NULL;
}

void popAtIndex(node_t *head, int data, int pos) {
  node_t *current = head;

  for (int i = 0; i < pos - 1; i++) {
    current = current->next;
  }

  node_t *tmp = current->next;
  current->next = tmp->next;
  free(tmp);
}

void pushAtIndex(node_t **head, int data, int pos) {
  node_t *current = *head;
  node_t *toBeInserted = createNode(data);

  for (int i = 0; i < pos - 1; i++) {
    current = current->next;
  }

  current->next = toBeInserted;
  toBeInserted->next = *head;
}

void print_list(node_t *head) {
  node_t *current = head;

  while (current != NULL) {
    printf("%d\n", current->val);
    current = current->next;
  }
}

int main(void) {
  node_t head;
  node_t *test_list = (node_t *)malloc(sizeof(node_t));
  test_list->val = 1;
  test_list->next = (node_t *)malloc(sizeof(node_t));
  test_list->next->val = 2;
  test_list->next->next = (node_t *)malloc(sizeof(node_t));
  test_list->next->next->val = 3;
  test_list->next->next->next = (node_t *)malloc(sizeof(node_t));
  test_list->next->next->next->val = 4;
  test_list->next->next->next->next = NULL;
  popAtIndex(test_list, 9, 2);

  print_list(test_list);

  return 0;
}



```




### Circular Buffer
![Circular Buffer](https://upload.wikimedia.org/wikipedia/commons/f/fd/Circular_Buffer_Animation.gif)



Source:https://embedjournal.com/implementing-circular-buffer-embedded-c/





### Array of Structs (AoS) 
Relativ Banal? 

```C
typedef struct A{ int val; }A;

int main(void)
{
	A test[3];
	
	for(int i = 0; i < 3; ++i)
	{
		test[i].val = ++i;
	}

	return 0;
}



```

### Struct of Arrays (SoA)
```C
struct Vector3List {
    float x[N];
    float y[N];
    float z[N];
};

struct Vector3List points;

float get_point_x(size_t i) {
    return points.x[i];
}



```


### **Array of structures of arrays** (**AoSoA**)

```C
struct Vector3x8 {
    float x[8];
    float y[8];
    float z[8];
};

struct Vector3x8 points[(N + 7) / 8];

float get_point_x(size_t i) {
    return points[i / 8].x[i % 8];
}


```
