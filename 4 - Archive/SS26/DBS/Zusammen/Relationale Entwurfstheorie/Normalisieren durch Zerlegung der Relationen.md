#DBS 
Anmerkung, da es hier nicht wirklich so viel zum Zusammenfassen gibt,
hier nur die Foliensätze dazu 

## Allgemein
Eine gute Zerlegung muss genau 2 Kriterien erfüllen
1. Verlustlos sein
2. Abhängigkeitsbewahrung
## <font color="#92cddc">Verlustlose Zerlegung</font>
### <font color="#9bbb59">Definitionen</font>
![[Pasted image 20260323213325.png]]
![[Pasted image 20260323213348.png]]
![[Pasted image 20260323213358.png]]

### Beispiel
![[Pasted image 20260329141223.png]]
![[Pasted image 20260329141054.png]]

Das obere Beispiel ist keine verlustlose Zerlegung, denn die Beziehung 
zwischen guest, pub und beer ging verloren

#### <font color="#953734">Anmerkungen</font>
- Infomationsverlust kann vorkommen
- Merke:
	- "Die Verletzung der Verlustlosigkeit kann manchmal auch bedeuten, dass bei der Wiederherstellung zusaetzliche Tupel entstehen."
	
## <font color="#ffc000">Abhängigkeitsbewahrung</font>
Ist das zweite Kriterium für eine gute Zerlegung
![[Pasted image 20260323220011.png]]
![[Pasted image 20260323220033.png]]


### Beispiel

Da es sehr unnötig abstrakt gehalten ist

--- 

zip:{[street,city,region,zip]}

FDs:
- {zip} $\to$  {city, region}
- {street,city,region } $\to$ {zip}

Zerlegung: 
- streets: {[zip,street]}
- cities: {[zip,city,region]}

Frage: Ist diese Zerlegung verlustlos? Bewahrt sie die Abhängigkeiten? 


|           | zipCatalog  |              |       |
| --------- | ----------- | ------------ | ----- |
| city      | region      | street       | zip   |
| Frankfurt | Hesse       | Goethestraße | 60313 |
| Frankfurt | Hesse       | Goethestraße | 60437 |
| Frankfurt | Brandenburg | Goethestraße | 15234 |

Wenn wir dann projezieren: $\pi_{zip, stret}$

|       | streets      |     |
| ----- | ------------ | --- |
| zip   | street       |     |
| 15234 | Goethestraße |     |
| 60313 | Goethestraße |     |
| 60437 | Goethestraße |     |

Dann auch: $\pi_{city,region,zip}$

| cities    |             |       |
| --------- | ----------- | ----- |
| city      | region      | zip   |
| Frankfurt | Hesse       | 60313 |
| Frankfurt | Hesse       | 60437 |
| Frankfurt | Brandenburg | 15234 |

---

- Diese Zerlegung ist verlustlos weil {zip}$\to${city,region} 
- Zerlegung bewahrt die Abhängigkeit <mark style="background:#ff4d4f">nicht</mark>
	- {street,city,region } $\to$ {zip} kann nicht über die über die Zerlegung überprüft werden und ist somit nicht garantiert 


#### Links
[[Normalisierung durch Zerlegung Beispiele]]







