# Asymptotic notation
## O-notation
f(n)=O(g(n)) means there are consts c>0 and n0>0 such that **0≤f(n)≤cg(n)** for all n>n0
- set definition: O(g(n))={f(n): there are consts c>0 and n0>0 such that 0≤f(n)≤cg(n) for all n>n0}
## Macro convention
- A set in a formula represents an anonymous function in that set
- Ex: f(n)=n^3+O(n^2)//means that f(n) is n^3 plus something in O(n^2)
- Ex: n^2+O(n)=O(n^2)//for any f(n) in O(n), there is h(n) in O(n^2), h(n)=n^2+f(n)
## Ω-notation
f(n)=Ω(g(n)) means there are consts c>0 and n0>0 such that **0≤cg(n)≤f(n)** for all n>n0
## Θ-notation
f(n)=Θ(g(n)) means there are consts c1,c2>0 and n0>0 such that **c1g(n)≤f(n)≤c2g(n)** for all n>n0
-**Θ(g(n))=O(g(n))∩ Ω(g(n))**
## o-notation(<) and ω-notation(>)
hold for **all c and exist n0**
- n = Θ(n) but n ≠ o(n)

# Solving Recurrences
## Substitution method

`The main idea is to guess the format and then use induction to prove its correctness.`

1. Guess the form of the solution
2. Verify by induction
3. solve the constants
Ex: T(n)=4T(n/2)+n
- Guess: T(n)=O(n^3)
- Assume: T(k)≤ck^3 for k<n **//we need to make sure that the constant does not change, therefore, we use c**
- T(n)=cn^3/2+n=cn^3-(cn^3/2-n) **≤cn^3** if cn^3/2-n≥0 e.g. c>T(1)(**base case**),n>1
- Tighter bound
  - Guess: T(n)=O(n^2)
  - Assume: T(k)≤ck^2 for k<n
  - T(n)=cn^2+n **//fail to use substitution method**
  - Assume: T(k)≤c1k^2-c2k for k<n
  - T(n)=c1n^2-2c2n+n=c1n^2-c2n-(c2n-n)≤c1n^2-c2n if c2n-n≥0 e.g. c2>1, c1-c2>=T(1)(**base case**)
 
## Recursion-tree method

`Use every node as the current cost and sum up all of them. The most important is to figure the cost on every floor and how high the tree is.`

Ex: T(n)=T(n/4)+T(n/2)+n^2
- compute it level by level and the number of level is bounded
It's recommanded that we use tree to guess and then use substution to check and prove.

## Master method

`Use a formular to figure out the answer of T(n)=aT(n/b)+f(n) form.`

