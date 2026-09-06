---
topic:
date: 2026-03-16
course:
tags:
  - studies
  - "#DBS"
---
## Key Concepts
- ) Entities can also be called substantives, and relation can be substituted via verbs, to make it more readable etc
- ) Every Entitytype -> Relation **See important details**
- ) Relations can also have a primary key
- ) If the primary keys are identical you can merge them together
- ) You can expand the relation via [[total participation]]
- ) if you don't want everything in one relation use [[partial participation]]
- ) unknown key (Fremdschlüssel) is an attribute of a relation, that relates to the primary to a different relation 
- ) Notation of merged keys $\{{R.A_{1}, R.A_{2}} \to {S.B_{1}, S.B_{2}}\}$
- ) Weak Entitytype to Strong Entitytype is a [N:1] relation
- ) Modeling and generalizing 
	- Parts of a specific entity are mapped to (many) other relations, duplicating the key
##### Key hierarchy
- Super-Key (Superschluessel) all Atributes together
- Key-candidate is a minimal key, if one key removed it breaks a subset of super-keys
- Primary-Key can be defined by person who setup the DBMS
--- 

## Important Details
![[Pasted image 20260316142510.png]]
![[Pasted image 20260316143556.png]]
![[Pasted image 20260316145217.png]]

## Examples
See images above, in important details

## Questions + TODO
- [x] Revisit the PP 
- [x] Expand the summaries
- [x] Expand the ER Key Words 
## Summary
![[Pasted image 20260316144202.png]]
![[Pasted image 20260316153156.png]]
## Related Topics
- [[DBS ER Modelle v1]]
## Notation
Da ich bei den Übungsaufgaben mir da schwer getan habe, hier nochmals eine Zusammenfassung der Notationen und wann sie einzusetzen sind. 

Es gibt Stelligkeit bzw. Grad 
- Anzahl der beteiligten Entitytype,
- Binär (oft)
- Weniger häufig: ternär
##### Bezüglich Kardinalität/ Funktionalität/ Participation Constrains
- Anzahl der Entitys die an einer Beziehung teilnehem
- Funktionalität ([[Chen Notation]]): 1:1 1:N, N:M 
- [[Participation Constraints]]: partiell oder total
- [[Kardinalität]] ([min,max]-Notation)