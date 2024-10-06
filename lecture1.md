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
  Idea: increase the sorting part one by one
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

  

