## 1. Mehrdimensionale Arrays & Jagged Arrays

In Java können Zeilen unterschiedliche Längen haben, da ein 2D-Array ein "Array von Arrays" ist.

### Das Pascalsche Dreieck

Hier wird für jede Zeile `i` ein neues Array mit der Länge `i + 1` erstellt.

Java

```java
int n = 5; 
int[][] p = new int[n][]; // Erste Dimension definiert, zweite offen

for (int i = 0; i < p.length; i++) {
    p[i] = new int[i + 1]; // Dynamische Zuweisung der Zeilenlänge
    for (int j = 0; j <= i; j++) {
        if (j == 0 || j == i) {
            p[i][j] = 1;
        } else {
            // Summe der beiden darüberliegenden Elemente
            p[i][j] = p[i - 1][j - 1] + p[i - 1][j];
        }
        System.out.printf("%2d ", p[i][j]);
    }
    System.out.println();
}
```

---

## 2. Arrays und Methoden (Referenz-Verhalten)

Dieses Beispiel ist essenziell für Prüfungen, da es den Unterschied zwischen Inhaltsänderung und Referenzänderung zeigt.

Java

```java
public class CallTest {
    private static void test(int[] a) {
        int[] x = new int[3];
        a[1] = 3; // ÄNDERT das Original-Array t, da a auf denselben Speicher zeigt
        a = x;    // ÄNDERT NUR die lokale Referenz a. t bleibt davon unberührt!
    }

    public static void main(String[] args) {
        int[] t = {5, 6, 7};
        test(t);
        System.out.println(t[1]); // Ausgabe: 3 (nicht 6 und nicht 0)
    }
}
```

---

## 3. Rekursion mit Memoisation

Die Memoisation verhindert, dass dieselben Werte (wie bei Fibonacci) immer wieder neu berechnet werden, was die Laufzeit von exponentiell auf linear verbessert.

Java

```java
public class FibonacciWithMemoization {
    // Speicher für bereits berechnete Ergebnisse
    private static final long[] f = new long[93];

    private static long fastFibonacci(int n) {
        if (n <= 2) return 1;
        
        // Wenn Wert noch nicht berechnet (Standard 0), berechne ihn
        if (f[n] == 0) {
            f[n] = fastFibonacci(n - 1) + fastFibonacci(n - 2);
        }
        return f[n]; // Gib gespeicherten Wert zurück
    }
}
```

---

## 4. Algorithmen-Vergleich: Maximale Abschnittssumme

Hier sieht man den krassen Unterschied in der Effizienz. Während die O(n3) Variante bei einer Million Zahlen Jahre bräuchte, erledigt der O(n) Algorithmus das in Millisekunden.

### Die effizienteste Lösung (Kadane-Algorithmus - O(n))

Java

```java
private static int maxSum3(int[] input) {
    int maxSum = input[0];
    int endSum = input[0];

    for (int pos = 1; pos < input.length; pos++) {
        // Entscheide: Aktuelles Element zur Kette hinzufügen oder neu starten?
        endSum = Math.max(endSum + input[pos], input[pos]);
        // Update das globale Maximum
        maxSum = Math.max(maxSum, endSum);
    }
    return maxSum;
}
```

---

## 5. Hilfsklasse `Arrays` (Java API)

Nutze diese Methoden, um Zeit zu sparen und Fehler zu vermeiden:

Java

```java
import java.util.Arrays;

int[] x = {3, 1, 4, 1, 5};
int[][] matrix = {{1, 2}, {3, 4}};

Arrays.sort(x);                         // Sortiert x zu {1, 1, 3, 4, 5}
System.out.println(Arrays.toString(x)); // Schöne Ausgabe: [1, 1, 3, 4, 5]
System.out.println(Arrays.deepToString(matrix)); // Für 2D: [[1, 2], [3, 4]]

boolean gleicherInhalt = Arrays.equals(x, new int[]{1, 1, 3, 4, 5}); // true
```


# Extension 2026S

#### Rekursiv Array-Inhalte ausgeben 
```java
public class RecursiveArrayOutputTest { 
//arr.length > 0 && 0 <= left < arr.length && 0 <= right < arr.length 
	private static void printArrayRecursively(int[] array, int left, int right) 
{ 
	if (left <= right)
	{
		 System.out.print(array[left] + " ");  
		 printArrayRecursively(array, left + 1, right); 
	}
} 
		 
public static void main(String[] args) 
{
 int[] x = new int[]{1, 5, 4, 2, 6, 8, 0, 7}; 
 printArrayRecursively(x, 0, x.length - 1); 
 System.out.println(); printArrayRecursively(x, 2, 5); 
}

}
```

![[Pasted image 20260512154456.png]]



