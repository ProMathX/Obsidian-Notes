# Rekursion – Zusammenfassung (EP1)

## 1. Grundlagen der Rekursion

Rekursion bedeutet, ein Problem zu lösen, indem man es auf kleinere Teilprobleme desselben Typs zurückführt.

- **Basisfall (Abbruchbedingung):** Der Fall, der ohne weiteren Selbstaufruf gelöst werden kann.
    
- **Rekursionsschritt:** Die Methode ruft sich selbst mit veränderten Argumenten auf, um dem Basisfall näher zu kommen.
    

### Beispiel: Summenberechnung (Lineare Rekursion)

Aus PDF: _Rekursion_Grundlagen_

Java

``` java
private static int sumRecursive(int n) {
    if (n <= 1) { // Basisfall
        return 1;
    } else { // Rekursionsschritt
        return n + sumRecursive(n - 1);
    }
}
```

## 2. Endrekursion (Tail Recursion)

Ein Spezialfall, bei dem der rekursive Aufruf die **letzte Aktion** vor der Rückkehr ist. Dies ist effizienter, da keine Berechnungen nach dem Aufruf im Stack verbleiben.

### Beispiel: Größter gemeinsamer Teiler (ggT)

```java
private static int gcdRecursive(int a, int b) {
    if (b == 0) {
        return a;
    }
    return gcdRecursive(b, a % b);
}
```

## 3. Verzweigte Rekursion (Branched Recursion)

Ein Aufruf erzeugt zwei oder mehr weitere rekursive Aufrufe. Dies führt zu einem exponentiellen Wachstum der Aufrufe.

### Beispiel: Fibonacci-Zahlen

Aus PDF: _Rekursion_Fortgeschrittene_Themen_

Java

``` java
private static long fibonacci(int n) {
    if (n <= 2) {
        return 1;
    } else {
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```

### Beispiel: Türme von Hanoi

Aus PDF: _Rekursion_Fortgeschrittene_Themen_

Java

``` java
private static void hanoi(int n, char start, char help, char end) {
    if (n > 0) {
        hanoi(n - 1, start, end, help);
        System.out.println("Move disk " + n + " from " + start + " to " + end);
        hanoi(n - 1, help, start, end);
    }
}
```

## 4. Wechselseitige & Verschachtelte Rekursion

- **Wechselseitig:** Methode A ruft Methode B, und Methode B ruft Methode A.
    
- **Verschachtelt:** Das Argument eines rekursiven Aufrufs ist selbst ein rekursiver Aufruf.
    

### Beispiel: Gerade/Ungerade (Wechselseitig)

Aus PDF: _Rekursion_Fortgeschrittene_Themen_

Java

``` java
private static boolean even(int n) {
    if (n == 0) return true;
    return odd(n - 1);
}
private static boolean odd(int n) {
    if (n == 0) return false;
    return even(n - 1);
}
```

### Beispiel: Ackermann-Funktion (Verschachtelt)

Aus PDF: _Rekursion_Fortgeschrittene_Themen_

Java

```java
private static long ackermann(long n, long m) {
    if (n == 0) return m + 1;
    else if (m == 0) return ackermann(n - 1, 1);
    else return ackermann(n - 1, ackermann(n, m - 1));
}
```

## 5. Terminierung und Fortschritt

Damit eine Rekursion sicher endet, muss sie zwei Kriterien erfüllen:

1. **Fundiertheit:** Es existiert eine erreichbare Abbruchbedingung.
    
2. **Fortschritt:** Jeder Schritt verkleinert das Problem (z.B. `n-1`, `start+1`).
    

## 6. Vergleich: Rekursion vs. Iteration

Aus PDF: _Iteration_Rekursion_

- **Gleichmächtigkeit:** Alles, was rekursiv lösbar ist, ist auch iterativ lösbar (und umgekehrt).
    
- **Speicher:** Rekursion nutzt den **JVM-Stack** (Gefahr des `StackOverflowError`), Iteration nutzt meist den Heap oder lokale Variablen.
    
- **Effizienz:** Iteration ist oft schneller und speicherschonender; Rekursion ist bei hierarchischen Strukturen (wie Bäumen) oft eleganter.