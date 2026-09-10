STYLE(9) Kernel Developer's Manual STYLE(9)

NAME

style — Kernel source file style guide (KNF), extended with examples

DESCRIPTION

This file specifies the preferred style for kernel source files in the OpenBSD source tree. It is also a guide for preferred userspace code style. These guidelines should be followed for all new code. In general, code can be considered "new code" when it makes up about 50% or more of the file(s) involved. This is enough to break precedents in the existing code and use the current style guidelines.

This version keeps every rule from the original text in the same order, and adds a worked example directly under each rule so the convention is not just stated but shown.

```
/*
 * Style guide for the OpenBSD KNF (Kernel Normal Form).
 */
```

```
/*
 * VERY important single-line comments look like this.
 */
```

```
/* Most single-line comments look like this. */
```

```
/*
 * Multi-line comments look like this.  Make them real sentences.
 * Fill them so they look like real paragraphs.
 */
```

Example, correct vs incorrect comment weight:

```c
/*
 * VERY important: this lock must be held before touching
 * the free list, or the kernel will panic under load.
 */
mtx_enter(&freelist_mtx);
```

```c
/* Skip the fast path if the cache is cold. */
if (cache_cold)
    goto slow;
```

```c
/* wrong: this is dressed up as a paragraph but says nothing */
/*
 * increment i
 */
i++;
```

Kernel include files (i.e., <sys/*.h>) come first; normally, you'll need <sys/types.h> OR <sys/param.h>, but not both! <sys/types.h> includes <sys/cdefs.h>, and it's okay to depend on that.

```c
#include <sys/types.h>	/* Non-local includes in brackets. */
```

If it's a network program, put the network include files next.

```c
#include <net/if.h>
#include <net/if_dl.h>
#include <net/route.h>
#include <netinet/in.h>
```

Then there's a blank line, followed by the /usr/include files. The /usr/include files, for the most part, should be sorted.

Example of a complete, correctly ordered include block for a small network utility:

```c
#include <sys/types.h>
#include <sys/socket.h>
```

```c
#include <net/if.h>
#include <netinet/in.h>
#include <arpa/inet.h>
```

```c
#include <err.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
```

```c
#include <paths.h>
```

```c
#include "pathnames.h"
```

Global pathnames are defined in /usr/include/paths.h. Pathnames local to the program go in pathnames.h in the local directory.

```c
#include <paths.h>
```

Example of a local pathnames.h:

```c
/* $OpenBSD$ */
```

```c
#define	_PATH_CONFIG	"/etc/myprog.conf"
#define	_PATH_LOCKFILE	"/var/run/myprog.lock"
```

Then there's a blank line, and the user include files.

```c
#include "pathnames.h"	/* Local includes in double quotes. */
```

All non-static functions are prototyped somewhere.

Function prototypes for private functions (i.e., functions not used elsewhere) go at the top of the first source module. In the kernel, private functions do not require a prototype as long as they are defined before they are used. In userspace, functions local to one source module should be declared 'static'. This should not be done in the kernel since it makes it impossible to use the kernel debugger.

Example of local prototypes at the top of a userspace module:

```c
static void	usage(void);
static int	parse_line(char *, struct entry *);
static char	*trim(char *);
```

```c
int
main(int argc, char *argv[])
{
	...
}
```

Functions used from other files are prototyped in the relevant include file.

Functions that are used locally in more than one module go into a separate header file, e.g., extern.h.

Example, extern.h shared by two source files in the same program:

```c
/* extern.h */
void	 log_init(const char *);
void	 log_warn(const char *, ...);
int	 db_open(const char *);
```

Prototypes should not have variable names associated with the types; i.e.,

```c
void	function(int);
```

not:

```c
void	function(int a);
```

Prototypes may have an extra space after a tab to enable function names to line up:

```c
static char	*function(int, const char *);
static void	 usage(void);
```

Example of a longer aligned block:

```c
static int	 open_db(const char *);
static void	 close_db(int);
static char	*read_record(int, size_t);
static void	 write_record(int, const char *, size_t);
```

There should be no space between the function name and the argument list.

```c
function(a1, a2);	/* correct */
function (a1, a2);	/* wrong */
```

Use __dead from <sys/cdefs.h> for functions that don't return, i.e.,

```c
__dead void	abort(void);
```

Example:

```c
__dead static void
usage(void)
{
	fprintf(stderr, "usage: %s [-v] file\n", getprogname());
	exit(1);
}
```

In header files, put function prototypes within __BEGIN_DECLS / __END_DECLS matching pairs. This makes the header file usable from C++.

Example:

```c
#ifndef _MYLIB_H_
#define _MYLIB_H_
```

```c
#include <sys/cdefs.h>
```

```c
__BEGIN_DECLS
int	 mylib_init(void);
void	 mylib_free(void);
__END_DECLS
```

```c
#endif /* !_MYLIB_H_ */
```

Macros are capitalized and parenthesized, and should avoid side-effects. If they are an inline expansion of a function, the function is defined all in lowercase; the macro has the same name all in uppercase. If the macro needs more than a single line, use braces. Right-justify the backslashes, as the resulting definition is easier to read. If the macro encapsulates a compound statement, enclose it in a "do" loop, so that it can safely be used in "if" statements. Any final statement-terminating semicolon should be supplied by the macro invocation rather than the macro, to make parsing easier for pretty-printers and editors.

```c
#define	MACRO(x, y) do {					\
	variable = (x) + (y);					\
	(y) += 2;						\
} while (0)
```

Example, a multi-line macro and its lowercase function counterpart:

```c
static inline int
max(int a, int b)
{
	return (a > b ? a : b);
}
```

```c
#define	SWAP(a, b) do {						\
	__typeof(a) __tmp = (a);				\
	(a) = (b);						\
	(b) = __tmp;						\
} while (0)
```

Example of why the "do { } while (0)" wrapper matters, showing the macro used safely inside an if statement without braces:

```c
if (needs_swap)
	SWAP(left, right);
