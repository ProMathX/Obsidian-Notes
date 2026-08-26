

#C
#studies 
#Betriebssysteme 



`const` -> you're not changing the value after it has been initialised
(https://www.youtube.com/watch?v=PC8-Y62Qnws&list=PL71Y0EmrppR0KyZvQWj63040UEzKQU7n8&index=39)



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

Mehr dazu siehe hier [goto](obsidian://open?vault=Obsidian-Notes&file=Betriebssysteme%2FC%20Programmierung%2Fgoto)

## Function Pointers

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





