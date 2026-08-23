#C
#studies 
#Betriebssysteme 



### ASan
Address Sanitazation 
`clang -fsanitize=address`

--> Nur im Test-branch o.Ä nutzen

### Valgrind

`valgrind --leak-check=full --show-leak-kinds=all -s ./myProgram`


Angenommen test.c gibt es nicht wir bekommen dann ein SIGABRT durch den assert
```C
int main(void)
{
	FILE *f = fopen("test.c","r");
	assert(f != NULL);
	int c;
	while ((c = fgetc(f)) != EOF)
	{
		fputc(c,f);
	}

	return 0;
}
```


die Standardbibliothek errno.h fixt es:
```C
#include <errno.h>
int main(void)
{
	FILE *f = fopen("test.c","r");

	if(f == NULL)
	{
		printf("%d\n",errno);
		perror(NULL); // perror("ERROR:\t")
		return 1;
	}

	int c;
	while ((c = fgetc(f)) != EOF)
	{
		fputc(c,f);
	}

	return 0;
}
```

um die Standarderrorliste zu sehen:
`errno --list`

Mit `perror` wird der System error mitgeprintet siehe man page.

Anhand des Integer Wertes von errno.


Ohne perror
```C
#include <errno.h>
int main(void)
{
	FILE *f = fopen("test.c","r");

	if(f == NULL)
	{
		printf("%d: %s\n",errno,sterror(errno));
		return 1;
	}

	int c;
	while ((c = fgetc(f)) != EOF)
	{
		fputc(c,f);
	}

	return 0;
}
```




