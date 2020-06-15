<https://leetcode.com/problems/insert-delete-getrandom-o1/>

O(1) lookup can be easily implemented with a Hash map (`dict` in Python); however, in order to get a random element, we have to maintain a list that contains all the inserted elements. To build the relationship between the dict and the list, we can use **the index of each element in the list** as **the value of that key in the dict**.  
To remove an existing element:

1. Look up the value of the element in the dict, which is the index of that element in the list.
2. In the list, overwrite the to-be-deleted element with the last element (it's ok if they are the same).
3. Remove the list element in the list, and update the value of this element with its new position in the list, which is just index that we used before.
4. Remove the to-be-deleted element in the dict.

```python
import random


class RandomizedSet:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.d = {}
        self.list = []      

    def insert(self, val: int) -> bool:
        """
        Inserts a value to the set. Returns true if the set did not already contain the specified element.
        """
        if val in self.d:
            return False
        else:
            self.d[val] = len(self.list)
            self.list.append(val)
            return True
                  
    def remove(self, val: int) -> bool:
        """
        Removes a value from the set. Returns true if the set contained the specified element.
        """
        if val not in self.d:
            return False
        else:
            idx = self.d[val]
            self.list[idx] = self.list[-1]
            self.d[self.list.pop()] = idx
            self.d.pop(val)
            return True      

    def getRandom(self) -> int:
        """
        Get a random element from the set.
        """
        rand_idx = random.randint(0, len(self.list) - 1)
        return self.list[rand_idx]
        

# Your RandomizedSet object will be instantiated and called as such:
# obj = RandomizedSet()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```

