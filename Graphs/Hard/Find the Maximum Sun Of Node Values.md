[3068. Find the Maximum Sum of Node Values](https://leetcode.com/problems/find-the-maximum-sum-of-node-values/)

There exists an **undirected** tree with `n` nodes numbered `0` to `n - 1`. You are given a **0-indexed** 2D integer array `edges` of length `n - 1`, where `edges[i] = [ui, vi]` indicates that there is an edge between nodes `ui` and `vi` in the tree. You are also given a **positive** integer `k`, and a **0-indexed** array of **non-negative** integers `nums` of length `n`, where `nums[i]` represents the **value** of the node numbered `i`.

Alice wants the sum of values of tree nodes to be **maximum**, for which Alice can perform the following operation **any** number of times (**including zero**) on the tree:

- Choose any edge `[u, v]` connecting the nodes `u` and `v`, and update their values as follows:
    - `nums[u] = nums[u] XOR k`
    - `nums[v] = nums[v] XOR k`

Return _the **maximum** possible **sum** of the **values** Alice can achieve by performing the operation **any** number of times_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2023/11/09/screenshot-2023-11-10-012513.png)

**Input:** nums = [1,2,1], k = 3, edges = [[0,1],[0,2]]
**Output:** 6
**Explanation:** Alice can achieve the maximum sum of 6 using a single operation:
- Choose the edge [0,2]. nums[0] and nums[2] become: 1 XOR 3 = 2, and the array nums becomes: [1,2,1] -> [2,2,2].
The total sum of values is 2 + 2 + 2 = 6.
It can be shown that 6 is the maximum achievable sum of values.

**Example 2:**

![](https://assets.leetcode.com/uploads/2024/01/09/screenshot-2024-01-09-220017.png)

**Input:** nums = [2,3], k = 7, edges = [[0,1]]
**Output:** 9
**Explanation:** Alice can achieve the maximum sum of 9 using a single operation:
- Choose the edge [0,1]. nums[0] becomes: 2 XOR 7 = 5 and nums[1] become: 3 XOR 7 = 4, and the array nums becomes: [2,3] -> [5,4].
The total sum of values is 5 + 4 = 9.
It can be shown that 9 is the maximum achievable sum of values.

**Example 3:**

![](https://assets.leetcode.com/uploads/2023/11/09/screenshot-2023-11-10-012641.png)

**Input:** nums = [7,7,7,7,7,7], k = 3, edges = [[0,1],[0,2],[0,3],[0,4],[0,5]]
**Output:** 42
**Explanation:** The maximum achievable sum is 42 which can be achieved by Alice performing no operations.

**Constraints:**

- `2 <= n == nums.length <= 2 * 104`
- `1 <= k <= 109`
- `0 <= nums[i] <= 109`
- `edges.length == n - 1`
- `edges[i].length == 2`
- `0 <= edges[i][0], edges[i][1] <= n - 1`
- The input is generated such that `edges` represent a valid tree.

>[!Intuition]
>Since the graph is a tree all nodes are connected either directly or indirectly and we know that **a^b^b = a** means that if we xor any number twice we will get the same number and thus we can chose any two nodes and xor them as long as we have a third node which is not xorred twice but we can only do so in pairs of numbers. So we must find the change in value for all numbers from doing xor and then calculate which ones should be xorred or not.

```python
class Solution:
    def maximumValueSum(self, nums: List[int], k: int, edges: List[List[int]]) -> int:

        n = len(nums)
        delta = [0]*n
        
        ans = sum(nums)

        for i in range(0,n):
            delta[i] = (nums[i]^k)-nums[i]

        delta.sort(reverse=True)

        for i in range(0,n,2):
            if i+1>=n:
                break
            temp = delta[i]+delta[i+1]

            if temp<=0:
                break
            ans+=temp

        return ans
```