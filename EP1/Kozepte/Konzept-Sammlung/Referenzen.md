## Referenzen in Java: Technische Dokumentation

### 1. Definition und Funktionsweise

In Java sind Variablen von Referenztypen (alle Klassen, Interfaces und Arrays) keine Container für das Objekt selbst, sondern für dessen **Referenz**. Technisch gesehen ist eine Referenz ein **Pointer** (Zeiger) auf den Speicherbereich im **Heap**, an dem das eigentliche Objekt liegt.

### 2. Speicherlayout: Stack vs. Heap

Um Java-Referenzen zu verstehen, muss man zwischen zwei Speicherbereichen unterscheiden:

- **Stack:** Hier liegen lokale Variablen (Primitive wie `int` sowie die Referenz-Werte selbst).
    
- **Heap:** Hier liegen die tatsächlichen Objekte (Instanzen).
    

#### Beispiel:

Java

```java
StringBuilder sb = new StringBuilder("Hallo");
```

**Was passiert technisch?**

1. `new StringBuilder("Hallo")`: Ein neues Objekt wird auf dem **Heap** erzeugt.
    
2. `sb`: Eine Variable auf dem **Stack** wird reserviert.
    
3. Die **Referenz** (die Adresse des Objekts) wird in `sb` gespeichert.
    

### 3. Verhalten bei Zuweisungen (Copy-by-Value)

Ein häufiges Missverständnis ist, dass Java bei Objekten "Pass-by-Reference" nutzt. Tatsächlich nutzt Java **immer** "Pass-by-Value" – bei Objekten ist der "Value" jedoch die **Referenz**.

#### Code-Beispiel: Identität vs. Kopie

Java

```
StringBuilder original = new StringBuilder("Daten");
StringBuilder kopie = original; // Nur die Referenz wird kopiert!

kopie.append(" verändert");

System.out.println(original); // Ausgabe: "Daten verändert"
```

**Analyse:** Da `original` und `kopie` denselben Referenzwert (dieselbe Adresse) halten, zeigen beide auf das identische Objekt im Heap. Eine Änderung über `kopie` betrifft also auch `original`.

### 4. Die Bedeutung von `null`

Eine Referenzvariable, die auf kein Objekt zeigt, hat den Wert `null`. Technisch gesehen ist dies ein spezieller "Null-Zeiger". Der Versuch, über eine solche Variable auf Methoden zuzugreifen, führt zur `NullPointerException`.

### 5. Vorteile der Referenz-Architektur

|Merkmal|Technische Auswirkung|
|---|---|
|**Speicherplatz**|Referenzen haben eine feste Größe (meist 32 oder 64 Bit), unabhängig davon, wie groß das referenzierte Objekt ist.|
|**Performance**|Beim Übergeben von Objekten an Methoden muss nicht das gesamte Objekt kopiert werden, sondern nur die kleine Referenz.|
|**Polymorphie**|Eine Referenz vom Typ `Animal` kann auf ein Objekt vom Typ `Dog` zeigen. Da die Referenzgröße fix ist, kann Java zur Laufzeit entscheiden, welche Methode aufgerufen wird (Dynamic Dispatch).|
|**Garbage Collection**|Java erkennt automatisch, wenn kein Stack-Eintrag (Referenz) mehr auf ein Heap-Objekt zeigt, und gibt den Speicher frei.|
