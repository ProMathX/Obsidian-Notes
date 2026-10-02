Beginnend bei Kapitel 2 "Datenabstraktion"

Disclaimer: 
Puntigamers "Abstraktion" heißt nichts anderes als, ich verschachtele und und erzeuge schnittstellen zu meiner Klasse. Falls möglich implementiere ich Datenstrukturen. 


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

Klassenvariablen sind mit `static` deklariert, eine Klassenvariable existiert nur einmal pro Klasse, nicht in jedem Objekt


