#C
#studies 
#Betriebssysteme

Dokumenation erfolgt mit Doxygen

`doxygen -g` im Projekt-Folder
Dann entsteht eine Doxyfile

Dann die Doxyfile editieren

```Doxyfile
PROJECT_NAME           = "Hello World Program"
OUTPUT_DIRECTORY       = docs
INPUT                  = .
RECURSIVE              = YES
EXTRACT_STATIC         = YES
GENERATE_LATEX         = NO

```

Dann 
`doxygen Doxyfile`

es kreiert dann ein docs/html in projekt verzeichnis 


dann 
`xdg-open doc/html/index.html`

---
24. Avoid side effects with && and ||, e.g., write if(b != 0) c = a/b; instead of if(b != 0 && c = a/b).
25. Each switch block must contain a default case. If the case is not reachable, write assert(0) to this case (defensive programmin

----
