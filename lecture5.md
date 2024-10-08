# How fast can we sort?
- Depend on the model of what you can do with elements. e.g. quicksort, heapsort, merge sort, insertion sort.
- Can we do better than Θ(nlogn)?
# Comparison sorting(model)
Only use comparisions to determine real order of elements.
## Decision-tree model
![DecisionTreeExample](https://github.com/Green-404/Notes-of-MIT-Algorithm/blob/main/decisiontree.png)
In general,<a1,a2,...,an>
- each internal node has label i:j, means compare ai and aj.
- left subtree gives subsequent comparisons if ai <= aj
- each leaf node gives a permutation
## Decision trees model comparison sort
- one tree for each n. *For randomize algorithm, not only one tree.*
- view algorithm as a way to split the subtree whenever it make a comparison
- finally, the tree lists comparisons along all possible instruction traces
- running time = length of the comparison path
- worst-case running time = height of the tree
**All the sorting algorithm can be transformed to the decision tree.**
### Lower bound on decision tree sorting
**Any decision tree sorting n elements, its height is Ω(nlogn).**
Proof: Number of leaves at least n!
1. height h has at most 2^h leaves, then **n!<=2^h**
2. Then, h>=logn!>=log(n/e)^n=nlogn-nloge.  *Stiring formula:n!>=log(n/e)^n*
3. Then, h=Ω(nlogn)
**Among comparison model, mergesort, heapsort and randomized quicksort are asymptotically optimal.**

# Sorting in linear time
## Counting Sort
Assume each 1=<ai<=k and ai is integer  
Aux storage space C[1...k]
```
Counting Sort:
for i from 1 to k
  C[i]=0            //initialization
for j from 1 to n
  C[A[j]]+=1        //C[key]={#key}
for i from 2 to k
  C[i]+=C[i-1]      //C[key]={#less than or equal to key}:the position the elements should go. 
for j from n down to 1
  B[C[A[j]]]=A[j]   //distribution:A[j] is at the C[A[j]] position
  C[A[j]]-=1
```
**T(k,n)=O(k+n)**
## 
