---
topic: C Programming
date: 2026-03-16
course: OSUE
tags:
  - studies
  - C
  - Betriebssysteme
---
# VO

### Introduction to make

#### Structure of a Makefile Rule

```Makefile
result: ingredients
	recipe
```

- **result** (target): flie that will be geenerated/updated by this rule
- **ingredients**(dependencies): files needed to create the target
- **recipe:** actual commands to create the target from the ingredients

Comments with # 
only us the tab key for intendation

Example:
![[Pasted image 20261016195240.png]]


How make works? 

We create with .o the object files, the reason for that is, that we don't have to recompile everything, so we can Link everything together


#### Variables

Variables are used like in a shell script with CC = gcc and using it with $(CC) 

Common and important flags:
- CC compiler
- CFLAGS compilerflags
- LDFLAGS linker flags


#### Patterns and Automatic variables

Pattern rules specify recipes for a whole class of targets
For instance: `%.o` for all object files

- We need speial variables to retrieve target and dependency names inthe recipe 
	- `$@` target 
	- `$<` first dependency
	- `$^` all dependencies


Example:
![[Pasted image 20261016195723.png]]

#### Phony targets
declared with `.PHONY`

![[Pasted image 20261016200214.png]]



A complete example would be:

![[Pasted image 20261016200231.png]]



### Argument Parsing

Before any inconveniences happen, argc also counts the program name 
![[Pasted image 20261016200331.png]]

A propriate example would be: 
![[Pasted image 20261016200356.png]]


An argument handling can be found here [[Parse Command Line Arguments]]

a getopt example:
![[Pasted image 20261016200433.png]]


When printing a usage message, use the syntax of the man pages 


Mandatory argument: `hello -o` 
Optional arguments [ ] `hello -a optarg [-o] arg1`
Alternative options: [x|y] `hello [-a optarg | -o] arg1`
Alternative requiered arguments {x|y} `hello {-a optarg | -o} arg1`
Conditionally valid options: `hello [-a optarg [-o]] arg1`
One or mor eoccureance of a positonal argument  `hello -a optarg file...`


A propriate Example 
![[Pasted image 20261016200752.png]]

Appropriate a way more detailed error handeling guide here: [[Error Handling]]


### Signals

A signal gives the UNIX system if an error occured, the most infamous one is the SIGSEGV for segfaults (segmentationfaults)
Other ones are:
- Ignore (SIGCHLD)
- Termiante Process (SIGTERM)
- Produce core dump (SIGSEGV)

For most signals you can define a custom handling

>[!CAUTION]
>SIGSTOP and SIGKILL cannot be handeld or ignored

Signals may interrupt certain system/library calls
- errno == EINTR
- In this case, retry
#### Configuring Signal Actions 

A detailed  man page on sigaction(2)


```C
int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact);

```

- signum: number of the signal to handle 
- act: pointer to new conifureate (NULL for unchanged)
- oldact: pointer to store old configuration (NULL to ignore)
0 success -1 on error

```C
#include <signal.h>

struct sigaction
{
	void (*sa_handler)(int);
	sigset_t sa_mask;
	int sa_flags;
	...
};

```

- sa_handler Address of signal handler or SIG_DFL (default signal handler) or SIG_IGN (ignore)
- sa_mask Signals that should be blocked wihile the hander for this signal is executed 
- sa_flas Additional options (see manual)


An example would be 
![[Pasted image 20261016201423.png]]


the internal function of signaling is trivial

![[Pasted image 20261016201642.png]]

#### Writing a `void handle_signal(int signal)`
- KISS
- Consistent
- YOU CANNOT BLOCK SIGKILL AND SIGSTOP

Use async-signal-sage functions only

![[Pasted image 20261016201804.png]]

Example 1

```C
void handle_signal(int signal)
{
	_exit(1); // Immediate termination
}
```

Example 2

```C 
volatile sig_atomic_t quit = 0;

void handle_signal(int signal)
{
	quit = 1;
}

int main(int argc, char **argv)
{
	...// setup the signal handler
	while(!quit)
	{
		.... //additional cleanup
	}
	return 0;
}
```


A proper example of mine

```C

volatile sig_atomic_t quit = false;
void
onSignal(int sig, siginfo_t *si, void *unused)
{
	quit = true;
}

void
initSignalHandler(void)
{
	struct sigaction sa;
	sa.sa_flags = SA_SIGINFO;
	sigemptyset(&sa.sa_mask);
	sa.sa_sigaction = onSignal;
	... 
}

```

from feedbackarcset [src](https://github.com/KernInformatik/FeedbackArcSet/blob/main/lib/sem_lib.c)

---

read 
man 1 getopt 
man 3 getopt
man 3 strerror
man 2 sigaction
man 7 signal
man 7 signal-safety 


#### Links
- [[Learn Lean]]
-  [man page for signals](https://linux.die.net/man/2/sigaction)
