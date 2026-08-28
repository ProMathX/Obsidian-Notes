#C 
#Betriebssysteme 
https://www.youtube.com/watch?v=ZA3QfmabUKg&list=PL71Y0EmrppR0KyZvQWj63040UEzKQU7n8&index=33

mit getopt
```C

int main(int argc, char **argv)
{
	int option;
	//: takes an argument
	while((option = getopt(argc,argv,":a:b")) != -1)
	{
		switch(option)
		{
			case 'a':
				printf("i got a: %s lol\n",optarg);
				break;
			case 'b':
				printf("i got b lol\n");
				break;
			case '?':
				printf("ERROR\n");
				break;
			case ':':
				printf("Where arguments?");
				break;	
				
		}
	
	}
	
	
	for(int i = 0; i < argc; i++)
	{
		printf("%d: %s\n",i,argv[i]);
	}

	return 0;
}

```

getopt_long nix posix standard nur gnu standard





