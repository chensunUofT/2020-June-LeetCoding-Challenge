<https://leetcode.com/problems/search-insert-position/>

This is a classic Binary Search problem: initialize variables `low` and `high` with `0` and `len(nums)`, and keep shrinking the search range until the `target` is found or the range is empty (i.e. `low == high`).

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        low, high = 0, len(nums)
        while low < high:
            mid = low + (high - low) // 2
            if target == nums[mid]:
                return mid
            elif target > nums[mid]:
                low = mid + 1
            else:
                high = mid
        return low
```

A few details here:  

1. We are using a "left-close, right-open" format for the search range, so the initial value of `high` is `len(nums)` instead of `len(nums)-1`, and the looping condition is `low < high` instead of `low <= high`;
2. To avoid overflow, use `low + (high - low) // 2` instead of `(low + high) // 2` although it's not a problem in Python;
3. Update `low` with `mid + 1` instead of `mid` (when necessary) to avoid infinite loop. 

