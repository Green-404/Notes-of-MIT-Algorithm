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