else
	SWAP(right, left);
```

If a macro with arguments declares local variables, those variables should use identifiers beginning with two underscores. This is required for macros implementing C and POSIX interfaces and recommended for all macros for consistency.

Example, shown above as __tmp in SWAP().

Enumeration values are all uppercase.

```c
enum enumtype { ONE, TWO } et;
```

Example, a state machine enum used later in a switch:

```c
enum connstate { CONN_CLOSED, CONN_LISTEN, CONN_ESTABLISHED };
```

When defining unsigned integers, use "unsigned int" rather than just "unsigned"; the latter has been a source of confusion in the past.

```c
unsigned int	count;	/* correct */
unsigned	count;	/* wrong */
```

When declaring variables in structures, declare them sorted by use, then by size (largest to smallest), then by alphabetical order. The first category normally doesn't apply, but there are exceptions. Each one gets its own line. Put a tab after the first word, i.e., use 'int^Ix;' and 'struct^Ifoo *x;'.

Major structures should be declared at the top of the file in which they are used, or in separate header files if they are used in multiple source files. Use of the structures should be by separate declarations and should be "extern" if they are declared in a header file.

```c
struct foo {
	struct	foo *next;	/* List of active foo */
	struct	mumble amumble;	/* Comment for mumble */
	int	bar;
};
struct foo *foohead;		/* Head of global foo list */
```

Example, a larger structure following the same ordering rule (use, then size largest to smallest, then alphabetical):

```c
struct session {
	struct	session *next;		/* linkage, used first */
	struct	sockaddr_storage peer;	/* largest field */
	uint64_t	bytes_in;
	uint64_t	bytes_out;
	time_t	last_active;
	int	fd;
	int	state;
};
```

Use queue(3) macros rather than rolling your own lists, whenever possible. Thus, the previous example would be better written:

```c
#include <sys/queue.h>
struct	foo {
	LIST_ENTRY(foo)	link;	/* Queue macro glue for foo lists */
	struct	mumble amumble;	/* Comment for mumble */
	int	bar;
};
LIST_HEAD(, foo) foohead;	/* Head of global foo list */
```

Example, the same session structure rewritten with TAILQ instead of a hand-rolled next pointer, plus the insert/remove calls that go with it:

```c
#include <sys/queue.h>
```

```c
struct session {
	TAILQ_ENTRY(session)	entries;
	struct	sockaddr_storage peer;
	uint64_t	bytes_in;
	uint64_t	bytes_out;
	time_t	last_active;
	int	fd;
	int	state;
};
TAILQ_HEAD(, session) sessions = TAILQ_HEAD_INITIALIZER(sessions);
```

```c
TAILQ_INSERT_TAIL(&sessions, sp, entries);
TAILQ_REMOVE(&sessions, sp, entries);
```

Avoid using typedefs for structure types. This makes it impossible for applications to use pointers to such a structure opaquely, which is both possible and beneficial when using an ordinary struct tag. When convention requires a typedef, make its name match the struct tag. Avoid typedefs ending in "_t", except as specified in Standard C or by POSIX.

Example:

```c
struct opaque_handle;			/* correct: plain struct tag */
struct opaque_handle *open_handle(void);
```

```c
typedef struct opaque_handle opaque_handle_t;	/* discouraged */
```

```c
/*
 * All major routines should have a comment briefly describing what
 * they do.  The comment before the "main" routine should describe
 * what the program does.
 */
