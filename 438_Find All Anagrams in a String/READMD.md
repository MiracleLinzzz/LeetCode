## Find All Anagrams in a String


通用模板

```
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        needs = {}
        for char in p:
            needs[char] = needs.setdefault(char, 0) + 1

        windows = {}
        left, right = 0, 0
        result = []
        valid = 0
        while right < len(s):
            char = s[right]
            right += 1
            if needs.get(char):
                windows[char] = windows.setdefault(char, 0) + 1
                if windows[char] == needs[char]:
                    valid += 1
            
            while valid == len(needs):
                if right - left == len(p):
                    result.append(left)
                d = s[left]
                left += 1
                if needs.get(d):
                    if windows[d] == needs[d]:
                        valid -= 1
                    windows[d] -= 1
                
        return result

```


固定窗口长度 感觉还有优化空间
```
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        if len(p) > len(s):
            return []
        needs = {}
        for char in p:
            needs[char] = needs.setdefault(char, 0) + 1

        windows = {}
        left, right = 0, len(p)-1
        result = []
        valid = 0
        for i in range(len(p)-1):
            char = s[i]
            windows[char] = windows.setdefault(char, 0) + 1
        while right < len(s):
            windows[s[right]] = windows.setdefault(s[right], 0) + 1
            right += 1
            if windows == needs:
                result.append(left)
            windows[s[left]] -= 1
            if windows[s[left]] == 0:
                windows.pop(s[left])
            left += 1
            
```