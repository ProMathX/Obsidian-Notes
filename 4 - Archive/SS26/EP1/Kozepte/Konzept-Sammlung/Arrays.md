
---

## 1. Arrays: Grundlagen

Ein Array ist eine Datenstruktur, die eine **Zusammenfassung von gleichartigen Elementen** (Elementen des gleichen Typs) ermöglicht.

### 1.1. Deklaration, Erzeugung und Initialisierung

Arrays müssen deklariert und erzeugt werden, bevor sie verwendet werden können.

| Konzept | Beschreibung | Beispiel Code |
| :--- | :--- | :--- |
| **Deklaration** | Legt den Typ und den Namen der Array-Variable fest. | `int[] number;` |
| **Erzeugung** | Der `new`-Operator fordert Speicher im **Heap** an und erzeugt das Array-Objekt. Die Größe muss angegeben werden. | `int[] arr = new int[10];` |
| **Standardinitialisierung** | Nach dem Erzeugen werden alle Array-Elemente automatisch initialisiert (z.B. `int` mit `0`, `boolean` mit `false`, Referenztypen wie `String` mit `null`). | |
| **Direkte Initialisierung** | Arrays können auch direkt mit Werten erzeugt werden. | `int[] arr = {3, 4, 5, 6, 7};` |

### 1.2. Zugriff und Iteration

*   **Index:** Der Zugriff auf Elemente erfolgt über einen Index. Die Zählung beginnt bei **0** und geht bis **(Länge - 1)**.
*   **Länge:** Die Länge eines Arrays wird über **`.length`** abgefragt.
*   **Zugriff:** Der Index wird in eckigen Klammern angegeben.
*   **Fehler:** Ein Zugriff außerhalb des gültigen Indexbereichs führt zur **`ArrayIndexOutOfBoundsException`**.
*   **Iteration (foreach):** Die for-Schleife in der Iterator-Form durchläuft alle Elemente in aufsteigender Reihenfolge.

```java
// Zugriff
int[] array = new int[5];
array[0] = 2;
array[1] = array[0] + 3;

// Iteration (foreach-Schleife)
int[] arr = {3, 4, 5, 6, 7};
for (int i : arr)
 System.out.println(i);
```

---

## 2. Arrays als Referenztypen (Speicher)

Array-Variablen sind **Referenztypen**. Die Variable speichert nicht die Daten selbst, sondern nur eine **Speicheradresse** (eine Referenz), die auf das Array-Objekt im **Heap** zeigt.

### 2.1. Stack und Heap

*   **Stack:** Speichert lokale Variablen, einschließlich der Array-Referenzen.
*   **Heap:** Speichert die eigentlichen Array-Objekte (die Daten).

### 2.2. Zuweisung von Referenzen

Bei der Zuweisung von Array-Variablen (z. B. `y = x;`) wird **nur die Referenz (Adresse) kopiert**, nicht der Inhalt.

*   Beide Variablen (z. B. x und y) zeigen danach auf dasselbe Array (**Aliase**).
*   Änderungen über die eine Variable sind sofort über die andere sichtbar.

```java
int[] x = new int[10], y;
y = x; // y und x zeigen auf das gleiche Array
y[1] = 7;
System.out.println(x[1]); // Gibt 7 aus
```

### 2.3. Speicherfreigabe (Garbage Collector)

*   Der Garbage Collector gibt Heap-Speicher automatisch frei, sobald dieser nicht mehr durch eine Variable referenziert wird.

---

## 3. Arrays kopieren und vergleichen

### 3.1. Vergleichen

*   `Arrays.equals(a, b)`: Vergleicht den Inhalt von eindimensionalen Arrays.
*   `Arrays.deepEquals(a, b)`: Vergleicht den Inhalt von mehrdimensionalen Arrays.

### 3.2. Kopieren

Um den Inhalt zu kopieren, muss ein neues Array erzeugt werden.

*   Manuelle Schleife oder `System.arraycopy()`.
*   `clone()`: Erzeugt eine (flache) Kopie des Arrays.

---

## 4. Mehrdimensionale Arrays

Mehrdimensionale Arrays (z. B. 2D-Arrays) sind in Java **"Arrays von Arrays"**. Die äußere Array-Variable enthält Referenzen auf die inneren Arrays (Zeilen).

