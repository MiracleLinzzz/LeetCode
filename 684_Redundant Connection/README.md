## Redundant Connection

```
class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:

        parent = {}
        def find(x):
            parent.setdefault(x, x)
            if parent[x] != x:
                parent[x] = find(parent[x])
            return parent[x]
        def union(p, q):
            rootP = find(p)
            rootQ = find(q)
            if rootP == rootQ:
                return [p,q]
            parent[rootP] = rootQ

        for edge in edges:
            temp = union(edge[0], edge[1])
            if temp:
                return temp



```