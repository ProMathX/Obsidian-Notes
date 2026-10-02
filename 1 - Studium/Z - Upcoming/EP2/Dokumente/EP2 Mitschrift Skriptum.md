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
Klassen die kein `public` haben sind **Hilfklassen**, die von einer *public* Klasse kontrolliert werden, bspw Hilfsmethoden in Klassen, also private Klassenmethoden.


![[Pasted image 20261002114427.png]]

2.5: 
- Datenkapselung:  Zusammenfügen von Variablen und Methoden
- Data-Hiding: Abschotten der Klasse, Sichtbarkeit verändern

2.6:
- Um die Daten zu schützen vor dem Anwender (Altern kann nicht negativ gesetzt werden)
- Änderbarkeit, interner Code kann einfacher geändert werden
- Öffentliche Schnittstelle bleibt klein und überschaubar

2.7:
- Außenansicht: Alles was der Anwender sieht und nutzden kann `public`
- Innenansicht: Alles was der Entwickler sehen und implementieren kann `private`, Anwender kein Zugriff auf Innenansicht

2.8: 
-  Siehe Public Klassen



##### 2.1.4 Objekterzeugung 
Ein neues Objekt wird mit den `new` Keyword aufgerufen.
Jedes erzeugte Objekt, besitzt seine eigene Identität. Das heißt für jede neue Instanz, also Objekt, wird neuer Speicher initialisiert. 
Bei jeder objekterzeugung, wird ein Konstruktor für die Klasse aufgerufen. Ein Konstruktur setzt die Objektvariablen. Jede Klasse hat einen Default-Konstruktor. Konstruktor dienen nur der Initialisierung von Objekten.

###### Constructor overloading
Ist wie Methoden overlaoding. Der Java compiler entscheidet darüber, anhand der Anzahl an deklarierten Typen der Argumente, welche Konstruktor auszuführen ist.

```Java
public class Point
{
	private int x,y;
	
	public Point
	{
		this(0,0);
	}
	
	public Point(x,y)
	{
		this.x = x;
		this.y = y;
	}
	
	public Point(Point p)
	{
		this(p.x,p.y);
	}
	
	public Point copy()
	{
		return new Point(this);
	}

}
```

Erster Konstruktor führt den 2 Konstruktor aus, der 3 Konstruktor führt wieder den 2 Konstruktor aus. 

Einschränkung: Anweisungen der Form this(...) dürfen nur gan am Anfang eines Konstruktors stehen, sonst nirgends. Wenn Programmtexte wie Methoden aufgerufen werden sollen, müssen wir auch Methoden verwenden, nicht Konstruktoren. Mehtoden sind in Konstruktoren uneingeschränkt abrufbar.

Selbstreferenz mit `this`. `this ` ist eine *Pseudovariable*, das bedeutet folgendes, es wird gelesen, aber kann nicht festgelegt werden was für einen Wert es annehmen soll.
Der Wert `this` ist immer eine Referenz auf das Objekt, in dem wir uns gerade befinden. 
Innerhalb des Konstruktors ist es das Objekt, das gerade initialisiert wird. 
Ist x eine Objektvariable, können wir statt `x` auch `this.x` schreiben um deutlich zu machen, dass das `x` aus dem aktuellen Objekt gemeint ist - im gegensatz von `p.x` eines anderen Objekts `p`. 

Falls die Parameter eines Konstruktors gleich heißen wie die Objektvariablen, siehe oben, verdeckt man die variablen mit `this.param`. Also mit dem `this.(param)` greifen wir auf die Objektvariablen zu. `this` greift man auf das Objekt zu.
Zur Errinerung, in Klassenmethoden ist `this` nicht anwendbar, da dort kein aktuelles Objekt zugreifbar ist und keine Objektvariablen sichtbar sind.

![[Pasted image 20261002122528.png]]

2.9
	Default Konstruktor
2.10 
	Zum Initialisieren eines Objekts, wenn eine neue Instanz aufgerufen wird, wodurch man Objektmethoden festlegen kann. 
2.11
	`this` referenziert auf das Objekt in dem man sich befindet, this(...) auf die Objektvariablen innerhalb eines Objekts. Eine Klassenmethode hat keinen Zugriff auf die Pseudovaribale `this`
##### 2.2 Datenstrukturen und abstrakte Datentypen
Was ist der Unterschied zwischen Datenstruktur und Datenabstraktion? 
- Ist eine Art und Weise, wie Daten dargestellt werden und wie sie zusammenhängen, wird meist als abstrakter Datentyp implementiert 
- Datenabstraktion wenn es um die Implementierung und oder deren Außenansicht geht

##### 2.2.1 Datensätze
Ist die einfachste Datenstruktur.  Besteht aus einer vorgegebenen Menge zusammengehöriger Variablen, auf die lesend und bei Bedarf schreibend zugegriffen wird.

![[Pasted image 20261002130529.png]]

Noch wichtiger ist, dass andere Datenstrukturen, Datensätze enthalten und Methoden Datensätze als Ergebnisse zurückgeben können.

![[Pasted image 20261002130722.png]]

Um so viel Programmänderung zu vermeiden, werden sog. *anwendungsspezifische* Operationen verwendet.

![[Pasted image 20261002131022.png]]

##### 2.2.2 Lineare Zugriffe
Auf die linearen Datenstrukturen *Queue* und *Stack* können nur linear auf die Daten zugegriffen werden. Das heißt, mann nicht wie bei einem Array beliebige Einträge einlesen und verändern. 
Einerseits schränkt diese Eigenschaft den *usecase* und anderersetits kann man ohne komplexer Indexberechnung nicht weiter vorankommen und brauchen somit beim Anlegen keine Größe anzugeben.

*Queue*
Kann man sich als Perlenschnurvorstellen, am Ende auf die Schnur kommen die Perlen (Daten) und am anderen Ende wird eine Perle entfernt -> FIFO. Also die erste eingefähdelte Perle wird wieder runtergenommen.

*Stack*
Kann man sich als ein Stapel von Tellern (Daten) vorstellen, jede neuer Teller wird ganz oben abgelegt und der benötigte Teller wieder von ganz oben genommen -> LIFO

![[Pasted image 20261002133434.png]]


![[Pasted image 20261002133520.png]]


*Wrapper* sind Methoden in einer Klasse die andere Klassen implementieren!

Die Verallgemeinerung von Queue und Stack, ist eine DEQueue (Double Ended Queue)
![[Pasted image 20261002134824.png]]

Beim Einfügen und Entfernen an unterschiedlichen Enden ergibt sich das Verhalten einer Queue, bei gleichen Enden das eines Stacks. Man kann es auch mischen, man kann die Daten an einem anderen Ende hinzufügen  oder entfernen.


