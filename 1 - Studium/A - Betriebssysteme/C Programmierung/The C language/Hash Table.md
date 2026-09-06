#C #Betriebssysteme 
 #Datenstrukturen  



They are in the standard libraries
```C

void print_entry(ENTRY *entry)
{
	if(entry == NULL)
	{
		printf("NULL");
		return;
	}
	printf("%s -> %d\n", entry->key, entry->data);

}


int main(void)
{
	hcreate(30); //-> this means only one hashtable 

	ENTRY entry = {.key = "hello", .data = (void *)1};
	ENTRY *result = hsearch(entry, ENTER);
	print_entry(result);

	result = hsearch(entry, FIND);
	print_entry(result);
	
	hdestroy();
	return 0;
}
```
