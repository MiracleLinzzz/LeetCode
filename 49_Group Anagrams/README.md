## Group Anagrams

### 排序方法

每一个anagram都有相同组合的字母，排序之后的字母是相同的，可以作为字典的键  
**Attention:** list和set 不能作为字典的键（unhashable）？

```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        result = []
        dic = {}
        for word in strs:
            anagram = "".join(sorted(word))
            if not dic.get(anagram):
                dic[anagram] = [word]
            else:
                dic[anagram].append(word)
        return list(dic.values())
```