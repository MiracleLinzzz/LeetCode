## Length of Last Word

```
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        
        count = len(s) - 1
        while count >= 0 and s[count] == " ":
            count -= 1
        temp = count
        while count >= 0 and s[count] != " ":
            count -= 1
        return temp - count

```