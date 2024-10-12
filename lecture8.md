# Hashing II
## Weakness of hashing
For any choice of hash function, exist bad set of keys that all hash to same slot.

Idea: choose a hash function at random, independently from keys.
## Universal hashing
Def: Let U be a universe of keys, and H be a finite collection of hash functions, mapping U to {0,1,...,m-1} slots. H is universal if **all x,y** in U where x!=y such that #{h in H: h(x)=h(y)} = #H/m.

I.e.: If we choose a hash function randomly from H, then the posibilty that collision occurs is 1/m.
