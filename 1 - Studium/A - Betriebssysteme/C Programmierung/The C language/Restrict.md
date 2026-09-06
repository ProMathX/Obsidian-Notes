#C #Betriebssysteme 

https://www.youtube.com/watch?v=xWQs59c78g4&list=PL71Y0EmrppR0KyZvQWj63040UEzKQU7n8&index=25


You specify the compiler that two seperate pointers point to different areas in memory




```C
void updatePointers(size_t* restrict a, size_t* restrict b, size_t* restrict x) {
    *a += *x;
    *b += *x;
}



```
