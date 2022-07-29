## Satisfiability of Equality Equations


完整版并查集
```
class Solution:
    class UnionFind:
        def __init__(self):
            self.parent = list(range(26))
        
        def find(self, index):
            if index == self.parent[index]:
                return index
            self.parent[index] = self.find(self.parent[index])
            return self.parent[index]
        
        def union(self, index1, index2):
            self.parent[self.find(index1)] = self.find(index2)


    def equationsPossible(self, equations: List[str]) -> bool:
        uf = Solution.UnionFind()
        for st in equations:
            if st[1] == "=":
                index1 = ord(st[0]) - ord("a")
                index2 = ord(st[3]) - ord("a")
                uf.union(index1, index2)
        for st in equations:
            if st[1] == "!":
                index1 = ord(st[0]) - ord("a")
                index2 = ord(st[3]) - ord("a")
                if uf.find(index1) == uf.find(index2):
                    return False
        return True

```

简单版并查集

```
class Solution:
    def equationsPossible(self, equations: List[str]) -> bool:
        parents = {}
        def find(x):
            parents.setdefault(x, x)
            if parents[x] != x:
                parents[x] = find(parents[x])
            
            return parents[x]
        
        def union(p, q):
            rootP = find(p)
            rootQ = find(q)
            if rootP == rootQ:
                return
            
            parents[rootP] = rootQ

        def isConnected(p, q):
            return find(p) == find(q)
        
        for equation in equations:
            if equation[1] == '=':
                union(equation[0], equation[-1])
        
        result = False
        for equation in equations:
            if equation[1] == '!':
                result = isConnected(equation[0], equation[-1])
            if result:
                return False

        return True
```