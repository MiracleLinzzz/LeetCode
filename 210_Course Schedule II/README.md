## Course Schedule II


拓扑排序其实就是图遍历的后序结果 翻转/不翻转

```
class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        graph = self.buildGraph(numCourses, prerequisites)
        self.result = []
        self.hasCycle = False
        self.onPath = [False for _ in range(numCourses)]
        self.visited = [False for _ in range(numCourses)]
        for i in range(numCourses):
            self.traverse(graph, i)
        self.result.reverse()
        return self.result if not self.hasCycle else []

    def traverse(self, graph, node):
        if self.onPath[node]:
            self.hasCycle = True
        if self.visited[node] or self.hasCycle:
            return

        self.onPath[node] = True
        self.visited[node] = True
        for n in graph[node]:
            self.traverse(graph, n,)
        self.result.append(node)
        self.onPath[node] = False


    def buildGraph(self, numCourses:int, prerequisites: List[List[int]]) -> List[List[int]]:
        graph = []
        for _ in range(numCourses):
            graph.append([])
        for prerequisite in prerequisites:
            graph[prerequisite[1]].append(prerequisite[0])
        return graph
```