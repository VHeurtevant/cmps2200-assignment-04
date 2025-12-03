# CMPS 2200 Assignment 4
## Answers

**Name:** Viv Heurtevant



- **1a.**
Given a d ary tree with n nodes and the root at the 0th level, we know that if the ith level is complete it will have $d^i$ nodes. Suppose k is the last completely filled level in the heap, then we have the total number of levels as $\sum_{i=0}^{k}d^i= \frac{d^{k+1}-1}{d-1}$. There are two possibilities; the final node is either on level k or it is on an incomplete k+1 level. This yields $\frac{d^{k+1}-1}{d-1} \leq n < \frac{d^{k+2}-1}{d-1}$. Taking log of both sides and simplifying, we have $k \leq \log_d(n(d-1)+1)-1<k+1$.So the maximum depth is $ \log_d(nd-n+1)-1$


- **1b.**
For insert, a comparison and swap is performed for each moved level which are both constant. The worst possible case is if the swap is from leaf to root, which means the work is determined by the height, O(h)=O$(\log_d(n))$.


For the delete min, we have to find the minimum child and swap with its parent. The worst case is if we have to traverse the entire tree. There will be h levels total and d children to be considered per level, so the total work is O(d*h).


- **1c.**
From the maximum depth, we have $\log_d(nd-n+1)-1 = O(log_d(|V|))$. Delete min will run once for each vertice and insert will run once for each edge. Therefore, the total work can be modeled as $|V|O(d*h)+|E|O(h)$. Expanding our definition of O(h), we have $O(|E|\log_d(|V|)+d|V|\log_d(|V|))=O(\log_d(|V|)(|E|+d|V|))$


- **1d.**
Choose $d=|V|^{\epsilon}$.

Given $|E| = |V|^{1+\epsilon}$, we have $O(\log_d(|V|)(|V|^{1+\epsilon}+d|V|))$. Note $\log_d(V) =\frac{\log V}{\log d}$, therefore $O(\frac{\log V}{\log d}(|V|^{1+\epsilon}+d|V|))$. Next, we factor out  $|V|^{1+\epsilon}$ to isolate |E|: $O(\frac{\log V}{\log d} |V|^{1+\epsilon}(1+d|V|^{-\epsilon}) =  O(\frac{\log V}{\log d} |E|(1+d|V|^{-\epsilon})$. Therefore, for O(|E|) we want to choose d such that $\frac{\log V}{\log d}*(1+d|V|^{-\epsilon}= O(1)$. Choosing $d=|V|^{\epsilon}$ will satisfy this equation, as $\frac{\log V}{\log V^{\epsilon}}=\frac{1}{\epsilon}$, which is O(1) and $1+|V^{\epsilon}V^{- \epsilon}=1+V^0=1+1=2$, which is also O(1). Therefore the terms multiplied give O(1), which gives the desired result that the bound will be O(E).


- **2a.**
First we initialize the graph by only considering direct edges:

| i\j | 0  | 1  | 2 |
| --- | -- | -- | - |
| 0   | 0  | -2 | 2 |
| 1   | -2 | 0  | 1 |
| 2   | 2  | 1  | 0 |


Next, for k=0 we update dist(1,2) as it gives path length of 0 which is less than the 1 length. We also find that dist(1,1) can be reduced to -4 by taking advantage of the negative vertice between 0 and 1. We see that we have a negative cycle from this.

| i\j | 0  | 1  | 2 |
| --- | -- | -- | - |
| 0   | 0  | -2 | 2 |
| 1   | -2 | -4 | 0 |
| 2   | 2  | 0  | 0 |


For k=1 we have improvements across most nodes- notably all except for (2,2) decrease by 4 in length . Note we only can traverse an intermediate vertex once.

| i\j | 0  | 1  | 2  |
| --- | -- | -- | -- |
| 0   | -4 | -6 | -2 |
| 1   | -6 | -8 | -4 |
| 2   | -2 | -4 | 0  |

For k=2, there are no improvement:

| i\j | 0  | 1  | 2  |
| --- | -- | -- | -- |
| 0   | -4 | -6 | -2 |
| 1   | -6 | -8 | -4 |
| 2   | -2 | -4 | 0  |



- **2b.**

  Interestingly, the relationship between ASPS(i,j,1) and ASPS(i,j,2) is the same which means that no shortests paths use 2 as an intermediate, so we can say that ASPS(i,j,2) = ASPS(i,j,1) for all i,j.
  If there was some node that did use 2 as an intermediate for the shortest path then we can write it as the sum of two k=1 subpaths ASPS(i,2,1) and ASPS(2,j,1).


- **2c.**
From the above problem, we see there are two possibilities for ASPS(i,j,k), where the optimal path either does or does not use k.

The first option, if the path does not contain vertice k in the optimal will just be ASPS(i,j,k-1). The second option builds two subpaths of k-1 from i,k and then k,j: ASPS(i,k,k-1) + ASPS(k,j,k-1).

So for the optimal substructure, we simply choose the minimum of these two: Min(ASPS(i,j,k-1), ASPS(i,k,k-1)+ASPS(k,j,k-1)
- **2d.**

Because we are using an undirected graph, the adjacency matrix will be symmetric- meaning we can store the value of each (i,j) to compute (j,i). This will reduce the amount of subproblems by roughly half. We will have n diagonals, and $\frac{n(n-1)}{2}$ non diagonals,so the total amount of suproblems will be $n + \frac{n(n-1)}{2}=\frac{n^2+n}{2}$. Next, we must compute these subproblems for each value of k from 0,1,2...n-1 , so this will happen n times. We multiply this by the number of subproblem to get the result: $O(\frac{n^3+n^2}{2})$, or more simply $O(n^3)$.

- **2e.**

From notes, we know that Johnson algorithm has work $O(nm+n^2 \log n)$. Which algorithm is dependent on the sparsity of the graph. The denser the graph, the larger m will be so when the graph is dense, $n^2 ~ m$ so Johnson will be roughly $O(n^3+n^2 \log n)$ which will be slightly worse than our algorithm. If the graph is sparse though, m will be small and Johnson algorithm will be more efficient.

- **3a.**
No, it is not neccesarily true as MST minimizes sum of all edgeweights, while MMET only wants to minimize the maximum single edge weight. For a counter example, consider a graph with vertices A,B,C,D with edges:
A-B = 1
B-C = 1
C-D = 10
A-D = 5
B-D = 6

Our MST would choose A-B + B-C+ C-D, which has a minimum sum of 12. However, this would fail the MMET as it uses the heaviest edge C-D. The MMET would instead pick A-B+B-C+A-D, where the maximum edge is minimized to 5.

- **3b.**
  Let the original MST be T. To find the next best MST, we can remove any given edge and find a replacement candidate with a new edge/path . We then choose the minimum weight edge to replace, when doing this we should consider subtracting our new weight from original edge's weight to compare the increase in cost. (For example, replacing a smaller edge will be more costly than replacing a larger edge) 

- **3c.**
The worst case is that the MST is V-1 edges long. We have to compare for each edge, so the total work will be around O(EV). It is possible this can be improved by checking edges in parallel.
