# Amortized Analysis
## Analysis Example: How large should a hash table be?
As large as possible, more fast to search. 

As small as possible, less space to allocate.

Θ(n) for n items

### Problems: If we don't know n in advance?

Solution: Dynamic tables

Idea: Whenever the table gets too full(overflows), "grow" it.

1. Allocate(malloc or new) a larger table
2. Move items from the old table to the new
3. Free the old table

Analysis:

Sequence of n insert oprations.

w.c. cost of 1 insert = Θ(n)

w.c. cost of n insert = n*Θ(n) = Θ(n^2)

**Wrong!** In fact, n insert do take Θ(n) time

## Amortized analysis idea
Analyse a seq of ops to show that ave. cost per op is small, even though 1 op may be expensive.

No probability - ave. perf in worst case

## Type of amortized arguments
Accounting and potential analysis are more precise because they allocate specific "amort cost" to each op.
### Aggregate analysis
Calculate the total and compute the expectation

`Calculate precisely`

Example:
```
c_i = cost of i th insert = i,if i-1 is the power of 2, 1, else
Cost of n inserts = Σc_i = n + Σ2^j(j from 0 to log(n-1) rounded lower) <= 3n = Θ(n)
Thus, average cost for insert is Θ(1)
```
### Accounting analysis

`Assume an amortized cost and prove that using this the data structure bank will never be negative. Then it will be an upper bound.`

- Charge i th op a **fictitious amortized cost** c_i(1 dollar pays for 1 unit of work)
- Fee is consumed to perform op.
- Unused amount stored in "bank" for use by later ops. Bank balance must not go negative.

**Provide an upper bound**: Must have Σc_i <= Σamortized c_i from 1 to n for every n

### Potential analysis

`Use a qualified potential function P(P0=0, Pi>=0 always) and then figure out every kind of operation under every condition, what is the amortized cost of it. amortized cost = cost + ΔP.`

Bank account viewed as potential energy of dynamic set

Framework:
- Start with data structure D0
- op i transforms Di-1 to Di
- Cost of op i is c_i
- Define **potential fuction** be F:{Di}->R, $ F(D0)=0 and F(Di)>=0 for every i.
- define the amortized cost C_i is **C_i = c_i + F(Di) - F(Di-1)** *change of potential + c_i*
  - If ΔF>0, then C_i>c_i, which means charge more than need, then op i stores work in data structure for later ops.
  - If ΔF<0, then C_i<c_i, which means charge less than need, then op i delivers up work in data structure to help pay for op i.
  - Overall, the potential is the bank, when we need, we store or deliver op.

Difference:

Accounting method first decides an amortized cost, and then analyse the bank account to make sure non-negtive.

Potential method first decides the bank, and then calculate the amortized cost.

Total amortized cost of n ops is:

ΣC_i = Σc_i + F(Dn) - F(D0) >= Σc_i

Therefore, potential method provides an upper bound.

Example:
```
Define F(Di)=2i-2^(logi rounded above) (Assume 2^log0 = 0)
Note: F(D0)=0 F(Di)>=0 for every i[at most 2i-2^(logi + 1)=0]

Amort cost of i th Insert:
C_i = c_i + F(Di) - F(Di-1)
c_i = i if i-1=2^k, 1 else.
Then, if i-1=2^k, C_i = i + 2 - 2(i-1) + (i-1) = 3
      else, C_i = 1 + 2 - 2^(ceiling of logi) + 2^(ceiling of logi-1) = 3
n Inserts cost Θ(n) in the worst case
```

Conclusion: Amortized costs provide a clean abstraction for data structure performance.


Different potential functions or accounting costs may yield different bounds.
