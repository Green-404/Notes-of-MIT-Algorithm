# Greedy Algorithm
## Minimum Spanning Tree
Input: connected undirected graph G=(V,E) with weight fuction w: E->R.

For simplicity, assume all edge weights are distinct.

Output: a spanning tree T(connect all the vertices) of minimum weight w(T)=Σw(u,v)

### Optimal substructure: hallmark1 of DP is satisfied
Remove (u,v), then T is partitioned into 2 subtrees T1, T2.

Therom: T1 is MST for the graph G1=(V1,E1), the subgraph of G induced by vertices in T1 and E1={(x,y) in E|x,y in V1}. And similar for T2.

Proof: **Cut and Paste**

w(T)=w(u,v)+w(T1)+w(T2)

Suppose T1' is better than T1 for G1, then T' = {(u,v)} and T1' and T2, which will be better than T for G.

### Overlapping subproblem? Yes

DP? Yes! But MST exibit a more powerful property.

## Hallmark for greedy algorithm
`Greedy choice property: A locally optimal choice is globally optimal.`

Theorom: Let T be MST of G=(V,E), and let A part of V, Suppose (u,v) is least-weight edge connecting A to V-A. Then(u,v) in T.

Proof: Cut&Paste

Suppose (u,v) is not in T, then consider unique simple path from u to v in T. Swap (u,v) with the first edge on this path that connects a vertex in A and a vertex in V-A. A lower weight spanning tree than T results. Contradiction.

### Prim's algorithm
Idea: maintain V-A as a priority queue Q. Key each vertex in Q with weight of least-weight edge connecting it to a vertex in A.
```
Q<-V
key[v]<-infinite for each v  //initilize
key[s]<-0 for arbitrary s  //randomly select

while Q!=empty:
  u<-Extract-Min(Q)      //minimum edge
  for each v in Adj[u]    //update Q
    if v in Q and key[v]>w(u,v)
        key[v]=w(u,v)
        P[v]=u            //record the locally front vertex, set pointer back
```

Analysis:
init key and Extract-Min: O(V) time

Degree(u) update each time. Then O(E) implict decrease keys.

Time=Θ(V\*T(Extract-Min)+E*T(Decrease-Key))

For array,



      
