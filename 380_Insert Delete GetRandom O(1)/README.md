## Insert Delete GetRandom O(1)


变长序列 + 记录索引的哈希表

```
class RandomizedSet:

    def __init__(self):
        self.nums = []
        self.numMap = {}

    def insert(self, val: int) -> bool:
        if self.numMap.get(val) != None:
            return False
        self.numMap[val] = len(self.nums)
        self.nums.append(val)
        return True

    def remove(self, val: int) -> bool:
        if self.numMap.get(val) == None:
            return False
        index = self.numMap[val]
        self.numMap[self.nums[-1]] = index
        del self.numMap[val]
        temp = self.nums[index]
        self.nums[index] = self.nums[-1]
        self.nums[-1] = temp
        self.nums.pop()
        return True

    def getRandom(self) -> int:
        return choice(self.nums)


# Your RandomizedSet object will be instantiated and called as such:
# obj = RandomizedSet()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```