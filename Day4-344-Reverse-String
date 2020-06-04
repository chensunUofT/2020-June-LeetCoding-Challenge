<https://leetcode.com/problems/reverse-string/>

Given that it is required to modify the array in-place, we can swap the elements in the array pairwise using two pointers which start from the beginning and end of the array respectively.

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        i, j = 0, len(s) - 1
        while i < j:
            s[i], s[j] = s[j], s[i]
            i += 1
            j -= 1
```

