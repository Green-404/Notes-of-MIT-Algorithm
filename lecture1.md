# Analysis of Algorithms
  The theoretical study of computer-program performance and resource usage.
  - What is more important than performance?
    - security user-friendly correctness etc.
  - Why study algs and perf?
    - sometimes perf decides whether feasible
    - theoretical communicate language
    - spend perf to realize other things you want
# Problem: sorting
## Insertion sort
  - **Idea: increase the sorted part one by one**
  - `The main idea is to keep the front subarray sorted, find the other's position and insert`
  ```
  Insertion-Sort(A,n)//sort A[1...n]
    for j from 2 to n
      do key = A[j]
      i = j-1
      while i>0 and A[i]>key
        do A[i+1] = A[i]
        i--
    A[i+1] = key
  ```
  - Running time
    - Depends on input and input size
    - Upper bound
  - Worst-case running time: input is reverse sorted
    - **Σ Θ(j) = Θ(j^2)**
## Merge sort
  - Idea: **Recursive program**
  - `The main idea is to decrease the problem's scale by using divide and conquer`
  ```
  Merge-Sort(A,1,n)
  1. If n = 1, done
  2. Recursively Merge-Sort(A,1,n/2) and Merge-Sort(A,n/2+1,n)
  3. Merge 2 sorted lists

  Key subroutine - Merge
  2 pointer on the head to select the smaller one
  ```
  - Running time
    - T(n)=Θ(1)+2T(n/2)+Θ(n)=2T(n/2)+Θ(n)
    - **T(n)=Θ(nlogn)**

# Kinds of analysis
## Worst-case(usually)
  - T(n)=max time on any input of size n
  - Depends on computers
      - relative speed(on same machine)
      - absolute speed(on diff machine)
## Average-case(sometimes)
  T(n)=**expected time** over all inputs of size n(need an assumption of statistic distribution)
## Best-case(bogus)
  cheat
# BIG IDEA: Asymptotic analysis
- Ignore machine dependent
- Focus on the growth. n is infinite
## Asymptotic notation
- Θ-notation
  - drop low-order terms and ignore leading constants
  - `provide both upper and lower bound`

# Recurrence
## Recursion tree
> this is the task of next class~~



  

