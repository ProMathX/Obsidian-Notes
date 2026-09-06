#Funktional #Ocaml  

[src](https://ocaml.org/docs/values-and-functions)

As any other high-level functional programming language, the source code reads like math, if you can say so. [expression-oriented](https://en.wikipedia.org/wiki/Expression-oriented_programming_language)

```Ocaml
# "Every expression has a type";;
- : string = "Every expression has a type"

# 2 * 21;;
- : int = 42

# int_of_float;;
- : float -> int = <fun>

# int_of_float (3.14159 *. 2.0);;
- : int = 6

# fun x -> x * x;;
- : int -> int = <fun>

# print_endline;;
- : string -> unit = <fun>

# print_endline "Hello!";;
Hello!
- : unit
```



