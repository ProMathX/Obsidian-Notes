Ja GDB verdient seinen eigenen Eintrag

1. - _backtrace full_: Complete backtrace with local variables
2. _up_, _down_, _frame_: Move through frames
3. _watch_: Suspend the process when a certain condition is met
4. _set print pretty on_: Prints out prettily formatted C source code
5. _set logging on_: Log debugging session to show to others for support
6. _set print array on_: Pretty array printing
7. _finish_: Continue till end of function
8. _enable_ and _disable_: Enable/disable breakpoints
9. _tbreak_: Break once, and then remove the breakpoint
10. _where_: Line number currently being executed
11. _info locals_: View all local variable
12. _info args_: View all function arguments
13. _list_: view source
14. _rbreak_: break on function matching regular expression


Source:https://stackoverflow.com/questions/1471226/most-tricky-useful-commands-for-gdb-debugger
Source: https://wiki.osdev.org/GDB

https://beej.us/guide/bggdb/



Um gdb zu starten:
	run $(program) ::arg1 ::arg2


## Breakpoints
<center>break main Break at the beginning of the main() function</center>
<center>break 5  Break at loine 4 of the current program</center>
<center>break hello.c:5 Break at line 5 of hello.c</center>


Natürlich können auch shortcuts verwendet werden wie:
- b main(b für break)
- r für run
- i b für info breakpoints (zeigt den jetzigen breakpoint)
- c oder clear um einen breakpoint zu clearen
- delete oder d um den breakpoint zu löschen
- enable / disable für einen breakpoint

Bsp.

```gdb
(gdb) **i b**
Num     Type           Disp Enb Address    What
1       breakpoint     keep y   0x08048395 in main at hello.c:5
(gdb) **disable 1**
(gdb) **i b**
Num     Type           Disp Enb Address    What
1       breakpoint     keep n   0x08048395 in main at hello.c:5
(gdb) **clear main**
Deleted breakpoint 1 
(gdb) **i b**
No breakpoints or watchpoints.

```


## Stepping

- `next`(n) für den nächsten schritt und nächsten schritt
- `continue` (c)für ein step over "größerer next"
- `step`(s) um in eine funktion von deiner funktion hineinzusteppen

## Printing
- `display` $variable
- `info display` um die gesetzte Variable zu sehen
- `print` um eine Varaible zu printen
	- Es geht auch printf() bspw printf "%d\n",i
- `list` listet den C code

## Stack Manipulation

- backtrace (bt) zeigt an in welcher funktion man sich gerade befinden und welche andere funktion die Funktion in der man sich befindet aufgerufen hat

```gdb
(gdb) **backtrace**
#0  subsubfunction () at hello.c:5
#1  0x080483a7 in subfunction () at hello.c:10
#2  0x080483cf in main () at hello.c:16
(gdb)
```

`help stack` für mehr info

## finish, stepi, advance

- `finish` um von der jetzigen funktion herauszukommen und zur caller funktion zu retourinieren

- `stepi` um eine einzige assembly instruction zu gehen

- `advance` ist ein `continue` an einem bestimmten punkt

- `jump ` äquivalent zu continue

## set varibales
```gdb
Breakpoint 1, main () at hello.c:15
15		int i = 10;
(gdb) **print i**
$1 = -1208234304
(gdb) **set (i = 20)**
(gdb) **print i**
$2 = 20
(gdb) **set variable i = 40**
(gdb) **print i**
$3 = 40
(gdb)
```


## Watch

wie in linux, beobachet / monitoring, einer variable die man festsetzt


```gdb
Breakpoint 1, main () at hello.c:5
5		int i = 1;
(gdb) **watch i**
Hardware watchpoint 2: i
(gdb) **continue**
Continuing.
Hardware watchpoint 2: i

Old value = -1208361280
New value = 2
main () at hello.c:7
7		while (i < 100) {
(gdb) **continue**
Continuing.
Hardware watchpoint 2: i

Old value = 2
New value = 3
main () at hello.c:7
7		while (i < 100) {
(gdb)
```


## attach a running process

mit `ps aux | less` 
(a für terminal)
(u für user)
(x für system)

dann kriegt man es BSD format, weil BSD Linux überlegener ist

mit der jeweiligen PID kann man den laufenden Prozess mit `attach` $(PID) attachen



## Window
im tui modus `gdb -tui foo`

- `focus`(fs) mit prev/next
- SRC source
- CMD
- REGS
- ASM


```gdb
(gdb) **info win**
        SRC     (36 lines)  <has focus>
        CMD     (18 lines)
(gdb) **fs next**
Focus set to CMD window.
(gdb) **info win**
        SRC     (36 lines)
        CMD     (18 lines)  <has focus>
(gdb) **fs SRC**
Focus set to SRC window.
(gdb)
```


## assembly

![[Pasted image 20260901132607.png]]




## TLDR

![[Pasted image 20260901132256.png]]



