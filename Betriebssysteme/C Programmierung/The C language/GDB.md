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

- next für den nächsten schritt, iterativ 





