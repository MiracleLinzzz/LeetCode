## Longest Common Prefix

```
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        res = ""
        flag = 0
        for i in range(len(strs[0])):
            prefix = strs[0][i]
            for word in strs:
                try:
                    if prefix != word[i]:
                        flag = 1
                        return res
                except:
                    return res
            if flag == 0:
                res += prefix
            else:
                break
        return res
```