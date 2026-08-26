#C 
#Betriebssysteme 

[src](https://www.youtube.com/watch?v=-9Z7aiz6fHg&list=PL71Y0EmrppR0KyZvQWj63040UEzKQU7n8&index=23)

es ist fnmath und glob 

aber die `errfunc` ist hier derfiniert [link](obsidian://open?vault=Obsidian-Notes&file=Betriebssysteme%2FC%20Programmierung%2FThe%20C%20language%2FFunktionen)

Was ziemlich handy sein kann 

```C

int errfunc(const char *epath, int errno)
{
	printf("Error for: %s: %s\n", epath, strerror(errno));
	exit(EXIT_SUCCES);
}


```

## Pattern Syntax

```C
int main(void)
{
	char *s = "hello World!";
	int result = fnmatch("he*wo*",s,0);
	
	if(result == 0) printf("match\n");
	
	else if( result == FNM_NOMATCH) printf("no match\n");

	return 0;

}
```


```man
       FNM_EXTMATCH
              If this flag (a GNU extension) is set, extended patterns are
              supported, as introduced by ’ksh’ and now supported by other
              shells.  The  extended  format  is  as  follows,  with  pat‐
              tern-list being a ’|’ separated list of patterns.

       ’?(pattern-list)’
              The pattern matches if zero or one occurrences of any of the
              patterns in the pattern-list match the input string.

       ’*(pattern-list)’
              The  pattern  matches  if zero or more occurrences of any of
              the patterns in the pattern-list match the input string.

       ’+(pattern-list)’
              The pattern matches if one or more occurrences of any of the
              patterns in the pattern-list match the input string.

       ’@(pattern-list)’
              The pattern matches if exactly one occurrence of any of  the
              patterns in the pattern-list match the input string.

       ’!(pattern-list)’
              The  pattern  matches  if the input string cannot be matched
              with any of the patterns in the pattern-list.
```

Mehr dazu [hier](obsidian://open?vault=Obsidian-Notes&file=Betriebssysteme%2FC%20Programmierung%2FThe%20C%20language%2FRegex)



## Glob


```C
int main(void)
{
	glob_t pglob;
	int result = glob("*.c",GLOB_MARK,NULL,&pglob);
	
	for(size_t i = 0; i < pglob.gl_pathc; i++)
	{
		printf("%zu: %s\n",i,pglob.glpathv[i]);
	}
	
	globfree(&pglob);
	return 0;

}
```


in kombination mir `errfunc`

```C
int errfunc(const char *epath, int errno)
{
	printf("Error for: %s: %s\n", epath, strerror(errno));
	exit(EXIT_SUCCES);
}


int main(void)
{
	glob_t pglob;
	int result = glob("*.c",GLOB_MARK,errfunc,&pglob);
	
	for(size_t i = 0; i < pglob.gl_pathc; i++)
	{
		printf("%zu: %s\n",i,pglob.glpathv[i]);
	}
	
	globfree(&pglob);
	return 0;

}
```



