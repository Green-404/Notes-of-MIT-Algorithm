# Quick Sort---Divide and Conquer
Sorts in place. Efficient in storage and practice.
1. Divide: **Partition** array into 2 subarrays around pivot x such that **elements in lower subarray<=x<=elements in upper subarray**.\
2. Conquer: recursively sort the 2 subarrays.
3. Combine: trivial
## Partition
Key: linear time partitioning subroutine.
```
Partition(A,p,q)
  x=A[q]//choose the last element as pivot
  i=p-1
  for j from p to q-1//use j as a pointer travelling through
    if A[j]<=x
      then i=i+1//use i as the barrier to partition subarrays
           exchange A[i] A[j]
  exchange A[i+1] A[q]//put x on the barrier
  return i+1
```
**Time=Θ(n)**
## Combine
```
QuickSort(A,p,q)
  if p<q
    then r=Partition(A,p,q)
    QuickSort(A,p,r-1)
    QuickSort(A,r+1,q)
```
## Analysis-assume all elems extinct
### Worst-case
T(n)=worst-case time *one side has no elem*  
T(n)=T(0)+T(n-1)+Θ(n)=T(n-1)+Θ(n)=Θ(n^2) *arith series*  
### Best-case
T(n)=best-case time *intuition only! Partition splits in the middle*  
T(n)=2T(n/2)+Θ(n)=Θ(nlogn)  
### Alternate
Suppose we alternate lucky, unlucky  
L(n)=2U(n/2)+Θ(n)
U(n)=L(n-1)+Θ(n)
Then, L(n)=2L(n/2-1)+Θ(n/2)+Θ(n)=Θ(nlogn)

# Randomized Quicksort
Running time is independent of input ordering.  
No assumption about input distribution.  
No specific input elicit w-c behavior.  
w-c determined only by random number generator.




