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




Das hat mich etwas offsetet, vor allem mit dem Multime File handling

Der Trick ist 
Wenn:

```C
FILE *INPUTFILE;
FILE *OUTPUTFILE = stdout
do{
	if((argc - optind) == 0)
	{
		INPUTFILE = stdin;
	}
	else
	{
		INPUTFILE = fopen(argv[optind], "r");
	}
		int c;
		
		while((c = fgetc(INPUTFILE)) != EOF)
		{
			fputc(foo(c),OUTPUTFILE);
			if(otherOption)
			{
				fflush(OUTPUTFILE);
				wait();
				
			}
		}
	fprintf(OUTPUTFILE,"\n");
	fclose(INPUTFILE)	

}while(++optind < argc)

fclose(OUTPUTSTREAM);
exit(EXIT_SUCCESS);


```

Als allgemeines Rezept kann ich nur das sagen:


Angenommen ein Programm soll, n viele dateien einlesen können, mindestens zwei flags haben und falls kein Output spezifiziert wurde dann stdout



Angenommen es gibt 2 Optionen optionA und optionB

```C
int main(int argc, char **argv)
{
	FILE *input = stdin;
	//Error hadnling
	FILE *output = stdout;
	//Error handling
	
	bool optionA= false;
	bool optionB = false;
	bool optionOut = false;
	
	
	int option;
	
	// Command Line parsing
	while((option = getop(argc, argv, "a:b:o:")) != -1)
	{
		switch(option)
		{
			case 'a' ... break;
			case 'b' ... break;
			case 'o' ... break;
			
			case ':' error() break;
			case '?' error() break;
		}	
	}
	
	
	// um bound checking von optind (von getopt bereitgestellt gibt an wie viele paramtere gecountet worden sind)
	
	if(optind >= argc){error();}
	
	// File Handling
	do
	{
		// Falls keine dateien eingeommen worden sind, dann stdin
		if((optind-argc) == 0)
		{
			input = stdin;
		}
		else
		{
			input = fopen(argv[optind], "r");
		}
		
		// jetzt datei einlesen
		int c
		
		while((c = fgetc(input)) != EOF)
		{
			if()
		
		}
	
	
	}while(++optind < argc);
	
	

}

```



