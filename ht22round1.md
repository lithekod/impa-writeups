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
[dpLink]: https://en.wikipedia.org/wiki/Dynamic_programming#Computer_programming
[dagLink]: https://en.wikipedia.org/wiki/Directed_acyclic_graph

<!---Document-->

# IMPA ht22 omgång 1, 29/8-18/9 - Writeup - (experimental)

The following document tries to provide solution ideas to all problems of categories [medlelsvår, ganska svår, mycket svår] of a previously finished IMPA round. The purpose of this document is to share solution ideas across all IMPA participants. Some problems in this document may have a red <span style="color:red"> Wanted</span> tag in their title. This means that a solution idea is not yet available and invites readears who know of a solution to contribute by emailing the document administrator. Any contributions will be creadited to the contributor, unless told otherwise by the contributor. Any questions, errors, suggestions, etc. can also be emailed to the document administrator.


**Contact:** ordf@lithekod.se (Lowe Kozak Åslöv)


# Ingenuous Cubrency - p11137

## Topics:
[Dynamic programming][dpLink]

## Solution idea:

Given denominations $D = \{d_1,d_2,...,d_n\}$, we may construct an array $dp[i]$ that counts the number of ways to pay the amount $i$. Initially, the whole array is set to zero, then we set $dp[0] = 1$ to declare that we can pay the amount of $0$ in one way. For each denomination $d_i$ in $D$, we iterate from $k= 0$ upwards, updating our array $dp[k] = dp[k] + dp[k-d_i]$ meaning that: if we can reach the amount $k-d_i$ in $dp[k-d_i]$ number of ways, then for each such way of constructing the amount $k-d_i$, adding $d_i$ to that amount results in a way to reach the amount $k$.

# Krochanska Is Here! - p11792

