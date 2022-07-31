## Minimum Height Trees

### 由外向内的BFS

```
class Solution:
    def findMinHeightTrees(self, n: int, edges: List[List[int]]) -> List[int]:
        if n == 1:
            return [0]
        graph = []
        degree = []
        for _ in range(n):
            graph.append([])
            degree.append(0)
        for edge in edges:
            degree[edge[0]] += 1
            degree[edge[1]] += 1
            graph[edge[0]].append(edge[1])
            graph[edge[1]].append(edge[0])

        stack = []
        for i in range(n):
            if degree[i] == 1:
                stack.append(i)

        while stack:
            result = []
            newStack = []
            for node in stack:
                result.append(node)
                for neighbor in graph[node]:
                    degree[neighbor] -= 1
                    if degree[neighbor] == 1:
                        newStack.append(neighbor)
            stack = newStack

        return result
```