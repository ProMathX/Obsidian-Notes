#DBS 
### Steps of Database drafts
Requirement-analysis
		What do we want?
		Object descriptions
		Constraints and Types
	 *Illustration on a conceptual model*
		Which data and relations?
	Illustration on a concrete model
	Practical execution and Implementation
### Entities
Objects in the real world
	Only attributes of Entities are saved, not the entities themselves
	Entities are ordered in Entity-types

### Attributes
Attributes have Domains
	Saved attributes
	derived Attributes (birthday -> age)

### Keys
Usually an ID
	Super-keys are made up of a set of attributes of an entity-type -> E(A_1, A_2, ...)
	The values of the key-attributes identify a specific entity.
	Attributes of the primary key are underlined

### Relation
Relations describe connections between entities
	A relation between entity-types can be seen as a relation in a mathematical sense
	Entities can be relation to themselves, they can be self-reflecting (reflectivitiy)
	if you want to simplify or make your diagram more readable add a new relation to remove redundancy

	 functionality 1:1 1:N N:1 N:M
		 Chen-Notation can bee seen a partial functions (at least many of them, but all of them)

![[Pasted image 20260309151417.png]]

Kardinalitaet 
	min{}
	max{}
![[Pasted image 20260309152351.png]]

#### ISA 
![[Pasted image 20260312091231.png]]
![[Pasted image 20260312091312.png]]
![[Pasted image 20260312091939.png]]