## Topics:
[Breadth-first search](https://en.wikipedia.org/wiki/Breadth-first_search)

## Solution idea:

By maintaining a set of *seen* stations while reading the input, we can easily figure out which of the stations that are *important*. Since the distances between stations is always one, we may use BFS to determine the shortest path from station X to all other stations in the graph. As the graph will contain at most $100$ *important* stations guaranteed by input, we can run BFS from each of these important stations and accumulate the sum of distances to all other *important* stations. The answer is the *important* stations with the least sum to all other *important* stations. 


# Hackers' Crackdown - p11825 <span style="color:red"> Wanted</span>


# Diving for Gold - p990
## Topics:
[Dynamic programming][dpLink]
## Solution idea:

Let an array $dp[t]$ saves the highest value of gold we can achieve using exactly $t$ time. Let $cost_i = 3wd_i$ denote the total cost in time that it takes to recover treasure $i$. Iterating over each treasure, we may then iterate from max time $t=1000$ downwards, checking if it is possible to reach $dp[t-cost_i]$, if so we might want to update dp[t]. If dp[t] has no previous value written to it, we may just set it to $dp[t-cost_i] + value_i$, else we must assure that $dp[t-cost_i] + value_i$ is better than current $dp[t]$. If not, then we do not write anything to $dp[t]$ and continue our iteration. Else we overwrite $dp[t]$. The next part of this problem is recreating the treasures that we picked. For this, we can extend our $dp$ array to save both the *value* and an array of indices of the treasures that we picked so far. On update, we first copy the array of indices of $dp[t-cost_i]$, and add current iteration treasure $i$ to it.
Lastly, iterate over $dp$ finding the index of the highest value of gold recovered and output the treasures stored in that treasure array.


# Flying to Fredericton - p11280

## Topics:
[Dynamic programming][dpLink]

[Graph theory][dagLink]
## Solution idea:
The problem bears with it a notion of "nearest" to "farthest" which essentially means that we are dealing with a Directed Acyclic Graph (DAG). Iterating over the DAG in topological order, meaning here that we iterate from "nearest" to "farthest", we can calculate the lowest cost of reaching a node using a certain amount of stopovers. Let $dp[i][j]$ denote the lowest cost we can achieve flying (from start) to node $i$ using exactly $j$ moves. Then we have the transition $dp[i][j] = min(dp[i][j], dp[a][j-1]+f(a,i))$ for all topologically smaller nodes $a$ with atleast one flight line $f(a,i)$ from node $a$ to node $i$. Answering the queries will then be a matter of iterating from $dp[n][Q]$ to $dp[n][1]$ and choosing the best answer, if there are only $+inf$ available then there exist no such path.

# Palindromic paths - 1244
## Topics:
[Dynamic programming][dpLink]

[Graph theory][dagLink]

## Solution idea:
Input descirbes a complete Directed Acyclic Graph (DAG) with $n$ nodes. Trying all paths would be

$$\sum_{i=0}^{n-2} choose(n-2,i) = 2^{n-2}$$

number of paths which times out. Instead, we notice that palindromes have this property that if you add a letter *ch* to the beginning, then we also must att *ch* to the end. i.e. $ch_1,ch_2,...,ch_2,ch1$. This here allows for some dynamic programming if we can compute $dp[l][r]$ with $l \leq r$, denoting the length of the longest palindrome we can construct between nodes $l$ and $r$.  Iterating over all pairs $(l,r)$ with $l \leq r$ in incrementing order with respect to $r-l$, we can assure that when we calculate $dp[l][r]$ we have already calculated all smaller interior pairs of $[l,r]$. For each pair $(l,r)$ we iterate over $k$ from  $[l+1,r]$ and $m$ from $[k,r]$, checking if $edge[l][k]$ has the same char as $edge[m][r]$ ($edge[from][to]$). If so, a candidate for our best answer for $dp[l][r]$ is $dp[k][m] + 2$. Simply choose the best of these options. That concludes how the calculation of the longest palindrome can be done, but this DOES NOT take either recreating of path nor the lexigraphic criteria into account. For that, we extend our $dp$ array to also save where we go next $dp[l][r]$, namely $k$ and $m$. Then we also construct a **recreate** function that from this information, recreates the whole palindrome string. Then before updating a value of $dp[l][r]$ we first check if the recreated path from our candidate is as large or larger in size and lexigraphically smaller. Answer will then be **recreate** of $dp[1][n]$ (1-indexed).

# Allergy Test - p11691 <span style="color:red"> Wanted</span>

# Partitioning for fun and profit - p10581

## Topics:
[Generating functions](https://www.whitman.edu/mathematics/cgt_online/book/section03.03.html)

## Solution idea:
Generating partitions with an naive implementation to find the $k:th$ partition will time out. Instead, we wish to compute our solution by calculating each digit in the answer separately, from left to right, by counting the **number of lexiographically smaller partitions** we skip over.

Introduce a variable $jmp=0$, denoting the number of lexiographically smaller partitions that we have skipped over so far. Denote our partition of n elements as $a = a_1,a_2,...,a_n$, initially it is set to the smallest lexiographic ordering $a = 1,1,...,1,m-n+1$. Next, we wish to increment $a_1$ as much as possible still maintaining the invariance $jmp < k$. Since $k > 0$ by input, the invariance holds to begin with. We may not set $a_1=0$ because then our partition will no longer consist of $n$ numbers. Therefore, let $a_1=1$ for the first iteration. Since we want to maintain the integrity of our partition, the interval $[a_2,a_n]$ must all be set to atleast the value of $a_1$. Therefore, the number of partitions of size $n$ with $a_1=1$ that sums to $m$, will be equal to <span style="color:red">**the sum of partitions over all positive sizes $k$ less than or equal to $n-1$ that sums to $m-a_1\cdot(n-1)$** </span>. For now, lets call this number <span style="color:red">**$X$**</span>. If $jmp+X$ should break the invariance imposed on $jmp$, we have found our value for $a_1$ and may move on to $a_2$ after updating $m := m-a_1$, at $a_n$ the answer is just the remaining $m$. Else we just set the new value of $jmp := jmp+X$ and try for higher values $a_1$.

More generally; if we let $p(n,k)$ denote the number of integer partitions of n of size k. Then

$$ f(i,a_i) =\sum_{j=1}^{n-i} p(m-a_i\cdot(n-i)),j)$$

is the number of lexiographically smaller partitions that we may choose skip over or not if we are evaluating position $i$ with the value of $a_i$. The question of how we calculate $p(n,k)$ remains. There is a [theorem](https://brilliant.org/wiki/partition-of-an-integer/) that states that 

*"The number p(n,k) of partitions of a positive integer n into exactly k parts equals the number of partitions of n whose largest part equals k".*

We can use this to slightly alter our generating function for integer partitions. Instead of 
$$ \prod_{d=1}^{M} \sum_{i=0}^{M}x^{id} \text{,}$$
we force the largest term to be present atleast once with

$$ G(x,n,k) =(\prod_{d=1}^{k-1} \sum_{i=0}^{n/d}x^{id}) \cdot(x^{k}+x^{2k}+...) \text{.}$$

Then $p(n,k) = [x^n]G(x,n,k)$,

```cpp
long long p(int n, int k) {
    vector<long long> x(n + 1,1); // x[i] is the coef infront of x^i
    for (int i = 2; i <= k; i++) {
        vector<long long> res(n + 1, 0); // result after multiplication
        long long r = 0; // 0,2,4 ... 0,3,6...
        if (i == k) r++; // must have a largest part eq to k.
        while (i * r <= n) {
            long long exp = i * r;
            for (int j = 0; j <= n - exp; j++) {
                res[exp + j] += x[j];
            }
            r++;
        }
        x = res;
    }
    return x[n];
}
```
and since our m in this problem is small, we can just evaluate all the multiplications in an array of size 220, excluding any higher exponents. Also, each position $a_i$ will never exceed 220, so our iteration over $a$ is very limited.

# Down Went The Titanic - p11380

## Topics:
[Maxflow](https://en.wikipedia.org/wiki/Maximum_flow_problem)

## Solution idea:
The problem breaks down to translating the grid into a flow network, and then solving the flow network with some known maxflow algorithm. Let $M=1000$ denote some large enough integer (infinity). The '~' we do not even have to include in our network. Other than that, there are two different types of blocks: blocks that disappear after usage and blocks that remain. Blocks that disappear after usage can be translated into a pair of nodes named $A$ (primary) and $A'$ (secondary) with an edge from $A$ to $A'$ holding the upper limit of flow for the given character. We set the limit of '\*'-nodes from primary to secondary node set to 1. We also connect a start node to all '\*'-nodes with flow limit $M$. The '.'-nodes we connect primary with secondary holding the flow limit of 1.

For blocks that remain we simple connect them with edges holding their specified limit, if '@' then we set the limit to some large enough number $M$, and if '#' then $p$. Also, we connect all '#'-nodes to a sink node with flow limit $p$. Next we connect the graph by iterating over the grid. If we are standing on position $(r,c)$ then we connect the secondary node of $(r,c)$ if such a node exist - else just the node itself, to all (primary) neighbours excluding '~'-nodes, with a limit of some large enough number $M$ once again.
