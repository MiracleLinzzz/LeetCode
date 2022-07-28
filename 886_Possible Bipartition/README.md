## Possible Bipartition

构建邻接表（无向图）  
二分图染色问题

```
class Solution:
    def possibleBipartition(self, n: int, dislikes: List[List[int]]) -> bool:
        graph = self.buildGraph(n, dislikes)
        visited = [False for _ in range(n)]
        color = [False for _ in range(n)]
        for i in range(n):
            queue = deque()
            queue.append(i)
            while queue:
                node = queue.popleft()
                for neighbor in graph[node]:
                    if not visited[neighbor]:
                        color[neighbor] = not color[node]
                        visited[neighbor] = True
                        queue.append(neighbor)
                    else:
                        if color[neighbor] == color[node]:
                            return False
    
        return True
    

    def buildGraph(self, num: int, dislikes: List[List[int]]) -> List[List[int]]:
        graph = []
        for i in range(num):
            graph.append([])
        for dislike in dislikes:
            graph[dislike[0]-1].append(dislike[1]-1)
            graph[dislike[1]-1].append(dislike[0]-1)
        return graph
```