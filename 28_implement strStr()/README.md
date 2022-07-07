# 朴素解法
* 匹配串可能比原串要长
* 两个index要一起运动
* 空串情况
```
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if not needle:
            return 0

        for i in range(len(haystack)-len(needle)+1):
            flag = True
            for j in range(len(needle)):
                if haystack[i+j] != needle[j]:
                    flag = False
                    break
            
            if flag:
                return i
        
        return -1
```