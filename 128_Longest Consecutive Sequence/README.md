## Longest Consecutive Sequence

并查集

```
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        class UnionFind():
            def __init__(self, nodeNums):
                self.count = nodeNums
                self.parent = [0 for _ in range(nodeNums)]
                self.size = [1 for _ in range(nodeNums)]
                for i in range(nodeNums):
                    self.parent[i] = i 
                    self.size[i] = 1
            
            def union(self, p, q):
                rootP = self.find(p)
                rootQ = self.find(q)
                if rootP == rootQ:
                    return
                self.parent[rootP] = rootQ
                self.size[rootQ] += self.size[rootP]

            def find(self, x):
                if self.parent[x] != x:
                    self.parent[x] = self.find(self.parent[x])
                
                return self.parent[x]
            
            def maxsize(self):
                return max(self.size)

        if not nums:
            return 0
        Map = {}
        UF = UnionFind(len(nums))
        for i in range(len(nums)):
            if Map.__contains__(nums[i]): continue
            if Map.__contains__(nums[i]-1):
                UF.union(i, Map.get(nums[i]-1))
            if Map.__contains__(nums[i]+1):
                UF.union(i, Map.get(nums[i]+1))

            Map[nums[i]] = i

        return UF.maxsize()

```

哈希集合

```
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        nums = set(nums)
        result = 0

        for num in nums:
            if not num-1 in nums:
                cur = 1
                curNum = num
                while curNum+1 in nums:
                    curNum = curNum+1
                    cur += 1 
                result = max(result, cur)
        return result    
```