applies to recurrences of the form **T(n)=aT(n/b)+f(n)**, where a≥1, b>1, f(n) is asymptotically positive(f(n)>0 for n>n0)
### compare f(n) with n^logb a
1. f(n)=**O**(n^logb a-δ) for some δ>0, then **T(n)=Θ(n^logb a)**
2. f(n)=O(n^logb a * (lgn)^k) for some `k>=0`, then **T(n)=Θ(n^logb a * (lgn)^k+1)**
3. f(n)=**Ω**(n^logb a+δ) for some δ>0 **and af(n/b)<=(1-δ')f(n) for some δ'>0** to `ensure that next level is less than the prior level`， then **T(n)=Θ(f(n))**
- Ex:T(n)=4T(n/2)+n^2 case2
- Ex:T(n)=4T(n/2)+n^2/lgn (master method does not apply) n^2lglgn

`You need to pay attention that the third case is for k>=0, for negative k, we need to use other way to calculate.` 

Example:

For T(n) = 3T(n/3) + n/lgn, we have k = -1, couldn't use master therom.

The solution is to use substitution. Let n=3^k, then we have T(k) = 3T(k-1) + 3^k/klg3.

Expand it, we have T(k) = 3^k/lg3 * Σ(1/i) i from k to 1

Σ(1/i) i from k to 1 could be appropAsymptotic notation
## O-notation
f(n)=O(g(n)) means there are consts c>0 and n0>0 such that **0≤f(n)≤cg(n)** for all n>n0
- set definition: O(g(n))={f(n): there are consts c>0 and n0>0 such that 0≤f(n)≤cg(n) for all n>n0}
## Macro convention
- A set in a formula represents an anonymous function in that set
- Ex: f(n)=n^3+O(n^2)//means that f(n) is n^3 plus something in O(n^2)
- Ex: n^2+O(n)=O(n^2)//for any f(n) in O(n), there is h(n) in O(n^2), h(n)=n^2+f(n)
## Ω-notation
f(n)=Ω(g(n)) means there are consts c>0 and n0>0 such that **0≤cg(n)≤f(n)** for all n>n0
## Θ-notation
f(n)=Θ(g(n)) means there are consts c1,c2>0 and n0>0 such that **c1g(n)≤f(n)≤c2g(n)** for all n>n0
-**Θ(g(n))=O(g(n))∩ Ω(g(n))**
## o-notation(<) and ω-notation(>)
hold for **all c and exist n0**
- n = Θ(n) but n ≠ o(n)

# Solving Recurrences
## Substitution method

`The main idea is to guess the format and then use induction to prove its correctness.`

1. Guess the form of the solution
2. Verify by induction
3. solve the constants
Ex: T(n)=4T(n/2)+n
- Guess: T(n)=O(n^3)
- Assume: T(k)≤ck^3 for k<n **//we need to make sure that the constant does not change, therefore, we use c**
- T(n)=cn^3/2+n=cn^3-(cn^3/2-n) **≤cn^3** if cn^3/2-n≥0 e.g. c>T(1)(**base case**),n>1
- Tighter bound
  - Guess: T(n)=O(n^2)
  - Assume: T(k)≤ck^2 for k<n
  - T(n)=cn^2+n **//fail to use substitution method**
  - Assume: T(k)≤c1k^2-c2k for k<n
  - T(n)=c1n^2-2c2n+n=c1n^2-c2n-(c2n-n)≤c1n^2-c2n if c2n-n≥0 e.g. c2>1, c1-c2>=T(1)(**base case**)
 
## Recursion-tree method

`Use every node as the current cost and sum up all of them. The most important is to figure the cost on every floor and how high the tree is.`

Ex: T(n)=T(n/4)+T(n/2)+n^2
- compute it level by level and the number of level is bounded
`It's recommanded that we use tree to guess and then use substution to check and prove.`

## Master method

`Use a formular to figure out the answer of T(n)=aT(n/b)+f(n) form.`

applies to recurrences of the form **T(n)=aT(n/b)+f(n)**, where a≥1, b>1, f(n) is asymptotically positive(f(n)>0 for n>n0)
### compare f(n) with n^logb a
1. f(n)=**O**(n^logb a-δ) for some δ>0, then **T(n)=Θ(n^logb a)**
2. f(n)=O(n^logb a * (lgn)^k) for some `k>=0`, then **T(n)=Θ(n^logb a * (lgn)^k+1)**
3. f(n)=**Ω**(n^logb a+δ) for some δ>0 **and af(n/b)<=(1-δ')f(n) for some δ'>0** to `ensure that next level is less than the prior level`， then **T(n)=Θ(f(n))**
- Ex:T(n)=4T(n/2)+n^2 case2
- Ex:T(n)=4T(n/2)+n^2/lgn (master method does not apply) n^2lglgn
## Special case
`You need to pay attention that the third case is for k>=0, for negative k, we need to use other way to calculate.` 

### Example1

For T(n) = 3T(n/3) + n/lgn, we have k = -1, couldn't use master therom.

The solution is to use substitution. Let n=3^k, then we have T(k) = 3T(k-1) + 3^k/klg3.

Expand it, we have T(k) = 3^k/lg3 * Σ(1/i) i from k to 1

Σ(1/i) i from k to 1 could be approximated into the integration of 1/i, that is logk.

Then, T(k) = 3^k/lg3 * Σ(1/i) i from k to 1 = 3^k/lg3 * logk = Θ(nloglogn)

### Example2
T(n) = 3T(n/3 - 2) + n/2

The minus constant don't affect, it is just equal to T(n) = 3T(n/3) + n/2

`In lots of cases, we use integration to substitute Σ`



### proof sketch



