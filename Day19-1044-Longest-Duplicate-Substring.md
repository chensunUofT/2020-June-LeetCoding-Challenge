<https://leetcode.com/problems/longest-duplicate-substring/>

We use a Binary Search approach to find the length of the substring, and use [Rabin-Karp algorithm](https://en.wikipedia.org/wiki/Rabin%E2%80%93Karp_algorithm) with [rolling hash](https://en.wikipedia.org/wiki/Rolling_hash) to check if there're duplicate substrings with the same length.

```python
class Solution:
    def longestDupSubstring(self, S: str) -> str:
        
        def RabinKarp(k):        
            def char2num(char):
                return ord(char) - ord('a')  
            base, m = 26, 2 ** 63 - 1
            p = pow(base, k, m)
            h = 0
            for char in S[:k]:
                h = (h * base + char2num(char)) % m
            existed = set()
            existed.add(h)
            i = k
            while i < n:
                h = (h * base + char2num(S[i]) - char2num(S[i-k]) * p) % m
                if h in existed:
                    return (True, S[i-k+1:i+1])
                else:
                    existed.add(h)
                    i += 1
            return (False, '')
        
        n = len(S)
        low, high = 0, n
        res = ''
        while low < high:
            mid = low + (high - low) // 2
            found, pattern = RabinKarp(mid)
            if found:
                res = pattern
                low = mid + 1
            else:
                high = mid
        return res
```



