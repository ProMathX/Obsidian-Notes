## 7. Algorithmen und Komplexitätsanalyse

### 7.1. Algorithmen

Ein Algorithmus ist ein endliches, schrittweises Verfahren, das Eingabedaten in Ausgabedaten transformiert. Wichtige Eigenschaften:

*   Endlichkeit (statisch und dynamisch).
*   Eindeutigkeit und Ausführbarkeit der Schritte.
*   Terminierung (hält nach endlich vielen Schritten an).

### 7.2. Komplexitätsanalyse (O-Notation)

Die O-Notation beschreibt das Wachstum der Laufzeit als Funktion der Eingabegröße `n` im Worst-Case (schlechtester Fall).

*   **Regel:** Es zählt nur der Term mit dem höchsten Grad.
    *   Beispiel: `5n^4 + 3n^3 + ...` ist in `O(n^4)`.
*   **Sequentiell (Addition):** Der dominante Term gewinnt. `O(n) + O(n^2) = O(n^2)`.
*   **Verschachtelt (Multiplikation):** Komplexitäten werden multipliziert. `O(n) ⋅ O(n) = O(n^2)`.

### 7.3. Typische Komplexitätsfunktionen

| Bezeichnung | Komplexität | Beispiel |
| :--- | :--- | :--- |
| Konstant | `O(1)` | Array-Länge abfragen (`.length`). |
| Logarithmisch | `O(log n)` | Binäre Suche. |
| Linear | `O(n)` | Summe aller Elemente in einem Array. |
| Log-Linear | `O(n log n)` | Schnelle Sortieralgorithmen. |
| Quadratisch | `O(n^2)` | Zwei verschachtelte Schleifen. |
| Kubisch | `O(n^3)` | Drei verschachtelte Schleifen. |
| Exponentiell | `O(k^n)` | Türme von Hanoi (`O(2^n)`). |

**Beispiel Maximale Abschnittssumme:**

| Variante | Komplexität | Anzahl Schleifen |
| :--- | :--- | :--- |
| `maxSum1` | `O(n^3)` | 3 verschachtelt |
| `maxSum2` | `O(n^2)` | 2 verschachtelt |
| `maxSum3` | `O(n)` | 1 Schleife (linear) |

```java
// Effizienteste Variante: O(n)
private static int maxSum3(int[] input) {
 int maxSum = input[0], endSum = maxSum;
 for (int pos = 1; pos < input.length; pos++) {
  endSum = Math.max(endSum + input[pos], input[pos]);
  maxSum = Math.max(maxSum, endSum);
 }
 return maxSum;
}
```

#  Suchalgorithmen (EP1)

---

## 1. Allgemeine Annahmen

*   **Datenstruktur:** Die Daten werden in einem **Array** gespeichert.
*   **Datentypen:** Die präsentierten Algorithmen funktionieren grundsätzlich auf verschiedenen Datentypen, die Beispiele verwenden jedoch ganze Zahlen (`int`).
*   **Implementierung:** Die Algorithmen werden in statischen Methoden implementiert und erwarten existierende (nicht `null`) Arrays.

---

## 2. Lineare Suche (Linear Search)

### 2.1. Prinzip und Komplexität

Die Lineare Suche (auch sequentielle Suche genannt) durchläuft ein Array von Anfang bis Ende, um den gesuchten Wert (`key`) zu finden.

*   **Voraussetzung:** Funktioniert auf **unsortierten** und sortierten Arrays.
*   **Rückgabe:** Position (Index) im Array, an der der Wert gefunden wurde. Bei Nichterfolg wird ein ungültiger Index zurückgegeben (häufig **-1**).
*   **Komplexität:** Im Worst-Case (Element nicht vorhanden oder am Ende) muss das gesamte Array durchsucht werden. Die Laufzeit ist **$O(n)$** (Linear).

### 2.2. Implementierung

```java
private static final int NOT_FOUND = -1;

private static int search(int[] data, int key) {
    for (int i = 0; i < data.length; i++) {
        if (data[i] == key) {
            return i; // Erfolgreich gefunden
        }
    }
    return NOT_FOUND; // Nicht gefunden
}
```

