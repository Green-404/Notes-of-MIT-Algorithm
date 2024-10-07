# Divide and Conquer
1. Divide: divide into subproblems
2. Conquer: conquer subproblems recursively
3. Combine: combine solutions

## Binary search
- Search x in a sorted array
1. Divide: compare x with middle element
2. Conquer: recurse in one subarray
3. Combine: nothing

## Powering a number
- given number x, integer n>=0, compute x^n
1. divide on n
2. if n is even, compute x^n/2, and multiply for one time in Θ(1) time
3. if n is odd, compute x^(n-1)/2, and multiply for two times in Θ(1) time
4. So, T(n) = T(n/2) + Θ(1)

## Fibonacci numbers

