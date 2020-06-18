<https://leetcode.com/problems/h-index-ii/>

We need to find the biggest `h` so that there're more than `h` elements in the array that are greater than or equal to `h`, which means `citations[n-h] >= h` where n is the length of the array. If we substitute `n-h` with `i`, the problem is equivalent to finding the smallest `i` so that `citations[i] >= n-i`.

```python
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        if not citations:
            return 0
        n = len(citations)
        low, high = 0, n
        while low < high:
            mid = low + (high - low) // 2
            if n - mid > citations[mid]:
                low = mid + 1
            else:
                high = mid
        return n - low
```

