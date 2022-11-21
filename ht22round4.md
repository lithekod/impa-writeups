<!---
Template -

# Problem name - pid
## Topics:
## Properties:
## Solution idea:
## Complexity analysis:
## Worked example:
\square 
-->

<!---Variables-->

[id_example]: https://www.google.se/
<!--- [link text to id src][id_example] -->
[bruteLink]: https://en.wikipedia.org/wiki/Brute-force_search
[bsLink]: https://en.wikipedia.org/wiki/Binary_search_algorithm
[sqrtdecomplink]: https://cp-algorithms.com/data_structures/sqrt_decomposition.html
[tsplink]: https://en.wikipedia.org/wiki/Travelling_salesman_problem
[lislink]: https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/
[dpLink]: https://en.wikipedia.org/wiki/Dynamic_programming#Computer_programming
[dagLink]: https://en.wikipedia.org/wiki/Directed_acyclic_graph
[dijk]: https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm
[dmst]: https://www.cs.tau.ac.il/~zwick/grad-algo-13/directed-mst.pdf
[dinic]: https://en.wikipedia.org/wiki/Dinic%27s_algorithm
[bfslink]: https://en.wikipedia.org/wiki/Breadth-first_search
[mstlink]: https://en.wikipedia.org/wiki/Minimum_spanning_tree
[prefixlink]: https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/
[2dseg]: https://www.geeksforgeeks.org/two-dimensional-segment-tree-sub-matrix-sum/
<!---Document-->

# IMPA ht22 omgång 4, 31/10-20/11 - Writeup - (experimental)

The following document tries to provide solution ideas to all problems of categories [medlelsvår, ganska svår, mycket svår] of a previously finished IMPA round. The purpose of this document is to share solution ideas across all IMPA participants. Some problems in this document may have a red <span style="color:red"> Wanted</span> tag in their title. This means that a solution idea is not yet available and invites readears who know of a solution to contribute by emailing the document administrator. Any contributions will be creadited to the contributor, unless told otherwise by the contributor. Any questions, errors, suggestions, etc. can also be emailed to the document administrator.


**Contact:** ordf@lithekod.se (Lowe Kozak Åslöv)

# Number of paths

## Topics:
[Directed Acyclic Graph][dagLink]

[Dynamic programming][dpLink]

## Solution idea:

To calculate the number of paths we may first prune the input by removing all 'S' characters as they have no impact on our final solution. We may tie each IF-ELSE-END_IF statement together by 
using two stacks, one IF-stack and one ELSE-stack. We go through the strings from first to last, and when we encounter an END_IF statement we pop one element from each of the two stacks and tie them together. Each IF-ELSE-END_IF statement evaluates as follows: 

If an IF statement evaluates TRUE, then we move to the line after IF. Otherwise we jump all the way to the line after the corresponding else statement. We may construct a DAG from this. Assume that IF is on index position x, ELSE is on index position y and END_IF on index position z. Then we add the edges:

- x -> x+1 (IF TRUE)
- x -> y+1 (IF FALSE)
- y -> z (IF was TRUE, jump over ELSE)
- z -> z+1 (jump into next IF-ELSE-END_IF statement)

This represents all the ways that we can move forward in our given program. Next we can calculate the number of paths by setting the number of paths to the first index position to 1. We iterate over index positions $i$ from left to right, and for each edge connecting node $i$ to node $j$ for $(j>i)$, we add $dp[j] = dp[j] + dp[i]$. Answer is found at the last index position.

# Coprimes <span style="color:red"> Wanted</span>

# Manhattan <span style="color:red"> Wanted</span>

# Eigensequence

## Topics:
[Dynamic programming][dpLink]

## Solution idea:

For a sequence S, in the eigensequence E(s) each element $a_{i}$ is the only number within $(a_{i-1},a_i]$ that is divisable by $d=a_i - a_{i-1}$ (eigen sequence property). Let $dp[i][j]$ denote the number of sequences with the first number equal to $i$ and the last element equal to $j$. Note that $dp[i][i+1] = 1$ for all valid $i$.
If we have $dp[i][j]$, we can calculate $dp[i][k]$ for $k > j$ by iterating over each $j$, $i \lt j \lt k$ and adding $dp[i][k] = dp[i][k] + dp[i][j]$ if and only if the eigensequence property holds for numbers $j$ and $k$. We must also evaluate the sequence consisting of just $i$ and $k$ here, and add one to $dp[i][k]$ if the property holds. The dp array can be precalculated. For input values $n$ and $m$, we simply output $dp[n][m]$.

# Census (Credit Fredrik Nääs)

## Topics:
[Brute force][bruteLink]


## Solution idea:

There exist data structures that can handle the standard sum,min & max queries fast even in two dimensions (see: [2D segtree][2dseg]). However, it suffice to just iterate with a for loop if you are using cpp, time limits are way to generous.

# Moogle <span style="color:red"> Wanted</span>

# Introspective Caching

## Topics:
[Brute force][bruteLink]

Strategy optimality proof - "Evaluation Techniques for Storage Hierarchies" av Mattson et. al. 1970

## Solution idea:

The idea here is to eject the value that will occur last (or never again) of the values currently in the cache must you eject a value. This is a known idea within the theory of caching. Your best approach for finding such a solution is by coding a brute force solution that solves for small test cases that you create yourself, and from there try to see this pattern.

The implementation part is a bit tricky aswell.

One might implement this with the help of the following setup

- next(element,index) -> std::map maps a pair to the next index of that element occurence
- cache(element) -> std::unordered_set true,false if element is currently in the cache
- ejectNext() -> std::set maintains priority queue of next(element,index), of elements currently in the cache. 

Then it becomes a matter of dynamically inserting and erasing from the sets.




# GATTACA

## Topics:
[Binary Serach][bsLink]


## Solution idea:

Let $t$ denote the largest substring of size $k$ that appears atleast twice in our given DNA string.
Notice that, if there exist a substring that appears atleast twice of size $k$, then there must exist a substring of size $k-1 \ge 0$ that appears atleast twice - for example the prefix of the substring of size $k$ dropping tha last character. Hence, we can find $t$ by binary searching over the maximum size $k$. This is sufficient, but the solution can made faster with string hashing when checking if a substring is appearing atleast twice. 

# Keys <span style="color:red"> Wanted</span>
