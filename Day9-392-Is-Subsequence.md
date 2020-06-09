<https://leetcode.com/problems/is-subsequence/>

We can use a two-pointer approach to iterate over the two strings and find out if every letter in `s` also exists in `t` with the same order.

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        i, j = 0, 0
        for i in range(len(s)):
            while j < len(t) and s[i] != t[j]:
                j += 1
            if j == len(t):
                return False
            j += 1
        return True
```

We can also use `list.index()` method to find the index of each letter in `s` and use it as the start of the next search.

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        i, j = 0, -1
        for i in range(len(s)):
            try:
                j = t.index(s[i], j + 1)
            except:
                return False
        return True
```

(Learned from Discussion) A magical trick here is using an [iterator](https://www.programiz.com/python-programming/iterator) so that `char in t` will only search in part of the string which has never been visited.

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        t = iter(t)
        return all(char in t for char in s)
```



