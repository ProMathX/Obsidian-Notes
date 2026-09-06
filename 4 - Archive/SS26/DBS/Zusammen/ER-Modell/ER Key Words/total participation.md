#DBS #studies 
Total particiapation (German: totale Partizipation)

### 1. Total Participation (Mandatory)

Total participation means that **every** entity in the entity set **must** be involved in at least one instance of the relationship. This is also known as **existence dependency** because the entity cannot exist in the database without being linked to the other side.

- **Visual Representation:** Usually shown as a **double line** connecting the entity to the relationship diamond.
    
- **Logical Constraint:** The minimum cardinality is **1**. In (min,max) notation, this is expressed as (1,n) or (1,1).
    
- **Example:** Consider the entities `Employee` and `Department` with the relationship `Works_In`.
    
    - If the business rule says "Every employee must be assigned to a department," then the participation of `Employee` in `Works_In` is **total**.

![[Pasted image 20260316213758.png]]
![[Pasted image 20260316214328.png]]