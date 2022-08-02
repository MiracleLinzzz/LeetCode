## LRU Cache

```
class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.map = {}
        self.cache = DoubleList()

    def get(self, key: int) -> int:
        if self.map.get(key) == None:
            return -1
        self.makeRecently(key)
        return self.map[key].value

    def put(self, key: int, value: int) -> None:
        if self.map.get(key) != None:
            self.deleteKey(key)
            # self.addRecently(key, value)
            # return 

        elif self.capacity == self.cache.size:
            self.removeLeastRecently()
        self.addRecently(key, value)

    def makeRecently(self, key: int) -> None:
        x = self.map.get(key)
        self.cache.remove(x)
        self.cache.addLast(x)

    def addRecently(self, key: int, value: int) -> None:
        x = Node(key, value)
        self.cache.addLast(x)
        self.map[key] = x

    def deleteKey(self, key: int) -> None:
        x = self.map.get(key)
        self.cache.remove(x)
        del self.map[key]
    
    def removeLeastRecently(self) -> None:
        deletedNode = self.cache.removeFirst()
        deletedKey = deletedNode.key
        del self.map[deletedKey]


class Node:
    def __init__(self, key=0, value=0):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None

class DoubleList:
    def __init__(self):
        self.head = Node(0, 0)
        self.tail = Node(0, 0)
        self.head.next = self.tail
        self.tail.prev = self.head
        self.size = 0

    def addLast(self, x:Node):
        x.prev = self.tail.prev
        x.next = self.tail
        self.tail.prev.next = x
        self.tail.prev = x
        self.size += 1

    def remove(self, x:Node):
        x.prev.next = x.next
        x.next.prev = x.prev
        self.size -= 1
    
    def removeFirst(self):
        if self.head.next == self.tail:
            return 
        first = self.head.next
        self.remove(first)
        return first
    
    def size(self):
        return self.size

# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```