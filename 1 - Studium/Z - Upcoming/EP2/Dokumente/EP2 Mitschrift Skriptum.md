Beginnend bei Kapitel 2 "Datenabstraktion"

Disclaimer: 
Puntigamers "Abstraktion" heißt nichts anderes als, ich verschachtele und und erzeuge schnittstellen zu meiner Klasse. Falls möglich implementiere ich Datenstrukturen. 

Kapitel 2 ist mit Abstand das wichtigste Kapitel und Kapitel 3.1 und 3.2 und 3.3.3
##### 2.1.2 Datenkapselung

- Objektvariablen sind variablen, die man nach erzeugung eines Objekts zugreifen kann, existieren solange das Objekt existiert
- Objektmethoden sind Methoden die erst zugreifbar werden, wenn man eine neues Objekt der jeweiligen Klasse erzeugt hat. Objektmethoden mit static, haben keinen Zugriff auf Objektvariablen

Das Zusammenfügen von Variablen und Methoden zu Objekten nennt man *Datenkapselung* - Objecte und Methoden kapseln Daten.


Methoden mit `static` sind *statische Methoden* oder *Klassenmethoden* und darf nicht auf Objektvariablen zugreifen.

Aufruf von Objektmethoden:

```Java
C.c(...); // Aufruf von c in Klasse C
C x = new C(); // Erzeugung von Objekt x in der Klasse C
x.o(...); // Aufruf von o in Objekt x
```


Btw, Objektmethoden können direkt ausgeführt werden, innerhalb der Klasse in der man sich befindet. Bspw A1.1

```Java
public class Vector2D
{
	private int x; 
	private int y;
	(...)
	
	public void getX{return x;}
	public void getY{ return y;}
	
	(...)
	
	public double[] toArray()
	{
		return new double[]{getX(),getY()};
	}
}
```

Klassenvariablen sind mit `static` deklariert, eine Klassenvariable existiert nur einmal pro Klasse, nicht in jedem Objekt. Auf Klassenvariablen können Klassenmethdoden und Objektmethoden zugreifen. 
Der sinnvolle Umgang mit Klassenvariablen ist schwierig, falls sie verwendet werden, dann nur mit `static final V`

###### Aufgabe 2.2 
Beschreiben Sie Gemeinsamkeiten und Unterschiede zwi-
schen Klassen- und Objektmethoden. Beschreiben Sie, anhand welcher
Kriterien Sie sich für welche Art von Methode entscheiden.

- Gemeinsakeiten: Beide werden in einer Klasse definiert, haben eine Parameterangabe (Signatur) (Name, Parameter, Rückgabetyp etc.), können überladen werden und unterliegen der gleichen Sichtbarkeit.
- Unterschiede: Klassenmethoden gehören zu einer Klasse und können über den Klassennamen aufgerufen werden, ohne einem Objekt. Sie dürfen nicht auf Objektvariablen zugreifen `this` und können nur auf statische Mitglieder der eigenen Klasse zugreifen. Objektmethoden gehören einem Objekt und können Objektvariablen lesen und verändern, außerdem sind Objektmethoden überschreibbar (@Override) statische Methoden nur verdeckbar (private)
- Entscheidungskriterien: 
	- Objektmethode: wenn die Methode den Zustand eines Objektsbraucht oder überschrieben werden soll (zB. `compareTo` etc.)
	- Klassenmethode: wenn das ergebnis von den Parametern abhängt (Hilfsmethoden wie Math.max bspw)
#####  2.1.3 Data-Hiding
Abschotten der Klasse, sprich die Sichtbarkeit ändern. Also eine Außenansicht und Innenansicht einführen/implementieren. 

- Außenansicht ist die Anwendersicht
- Innenansicht konzentriet sich auf Implementierung der Methoden. Variablen und Typen werden so gewählt, dass die Implementierung möglichst einfach sind und dennoch den Beschreibungen entsprechen.


Bei Data-Hiding geht es darum welche Methoden und Variablen als public und welche als private deklariert sind.
- `private` alles für die Innenansicht, bspw Hilfmethoden
- `public` alles für die Aussenansicht

Das heißt, private ist die bevorzugte Variante für das Implementieren.

*Setter-* und *Getter-Methoden*


Bsp:
![[Pasted image 20261002113244.png]]

Anmerkung, der Kommentar zu origin() ist irreführend, man verändert den Koordinatenursprung 

Bei diesem Beispiel schreibt man ja x -= p.x und nicht p.getX();
Das ist möglich, weil der deklarierte Typ von p gleich der Klasse ist, in der der wir uns befinden. Tatsächlich bedeutet `private`, dass nur innerhalb der Klasse auf mit diesem Modifier versehen Variablen und Methoden zugegriffen werden kann. Also in anderen Worten, wenn eine Objektmethode eine Klasse des gleichen Typs ändert, kann man auch `private` Objektvariablen ändern. `private` beschränkt nur die Sichtbarkeit außerhalb dieser jeweiligen Klasse. 

###### Public Klassen
Klassen die `public` sind eigen. Jede `public` Klasse muss in der Date desselben Namens sein, bspw `Hello.java` muss `public class Hello{}` haben. 
Klassen die kein `public` haben sind **Hilfklassen**, die von einer *public* Klasse 
