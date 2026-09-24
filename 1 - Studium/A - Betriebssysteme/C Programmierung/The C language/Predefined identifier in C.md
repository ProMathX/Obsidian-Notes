```C
// C program to demonstrate working of a
// Predefined Identifier __func__

#include <stdio.h>

int main()
{
    // %s indicates that the program will read strings
    printf("%s", __func__);
    return 0;
}
```

Output: `main`




```C
       #include <err.h>
       #include <errno.h>
       #include <semaphore.h>
       #include <signal.h>
       #include <stdio.h>
       #include <stdlib.h>
       #include <time.h>
       #include <unistd.h>

       #include <assert.h>

       sem_t sem;

       static void
       handler(int sig)
       {
           write(STDOUT_FILENO, "sem_post() from handler\n", 24);
           if (sem_post(&sem) == -1) {
               write(STDERR_FILENO, "sem_post() failed\n", 18);
               _exit(EXIT_FAILURE);
           }
       }

       int
       main(int argc, char *argv[])
       {
           struct sigaction sa;
           struct timespec ts;
           int s;

           if (argc != 3) {
               fprintf(stderr, "Usage: %s <alarm-secs> <wait-secs>\n",
                       argv[0]);
               exit(EXIT_FAILURE);
           }

           if (sem_init(&sem, 0, 0) == -1)
               err(EXIT_FAILURE, "sem_init");

           /* Establish SIGALRM handler; set alarm timer using argv[1].  */

           sa.sa_handler = handler;
           sigemptyset(&sa.sa_mask);
           sa.sa_flags = 0;
           if (sigaction(SIGALRM, &sa, NULL) == -1)
               err(EXIT_FAILURE, "sigaction");

           alarm(atoi(argv[1]));

           /* Calculate relative interval as current time plus
              number of seconds given argv[2].  */

           if (clock_gettime(CLOCK_REALTIME, &ts) == -1)
               err(EXIT_FAILURE, "clock_gettime");

           ts.tv_sec += atoi(argv[2]);

           printf("%s() about to call sem_timedwait()\n", __func__);
           while ((s = sem_timedwait(&sem, &ts)) == -1 && errno == EINTR)
               continue;       /* Restart if interrupted by handler.  */

           /* Check what happened.  */

           if (s == -1) {
               if (errno == ETIMEDOUT)
                   printf("sem_timedwait() timed out\n");
               else
                   perror("sem_timedwait");
           } else
               printf("sem_timedwait() succeeded\n");

           exit((s == 0) ? EXIT_SUCCESS : EXIT_FAILURE);
       }

```


Output
```
           $ ./a.out 2 3
           About to call sem_timedwait()
           sem_post() from handler
           sem_timedwait() succeeded
           $ ./a.out 2 1
           About to call sem_timedwait()
           sem_timedwait() timed out
```


