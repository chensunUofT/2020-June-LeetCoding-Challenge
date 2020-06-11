<https://leetcode.com/problems/sort-colors/>

The key idea here is to swapping all the `2`'s to the end of the array and all the `0`'s to the front in one pass. We can use two pointers `pzero` and `ptwo` pointing at **the first non-zero element** and **the last non-two element** respectively. Use another pointer `i` to iterate over the array and swap `nums[i]` with `nums[ptwo]` or `nums[pzero]` when necessary.

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        i, pzero, ptwo = 0, 0, len(nums) - 1
        while pzero < len(nums) and nums[pzero] == 0:
            pzero += 1
        while ptwo >= 0 and nums[ptwo] == 2:
            ptwo -= 1
        i = pzero
        while i <= ptwo:
            if nums[i] == 2:
                nums[i], nums[ptwo] = nums[ptwo], 2
                ptwo -= 1
            else:
                if nums[i] == 0:
                    nums[i], nums[pzero] = nums[pzero], 0
                    pzero += 1
                i += 1
```

Another similar solution:

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        i, pzero, ptwo = 0, 0, len(nums) - 1
        while i <= ptwo:
            while nums[i] == 2 and i < ptwo:
                nums[i], nums[ptwo] = nums[ptwo], 2
                ptwo -= 1
            while nums[i] == 0 and i > pzero:
                nums[i], nums[pzero] = nums[pzero], 0
                pzero += 1
            i += 1  
```

