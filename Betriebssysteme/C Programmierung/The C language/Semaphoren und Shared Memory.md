#C #Betriebssysteme #studies 


Also konzeptuell etwas schwer zu verstehen, weil ohne Verstaendnis ist es schwer zu fassen, deshalb werde ich es versuchen in eigenen Worten zusammenzufassen.




## Exchange data via same memory

![[Pasted image 20260902160654.png]]


Ist eine Unix Drive directory, man kann zum Beispiel read oder access rights garantieren etc
(Festplatten und anderen Speichermedien sind in /dev/ anzutreffen)


## Example
![[Pasted image 20260902161019.png]]



EIn neues Objekt mit `shm_open()` 

```C
#include <sys/mman.h>
#include <fcntl.h>
int shm_open(const char *name, int oflag, mode_t mode);
```

man 3 shm_open fuer mehr details


- name Name like “/somename”
- oflag Bit mask: O_RDONLY or O_RDWR and eventually. . .
	- O_CREAT: creates an object unless it exists
	- additionally O_EXCL: error if already created
- mode Access rights at creation time, otherwise 0
- Return value: file descriptor on success,
	-1 on error (→ errno

Objekt kann unter /dev/shm/somemone gfundem werden

Groesse festlegen 
```C
#include <sys/mman.h>
#include <fcntl.h>
int ftruncate(int fd, off_t length);
```
0 bei success 
>Then the file descriptor can be used to create a common
mapping (mmap(2)) and finally it can be closed (close(2))


Shared Memory  (shm_unlik(3))

```C
int shm_unlink(const char *name);
```


close the file descriptor mit close() und unmap the memory with munmap()




---

## Memory mapping

mmap(2)
```C
#include <sys/mman.h>
void *mmap(void *addr, size_t length, int prot,
int flags, int fd, off_t offset);
```

![[Pasted image 20260902162116.png]]

FD kann geschlossen werden nachdem man das mapping kreiert hat
in Linux sind die mappings in /proc/PID/maps
keine virtuelle memory page auf kosten des Speichers(persistent)


remove memory page 

```C
int munmap(void *addr, size_t length);
```




### Anmerkung

Es wird laut LVA empfohlen, wenn man eine Memorypage anlehgt,dann mit eigener matrikelnummer etc 

Grundstruktur
```C
#include <fcntl.h>
#include <stdio.h>
#include <sys/mman.h>
#include <sys/types.h>
#include <unistd.h>

#define SHM_NAME "/myshm"
#define MAX_DATA (50)
struct myshm {
	unsigned int state;
	unsigned int data[MAX_DATA];
};
```

## Beispiele

```C
// create and/or open the shared memory object:
int shmfd = shm_open(SHM_NAME, O_RDWR | O_CREAT, 0600);

if (shmfd == -1)
	... // error
	
// set the size of the shared memory:
if (ftruncate(shmfd, sizeof(struct myshm)) < 0)
	... // error
	
// map shared memory object:
struct myshm *myshm;
myshm = mmap(NULL, sizeof(*myshm), PROT_READ | PROT_WRITE,
MAP_SHARED, shmfd, 0);

if (myshm == MAP_FAILED)
	... // error
if (close(shmfd)) == -1)
	... // error

// unmap shared memory:
if (munmap(myshm, sizeof(*myshm)) == -1)
	... // error
	
// remove shared memory object:
if (shm_unlink(SHM_NAME) == -1)
	... // error
```


