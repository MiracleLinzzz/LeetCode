## Is Graph Bipartite?

二分图染色问题

### DFS
```
class Solution:
    def isBipartite(self, graph: List[List[int]]) -> bool:
        def traverse(node):
            if not self.result:
                return
            
            visited[node] = True
            for n in graph[node]:
                if not visited[n]:
                    color[n] = not color[node]
                    traverse(n)
                else:
                    if color[n] == color[node]:
                        self.result = False
            return self.result
        
        self.result = True
        color = [False for _ in range(len(graph))]
        visited = [False for _ in range(len(graph))]
        for i in range(len(graph)):
            traverse(i)
        return self.result 

```

### BFS

```
class Solution:
    def isBipartite(self, graph: List[List[int]]) -> bool:
        
        result = True
        color = [False for _ in range(len(graph))]
        visited = [False for _ in range(len(graph))]

        for i in range(len(graph)):
            queue = [i]
            while queue and result:
                node = queue.pop(0)
                for neighbor in graph[node]:
                    if not visited[neighbor]:
                        visited[neighbor] = True
                        color[neighbor] = not color[node]
                        queue.append(neighbor)
                    else:
                        if color[neighbor] == color[node]:
                            result = False
                            break
        return result 
```