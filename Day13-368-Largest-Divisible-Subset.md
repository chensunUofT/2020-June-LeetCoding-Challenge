<https://leetcode.com/problems/largest-divisible-subset/>

Use a list `dp[j]` to store the number of divisors of `nums[j]` in `nums` and their indices. For each `nums[j]`, find the `i` such that `nums[i]` is a divisor of `nums[j]` and has the most divisors, and store the number of divisors (which is `dp[i][0] + 1`) and the indices along with `j` itself as `dp[j]`.

After traversing the array, find the largest number of divisors and the corresponding indices, and return the elements of those indices.

```python
class Solution:
    def largestDivisibleSubset(self, nums):
        if not nums:
            return []
        nums.sort()
        dp = []
        for j in range(len(nums)):
            div, idxs = 0, []
            for i in range(len(dp)):
                if nums[j] % nums[i] == 0 and dp[i][0] > div:
                    div = dp[i][0]
                    idxs = dp[i][1]
            dp.append([div + 1, idxs + [j]])
        longest_idxs = max(dp, key = lambda x: x[0])[1]
        return [nums[i] for i in longest_idxs]
```



