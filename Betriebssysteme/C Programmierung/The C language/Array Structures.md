https://www.geeksforgeeks.org/c/c-array-of-structure/
https://en.wikipedia.org/wiki/AoS_and_SoA



Teilweise sind array of structures geistig behindert.


Hier 
```C
#include <stdint.h>
#include <stdio.h>
typedef struct Test {
  uint8_t uid;
} Test;

void initialize(Test *data, uint8_t value) { data->uid = value; }

int main(int argc, char **argv) {
  Test test[3] = {0};

  Test *read = &test[0];

  for (int i = 0; i < 3; ++i) 
  {
    Test *loop = &read[i];
    initialize(loop, i * 2);
  }
  // ODER

  for (int i = 0; i < 3; ++i) 
  {
    initialize(loop, i * 2);
  }  
  

  for (int i = 0; i < 3; ++i) {
    printf("%d\n", read[i].uid);
  }


  return 0;
}



```

Also das geistig behinderte an der Sache ist die, `read`, was ein pointer ist, derefenziert automatisch bei `read[i]` 
Deshlab muss es bei der Funktion eingelesen werden.

```C
#include <stdint.h>
#include <stdio.h>
typedef struct Test {
  uint8_t uid;
} Test;

void initialize(Test *data, uint8_t value) { data->uid = value; }

int main(int argc, char **argv) {
  Test test[3] = {0};


  for (int i = 0; i < 3; ++i) {
    initialize(&test[i], i * 2);
  }

  for (int i = 0; i < 3; ++i) {
    printf("%d\n", test[i].uid);
  }


  return 0;
}


```


# Warum Pointer? 

[src](https://www.reddit.com/r/C_Programming/comments/1ignu4n/why_and_when_should_i_use_pointers/)


>Say you want to pass a large object into a function, modify it and then return it. Without pointers you would have to copy the variable twice (excluding RVO) whereas with a pointer/reference you just have to pass the location and don’t have to return anything.

>Another example is with using external libraries, most of the time they handle their memory and the way to access the objects created via the library is via pointers.

