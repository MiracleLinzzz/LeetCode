## Longest Substring Without Repeating Characters

```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        window = {}
        maxlength = 0
        left, right = 0, 0
        while right < len(s):
            char = s[right]
            right += 1
            window[char] = window.setdefault(char, 0) + 1
            while window[char] > 1:
                d = s[left]
                left += 1
                window[d] -= 1
            maxlength = max(maxlength, right-left)
        return maxlength
            
```