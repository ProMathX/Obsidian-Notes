#C #Prozesse #Threads 

Fork Exec Pipe, also Process exec Pipes



## Part 1

### Creating a process

[Osdev wiki](https://wiki.osdev.org/Processes_and_Threads)

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
