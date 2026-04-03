#DBS 
Die Division $\div$

Achtung die Division wird gerne abgefragt, ein Keyword dafür (oft) ist, dass man eine Allbedingung mit Exceptions hat.

![[Pasted image 20260309184427.png]]

Da die Division eine abgeleitete Operation ist, definieren wir sie mit Hilfe der anderen Operationen der Relationenalgebra. Seien R,S Relationen und β die zu R sowie γ die zu S dazugehörigen Attributmengen mit γ⊊β. Sei R′:=β∖γ.

Die Division ist dann definiert durch:

R÷S:=πR′​(R)−πR′​((πR′​(R)×S)−R)

*Anschaulich gesprochen enthält R÷S also diejenigen Attribute aus R′, welche in jeder Kombination mit den Attributen aus S in R vorkommen.*
