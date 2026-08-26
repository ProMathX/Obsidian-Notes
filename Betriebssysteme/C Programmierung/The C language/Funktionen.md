#C
#studies 
#Betriebssysteme 



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



Wann braucht man das? 

Beispiel man hat eine Funtkion und man benötigt einen Wert innerhlab der Funktion.
[bsp](https://github.com/cacharle/globule/blob/master/src/glob.c)
```C
int
glbl_glob(const char *pattern,
          int         flags,
          int (*errfunc)(const char *epath, int eerrrno),
          glbl_glob_t *pglob)
{



```

### Funktionen und return value
Angenommen wir haben eine funktion `double atof(char s[])`, wir können die funktion in main.c so aufraufen
(Entnommen aus dem C Buch)

```C
double sum, atof(char []);
```

somit ist char [] ein placeholder wodurch wir mit getline einen String rein parsen können

