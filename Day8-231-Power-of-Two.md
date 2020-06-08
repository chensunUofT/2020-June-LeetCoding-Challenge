<https://leetcode.com/problems/power-of-two/>

We can recurrently divide the number by 2 until it's smaller than or equal to 1. 

```python
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        while n > 1:
            n /= 2
        return n == 1
```

Or use a smart bit manipulation:

```python
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        return n and not n & (n-1)
```

