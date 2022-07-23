## Minimum Window Substring

滑动窗口

```
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        needs = {}
        for char in t:
            needs[char] = needs.setdefault(char, 0) + 1
        
        windows = {}
        left, right = 0, 0
        valid = 0
        start = 0
        end = 0
        while right < len(s):
            char = s[right]
            right += 1
            if needs.get(char):
                windows[char] = windows.setdefault(char, 0) + 1
                if windows[char] == needs[char]:
                    valid += 1

            while valid == len(needs):
                if not end or right - left < end - start:
                    start = left
                    end = right
                char = s[left]
                left += 1
                if needs.get(char):
                    if windows[char] == needs[char]:
                        valid -= 1
                    windows[char] -= 1

        return s[start:end]


        
```