#DBS
#### Äquivalente FD-Mengen
FDs F und G sind äquivalent wenn deren Hüllen also $F^{+} = G^{+}$  gilt
Beide Mengen erlauben die gleiche Menge von FDs

*Achtung*
- $F^{+}$ kann riesig sein
- Viel redundante Abhängigkeiten 
- in der Praxis unübersichtlich 

Deshalb ist das Ziel eine minimal-Menge $F_{c}^{+} = F^{+}$ zu finden
*Achtung* mehrere minimal-Mengen.
#### Kanonische Überderdeckung
![[Pasted image 20260323211726.png]]
![[Pasted image 20260323212930.png]]
![[Pasted image 20260323212937.png]]

#### Algorithmus 
![[Pasted image 20260323213009.png]]





#### Beispiel

**R:={ABCDE}**


FDs={
	 **BD->AE  
	  D->E  
     ACDE->B  
     A->BD**
     }

##### Linksreduktion:
$(D)⁺ = \{E\}$ B bleibt
$(B)⁺ = \{\}$ D bleibt

D->E Atomar unverändert

$(C)⁺ = \{\}$ A bleibt
$(A)⁺ = \{\}$ C bleibt

A -> BD atomar

##### Rechtsreduktion
$(BDA)⁺=\{E,B,D\}$ E geht weg (weil D->E)

$(AC)⁺=\{B,D\}$ B geht weg

$(AD)⁺=\{E\}$ B bleibt
$(AD)⁺=\{\}$ D bleibt


##### Vereinigen
BD -> A
D -> E
~~AC -> $\emptyset$  ~~
A  -> BD

##### Final 
BD->A
D->E
A->BD


##### Schlüsselkandidat

N={ }
R={ }
L={ }
M={A,B,D,E}

Schlüsselkandidat $K = (N \cup L \cup M) \implies \{A,B,D,E\}$










