#C
#studies 
#Betriebssysteme


Um alle möglichen EInträge zu sehen

`man -f PAGE_NAME`

ZB. 
`man -f open`
liefert 

```bash
$~ man -f open
open (2)             - open and possibly create a file
open (3p)            - open file
open (3perl)         - perl pragma to set default PerlIO layers for input and output
open (n)             - Open a file-based or command pipeline channel
```

Um es zu öffnen:
´man 2 open´

#### Suchen 
`man -k keyword`
`apropos keyword`

Here is a short list of the man pages I found most helpful in this course (check out the `manExamples.py` script in this directory to find more of them for yourself!):

_getopt_

- `man 3 getopt`
- `man 3 string`

_shared memory_

- `man 3 shm_open`
- `man 7 sem_overview`
- `man 7 shm_overview`

_fork, pipe, execle_

- `man 2 pipe` - also has fork
- `man 2 dup2`
- `man 2 wait`
- `man 3 system`

_socket_

- `man 2 select_tut` - also has sigaction
- `man 7 unix` - has overview
- `man 3 getaddrinfo` - fallback, if no ipv4 given
[src](https://github.com/sueszli/osue/tree/master)


paar wichtige manpages:

    man shm_overview -> ablauf was du wann machen musst für shm
    man sem_overview -> was du wann machen musst für semaphore
    man shm_open (ganz unten die examples sind basically ganzer ablauf den wir wissen müssenvorgegeben)
(Aus dem TU INF discord)




