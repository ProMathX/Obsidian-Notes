#C
#studies 
#Betriebssysteme 



Die Bibliothek <regex.h> hinzufügen und dann manpages lesen


```C
int main(void)
{
	regex_t preg;
	assert(regcomp(&preg,"ab*", REG_EXTENDED) == 0); // for amore detailed error see Error Handling, keyword perror
	
	assert(regcomp(&preg,"(ab*)(ac+)", REG_EXTENDED) == 0);	
		
	int result = regexec(&preg, "cbbbb",0,NULL,0);
	if(result == 0)
		printf("match")
	else if(result == REG_NOMATCH)
		printf("no match");
	
	regfree(&preg);
	return 0;
}
```



### Regex Arrays
siehe für .rm_so und rm_eo man regex.h (benötigt die posix programmers manual)

```C
	regex_t preg;	
	assert(regcomp(&preg,"(ab*)(cd*)", REG_EXTENDED) == 0);	
	const size_t nmatch = 10;
	regmatch_t pmatch[nmatch+1];
	char *s = "abbcdddddd";
	int result = regexc(&preg,s,nmatch,pmatch,0);
	
	if(result == 0)
	{
		printf("match\n");
		
		for(size_t i = 0; pmatch[i].rm_so != -1 && i < nmatch;i++)
		{
			char buff[256] = {0};
			strncpy(buf,s+pmatch[i].rm_so, pmatch[i].rm_so-pmatch[i].rm_eo);
			printf("start %d, end: %d: %s\n",pmatch[i].rm_so,pmatch[i].rm_eo,buf);
		
		}
		
	}
	else if(result == REG_NOMATCH)
		printf("no match\n");
	
	regfree(&preg);
	return 0;

```

### Regex Error Handling
```C
int main(void)
{
	regex_t preg;
	int errorcode = regcomp(&preg, "ab***", 0);
	
	if(errorcode != 0)
	{
		const size_t buff_size = 129;
		char errbuf[buff_size+1];		
		regerror(errorcode,&preg,errbuf,buff_size);
		printf("regex error: '%s': '%s'\n","ab***",errbuf);
		
	}
	
	regfree(&preg);
	return 0;
}
```
