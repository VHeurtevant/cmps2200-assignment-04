# CMPS 2200 Assignment 4
## Answers

**Name:** Viv Heurtevant










c) Now, suppose we use a $d$-ary heap for Dijkstra's algorithm. What is the
new bound on the work? Your bound will be a function of
$|V|$, $|E|$, and $d$ and will account for the `delete-min` and
`insert` operations separately.

From the maximum depth, we have $\log_d(nd-n+1)-1 = O(log_d(|V|))$. Delete min will run once for each vertice and insert will run once for each edge. Therefore, the total work can be modeled as $|V|O(d*h)+|E|O(h)$. Expanding our definition of O(h), we have $O(|E|\log_d(|V|)+d|V|\log_d|(V|)$


d) Now that we have a characterization of how Dijkstra's algorithm
performs with a $d$-ary heap, let's look at how we might be able to
optimize the choice of $d$ under certain assumptions. Let's suppose
that we have a moderate number of edges, that is  $|E| = |V|^{1+\epsilon}$ for $0<\epsilon
< 1$. What value of $d$ yields an overall running time of $O(|E|)$?

Choose $d=|V|^{\epsilon$}. Then, $|E| = |V|^{1+\epsilon}$. Substituting $|E|$, we have O(|E|\log_d(|V|)+d|V|\log_d|(V|)$



**put in answers.md**

.  
.  
.  







- **1a.**
Given a d ary tree with n nodes and the root at the 0th level, we know that if the ith level is complete it will have $d^i$ nodes. Suppose k is the last completely filled level in the heap, then we have the total number of levels as $\sum_{i=0}^{k}d^i= \frac{d^{k+1}-1}{d-1}$. There are two possibilities; the final node is either on level k or it is on an incomplete k+1 level. This yields $\frac{d^{k+1}-1}{d-1} \leq n < \frac{d^{k+2}-1}{d-1}$. Taking log of both sides and simplifying, we have $k \leq \log_d(n(d-1)+1)-1<k+1$.So the maximum depth is $ \log_d(nd-n+1)-1$


- **1b.**
For insert, a comparison and swap is performed for each moved level which are both constant. The worst possible case is if the swap is from leaf to root, which means the work is determined by the height, O(h)=O$(\log_d(n))$.


For the delete min, we have to find the minimum child and swap with its parent. The worst case is if we have to traverse the entire tree. There will be h levels total and d children to be considered per level, so the total work is O(d*h).


- **1c.**
- From the maximum depth, we have $\log_d(nd-n+1)-1 = O(log_d(|V|))$. Delete min will run once for each vertice and insert will run once for each edge. Therefore, the total work can be modeled as $|V|O(d*h)+|E|O(h)$. Expanding our definition of O(h), we have $O(|E|\log_d(|V|)+d|V|\log_d|(V|)$

- **1d.**


- **2a.**


- **2b.**


- **2c.**

- **2d.**

- **2e.**



- **3a.**


- **3b.**


- **3c.**
