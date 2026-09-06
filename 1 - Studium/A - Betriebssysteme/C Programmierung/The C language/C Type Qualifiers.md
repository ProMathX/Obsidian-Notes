### `volatile`
[src](https://en.cppreference.com/c/language/volatile)
[Zitat:](https://stackoverflow.com/questions/246127/why-is-volatile-needed-in-c)
> [!cite]
> volatile tells the compiler not to optimize anything that has to do with the volatile variable.
> 
> There are at least three common reasons to use it, all involving situations where the value of the variable can change without action from the visible code:
> 
>     When you interface with hardware that changes the value itself.
>     
>     When there's another thread running that also uses the variable.
>     
>     When there's a signal handler that might change the value of the variable.


> [!cite] Zitat 2
> volatile in C actually came into existence for the purpose of not caching the values of the variable automatically. It will tell the compiler not to cache the value of this variable. So it will generate code to take the value of the given volatile variable from the main memory every time it encounters it. This mechanism is used because at any time the value can be modified by the OS or any interrupt. So using volatile will help us accessing the value afresh every time.


Aber achtung, laut dem Linux kernel contributers, nicht volatile nutzen
https://mjmwired.net/kernel/Documentation/volatile-considered-harmful.txt

Jedoch ist die beste Quelle von OSDEV,: https://wiki.osdev.org/Volatile_(keyword)

Kurz: Volatile wird verwendet, wenn ich dem Compiler sage, hey, lies den Wert immer wieder ein, das ist nützlich wenn ich es update durch eine andere Funktion zb. 

Also 
`The volatile  keyword gives an indication to the compiler/optimizer that it should always perform a read or write to a variable or memory without caching it locally.`

---


### `restrict` 
Von Wikipedia:
[src](https://en.wikipedia.org/wiki/Restrict)
> [!cite]
> In the C programming language, restrict is a type qualifier that can be applied to a pointer to hint to the compiler that for the lifetime of that pointer, no other pointer will be used to access the same pointed-to object.


Bsp:

```C
#include <stdio.h>

void multiply_arrays(int *restrict arr1, int *restrict arr2, int *restrict result, int size) {
  
    // Loop through the arrays and multiply corresponding elements
    for (int i = 0; i < size; i++) {
      
        // Multiply and store the result in the result array
        result[i] = arr1[i] * arr2[i];  
    }
}

int main() {
  
    // Initialize two arrays with values
    int arr1[] = {1, 2, 3};
    int arr2[] = {4, 5, 6};
    int result[3];

    // Call the multiply_arrays function to multiply elements of arr1 and arr2
    multiply_arrays(arr1, arr2, result, 3);

    // Print the resulting array
    for (int i = 0; i < 3; i++) {
        printf("%d ", result[i]);
    }

    return 0;
}

```
[src](https://www.geeksforgeeks.org/c/restrict-keyword-c/)