int
main(int argc, char *argv[])
{
	int aflag, bflag, ch, num;
	const char *errstr;
```

For consistency, getopt(3) should be used to parse options. Options should be sorted in the getopt(3) call and the switch statement, unless parts of the switch cascade. Elements in a switch statement that cascade should have a FALLTHROUGH comment. Numerical arguments should be checked for accuracy.

```c
while ((ch = getopt(argc, argv, "abn:")) != -1) {
	switch (ch) {		/* Indent the switch. */
	case 'a':		/* Don't indent the case. */
		aflag = 1;
		/* FALLTHROUGH */
	case 'b':
		bflag = 1;
		break;
	case 'n':
		num = strtonum(optarg, 0, INT_MAX, &errstr);
		if (errstr) {
			warnx("number is %s: %s", errstr, optarg);
			usage();
		}
		break;
	default:
		usage();
	}
}
argc -= optind;
argv += optind;
```

Example, a getopt loop with more option letters, still sorted "abcdv" in both the optstring and the switch:

```c
int aflag = 0, bflag = 0, cflag = 0, vflag = 0;
const char *dvalue = NULL;
```

```c
while ((ch = getopt(argc, argv, "abcd:v")) != -1) {
	switch (ch) {
	case 'a':
		aflag = 1;
		break;
	case 'b':
		bflag = 1;
		break;
	case 'c':
		cflag = 1;
		break;
	case 'd':
		dvalue = optarg;
		break;
	case 'v':
		vflag++;
		break;
	default:
		usage();
	}
}
```

Use a space after keywords (if, while, for, return, switch). No braces are used for control statements with zero or only a single statement unless that statement is more than a single line, in which case they are permitted.

```c
for (p = buf; *p != '\0'; ++p)
	continue;
for (;;)
	stmt;
for (;;) {
	z = a + really + long + statement + that + needs +
	    two + lines + gets + indented + four + spaces +
	    on + the + second + and + subsequent + lines;
}
for (;;) {
	if (cond)
		stmt;
}
```

Example, an if/while pair showing the "space after keyword" rule and brace omission for single statements:

```c
if (fd < 0)
	err(1, "open");
```

```c
while (n-- > 0)
	buf[n] = 0;
```

```c
if (fd < 0) {
	warn("open %s", path);
	return (-1);
}
```

Parts of a for loop may be left empty.

```c
for (; cnt < 15; cnt++) {
	stmt1;
	stmt2;
}
```

Example, all three clauses used for their intended purpose versus one left empty because the initialization already happened above it:

```c
for (i = 0; i < nitems; i++)
	total += items[i];
```

```c
i = 0;
for (; i < nitems && !found; i++)
	found = matches(items[i]);
```

Indentation is an 8 character tab. Second level indents are four spaces. All code should fit in 80 columns.

```c
while (cnt < 20)
	z = a + really + long + statement + that + needs +
	    two + lines + gets + indented + four + spaces +
	    on + the + second + and + subsequent + lines;
```

Example, a wrapped function call using the same four-space continuation rule:

```c
error = copyin(uaddr, kaddr, len);
if (error != 0)
	printf("copyin failed: uaddr=%p kaddr=%p "
	    "len=%zu error=%d\n", uaddr, kaddr, len, error);
```

Do not add whitespace at the end of a line, and only use tabs followed by spaces to form the indentation. Do not use more spaces than a tab will produce and do not use spaces in front of tabs.

Closing and opening braces go on the same line as the else. Braces that aren't necessary may be left out, unless they cause a compiler warning.

```c
if (test)
	stmt;
else if (bar) {
	stmt;
	stmt;
} else
	stmt;
```

Example, a longer if/else if/else chain following the same brace placement:

```c
if (state == CONN_CLOSED) {
	open_conn();
} else if (state == CONN_LISTEN) {
	accept_conn();
} else if (state == CONN_ESTABLISHED) {
	service_conn();
} else
	warnx("unknown state %d", state);
```

Do not use spaces after function names. Commas have a space after them. Do not use spaces after '(' or '[' or preceding ']' or ')' characters.

```c
if ((error = function(a1, a2)))
	exit(error);
```

Example, a similar call with an array index, again with no space after '[' or before ']':

```c
if ((error = process(argv[i], flags)))
	err(error, "process");
```

Unary operators don't require spaces; binary operators do. Don't use parentheses unless they're required for precedence, the statement is confusing without them, or the compiler generates a warning without them. Remember that other people may be confused more easily than you. Do YOU understand the following?

```c
a = b->c[0] + ~d == (e || f) || g && h ? i : j >> 1;
k = !(l & FLAGS);
```

Example, an expression that needs no extra parentheses because normal precedence already reads correctly, versus one that needs them because the reader cannot be expected to remember bitwise-vs-logical precedence:

```c
total = a + b * c;		/* fine, standard precedence */
ready = (flags & READY) != 0;	/* parens needed for clarity */
```

Exits should be 0 on success, or non-zero for errors.

```c
/*
 * Avoid obvious comments such as
 * "Exit 0 on success."
 */
exit(0);
```

Example, an error path with a non-zero exit code and a matching comment that explains why, not what:

```c
if (nfiles == 0) {
	/* Nothing to process; treat as a caller error. */
	exit(1);
}
```

The function type should be on a line by itself preceding the function.

```c
static char *
function(int a1, int a2, float fl, int a4)
{
```

Example:

```c
static int
parse_line(char *line, struct entry *ep)
{
	...
}
```

When declaring variables in functions, declare them sorted by size (largest to smallest), then in alphabetical order; multiple ones per line are okay. If a line overflows, reuse the type keyword.

Be careful not to obfuscate the code by initializing variables in the declarations. Use this feature only thoughtfully. DO NOT use function calls in initializers!

```c
struct foo one, *two;
double three;
int *four, five;
char *six, seven, eight, nine, ten, eleven, twelve;
```

```c
four = myfunction();
```

Example, a function-local declaration block sorted by size then alphabetically, with the disallowed initializer shown for contrast:

```c
struct timeval tv;
double average;
long total, *countp;
int fd, i, n;
char *path, buf[BUFSIZ];
```

```c
fd = open(path, O_RDONLY);	/* correct: assignment after declaration */
```

```c
int fd = open(path, O_RDONLY);	/* wrong: function call in initializer */
```

Do not declare functions inside other functions.

Example of the wrong way:

```c
int
outer(void)
{
	int				/* wrong */
	inner(void)
	{
		return (1);
	}
	return inner();
}
```

Casts and sizeof() calls are not followed by a space. Note that indent(1) does not understand this rule.

```c
p = (struct foo *)buf;
n = sizeof(struct foo);
```

Use of the "register" specifier is discouraged in new code. Optimizing compilers such as gcc can generally do a better job of choosing which variables to place in registers to improve code performance. The exception to this is in functions containing assembly code where the "register" specifier is required for proper code generation in the absence of compiler optimization.

Example, the exception case, a variable pinned to a register for use inside inline assembly:

```c
register int result asm("eax");
```

```c
__asm volatile("syscall" : "=a" (result) : "0" (nr) : "cc");
```

When using longjmp() or vfork() in a program, the -W or -Wall flag should be used to verify that the compiler does not generate warnings such as

```c
warning: variable `foo' might be clobbered by `longjmp' or `vfork'.
```

If any warnings of this type occur, you must apply the "volatile" type-qualifier to the variable in question. Failure to do so may result in improper code generation when optimization is enabled. Note that for pointers, the location of "volatile" specifies if the type-qualifier applies to the pointer, or the thing being pointed to. A volatile pointer is declared with "volatile" to the right of the "*". Example:

```c
char *volatile foo;
```

says that "foo" is volatile, but "*foo" is not. To make "*foo" volatile use the syntax

```c
volatile char *foo;
```

If both the pointer and the thing pointed to are volatile, use

```c
volatile char *volatile foo;
```

"const" is also a type-qualifier and the same rules apply. The description of a read-only hardware register might look something like:

```c
const volatile char *reg;
```

Example tying the three variants together, as they would appear declared side by side:

```c
char *volatile p1;			/* p1 itself is volatile */
volatile char *p2;			/* *p2 is volatile */
volatile char *volatile p3;	/* both are volatile */
const volatile char *devreg;	/* read-only hardware register */
```

Global flags set inside signal handlers should be of type "volatile sig_atomic_t" if possible. This guarantees that the variable may be accessed as an atomic entity, even when a signal has been delivered. Global variables of other types (such as structures) are not guaranteed to have consistent values when accessed via a signal handler.

Example:

```c
volatile sig_atomic_t got_sigint;
```

```c
static void
sigint_handler(int signo)
{
	got_sigint = 1;
}
```

```c
...
while (!got_sigint)
	do_work();
```

NULL is the preferred null pointer constant. Use NULL instead of (type *)0 or (type *)NULL in all cases except for arguments to variadic functions where the compiler does not know the type.

Example, the variadic exception:

```c
p = NULL;			/* correct */
p = (struct foo *)0;	/* wrong */
```

```c
execl("/bin/sh", "sh", "-c", cmd, (char *)NULL);	/* cast needed here */
```

Don't use '!' for tests unless it's a boolean, i.e., use

```c
if (*p == '\0')
```

not

```c
if (!*p)
```

Example, contrasting a genuine boolean test with a pointer/character test:

```c
if (!done)		/* fine: done is a boolean flag */
	continue;
```

```c
if (*cp == '\0')	/* correct */
	break;
if (!*cp)		/* wrong */
	break;
```

Routines returning void * should not have their return values cast to any pointer type.

Example:

```c
char *cp;
```

```c
cp = malloc(len);	/* correct: no cast on the void * return */
cp = (char *)malloc(len);	/* wrong */
```

Use the err(3) and warn(3) family of functions. Don't roll your own!

```c
if ((four = malloc(sizeof(struct foo))) == NULL)
	err(1, NULL);
if ((six = (int *)overflow()) == NULL)
	errx(1, "Number overflowed.");
return eight;
```

Example, warn() used for a non-fatal condition versus err() for a fatal one, matching the errno-reporting and no-errno-reporting split between the two families:

```c
if (unlink(path) == -1)
	warn("unlink %s", path);	/* non-fatal, reports errno */
```

```c
if ((fd = open(path, O_RDONLY)) == -1)
	err(1, "open %s", path);	/* fatal, reports errno, exits */
```

Always use ANSI function definitions. Long parameter lists are wrapped with a normal four space indent.

Example, a long parameter list wrapped with a four-space continuation indent:

```c
int
session_open(const char *host, unsigned short port, int timeout,
    int flags, const struct options *opts)
{
	...
}
```

Variable numbers of arguments should look like this:

```c
#include <stdarg.h>
```

```c
void
vaf(const char *fmt, ...)
{
	va_list ap;
	va_start(ap, fmt);
```

```c
	STUFF;
```

```c
	va_end(ap);
```

```c
	/* No return needed for void functions. */
}
```

Example, a small logging wrapper built on the same pattern:

```c
#include <stdarg.h>
#include <stdio.h>
```

```c
void
log_warnf(const char *fmt, ...)
{
	va_list ap;
```

```c
	va_start(ap, fmt);
	vfprintf(stderr, fmt, ap);
	va_end(ap);
}
```

```c
static void
usage(void)
{
```

Usage statements should take the same form as the synopsis in manual pages. Options without operands come first, in alphabetical order inside a single set of braces, followed by options with operands, in alphabetical order, each in braces, followed by required arguments in the order they are specified, followed by optional arguments in the order they are specified.

A bar ('|') separates either-or options/arguments, and multiple options/arguments which are specified together are placed in a single set of braces.

If numbers are used as options, they should be placed first, as shown in the example below. Uppercase letters take precedence over lowercase.

```c
"usage: f [-12aDde] [-b b_arg] [-m m_arg] req1 req2 [opt1 [opt2]]\n"
"usage: f [-a | -b] [-c [-de] [-n number]]\n"
```

Example, a usage() for a hypothetical tool with two no-operand flags, one flag taking an operand, a required argument, and an optional argument:

```c
static void
usage(void)
{
	fprintf(stderr,
	    "usage: %s [-qv] [-o outfile] infile [count]\n",
	    getprogname());
	exit(1);
}
```

The getprogname(3) function may be used instead of hard-coding the program name.

```c
fprintf(stderr, "usage: %s [-ab]\n", getprogname());
exit(1);
```

New core kernel code should be reasonably compliant with the style guides. The guidelines for third-party maintained modules and device drivers are more relaxed but at a minimum should be internally consistent with their style.

Whenever possible, code should be run through a code checker (e.g., "gcc -Wall -W -Wpointer-arith -Wbad-function-cast ..." or splint from the ports tree) and produce minimal warnings. Since lint has been removed, the only lint-style comment that should be used is FALLTHROUGH, as it's useful to humans. Other lint-style comments such as ARGSUSED, LINTED, and NOTREACHED may be deleted.

Example build invocation matching the checker flags mentioned above:

```c
cc -Wall -W -Wpointer-arith -Wbad-function-cast -o prog prog.c
```

Note that documentation follows its own style guide, as documented in mdoc(7).

FILES

```c
/usr/share/misc/license.template
    Example license for new code.
```

SEE ALSO

```c
indent(1), err(3), queue(3), warn(3), mdoc(7)
```

HISTORY

This man page is largely based on the src/admin/style/style file from the 4.4BSD-Lite2 release, with updates to reflect the current practice and desire of the OpenBSD project. This extended version keeps the original text intact and adds a worked example under each rule.

OpenBSD-current September 11, 2022 STYLE(9)