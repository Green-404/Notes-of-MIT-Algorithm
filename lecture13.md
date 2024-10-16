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

Example:
```
c_i = cost of i th insert = i,if i-1 is the power of 2, 1, else
Cost of n inserts = Σc_i = n + Σ2^j(j from 0 to log(n-1) rounded lower) <= 3n = Θ(n)
Thus, average cost for insert is Θ(1)
```
### Accounting analysis
- Charge i th op a **fictitious amortized cost** c_i(1 dollar pays for 1 unit of work)
- Fee is consumed to perform op.
- Unused amount stored in "bank" for use by later ops. Bank balance must not go negative.

**Provide an upper bound**: Must have Σc_i <= Σamortized c_i from 1 to n for every n

### Potential analysis
