Der Join(t) $\bowtie$
#DBS 

Ein Join (zu deutsch Verbund) bezeichnet die beiden hintereinander 
ausgeführten Operationen [kartesisches Produkt](https://de.wikipedia.org/wiki/Relationale_Algebra#Kartesisches_Produkt_\(Kreuzprodukt\)) und [Selektion](https://de.wikipedia.org/wiki/Relationale_Algebra#Selektion). 
Die Selektionsbedingung ist dabei üblicherweise ein Vergleich 
von Attributen A θ B $A \theta B$ , wobei $\theta$ ein passender 
Vergleichsoperator ist. Man bezeichnet den 
allgemeinen Verbund daher auch als $\theta$  (Theta-Verbund). Ein 
Spezialfall des 
allgemeinen Verbundes ist der [Equi-Join](https://de.wikipedia.org/wiki/Relationale_Algebra#Equi-Join) .
##### Definition
Fuer zwei Relationen $R(A_{1},A_{2},A_{3},\dots)$ $S(B_{1},B_{2},B_{3} \dots)$

Gilt: $S \bowtie_{Ausdruck} S := \{r \cup s | r \in R \wedge \in S \wedge A\}$

Was ja $S \bowtie_{Ausdruck} S := \sigma_{Ausdruck} \{R \times S\}$ was ja an sich der $R \bowtie_{\theta} S$ entspricht

![[Pasted image 20260309182933.png]]
Der Join ist kommutativ

### Ueberblick zu den Join Varianten
![[Pasted image 20260309183327.png]]

#### Left Outer Join![[Pasted image 20260309183411.png]]

![[Pasted image 20260309183513.png]]

#### Right Outer Join![[Pasted image 20260309183427.png]]

![[Pasted image 20260309183526.png]]
#### Full Outer Join![[Pasted image 20260309183437.png]]

![[Pasted image 20260309183541.png]]

### Semi Joins
![[Pasted image 20260309183704.png]]

#### Semi Join (Links)
![[Pasted image 20260309183732.png]]

#### Semi Join (Rechts)
![[Pasted image 20260309183754.png]]
