## `malloc` vs. String-Terminator
Achtung: KI

`malloc(n)` reserviert `n` Bytes und initialisiert **nichts** (kein Zero-Fill, im Gegensatz zu `calloc`).

- Ein C-String braucht **immer** ein `'\0'` am Ende.
- Wenn du `k` Zeichen speichern willst → `malloc(k + 1)`, letztes Byte selbst auf `'\0'` setzen.
- `strlen()` liest so lange, bis es _irgendwo_ im Speicher ein Nullbyte findet — ohne Terminator ist das **undefined behavior** (Absturz, Müll, oder "funktioniert zufällig").

```c
// FALSCH – kein Platz/Wert für '\0'
char *s = malloc(len);

// RICHTIG
char *s = malloc(len + 1);
s[len] = '\0';

// Alternative: calloc zerot automatisch
char *s = calloc(len + 1, sizeof(char));
```

**Faustregel:** Jede Funktion, die einen `char*`-Buffer zurückgibt und danach mit `strlen`/`fputs`/`printf("%s", ...)` benutzt wird, MUSS terminiert sein.

---

## `malloc`/`free` vs. `fopen`/`fclose` – zwei getrennte Welten

|Kommt von|Freigeben mit|
|---|---|
|`malloc`, `calloc`, `realloc`|`free()`|
|`fopen()`, oder `stdin`/`stdout`/`stderr`|`fclose()`|

- **Niemals** `free()` auf einen `FILE*` aufrufen → UB, glibc meldet meist `free(): invalid pointer`.
- **Niemals** `stdin`/`stdout`/`stderr` schließen oder freigeben, außer du willst das bewusst.
- Jeder `fopen()` braucht genau **ein** `fclose()`. Zweimal schließen = **double close**, auch UB.

---

## Uninitialisierte Variablen

```c
FILE *f;
if (f == NULL) // UB: f hat noch gar keinen definierten Wert
```

- Lokale Variablen ohne `= ...` haben einen **unbestimmten** Wert, nicht automatisch `NULL`.
- Immer explizit initialisieren (`FILE *f = NULL;`) oder erst prüfen, nachdem der Wert wirklich gesetzt wurde.
- Compiler-Flag `-Wall -Wextra` warnt meistens davor — immer mitkompilieren.

---

## Debug-Werkzeug: Sanitizer

```bash
gcc -fsanitize=address,undefined -Wall -Wextra -g -o prog main.c
```

- **ASan** (`address`) findet: Buffer-Overflows, use-after-free, double-free, invalid `free()`.
- **UBSan** (`undefined`) findet: uninitialisierte Reads, Integer-UB, etc.
- Fängt genau die Bugs oben ab, _bevor_ sie zufällig "funktionieren".

---

## Checkliste vor jedem PR/Commit

- [ ] Jeder `malloc`-Aufruf für Strings: `+1` für `'\0'` eingeplant und gesetzt?
- [ ] Jeder `fopen` hat genau ein `fclose`, kein `free` auf `FILE*`?
- [ ] Alle Pointer/Variablen bei Deklaration initialisiert?
- [ ] Mit `-fsanitize=address,undefined -Wall -Wextra` kompiliert & getestet?