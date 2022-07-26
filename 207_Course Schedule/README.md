## Course Schedule

```
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        def traverse(node):
            if onPath[node]:
                self.hasCycle = True 
            if visited[node] or self.hasCycle:
                return 

            onPath[node] = True
            visited[node] = True
            for n in graph[node]:
                traverse(n)
            onPath[node] = False


        graph = self.buildGraph(numCourses, prerequisites)
        onPath = [False for _ in range(numCourses)]
        visited = [False for _ in range(numCourses)]
        self.hasCycle = False
        for i in range(numCourses):
            traverse(i)
        return not self.hasCycle


    def buildGraph(self, numCourses: int, prerequisites: List[List[int]]):
        graph = []
        for i in range(numCourses):
            graph.append([])
        for path in prerequisites:
            nodeFrom = path[1]
            nodeTo = path[0]
            graph[nodeFrom].extend([nodeTo])
        return graph
```