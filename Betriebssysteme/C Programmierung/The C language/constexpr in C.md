#C #Betriebssysteme 

## C23 Standard btw



constant in c 

```C

#define LEN 10 
static const size_t len = 10;

static int xs[LEN] = {-1}; // works

static int xs[len] = {-1}; //error

```

```C
constexpr size_t len = 10;
static int xs[len] = {-1}; //works
```

`gcc -std=c23 main.c`