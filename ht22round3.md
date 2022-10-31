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
<!---Document-->

# IMPA ht22 omgång 3, 10/10-30/10 - Writeup - (experimental)

The following document tries to provide solution ideas to all problems of categories [medlelsvår, ganska svår, mycket svår] of a previously finished IMPA round. The purpose of this document is to share solution ideas across all IMPA participants. Some problems in this document may have a red <span style="color:red"> Wanted</span> tag in their title. This means that a solution idea is not yet available and invites readears who know of a solution to contribute by emailing the document administrator. Any contributions will be creadited to the contributor, unless told otherwise by the contributor. Any questions, errors, suggestions, etc. can also be emailed to the document administrator.


**Contact:** ordf@lithekod.se (Lowe Kozak Åslöv)

# II Gioco dell'X - p260

## Topics:
[Breadth First Search][bfslink]

## Solution idea:

Since only one player will always win we can evaluate the board for a single player alone and confirm from that infromation who was the winner. Pick one of the colors, and use Breadth First Search (BFS) conditionally by only moving on the same colour and only moving in the directions that the game specifies. Iterate over all possible starting positions for the picked colour. If at any moment of the BFS we reach a cell from the opposite side from where the algorithm started, then the winner is the picked colour.


# Heavy Cycle Edges - p11747

## Topics:
[Minimum spanning tree][mstlink]

## Solution idea:

Consider starting with a minimum spanning tree (MST) of the graph $G=(V,E)$. Adding any edge $v$ in $V$ to the MST that is not already part of the MST will make it so that we no longer have a tree since $v$ is sure to create a cycle. This same edge $v$ must also be the most expensive edge occuring in the could have been cycle. If it weren't then there must have existed a cheaper MST. Which violates the presupposition we had starting from a MST. Therefore, every edge not part of the MST should be written in the answer.

# SMS - p11171

## Topics:
[Dynamic programming][dpLink]

## Solution idea:

Note that it is guaranteed that some combination of words from our given dictionary is the answer. Further note that the maximum length of a word is 10 characters. We can use dynamic programming to build the desired string $s$ from the back with minimum cost. Let $dp[i]$ be an array storing the lowest cost building $s$ from position $i$ to the back. Let $i$ iterate from the back of $s$. We always examining the position $i$ that we're at, and 9 steps forward (max word len). For each step $k$, $0 <= k <= 9$ forward, we look if the string s[i,i+k] (inclusive) is a word from our dictionary. If it is, then we can note the potentially best cost from position $i$ forwards as $dp[i] = cost(s[i,i+k]) + dp[i+k+1]$. Calculating the cost of a word is simply done by saving a vector of all words with the same type sequence in a map. Then simultanously iterate from start and back in order to choose the lowest cost of U(x) and D(x). Further extending our dp array to save also the word that we typed from position $i$ allows for linear recreation of the answer.

# A Grouping Problem - p11026

## Topics:
[Suffix sum array][prefixlink]

## Solution idea:

The key observation is to see the nice pattern that emerges if we store the element summations in a prefix/suffix array. Consider the given example with four elements $a,b,c \text{ and } d$.
If $K = 1$ we have the suffix array  $S_K = S_1 = [a+b+c+d;b+c+d;c+d;d;0]$ with the total summation occuring at the first position.
For $K=2$, we have the total summation $ab + ac + ad + bc + bd + cd$ which can be obtained by multiplying $c$ with the last position of $S_1$, $b$ with the second last position of $S_1$, $a$ with the third last position of $S_1$ and adding them all together. If we construct the next suffix array as we do the multiplications we get $S_2 = [0,ab + ac + ad + bc + bd + cd; bc + bd + cd; cd;0]$. This can be repeated for all possible $K$. In general, $S_n[i] = S_n[i+1] + S_{n-1}[i] \cdot (i-n+1)\text{:th element}$ for $i \lt \text{number of elements with } (i-n+1) \ge 0 \text{ and }  n \ge 2$. Do an exhastive search for every K and take each position mod M in every iteration. Answer is the maximum total summation to every occur.


# Shopping - p11813

## Topics:
[Traveling Salesman][tsplink]

[Dijkstra's][dijk]
## Solution idea:

Let $T$ denote the set of nodes that occur in the shopping tour. Run dijkstra's for each node $t \in T$. Replace the given graph with only the nodes appearing in $T$, the edges between nodes are the calculated dijkstra values with shorest distances. Next run the exponential dp algorithm to solve the TSP for the new graph.


# Murica's Skyline - p11790
## Topics:
[Longest (strictly) Increasing Subsequence][lislink]

## Solution idea:

We only have to consider solving for the longest strictly increasing subsequence (LIS). If we create a function $f$ that solves for LIS, we can just reverse the array and run it again to get the result of the best right-to-left possibilities. Note that the LIS that we are asked to solve for differs slightly from the generic implementation. In this problem, what we want to maximize is the sum of the sequences's width. Let $dp$ be an array of pairs where $dp[i] \text{ stores the heigth (first) and the best width possible using the i:th building (second) }$. We calculate for $i$ from 0 to $n$ and $j$ from 0 to $i-1$:
```cpp
if (height[i] > dp[j].first && dp[i].second < width[i] + dp[j].second) dp[i].second = width[i] + dp[j].second$
```
Which first asserts that we can use this building (has higher height than the sequence that we are extending onto) and also that we have not already achieved a better answer. Answer is the sequence with the greatest width summation.


# Cache Simulator - p11423
## Topics:
[Square root decomposition (range queries)][sqrtdecomplink]

## Solution idea:

For this problem, the time limit is set to 10 seconds. Simulating the whole process using a set for each cache is too slow. What we want to do instead is try to maintain a single data structure from which we can determine whether an element is still inside the cache, for each cache. If we have a running variable that simulates the time, $time = 1$, which increments by one after each insert action, we can store the insert time for each element in an array of size up to the maximum number that can occur as an element. Futhermore, we maintain a range sum data structure in which we handle two types of inserts.

Insert an element not inserted before (prevInsertTime[el] = 0): Simple set rangeQueryStruct[time] to 1, set prevInsertTime[el] = time and increment time by one.


Insert an element which has appeared before (prevInsertTime[el] != 0): Set rangeQueryStruct[prevInsertTime[el]] to 0, set rangeQueryStruct[time] to 1 and increment time by one. This ensures that elements that was inserted prior to el does not double count el.


Calculating the cache size required for a previously inserted element, we query the sum range interval [prevInsertTime[el],time] (inclusive). If this number is greater than cacheSize[i], then it is a miss. Otherwise it is a hit.

Note: Using python instead of cpp you might have to use a data structure with log(n) queries such as segment tree, instead of sqrt(n).


# Shoveling Snow - p10863 <span style="color:red"> Wanted</span>

# Curoius Fleas - p11329 <span style="color:red"> Wanted</span>
