<https://leetcode.com/problems/random-pick-with-weight/>

This can be done with [random.choices() function](https://docs.python.org/3/library/random.html#functions-for-sequences).

```python
import random

class Solution:

    def __init__(self, w: List[int]):
        self.population = list(range(len(w)))
        self.weights = w

    def pickIndex(self) -> int:
        return random.choices(self.population, self.weights)[0]


# Your Solution object will be instantiated and called as such:
# obj = Solution(w)
# param_1 = obj.pickIndex()
```

Or using [itertools.accumulate()](https://docs.python.org/3/library/itertools.html#itertools.accumulate) and [bisect.bisect_left()](https://docs.python.org/3/library/bisect.html#bisect.bisect_left).

```python
class Solution:

    def __init__(self, w: List[int]):
        self.cumsum = list(accumulate(w))

    def pickIndex(self) -> int:
        return bisect.bisect_left(self.cumsum, random.randint(1, self.cumsum[-1]))
```