### 4.1. "Jagged Arrays" (Verzahnte Arrays)

Die inneren Arrays können unterschiedliche Längen haben, da jede Zeile ein eigenes Array-Objekt ist.

```java
int[][] arr1 = new int[2][]; // Nur äußeres Array
for (int i = 0; i < arr1.length; i++)
 arr1[i] = new int[i + 2]; // Erzeugt Zeilen mit Länge 2 und 3
```

### 4.2. Flache vs. Tiefe Kopie (Shallow vs. Deep Copy)

*   **Flache Kopie** (z. B. mit `clone()`): Nur die erste Ebene wird kopiert. Die inneren Arrays werden geteilt.
*   **Tiefe Kopie:** Es müssen alle Ebenen manuell kopiert werden.

```java
// Beispiel: Tiefe Kopie
int[][] a = new int[][]{{3, 2, 1}, {1, 0}};
int[][] b = new int[a.length][];
for (int i = 0; i < a.length; i++) {
 b[i] = new int[a[i].length]; // Neues inneres Array erzeugen
 for (int j = 0; j < a[i].length; j++) {
  b[i][j] = a[i][j]; // Werte kopieren
 }
}
```

---

## 5. Arrays und Methoden

### 5.1. Parameterübergabe

Wenn ein Array an eine Methode übergeben wird, wird nur die Referenz kopiert.

*   **Seiteneffekt:** Änderungen am Inhalt des Arrays sind außerhalb sichtbar.
*   **Kein Seiteneffekt:** Eine Zuweisung der Referenz selbst innerhalb der Methode ist außerhalb nicht sichtbar.

```java
private static void test(int[] a) {
 int[] x = new int[3];
 a[1] = 3; // Diese Änderung ist AUẞEN sichtbar
 a = x;    // Diese Zuweisung ist NICHT außen sichtbar
}
public static void main(String[] args) {
 int[] t = {5, 6, 7};
 test(t);
 System.out.println(t[1]); // Gibt 3 aus (der Seiteneffekt)
}
```

### 5.2. Kommandozeilenargumente und Varargs

*   `main(String[] args)`: Die main-Methode empfängt Kommandozeilenargumente als String-Array.
*   **Varargs (`...`)**: Ermöglicht die Übergabe einer variablen Anzahl von Argumenten, die intern als Array behandelt werden (z. B. `private static int sum(int... values)`).

### 5.3. Rekursion und Memoisation

Arrays werden zur Memoisation (Zwischenspeicherung von Ergebnissen) in rekursiven Funktionen verwendet, um doppelte Berechnungen zu vermeiden (z. B. bei der Fibonacci-Folge).

```java
public class FibonacciWithMemoization {
 private static final long[] f = new long[93];
 private static long fastFibonacci(int n) {
  if (n <= 2) {
   return 1;
  } else if (f[n] == 0) { // Prüfen, ob Wert schon berechnet
   f[n] = fastFibonacci(n - 1) + fastFibonacci(n - 2); // Berechnen und speichern
  }
  return f[n];
 }
}
```

---

## 6. Hilfsklassen und IDE-Unterstützung

### 6.1. Die Klasse java.util.Arrays

Bietet nützliche statische Methoden (muss importiert werden):

| Methode | Beschreibung |
| :--- | :--- |
| `sort(a)` | Sortiert ein Array aufsteigend. |
| `binarySearch(a, key)` | Führt eine binäre Suche in einem sortierten Array durch. |
| `fill(a, val)` | Befüllt alle Stellen mit einem Wert. |
| `toString(a)` | Gibt den Inhalt eines eindimensionalen Arrays als String zurück. |
| `deepToString(a)` | Gibt den Inhalt eines mehrdimensionalen Arrays als String zurück. |

### 6.2. IDE-Unterstützung (IntelliJ)

*   **Debugger:** Ermöglicht das detaillierte Inspizieren von Array-Inhalten (auch 2D-Arrays) zur Laufzeit.
*   **Java Visualizer:** Ein Plugin zur grafischen Darstellung der Speicherbelegung (Stack und Heap) von Arrays.

---