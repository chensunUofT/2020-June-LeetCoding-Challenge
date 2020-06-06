<https://leetcode.com/problems/queue-reconstruction-by-height/>

We can sort the people in the input array by the descending order of heights, then insert them one-by-one with `k` (number of taller people in front of this person) as the inserting index.

```python
class Solution:
    def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
        people.sort(key=lambda p: (-p[0], p[1]))
        res = []
        for p in people:
            res.insert(p[1], p)
        return res
```

Alternatively, we can sort the `people` by the ascending order of heights and placing the shortest people first with index from `idxs` which is initialized with the range of integers from `0` to `N-1`. Every time we need to place an item in the sorted `people`, we pop an element from `idxs` with popping index `k` so that we can assure that `k` taller people will be placed in front of this person.

```python
class Solution:
    def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
        people.sort(key=lambda p: (p[0], -p[1]))
        res = [None for _ in range(len(people))]
        idxs = list(range(len(people)))
        for p in people:
            res[idxs.pop(p[1])] = p
        return res
```