## 3. Binäre Suche (Binary Search)

### 3.1. Prinzip und Voraussetzungen

Die Binäre Suche nutzt die Sortierung der Daten, um den Suchbereich exponentiell zu verkleinern.

*   **Voraussetzung:** Das Array muss sortiert sein.
*   **Prinzip:** Vergleicht den gesuchten Wert (key) mit dem Element in der Mitte (mid) des aktuellen Suchbereichs. Entsprechend dem Ergebnis wird die obere (high) oder untere (low) Grenze des Suchbereichs halbiert.

### 3.2. Implementierung

Die Binäre Suche wird typischerweise iterativ implementiert.

```java
private static int binarySearch(int[] data, int key) {
    int low = 0;
    int high = data.length - 1;

    while (low <= high) {
        // Berechnet den mittleren Index.
        // Die Formel low + (high - low) / 2 verhindert einen Überlauf
        int mid = low + (high - low) / 2; 

        if (key == data[mid]) {
            return mid; // Erfolgreich gefunden
        } else if (key < data[mid]) {
            high = mid - 1; // Suche in der unteren Hälfte
        } else {
            low = mid + 1; // Suche in der oberen Hälfte
        }
    }
    return NOT_FOUND; // Nicht gefunden
}
```

### 3.3. Komplexität

*   Da der Suchbereich in jedem Schritt halbiert wird, ist die Laufzeit sehr effizient.
*   **Komplexität:** $O(\log n)$ (Logarithmisch).

## 4. Java API: `Arrays.binarySearch()`


Die Methode `Arrays.binarySearch()` aus der Hilfsklasse `java.util.Arrays` implementiert die Binäre Suche.

### Rückgabewert bei erfolgloser Suche

Wenn der Wert nicht gefunden wird, liefert die Methode einen negativen Wert zurück. Aus diesem negativen Wert kann die Stelle rekonstruiert werden, an der der Wert in der sortierten Reihenfolge stehen würde:


`Rückgabewert = -(Einfügeposition + 1)`

Der Absolutbetrag des Rückgabewerts abzüglich 1 entspricht der Position, an der das Element stehen sollte.

## 5. Vergleich: Lineare vs. Binäre Suche


| Kriterium                  | Lineare Suche                       | Binäre Suche                       |
| -------------------------- | ----------------------------------- | ---------------------------------- |
| **Voraussetzung (Sortierung)** | Funktioniert auf unsortierten Arrays | Funktioniert nur auf sortierten Arrays |
| **Laufzeit**               | $O(n)$ (Linear)                     | $O(\log n)$ (Logarithmisch)        |
| **Effizienz**              | Langsam für große n                 | Sehr schnell für große n           |

#  Elementare Sortieralgorithmen (EP1)

---

## 1. Allgemeine Annahmen

* [cite_start]**Datenstruktur:** Die Daten (sog. **Schlüssel**) werden in einem **Array** gespeichert[cite: 5].
* [cite_start]**Ordnung:** Auf den Daten ist eine Ordnungsrelation ($\le$) definiert[cite: 5].
* [cite_start]**Implementierung:** Die Algorithmen werden in Methoden implementiert und erwarten existierende (nicht `null`) Arrays[cite: 5]. O. B. d. [cite_start]A. wird immer **aufsteigend** sortiert[cite: 5].
* [cite_start]**Beispiele:** Die Beispiele verwenden zunächst ganze Zahlen, die Algorithmen funktionieren aber grundsätzlich auch auf anderen Datentypen[cite: 5].

---

## 2. Bubblesort

### 2.1. Prinzip

[cite_start]Bubblesort durchläuft das Array von links nach rechts[cite: 6].

