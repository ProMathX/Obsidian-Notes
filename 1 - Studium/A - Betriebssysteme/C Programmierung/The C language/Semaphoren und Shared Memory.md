#C #Betriebssysteme #studies  #Datenstrukturen   


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


---
# Skeleton-Code

```C
/* ---------- common.h ---------- */

#define SHM_PATH "/myshm"(Matrikelnummer)
#define BUF_LEN 64

struct data {
    /* your payload type */
} data;

struct semaphore{
    data_t buf[BUF_LEN];
    size_t writeIndex;
    size_t readIndex;
    size_t numProducers;
    bool terminate;
    sem_t mutex;      /* protects writeIndex / numProducers */
    sem_t numFree;    /* slots available to write */
    sem_t numUsed;    /* slots available to read */
} semaphore;

void error(const char *msg);

/* ---------- server.c (creator / consumer) ---------- */

#include "common.h"

static volatile sig_atomic_t quit = false;
static void onSignal(int sig) { quit = true; }

static void initSignalHandler(void) {
    struct sigaction sa = {0};
    sa.sa_handler = onSignal;
    sigemptyset(&sa.sa_mask);
    sigaction(SIGINT, &sa, NULL);
    sigaction(SIGTERM, &sa, NULL);
}

static shm_t *shmCreate(int *fd_out) {
    int fd = shm_open(SHM_PATH, O_CREAT | O_EXCL | O_RDWR, 0600);
    if (fd == -1) error("shm_open");
    if (ftruncate(fd, sizeof(shm_t)) == -1) error("ftruncate");

    shm_t *shmp = mmap(NULL, sizeof(*shmp), PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
    if (shmp == MAP_FAILED) error("mmap");

    shmp->writeIndex = 0;
    shmp->readIndex = 0;
    shmp->numProducers = 0;
    shmp->terminate = false;

    sem_init(&shmp->mutex, 1, 1);
    sem_init(&shmp->numFree, 1, BUF_LEN);
    sem_init(&shmp->numUsed, 1, 0);

    *fd_out = fd;
    return shmp;
}

static void shmDestroy(shm_t *shmp, int fd) {
    sem_destroy(&shmp->mutex);
    sem_destroy(&shmp->numFree);
    sem_destroy(&shmp->numUsed);
    munmap(shmp, sizeof(*shmp));
    close(fd);
    shm_unlink(SHM_PATH);
}

int main(void) {
    initSignalHandler();

    int fd;
    shm_t *shmp = shmCreate(&fd);

    while (!quit) {
        if (sem_wait(&shmp->numUsed) == -1) {
            if (errno == EINTR) continue;
            error("sem_wait");
        }

        data_t entry = shmp->buf[shmp->readIndex];
        shmp->readIndex = (shmp->readIndex + 1) % BUF_LEN;

        sem_post(&shmp->numFree);

        /* process entry */
    }

    shmp->terminate = true;
    for (size_t i = 0; i < shmp->numProducers; i++) {
        sem_post(&shmp->numFree);
    }

    shmDestroy(shmp, fd);
    return EXIT_SUCCESS;
}

/* ---------- client.c (attacher / producer) ---------- */

#include "common.h"

static shm_t *shmAttach(int *fd_out) {
    int fd = shm_open(SHM_PATH, O_RDWR, 0);
    if (fd == -1) error("shm_open");

    shm_t *shmp = mmap(NULL, sizeof(*shmp), PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
    if (shmp == MAP_FAILED) error("mmap");

    *fd_out = fd;
    return shmp;
}

int main(void) {
    int fd;
    shm_t *shmp = shmAttach(&fd);

    sem_wait(&shmp->mutex);
    shmp->numProducers++;
    sem_post(&shmp->mutex);

    while (!shmp->terminate) {
        if (sem_wait(&shmp->numFree) == -1) {
            if (errno == EINTR) continue;
            error("sem_wait");
        }
        if (shmp->terminate) break;

        data_t entry; /* produce entry */

        sem_wait(&shmp->mutex);
        shmp->buf[shmp->writeIndex] = entry;
        shmp->writeIndex = (shmp->writeIndex + 1) % BUF_LEN;
        sem_post(&shmp->mutex);

        sem_post(&shmp->numUsed);
    }

    munmap(shmp, sizeof(*shmp));
    close(fd);
    return EXIT_SUCCESS;
}
```