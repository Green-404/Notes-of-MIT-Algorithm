# Dynamic Programming
Design technique, like D&C

## Example: longest common subsequence LCS
Given 2 sequence x[1...m] and y[1...n], find **a** longest sequence to both.

### Brute-force algorithm
Check every subsequence of x to see if it is also a subseq of y.

**Analysis**

Time is O(n*2^m). 2^m subseq of x and scan y in n time.

Exponential time = slow!

### Simplification
1. Look at **length** of LCS(x,y), that is first compute the length
2. Extend the algo to find LCS itself, just record

Strategy: Consider prefixes of x and y

Define c[i,j] = |LCS(x[1...i],y[1...j])|, then c[m,n]=|LCS(x,y)|

Therom: c[i,j] = c[i-1,j-1] + 1 if x[i]=y[j]

                 max{c[i,j-1],c[i-1,j]} otherwise
