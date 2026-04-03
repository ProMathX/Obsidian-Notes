### Sets (Mengen)

**`HashSet<E>`**

> `HashSet<E>` ist eine Implementierung von `Set<E>` als Hash-Tabelle. Im Konstruktor kann die Anfangsgröße der Tabelle und der Füllgrad, ab dem die Tabelle vergrößert wird, angegeben werden. Meist wird darauf verzichtet, da die Default-Werte gut gewählt sind. Da es sich um eine Hash-Tabelle handelt, geben Iteratoren die Einträge in unvorhersehbarer Reihenfolge zurück.

Java

``` java
// Beispiel aus der Javadoc-Praxis:
Set<String> hashSet = new HashSet<>();
hashSet.add("Apfel");
hashSet.add("Banane");
hashSet.add("Apfel"); // Wird ignoriert, da Sets keine Duplikate erlauben

// Die Ausgabe-Reihenfolge ist nicht garantiert
for (String fruit : hashSet) {
    System.out.println(fruit); 
}
```

**`LinkedHashSet<E>`**

> Eine Variante namens `LinkedHashSet<E>` verkettet alle Einträge zusätzlich in einer linearen Liste, sodass Iteratoren die Einträge in der Reihenfolge des Eintragens zurückgeben.

Java

``` java
Set<String> linkedHashSet = new LinkedHashSet<>();
linkedHashSet.add("Zuerst");
linkedHashSet.add("Zweiter");
linkedHashSet.add("Dritter");

// Die Ausgabe erfolgt garantiert in Einfügereihenfolge
for (String element : linkedHashSet) {
    System.out.println(element); 
}
```

**`TreeSet<E>`**

> `TreeSet<E>` ist eine Implementierung von `SortedSet<E>` als balancierter binärer Suchbaum (nicht AVL-Baum). Im Konstruktor kann bestimmt werden, auf welche Weise die Sortierung erfolgt.

Java

``` java
// Verwendet die natürliche Sortierung (alphabetisch)
SortedSet<String> treeSet = new TreeSet<>();
treeSet.add("Zebra");
treeSet.add("Affe");
treeSet.add("Löwe");

// Die Ausgabe ist automatisch sortiert: Affe, Löwe, Zebra
System.out.println(treeSet.first()); // Gibt "Affe" zurück
```

---

### Maps (Schlüssel-Wert-Paare)

**`HashMap<K,V>` & `LinkedHashMap<K,V>`**

> `HashMap<K,V>` ist eine Implementierung von `Map<K,V>` als eine Hash-Tabelle. Abgesehen davon gilt das gleiche wie für `HashSet<E>` mit der Variante `LinkedHashMap<K,V>`.

Java

``` java
// HashMap Beispiel (keine garantierte Reihenfolge)
Map<String, Integer> hashMap = new HashMap<>();
hashMap.put("Max", 25);
hashMap.put("Anna", 30);
System.out.println("Alter von Anna: " + hashMap.get("Anna"));

// LinkedHashMap Beispiel (Einfügereihenfolge bleibt erhalten)
Map<String, Integer> linkedHashMap = new LinkedHashMap<>();
linkedHashMap.put("Eins", 1);
linkedHashMap.put("Zwei", 2);
```

**`TreeMap<K,V>`**

> `TreeMap<K,V>` ist eine Implementierung von `Map<K,V>` als balancierter Baum, der auf derselben Basis wie `TreeSet<E>` beruht.

Java

``` java
SortedMap<String, Integer> treeMap = new TreeMap<>();
treeMap.put("C", 3);
treeMap.put("A", 1);
treeMap.put("B", 2);

// Die Schlüssel sind hier automatisch aufsteigend sortiert (A, B, C)
```

---

### Lists (Listen)

**`ArrayList<E>`**

> `ArrayList<E>` ist eine Implementierung von `List<E>` als Array, dessen Größe automatisch an die Verwendung (größter Index) angepasst wird. Übliche Arrayzugriffe erfolgen daher sehr effizient, während fast alle anderen Operationen eher ineffizient sind. Objekte von `ArrayList<E>` werden daher häufig anstelle normaler Arrays verwendet, wenn die benötigte Größe im Vorhinein unbekannt ist. Sie werden nur selten wie Listen eingesetzt.

Java

``` java
List<String> arrayList = new ArrayList<>();
arrayList.add("Java");
arrayList.add("Python");

// Sehr effizienter Index-Zugriff:
String language = arrayList.get(0); 
```

**`LinkedList<E>`**

> `LinkedList<E>` ist eine Implementierung von `List<E>` und `Deque<E>` als doppelt verkettete Liste. Der Eintrag von `null` ist erlaubt.

Java

``` java
LinkedList<String> linkedList = new LinkedList<>();
linkedList.add("Element 1");
linkedList.add(null); // Explizit erlaubt
linkedList.addFirst("Neues erstes Element"); // Spezifische LinkedList/Deque Methode
```

---

### Deques (Double Ended Queues)

**`ArrayDeque<E>`**

> `ArrayDeque<E>` ist eine effiziente Implementierung von `Deque<E>` als Array mit automatischer Anpassung der Größe. Da die Effizienz im Mittelpunkt steht, ist die Anwendbarkeit beschränkt. So ist `null` als Eintrag verboten.

Java

``` java
Deque<String> stack = new ArrayDeque<>();
stack.push("Unten");
stack.push("Oben");

// stack.push(null); // Dies würde sofort eine NullPointerException werfen!

// Arbeitet extrem effizient als Stack (LIFO) oder Queue (FIFO)
System.out.println(stack.pop()); // Gibt "Oben" zurück
```
