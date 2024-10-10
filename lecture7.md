# Hashing I
Problems: Symbol-table Problem  
Operation: Insert, Delete, Search
# Direct access table
- Sup: keys are drawn from U={0,1,...,m-1}. Assume keys are distinct.
- T[k]=x if x.key=k
- If key is huge range or not integer, then it fails.
# Hashing
Hash function h maps keys "randomly" into **slots** of table T.  
**collision may occur**  
# resolving collisions by chaining
Idea: link records in the same slot into a list  
Analysis:
- Worst-case: All elements hash to same slots.
  - Search/Access: Θ(n) time
- Average-case: assumption of **simple uniform hashing**: each key k is **equally likely** to be hashed to any slot in T, **independent** of where other keys are hashed.
  - Define: **load factor** of hash table with n keys and m slots is to **α=n/m=#keys per slot**
  - Expected unsuccessful search time: Θ(1+α) (calculate hash and search time). If α is Θ(1) (that is **n=Θ(m)**), then expected-search time is Θ(n).
## Choosing a hash function
- should distribute keys uniformly into slots
- regularity in key distribution should not affect uniformity
### Division method  
h(k)=k mod m
- Don't pick m with small divisor d
- Pick m = prime not too close to power of 2 or 10.
- Example:
  - if d=2, then all even keys will be distributed into even number's slots. That means odd slots are wasted.
  - if m = 2^r, then hash doesn't depend on all bits of k. In fact, we just use lower r bits.
### Multiplication method
m=2^r, computer has w-bit words  
h(k)=(A*k mod 2^w) rsh (w-r) *(A is an odd integer 2^(w-1)<A<2^w)*
- don't pick A too close to power of 2
- fast method: multiply mod rsh faster than division
- Example:m=2^3, w=7, A=1011001, k=1101011
## resolving collisions by open addressing
No storage for links.  
Idea: probe the table systematically until an empty slot is found  
h: U*{0,1,...,m-1}*(number of probe)*->{0,1,...,m-1}*(slot position)*  
Table may fill up, so n need to less than m.  
- Example: Insert k=496. Probe h(496,0) h(496,1) until find an empty slot. Search will use the same probe sequence.
## Probing Strategy
### Linear: h(k,i)=(h(k,0)+i) mod m  
- suffer from "primary clustering", almost all gather in an area, it takes long time to fill slots.
### Double hashing:h(k,i)=(h1(k)+i*h2(k)) mod m
- excellent method
- usually pick m=2^r and h2(k) odd  
- **Analysis**:    
- Assumption of uniform hashing: Each key equally likely to have any one of the m! permutations as its probe sequence, independent of other keys.    
- Theorem: **E[#probes]<=1/(1-α) if α<1**  
- Proof: unsuccessful search(*could use indicator random variable to be more precise*)
  - 1 probe is neccessory
  - Pr[first probe collision]=n/m
  - Pr[second probe collision|first probe collision]=n-1/m-1
  - E[#probes]=1+n/m(1+n-1/m-1(1+...))<=1+α(1+α(1+...))<=1+α+α^2+...=1/(1-α)
