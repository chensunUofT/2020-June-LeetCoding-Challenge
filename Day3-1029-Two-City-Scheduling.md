<https://leetcode.com/problems/two-city-scheduling/>

For each person in this problem, the difference between the cost of going to city A and city B (let's call it `diff`) can be easily calculated. It can be proved that the minimum cast is achieved when **the first half of people with lower `diff` values going to city A and the other half of people going to city B**.  
Therefore, we can firstly sort the `costs` array using the difference between the two values as the key, then calculating the total cost with the cost of going to city A of the first half and city B for the second half.

```python
class Solution:
    def twoCitySchedCost(self, costs: List[List[int]]) -> int:
        costs.sort(key=lambda x: x[0] - x[1])
        N = int(len(costs) / 2)
        return sum(cost[0] for cost in costs[:N]) + sum(cost[1] for cost in costs[N:])
```

