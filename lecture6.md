# Order statistics
Given n elements in array, find k th smallest element(element of rank k).  
## Naive algorithm: sort
## Randomized divide and conquer alog: RandomSelect
```
RandomSelect(A,p,q,i)://i th smallest in A[p,...,q]
  if p=q then return A[p]
  r=RandomPartition(A,p,q)  //linear time. After this, left subarray will <= A[r]
  k=r-p+1  //k=rank(A[r]) in A[p...q]
  if i=k  then return A[r]
  if i<k  then return RandomSelect(A,p,r-1,i)  //target is at left subarray i th
  else return RandomSelect(A,r+1,q,i-k)  //target is at right subarray i-k th
```
### Intuition of analysis
Assuse elements are extinct.  
Lucky case: T(n)=T(9/10n)+Θ(n)=Θ(n)  (master method)  
Unlucky case: T(n)=T(n-1)+Θ(n)=Θ(n^2)  (arith series)  
### Analysis of expected time
- Let T(n) be the random variable for running time of RandomizedSelect on input of size n. Generating random number is independent with each other.
- Define indicator random variable Xk for k=0,...,n-1, Xk=1 if Partition generate k:n-1-k splits, else 0.
- T(n)=Σ Xk * [T(max{k,n-1-k}) + Θ(n)]
E[T(n)]=E[Σ Xk * [T(max{k,n-1-k}) + Θ(n)]]  
       =Σ E[Xk] * E[T(max{k,n-1-k}) + Θ(n)](*linear and independent property: the first random number is independent with the following steps' random numbers which decide the time of T(max)*)  
       =Σ 1/n * E[T(max{k,n-1-k}) + Θ(n)]  
       =Σ 1/n * E[T(max{k,n-1-k})] + Σ 1/n * Θ(n)  
       <=2/n * Σ E[T(k)](*k from n/2 rounded to lower integer to n-1*) + Θ(n)  
- Claim: E[T(n)]<=cn for sufficient large constant c>0
- Proof: Substitution
  - Assume true for k<n
  - E[T(n)]<=2/n\*Σ E[T(k)] + Θ(n) <= 2/n\*Σ ck + Θ(n) <= 3c/4*n + Θ(n) = cn-(cn/4 - Θ(n)) <= cn if cn/4 - Θ(n)>0, that is for c sufficient large.
- **Time: expected time Θ(n); worst-case Θ(n^2)**
## Worst-case linear time order statistics
Idea: generate good pivot --- recurse
```
Select(i,n)  //i th in n elems. The purpose is to select a good pivot.
1. Divide n elems into n/5 rounded lower groups with 5 elems each. Find the median in each group.  //Θ(n)
2. Recursively Select the median x of the n/5 group medians.    //T(n/5)
3. Partition with x as pivot. Let k=rank(x)      //Θ(n)
4. If i=k, then return x.                                        //same with random select
   If i<k, then recursively select i th in the lower part.
   If i>k, then recursively select i-k th in the higher part.
```
> Here, **half** of the **n/5 rounded lower** groups' **3 elements** are less than or equal to the pivot.  
> Therefore, we have a partition with left side at least 3 times n/10 rounded lower.  
> Simplification: For n>=50,  3 times n/10 rounded lower >= n/4.  
> And, the worst case is that n/4 : 3n/4. That is T(n)=Θ(n)(*Divide and find medians*) + T(n/5)(*recursively find the median x*) + Θ(n)(*partition with pivot x*) +　T(3n/4)(*the biggest part of the partition*) = **Θ(n)(*using substitution*)**
Qusetion: Why 5 elems per group? Because 5 is the minimum number with what the algo could success.
- If 3 each group, divide and find medians Θ(n), recurse T(n/3), partition Θ(n), search in bigger(worst-case) part T(n- n/3 /2 *2)=T(2n/3), which could not run in lenear time.
