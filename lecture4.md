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
T(n)=worst-case time   *one side has no elem*  
T(n)=T(0)+T(n-1)+Θ(n)=T(n-1)+Θ(n)=Θ(n^2)   *arith series*  
### Best-case
T(n)=best-case time   *intuition only! Partition splits in the middle*  
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
**Pivot on random element**   *choose and exchange with the last element and run quicksort*
## Analysis
### indicator random variable
x_k=1 if partition is k:n-k-1 and 0 otherwise (k=0,2,...,n-1)
E\[x_k\]=0/*Pr{x_k=0}+1/*Pr{x_k=1}=Pr{x_k=1}=1/n
T(n)=Σ x_k\*(T(k)+T(n-k)+Θ(n))   *If we choose x, then k has n choice, only one situation x_k is 1. Because x could only participate in one way.*  
E\[T(n)\]=ΣE\[x_k\*(T(k)+T(n-k)+Θ(n))\]     *linear probility of expection*  
         =ΣE\[x_k\]\*E\[(T(k)+T(n-k)+Θ(n))\]      *independent:x_k is independent with the partition time*  
         =1/nΣ*E\[(T(k)+T(n-k)+Θ(n))\]  
         =2/nΣE\[(T(k)\]+1/n\*ΣΘ(n)  
         =2/nΣE\[(T(k)\]+Θ(n)     *arithmetic series*  
- Prove E\[T(n)\]<=anlogn for constant a>0 (use substitution)  
1. For k=0,1, absorb E\[T(k)\] into Θ(n)    *To avoid 0,1 in anlogn*
2. Fact: Σklgk from 2 to n-1 <= 1/2 * n^2lgn - 1/8 * n^2     *integral method or use property of klogk to prove*
3. Substitution: E\[T(n)\] <= 2/n * Σaklgk from 2 to n-1 + Θ(n) <= 2a/n * (1/2 * n^2lgn - 1/8 * n^2) + Θ(n) =anlogn - (a/4 *n - Θ(n)) <= anlogn if (a/4 *n - Θ(n)) > 0    *if a is big enough, so that a/4 * n dominate*
- Good in virtual cache.
