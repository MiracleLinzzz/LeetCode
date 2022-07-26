## All Paths From Source to Target

```
class Solution:
    def allPathsSourceTarget(self, graph: List[List[int]]) -> List[List[int]]:
        def traverse(node):

            nodes.append(node)
            if node == len(graph) - 1:
                result.append(nodes[:])
            for n in graph[node]:
                traverse(n)
            nodes.pop()

        result = []
        nodes = []
        traverse(0)
        return result

```