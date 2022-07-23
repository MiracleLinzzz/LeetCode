## Permutation in String

```
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        if len(s1)>len(s2):
            return False
        needs = {}
        for char in s1:
            needs[char] = needs.setdefault(char, 0) + 1
        
        windows = {}
        left = 0
        right = len(s1)-1
        for i in range(len(s1)-1):
            windows[s2[i]] = windows.setdefault(s2[i], 0) + 1
        while right < len(s2):
            char = s2[right]
            windows[char] = windows.setdefault(char, 0) + 1
            if windows == needs:
                return True
            right += 1

            d = s2[left]
            windows[d] -= 1
            if not windows.get(d):
                windows.pop(d)
            left += 1
        return False
```