* [cite_start]Es werden immer **zwei benachbarte Elemente** betrachtet[cite: 6].
* [cite_start]Wenn sie in **falscher Reihenfolge** vorkommen, werden sie **vertauscht**[cite: 6].
* [cite_start]Dieser Schritt wird so lange wiederholt, bis das Array komplett sortiert ist[cite: 6].
* [cite_start]Das **letzte Element** des vorherigen Durchlaufs muss nicht mehr beachtet werden, da es sich an der richtigen Position befindet[cite: 6].

### 2.2. Implementierung

```java
private static void bubbleSort(int[] data) {
    for (int i = 0; i < data.length - 1; i++) {
        boolean swapped = false;
        // Der letzte i-Elemente sind bereits an richtiger Position
        for (int j = 0; j < data.length - 1 - i; j++) {
            if (data[j] > data[j + 1]) {
                // Tauschen
                int temp = data[j];
                data[j] = data[j + 1];
                data[j + 1] = temp;
                swapped = true;
            }
        }
        // Optimierung: Wenn nichts getauscht wurde, ist das Array sortiert
        if (!swapped) {
            break;
        }
    }
}
````

### 2.3. Komplexität

  * [cite_start]Die zwei verschachtelten Schleifen ergeben eine Komplexität von **$O(n^2)$**[cite: 8].

-----

## 3\. Insertionsort (Einfügesort)

### 3.1. Prinzip

[cite_start]Insertionsort arbeitet in zwei Bereichen: einem bereits **sortierten** linken Teil und einem **unsortierten** rechten Teil[cite: 9].

  * [cite_start]Das Verfahren beginnt mit dem zweiten Element (`i=1`)[cite: 9].
  * [cite_start]Dieses Element wird mit den Elementen im bereits sortierten Teil verglichen[cite: 9].
  * [cite_start]Das Element wird an die richtige Stelle in den sortierten Teil eingefügt, wobei die größeren Elemente nach rechts verschoben werden[cite: 9].

### 3.2. Implementierung

```java
private static void insertionSort(int[] data) {
    // Die Schleife startet bei 1, da das erste Element (Index 0) als sortiert gilt
    for (int i = 1; i < data.length; i++) {
        int current = data[i];
        int j = i - 1;

        // Verschiebe Elemente des sortierten Bereichs, die größer 
        // als 'current' sind, eine Position nach rechts
        while (j >= 0 && data[j] > current) {
            data[j + 1] = data[j];
            j--;
        }
        // Füge 'current' an die korrekte Position ein
        data[j + 1] = current;
    }
}
```

### 3.3. Komplexität

  * **Best-Case:** Array ist bereits sortiert, nur die äußere Schleife läuft. [cite_start]Komplexität **$O(n)$**[cite: 13].
  * **Worst-Case:** Array ist umgekehrt sortiert. [cite_start]Komplexität **$O(n^2)$**[cite: 13].
  * [cite_start]**Average-Case:** Komplexität **$O(n^2)$**[cite: 13].

-----

## 4\. Selectionsort (Auswahlsort)

### 4.1. Prinzip

[cite_start]Selectionsort unterteilt das Array in einen **sortierten** (links) und einen **unsortierten** (rechts) Teil[cite: 14].

  * [cite_start]In jedem Durchlauf wird das **kleinste Element** im unsortierten Teil gesucht[cite: 14].
  * [cite_start]Dieses kleinste Element wird an die erste Position des unsortierten Teils (Ende des sortierten Teils) **getauscht**[cite: 14].

### 4.2. Implementierung

```java
private static void selectionSort(int[] data) {
    for (int i = 0; i < data.length - 1; i++) {
        int minIndex = i;

        // Finde den Index des kleinsten Elements im Rest des Arrays
        for (int j = i + 1; j < data.length; j++) {
            if (data[j] < data[minIndex]) {
                minIndex = j;
            }
        }
        
        // Vertausche das kleinste Element mit dem Element an Position i
        if (minIndex != i) {
            int temp = data[minIndex];
            data[minIndex] = data[i];
            data[i] = temp;
        }
    }
}
```

### 4.3. Komplexität

  * [cite_start]In jedem Fall (Best-Case und Worst-Case) müssen zwei verschachtelte Schleifen ausgeführt werden[cite: 17].
  * [cite_start]**Komplexität:** **$O(n^2)$**[cite: 17].

-----

## 5\. Stabilität von Sortieralgorithmen

### 5.1. Definition

[cite_start]Ein Sortieralgorithmus ist **stabil**, wenn die **relative Reihenfolge** von Elementen mit **gleichem Schlüssel** (Wert) nach der Sortierung erhalten bleibt[cite: 25].

  * [cite_start]Stabilität ist nur bei zusammengesetzten Datensätzen (z.B. Personen mit Name und Abteilungsnummer) relevant[cite: 25].

### 5.2. Vergleich

| Algorithmus | Stabilität | Begründung |
| :--- | :--- | :--- |
| **Bubblesort** | **Stabil** | [cite_start]Vertauscht nur, wenn das linke Element streng größer als das rechte ist[cite: 26]. |
| **Insertionsort** | **Stabil** | [cite_start]Elemente mit gleichem Schlüssel werden nie vertauscht, nur verschoben[cite: 26]. |
| **Selectionsort** | **Instabil** | [cite_start]Tauscht Elemente über große Distanzen, was die relative Ordnung gleicher Schlüssel zerstören kann[cite: 26]. |

Diese Algorithmen basieren auf dem Prinzip des **Teile-und-herrsche-Verfahrens** (Divide-and-Conquer):

1.  **Teilen (Divide):** Teile das Problem in Teilprobleme.
2.  **Herrschen (Conquer):** Löse die Teilprobleme rekursiv.
3.  **Kombinieren (Combine):** Kombiniere die Teillösungen zur Gesamtlösung.

-----

## 1\. Mergesort (Fusionssortierung)

Mergesort ist ein **stabiler** Sortieralgorithmus, der garantiert in $O(n \log n)$ läuft.

###  Funktionsweise

Mergesort verwendet das **Teile-und-herrsche-Prinzip** wie folgt:

1.  **Teilen:** Das Array wird rekursiv in zwei Hälften geteilt, bis nur noch Arrays der Größe 1 übrig sind (diese sind per Definition sortiert).
2.  **Herrschen:** Die Einzel-Arrays werden rekursiv zu sortierten Unter-Arrays zusammengeführt (verschmolzen).
3.  **Verschmelzen (Merge):** Zwei bereits sortierte Unter-Arrays werden zu einem neuen, sortierten Array zusammengeführt. Hierzu werden die Elemente beider Unter-Arrays der Größe nach verglichen und der Reihe nach in ein **Hilfsarray** kopiert.

###  Komplexität

| Fall | Laufzeit (O-Notation) | Begründung |
| :--- | :--- | :--- |
| **Best/Average/Worst Case** | $O(n \log n)$ | Die Aufteilung ($\log n$) und das anschließende Verschmelzen ($n$) finden immer statt, unabhängig von der Vorsortierung der Daten. |
| **Speicherbedarf** | $O(n)$ | Es wird ein zusätzliches Hilfsarray der Größe $n$ für die Merge-Operation benötigt. |

###  Code-Snippet (Grundstruktur der Rekursion)

```java
private static void mergeSort(int[] data, int[] help, int lo, int hi) {
    if (hi <= lo) return; // Basisfall: Array der Größe 1 ist sortiert
    
    int mid = lo + (hi - lo) / 2;
    
    // 1. und 2. Schritt: Teilen und rekursiv Herrschen
    mergeSort(data, help, lo, mid);
    mergeSort(data, help, mid + 1, hi);
    
    // 3. Schritt: Kombinieren (Verschmelzen)
    merge(data, help, lo, mid, hi); 
}
// Die 'merge'-Methode (nicht gezeigt) führt das eigentliche Zusammenführen
// der zwei sortierten Hälften lo..mid und mid+1..hi durch.
```

-----

## 2\. Quicksort (Schnelles Sortieren)

Quicksort ist ein **instabiler** Sortieralgorithmus und in der Praxis oft der schnellste vergleichsbasierte Sortieralgorithmus.

###  Funktionsweise

Quicksort basiert ebenfalls auf dem **Teile-und-herrsche-Prinzip**, wobei der Fokus auf dem "Teilen" liegt:

1.  **Partitionierung (Teilen):** Wähle ein **Pivot-Element** (oft das erste, letzte oder ein zufälliges Element). Ordne das Array so um, dass alle Elemente, die **kleiner** als das Pivot sind, links stehen und alle Elemente, die **größer oder gleich** dem Pivot sind, rechts stehen. Das Pivot steht nun an seiner endgültigen, sortierten Position.
2.  **Herrschen:** Sortiere die beiden Hälften (links und rechts vom Pivot) rekursiv.
3.  **Kombinieren:** Es ist keine explizite Kombinierung nötig, da das Array bereits "in-place" (am Ort) sortiert wurde.

###  Komplexität

| Fall | Laufzeit (O-Notation) | Begründung |
| :--- | :--- | :--- |
| **Average Case / Best Case** | $O(n \log n)$ | Die Pivot-Wahl teilt das Array gleichmäßig auf. |
| **Worst Case** | $O(n^2)$ | Die Pivot-Wahl führt zu einer sehr ungleichmäßigen Aufteilung (z.B. wenn immer das kleinste oder größte Element als Pivot gewählt wird). |
| **Speicherbedarf** | $O(\log n)$ (rekursiv) | Benötigt nur wenig zusätzlichen Speicherplatz, da die Sortierung **In-Place** erfolgt. |

###  Code-Snippet (Grundstruktur der Rekursion)

```java
private static void quickSort(int[] data, int lo, int hi) {
    if (hi <= lo) return; // Basisfall: Array der Größe 1 ist sortiert
    
    // 1. Schritt: Partitionierung (Rückgabe des Index j des Pivots)
    int j = partition(data, lo, hi); 
    
    // 2. Schritt: Rekursives Sortieren der beiden Hälften
    quickSort(data, lo, j - 1); // Linke Hälfte
    quickSort(data, j + 1, hi); // Rechte Hälfte
}
// Die 'partition'-Methode (nicht gezeigt) wählt das Pivot und ordnet
// die Elemente des Array-Teils lo..hi entsprechend um.
```

-----

## 3\. Countingsort (Lineares Sortieren)

Ein Spezialfall, der nicht auf Vergleichen basiert und unter bestimmten Annahmen extrem effizient ist.

### Funktionsweise

Countingsort funktioniert in $O(n)$, setzt aber voraus, dass die zu sortierenden $n$ Elemente ganze Zahlen in einem **kleinen, bekannten Bereich** von $0$ bis $max$ sind.

1.  **Zählen:** Ein Hilfsarray (`counts`) der Größe $max+1$ wird verwendet, um zu zählen, wie oft jede Zahl im Eingabearray vorkommt.
2.  **Zurückschreiben:** Die Zahlen werden gemäß den Zählergebnissen in das ursprüngliche Array zurückgeschrieben.

###  Komplexität

  * **Laufzeit:** $O(n)$
  * **Speicherbedarf:** $O(max)$ für das Hilfsarray. (Dies ist nur effizient, wenn $max$ nicht viel größer als $n$ ist).

###  Code-Snippet (Kernfunktionalität)

```java
private static void countingSort(int[] data, int max) {
    int[] counts = new int[max + 1];
    
    // Zähle Vorkommen O(n)
    for (int i = 0; i < data.length; i++) {
        counts[data[i]]++;
    }
    
    // Schreibe sortiert zurück O(max + n) -> O(n)
    int i = 0;
    for (int j = 0; j <= max; j++) {
        for (int k = 0; k < counts[j]; k++) {
            data[i++] = j;
        }
    }
}
```

Das Pivot-Element und die Suchalgorithmen sind grundlegende Konzepte in der Programmierung.

Hier sind die detaillierten Erklärungen:

-----

## 1\. Das Pivot-Element (Quicksort)

Das Pivot-Element ist das Herzstück des **Quicksort-Algorithmus**.

### Was ist das Pivot-Element?

Das Pivot-Element ist ein Element, das aus dem zu sortierenden Array-Ausschnitt gewählt wird. Es dient als **Teilungsachse** oder **Dreh- und Angelpunkt** (Pivot) für den Sortiervorgang in diesem Teilbereich.

### Die Rolle des Pivot-Elements bei der Partitionierung

Die Hauptarbeit in Quicksort ist die sogenannte **Partitionierung** (Teilung). Das Ziel ist, das Pivot-Element an seine endgültige, sortierte Position $j$ zu bringen und gleichzeitig das Array in zwei Abschnitte zu teilen:

1.  **Linker Teil:** Alle Elemente mit einem Wert **kleiner** als das Pivot.
2.  **Rechter Teil:** Alle Elemente mit einem Wert **größer oder gleich** dem Pivot.

Nach der Partitionierung steht das Pivot an seiner korrekten Position. Anschließend wird Quicksort auf die linken und rechten Teil-Arrays **rekursiv** angewendet.

### Bedeutung der Pivot-Wahl

Die Wahl des Pivot-Elements ist entscheidend für die Effizienz von Quicksort:

| Fall | Pivot-Wahl | Laufzeit |
| :--- | :--- | :--- |
| **Best Case** | Das Pivot teilt das Array immer fast genau in der Mitte. | **$O(n \log n)$** |
| **Worst Case** | Das Pivot ist immer das kleinste oder größte Element des Array-Ausschnitts (z.B. bei einem vorsortierten Array, wenn immer das erste Element gewählt wird). | **$O(n^2)$** |

-----

## 2\. Suchalgorithmen

Es wurden zwei grundlegende Suchalgorithmen besprochen, die sich in ihren Voraussetzungen und ihrer Effizienz stark unterscheiden:

### A) Lineare Suche (Linear Search)

#### Funktionsweise

Die Suche geht das Array von vorne nach hinten, **Element für Element**, durch und vergleicht jedes Element mit dem gesuchten Schlüssel ($key$).

#### Voraussetzung

Funktioniert auf **unsortierten** und **sortierten** Arrays.

#### Komplexität

  * **Worst Case:** $O(n)$. Die Laufzeit ist proportional zur Länge des Arrays.

#### Code-Snippet

```java
private static final int NOT_FOUND = -1;

