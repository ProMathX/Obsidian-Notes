#C #Datenstrukturen #Betriebssysteme 


`mmap(2)`
für Anwendungsbereiche siehe: [[Semaphoren und Shared Memory]]

```C
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>
#include <sys/mman.h>
#include <sys/stat.h>

int main(void) {
    const char *path = "example.txt";

    int fd = open(path, O_RDONLY);
    if (fd == -1) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    struct stat sb;
    if (fstat(fd, &sb) == -1) {
        perror("fstat");
        close(fd);
        exit(EXIT_FAILURE);
    }

    size_t length = sb.st_size;

    char *mapped = mmap(NULL, length, PROT_READ, MAP_PRIVATE, fd, 0);
    if (mapped == MAP_FAILED) {
        perror("mmap");
        close(fd);
        exit(EXIT_FAILURE);
    }

    /* fd can be closed right after mmap succeeds; the mapping stays valid */
    close(fd);

    fwrite(mapped, 1, length, stdout);

    if (munmap(mapped, length) == -1) {
        perror("munmap");
        exit(EXIT_FAILURE);
    }

    return 0;
}
```