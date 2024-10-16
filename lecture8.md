# Hashing II
## Weakness of hashing
For any choice of hash function, exist bad set of keys that all hash to same slot.

Idea: choose a hash function at random, independently from keys. And then in the real world, your competitor could not pick up a bad set of keys to defeat our hashing algo because the hash function we choose is unknown.
## Universal hashing
Def: Let U be a universe of keys, and H be a finite collection of hash functions, mapping U to {0,1,...,m-1} slots. H is universal if **all x,y** in U where x!=y such that #{h in H: h(x)=h(y)} = #H/m.

I.e.: If we choose a hash function randomly from H, then the posibilty that collision occurs is 1/m.

Therom: Choose h randomly from H, suppose hashing n keys into m slots in table T. Then, for a given key x, E[#collisions with x] < n/m(load factor of T).
- **This means that if we find a set of universal hash fuction, then it could distribute keys evenly which is our expectation.**
- Proof: Let C_x be random variable denoting total #collisions of keys in T with x, and let c_xy = 1 if h(x)=h(y) and 0 otherwise.
  - Note that E[c_xy]=1/m(because of the definition of universal hashing) and C_x=Σc_xy
  - E[C_x] = E[Σc_xy] = ΣE[c_xy](linearity of expectation) = (n-1)/m

### Construct a universal hash function
Let m be prime. Decompose key k into r+1 digits: k=<k0,k1,...,kr> where 0<=ki<=m-1.

Pick a random number a=<a0,...,ar>, each ai is chosen randomly from {0,...,m-1}.

Define h_a(k)=(Σai*ki)mod m

How big is H={h_a}? m^(r+1)

**Therom: H is universal.**

Proof: Let x=<x0,...,xr> y=<y0,...,yr> be distinct keys. They differ at least one digit, without loss of generality(wlog), position 0. For how many h_a in H do x and y collide?

Must h_a(x)=h_a(y), that is (Σai\*xi) = (Σai\*yi) (mod m), that is Σai*(xi-yi)=0 (mod m).

a0*(x0-y0)+Σai*(xi-yi)=0 (mod m)

> Number theory Fact:
>
> Let m be prime. For any z in Zm(integer mod m), $z!=0, there exists unique z^-1 in Zm, $ z*z^-1=1 (mod m).

Since x0!=y0, there exists (x0-y0)^-1 such that a0=-(Σai*(xi-yi))*(x0-y0)^-1 (mod m). This means that if two distinct elems are hashed into same slot, that means for any choice of a1...ar, exactly 1 of m choice for a0 causes x and y collide, and no collision for m-1 choices for a0.

#ha that cause x,y to collide=m^r*1=m^r=#H/m

## Perfect hashing
Problems: Given n keys, construct a static hash table of size m=O(n) $ search takes **O(1)** time in the worst case.

Application: You want to store something that you know before in small space and want to search it fast.

Idea: Two level scheme with universal hashing at both levels. Use hash to replace the original chaining method. No collision at level 2.

Structure: the elem at level 1 consists of the random number a(universal hash) and a pointer to level 2 hash table.

Procedure: use hash1 function to select slot at level 1, and then use ha to find slot at level 2.

If n_i items that hash to level-1 slot i, then use mi=n_i^2 slots in level-2 table S_i.

Level-2 Analysis:

### Theorem: Hash n keys into m=n^2 slots, using a random hash function in a universal H. Then E[#collisions]<1/2.

Proof: Prob of 2 given keys collide under h is 1/m = 1/n^2.

#pairs of keys=n choose 2=n(n-1)/2

E[#collisions]=1/2-1/n<1/2

### Markov inequality: For random variable X>=0, Pr{X>=t}<=E[X]/t.
Relate expectation with probability.

Proof: E[X]=Σx\*Pr[X=x]>=Σx\*Pr[X=x] from t to infinite>=Σt\*Pr[X=x] from t to infinite=t\*ΣPr[X=x] from t to infinite=t\*Pr[X>=t]

### Corollary: Pr{no collision} >= 1/2.

Proof: Pr{>=1 collision} <= E[#collisions]/1(*Markov*) < 1/2 (*Therom above*)

To find a good level-2 hash funcction, we just test a few at random. Find one quickly, since >=1/2 works.
### Analysis of storage
For level-1, choose m=n slots, that is O(n). Let n_i be r.v. for #keys that hash to slot i in T. Use m_i=n_i^2 slots in each level-2 table Si.

E[total storage]=n+E[Σm_i]=n+E[ΣO(n_i^2)]=Θ(n) by bucket-sort analysis
