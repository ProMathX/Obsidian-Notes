#C #Prozesse #Threads 

Fork Exec Pipe, also Process exec Pipes

Recap on process vs thread

[Osdev wiki](https://wiki.osdev.org/Processes_and_Threads)
![[Pasted image 20261103211633.png]]

![[Pasted image 20261103211638.png]]




## Part 1

### Creating a process

- a process is how the os represtens a running program 
- Every process has a PID
- Except PID 1, every process has a parent process
- We can also let a process create related child processes

![[Pasted image 20261103203320.png]]


With fork

```C
#include <uninstd.h>
pid_t fork(void);
```

Return s 
- -1 on error
- 0 in the child process
- >0 in the parent process

```C
pid_t pid = fork();

swtich(pid)
{
	case -1:
		fprintf(stderr,"fork failed: %s", strerror(errno));
		exit(EXIT_FAILURE);
	
	case 0: /*child instructions*/ break;
	
	case default: /*parent instructions*/ break;

}
```


Child inherits from parent: 
- Opened files (common access!)
- File buffers
- Signal handling
- Current values of variables

However, signal handleing can be re-configured independently. Variables are independent (seperate memory space). IPC needed for sharing data


#### Pitfalls
![[Pasted image 20261103204017.png]]



fflush stdout!

#### Terminating a process

```C
void exit(int status);
```

- status: Number in the 0-255 range. Conventionally:
	- exit(EXIT_SUCCESS)
	- exit(EXIT_FAILURE)
- Actions performed by exit()
	- Flush and close stdio stream buffers
	- close all open files 
	- delete temporary files 
	- call exit handlers

![[Pasted image 20261103204356.png]]

- wait() blocks until a child (any child) terminatres or an error occurs
- waitpid() blocks until the specified child terminates (-1 = any child)
- Returns PID of the terminated child or -1
- status will contain additional informatiion 
	- WIFEXITED(status)
	- WEXITSTATUS(status)
	- WIFSIGNALED(status), WTERMSIG(sig)
- options customise behaviour of waitpid()


```C
#include <sys/wait.h>

int status; 
pdi_t child_pid, pid; 

pid = wait(&status);
if(WEXITSTATUS(status) == EXIT_SUCCESS){/*Child pid succeeded*/}
pid = waitpid(-1, &status,0);

child_pid = fork();
if(child_pid) waitpid(child_pid,&status,0);

```

#### Zombies 
![[Pasted image 20261103205128.png]]

![[Pasted image 20261103205138.png]]


### The exec Family

- Family of calls (from unistd.h) to launch an executable 
- They load the new preogram ini to the same process (PID remains the same, but memory is replaced)
- if successful in launching the program, they dont return to the caller
- Trick>>> combine with fork()

![[Pasted image 20261103205714.png]]
![[Pasted image 20261103205728.png]]

##### Examples


```C
#include <unistd.h>

char *cmd[] = {"ls","-l", (char *)0};
execv("/bin/ls",cmd);

execl("/bin/ls","ls","-l",NULL); 

int fd = open("/binls",O_RDONLY);
fexecve(fd,cmd,NULL);
```

>![Note on Arguments]
>Provide the full argument list, including argv[0] (program name)
>
>Last argument must be a NULL pointer!




### Pipes

#### UNIX Pipes
![[Pasted image 20261103210141.png]]

#### Creating a pipe

```C
#include <unistd.h>
int pipe(int pipefd[2]);
```

- Places two file descriptors into pipefd
	- pipefd[0] read end
	- pipefd[1]  write end
- Returns 0 on success -1 on error


![[Pasted image 20261103210301.png]]





#### Implicit Synchronisation with Pipes

- read() blocks when pipe is empty
- write() blocks when pipe is full

- read indicates EOF if all write ends are closed (rv 0)
- write creates signal SIGPIPE if all read ends are closed
- Writing on closed pipe -> error EPIPE

>[!внима́ние]
>Lets other process know what is happenning 
>OS cleans ups pipes when all their ends are closed

#### Named pipes
- unnamed pipes pipe or |
- named pipes `mkfifo(1), mknod(2)`
- similar to files
- However, reading from empty pipe blocks


#### Redirection of stdin/stdout
![[Pasted image 20261103210837.png]]




#### Duplicating a FD
![[Pasted image 20261103210856.png]]

#### Example
![[Pasted image 20261103211007.png]]


#### Pitfalls

- Need two pipes for two-way communication
	- Process A writes on pipe P1 and reads from P2
	- Process B writes on pipe P2 and reads from pipe P1

- What if they both try to read, and both pipes are empty?
	- Deadlock

- Design carefully
- poll(2) fcntl(2) to do non-blockin checks

Buffer I/O may surprising effects
- Flush buffers especially before fork()
- Buffers may be configured setbuf(3) and setvbuf(3)



---

#### Tips for the Exercise

- Try to parallelize as much as possible
- Do not explot copy of memory areas
	- Exceptions: piopes argc,argv


>[!Не]
>Parent reads entire file into an array then forks
>
>child processes data from (copy of) array
>


>[!вместо этого сделайте]
>Parent creates pipe and forks, then reads file line by line (fgets)
>
>Lines are sent to child over a pipe 
>
>Child processes each line as it arrives
>
>Reading and processing are parallelized








