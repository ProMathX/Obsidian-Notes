---
topic: Introduction to Unix and Linux
date: 2026-03-16
course: OSUE
tags:
  - studies
  - Betriebssysteme
---
## VO
Keine neuen Erkenntnisse.

![[Pasted image 20261006175643.png]]



Wichtig sind die Datenstrutkturen in Linux und der Process Communcation im UNIX Kernel oder auch im Linux Kernel
![[Pasted image 20261006175727.png]]

#### Shell redirections
```bash 
cmd < file Read input from 'file' instead of keyboard (stdin)
cmd > file Send output to 'file' instead of the display (stdout)
cmd 2> file Send errors to file instead of the display
cmd &> file Send both stdout and stderr to file
```


- Variants `>>, 2>>m &>>` >> for new line in the output file if not given, prior input will be overwritten
- Composable: 'cmd < in_file > >out_file 2> err_file'

#### Process Management
![[Pasted image 20261006183216.png]]

#### Wildcards
Regex in Shell
![[Pasted image 20261006183410.png]]
#### Links
- [[Learn Lean]]
