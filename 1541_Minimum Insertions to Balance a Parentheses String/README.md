## Minimum Insertions to Balance a Parentheses String


"(()))(()))()())))"  
右括号必须连续，原本就能匹配的左括号记为“L”，右括号记为“R”本例中完成匹配后应为 "(LRR)(LRR)L)LRRRR" 最右边两个未匹配右括号不连续所以是4次。

```
class Solution:
    def minInsertions(self, s: str) -> int:
        left = 0
        right = 0
        for char in s:
            # print(left, right)
            if char == '(':
                if right % 2 == 1:
                    left += 1
                    right -= 1
                right += 2
            else:
                right -= 1
                if right < 0:
                    right = 1
                    left += 1
        return left + right
```