private static int search (int[] data, int key) {
    // Schleife über alle n Elemente
    for (int i = 0; i < data.length; i++) {
        if (data[i] == key) {
            return i; // Index gefunden
        }
    }
    return NOT_FOUND; // Nicht gefunden
}
```

### B) Binäre Suche (Binary Search)

#### Funktionsweise

Die Binäre Suche nutzt die Sortierung des Arrays aus, um den Suchbereich in jedem Schritt zu halbieren:

1.  Wähle das Element in der **Mitte** des aktuellen Suchbereichs (`mid`).
2.  Vergleiche `data[mid]` mit dem gesuchten Schlüssel ($key$).
3.  Ist das Element gefunden, ist die Suche beendet. Ist es kleiner/größer, wird der Suchbereich auf die linke/rechte Hälfte reduziert.

#### Voraussetzung

Funktioniert **nur auf sortierten** Arrays.

#### Komplexität

  * **Worst Case:** $O(\log n)$. Die Laufzeit wächst nur logarithmisch zur Eingabegröße, da sich der Suchbereich halbiert.

#### Code-Snippet

```java
private static int binarySearch(int[] data, int key) {
    int low = 0; 
    int high = data.length - 1; 
    
    while (low <= high) { 
        int mid = low + (high - low) / 2; 
        
        if (data[mid] < key) 
            low = mid + 1; // Suche in der oberen Hälfte
        else if (data[mid] > key) 
            high = mid - 1; // Suche in der unteren Hälfte
        else 
            return mid; // Schlüssel gefunden
    } 
    return NOT_FOUND; 
}
```

