<https://leetcode.com/problems/coin-change-2/>

Use a 2-d array `dp[i][j]` to represent **the number of combinations making up amount `j` with the first `i` coins**. We can consider that `dp[i][j]` consist of two parts:

- the number of combinations of amount `j` without using the `i`-th coin, which is `dp[i-1][j]`
- the number of combinations of amount `j` using the `i`-th coin, which is equivalent to the number of combinations of amount **`j` minus the amount of the `i`-th coin** using the first `i` coins, which is either `dp[i][j-coins[i-1]]` if `j` is not smaller than `coins[i-1]`, or `0` otherwise.

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [[0 for _ in range(amount + 1)] for _ in range(len(coins) + 1)]
        dp[0][0] = 1
        for i in range(1, len(coins) + 1):
            dp[i][0] = 1
            for j in range(1, amount + 1):
                dp[i][j] = dp[i-1][j] + (dp[i][j-coins[i-1]] if j-coins[i-1] >= 0 else 0)
        return dp[-1][-1]
```

We can do some optimization on this solution. First of all, `dp[i][j]` only depends on the current and previous row, so we can actually maintain a 1-d array instead of 2-d, and iterate over each `coin` element in `coins`; besides, it is necessary to update `dp[j]` (`dp[i][j]` in the previous solution) only when `j` is greater than or equal to `coin`, which means that we can start the iteration of  `j` with the value of variable `coin` instead of 0.

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [1] + [0 for _ in range(amount)]
        for coin in coins:
            for j in range(coin, amount + 1):
                dp[j] += dp[j-coin]
        return dp[-1]
```



