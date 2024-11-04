# Divide and Conquer
1. Divide: divide into subproblems
2. Conquer: conquer subproblems recursively
3. Combine: combine solutions

## Binary search
- Search x in a sorted array
1. Divide: compare x with middle element
2. Conquer: recurse in one subarray
3. Combine: nothing

### Binary search with prediction
If we could not figure out the length of the array we would like to search. Then we need to have a predictor.

The predictor returns the best guess for the start position h. And then we probe h+2, h+4, until we find a range whose length is known and the key is in it, then use simple binary search.

## Powering a number
- given number x, integer n>=0, compute x^n
1. divide on n
2. if n is even, compute x^n/2, and multiply for one time in Θ(1) time
3. if n is odd, compute x^(n-1)/2, and multiply for two times in Θ(1) time
4. So, T(n) = T(n/2) + Θ(1)

## Fibonacci numbers
### recursive algorithm
T(n)=φ^n φ=1+3^0.5/2
### bottom-up algorithm
- compute F0,F1,...,Fn
- because Fn-1 include Fn-2's calculation
- T(n)=Θ(n)
### naive recursive squring algorithm
- Fn=φ^n/5^0.5 rounded to the nearest integer
- recursive squring **Θ(logn)** time
- but in a real machine, float number calculation may lose some bit. Therefore, the rounded step may make mistake.
### recursive squring algorithm
**Thm: (Fn+1,Fn;Fn,Fn-1)=(1,1;1,0)^n 2*2matrix**
- T(n)=Θ(logn)
- Proof: Induction on n
1. Base: n=1, (1,1;1,0) is right
2. Step: suppose n (Fn+1,Fn;Fn,Fn-1), then n+1 (Fn+2,Fn+1;Fn+1,Fn)=(Fn+1,Fn;Fn,Fn-1)*(1,1;1,0)

## Matrix Multiplication
### Standard alog
n^2 elements, each needs n multiplications **T(n)=Θ(n^3)**
### Divide and conquer alog
- Idea: block the matrix to 2*2 blocked matrix
- C[r,s;i,u]=A[a,b;c,d]*B[e,f;g,h]
- r=a*e+b*g etc.
  - 8 times n/2\*n/2 matrix multiplication and 4 times n/2\*n/2 matrix addition
  - **T(n)=8T(n/2)+Θ(n^2) T(n)=n^3**
### Strassen's alog
- Idea: reduce # multiplications
1. Divide A,B into 4 matrix each and compute products for P (use simple add and minus) Θ(n^2)
2. Conquer: compute 7 multiplications to produce P
3. Combine: use addition to produce C Θ(n^2)
- 7 times n/2\*n/2 matrix multiplication and 4 times n/2\*n/2 matrix addition
- **T(n)=7T(n/2)+Θ(n^2) T(n)=n^log2 7**

## Polynomial multiplication
use divide and conquer
### simple way
```
A(x) = P(x) + x^(n/2) * Q(x)
B(x) = R(x) + x^(n/2) * S(x)
C(x) = P(x)·R(x) + xn/2(P(x)·S(x) + R(x)·Q(x)) + xnQ(x)·S(x)
```

T(n)=4T(n/2)+Θ(n).  Therefore, T(n) = Θ(n2)
### clever way
Similar to matrix calculation, let m1 = (P+Q)*(R+S), m2 = PR, m3 = QS, then PS+RQ = m1-m2-m3

T(n)=3T(n/2)+Θ(n).  Therefore, T(n) = Θ(n ^ log2 3)

## VLSI layout(Very large-scale integration)
- Problem: circut is a complete binary tree on **n leaves** in a grid with minimum area
### Naive embedding
- Use tree-like design like -*-
- H(n)=H(n/2)+Θ(1)=Θ(logn)
- W(n)=2W(n/2)+O(1)=Θ(n)
- Area=Θ(nlogn)
```
  ---*---
--*-- --*--
*   * *   *
```
### H embedding
- Goal: W(n)=Θ(root n) H(n)=Θ(root n) Area=Θ(n)
- Assumption: if b=4,a=2,f(n) is polynomial smaller than root n, then we get it. That is, T(n)=2T(n/4)+Θ(n^0.5-δ)
- L(n)=2L(n/4)+Θ(1)=Θ(root n)
```
* * * *
*** ***
* * * *
 * * *
* * * *
*** ***
* * * *
Basic element:
* *
***
* *
```
