#C
#studies 
#Betriebssysteme 


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


[BeeJee](https://beej.us/guide/bgc/html/index-wide.html#multifile-projects)

----


Endlich wieder vom C Buch:

Wenn man meherere C Dateien hat kann man miteinander glecihzeitig kompilieren.


Im Buch steht (veralllgemeinert) `cc main.c foo.c`, aber es kommt irgendwie zu einem
kompilierungsfehler. Deshlab ist es in C ja auch möglich `foo.c`als local header in `main.c`zu inkludieren.


Beispiel:
```C
/*main.c*/
#icluude "foo.c"

int main(void){
	foob();
	return 0;
}


```

und dann foo.c
```C
#include <stdio.h>
void foob(void)
{
	printf("Hello World"\n);
}
```



