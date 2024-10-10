# Hashing I
Problems: Symbol-table Problem  
Operation: Insert, Delete, Search
## Direct access table
- Sup: keys are drawn from U={0,1,...,m-1}. Assume keys are distinct.
- T[k]=x if x.key=k
- If key is huge range or not integer, then it fails.
## Hashing
Hash function h maps keys "randomly" into **slots** of table T.  
**collision may occur**  
### resolving collisions by chaining
Idea: link records in the same slot into a list  
Analysis:
- Worst-case: All elements hash to same slots.
  - Search/Access: Θ(n) time
- Average-case: 
