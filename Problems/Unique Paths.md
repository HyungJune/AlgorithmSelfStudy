### Unique Paths
#### Writer: Donggyu Cho
#### Refer: LeetCode#62 (Medium)
* * *
### Problem

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

<b>Example 1</b>
<pre>
<b>Input</b>: m = 3, n = 7
<b>Output</b>: 28
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: m = 3, n = 2
<b>Output</b>: 3
<b>Explanation</b>: 
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
</pre>

<b>Example 3</b>
<pre>
<b>Input</b>: m = 7, n = 3
<b>Output</b>: 28
</pre>


#### Constraints
- 1 <= m, n <= 100
- It's guaranteed that the answer will be less than or equal to 2 * 109


### Solution
```python3
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[0] * n for i in range(m)]
        for i in range(m):
            for j in range(n):
                if i == 0 or j == 0:
                    dp[i][j] = 1
                else:
                    dp[i][j] += (dp[i-1][j] + dp[i][j-1])
        return dp[m-1][n-1]
```

- 해당 문제는 DP로 해결이 가능하며 마지막 지점은 바로 위와 왼쪽의 합으로 구성됨
- 피보나치 방식과 동일한 방식으로 해결 가능
