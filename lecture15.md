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
`Main idea: Decrease the length to find in x and y`

Define c[i,j] = |LCS(x[1...i],y[1...j])|, then c[m,n]=|LCS(x,y)|

Therom: c[i,j] = c[i-1,j-1] + 1 if x[i]=y[j]

                 max{c[i,j-1],c[i-1,j]} otherwise

Proof:

1. Case1: x[i]=y[j]

Let z[1...k] = LCS(x[1...i],y[1...j]) where c[i,j] = k

Then z[k]=x[i]=y[j], or else z could be extended by tacking on x[i].

Then z[1...k-1] is at least a CS of x[1...i-1] and y[1...j-1]

**Claim: z[1...k-1] = LCS(x[1...i-1],y[1...j-1])**

Suppose w is a longer CS, that is |w|>k-1

**Cut and paste**: w || z[k] (concatenate) is a CS of x[1...i] and y[1...j], longer than k, Contradiction.

`Important method!!`

Then c[i-1,j-1] = k-1, which implies c[i,j] = c[i-1,j-1]+1

2. Case2:...

### Recursive alg for LCS
```
LCS(x,y,i,j)
  if x[i]=y[j]
    then c[i,j] <- LCS(x,y,i-1,j-1)+1
  else
    c[i,j] <- max{LCS(x,y,i-1,j)+LCS(x,y,i,j-1)}
  return c[i,j]
```

Worst case: x[i]!=x[j] for all i,j. Binary tree with and i+j height, then we work expotential time 2^(i+j), slow. Lots of repeated work.

### Memo-ization alg "not memorization"

```
LCS(x,y,i,j)
  if c[i,j] != nil
    return c[i,j]
  if x[i]=y[j]
    then c[i,j] <- LCS(x,y,i-1,j-1)+1
  else
    c[i,j] <- max{LCS(x,y,i-1,j)+LCS(x,y,i,j-1)}
  return c[i,j]
```
Time=O(mn)=const work per entry

Space=O(mn)

### DP alg
Idea: Compute the table `bottom-up`.

Reconstruct LCS by tracing backwards

Time=Θ(mn)

Space=O(min{m,n}) 1row and O(1)elem(just above 2 elements and 1 end number)

## DP hallmark!!!
### Optimal substructure

An optimal solution to a problem(instance) contains optimal solutions to subproblems

```
If z=LCS(x,y), then any prefix of z is an LCS of a prefix of x and a prefix of y.
```

### Overlapping subproblems

A recursive solution contains a "small" number of distinct subproblems repeated many times.

```
LCS subproblem space contains m*n distinct subproblems.
```
