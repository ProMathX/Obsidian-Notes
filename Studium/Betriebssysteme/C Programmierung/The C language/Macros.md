#C
#studies 
#Betriebssysteme 


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





