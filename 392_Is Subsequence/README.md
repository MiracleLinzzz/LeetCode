## Is Subsequence

### 经典的双指针写法
时间复杂度O(N)
```
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        left = 0
        right = 0
        while left < len(s):
            if right >= len(t):
                return False
            if s[left] == t[right]:
                left += 1
            right += 1
            
        return True
```

### 花里胡哨的二分查找 复用思想
时间复杂度O(MlogN) M < N
```
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        
        def left_bound(array, target):
            left = 0
            right = len(array)
            while left < right:
                mid = left + (right - left) // 2
                if array[mid] >= target:
                    right = mid
                elif array[mid] < target:
                    left = mid + 1
            if left == len(array):
                return -1
            return left

        dic = {}
        for i in range(len(t)):
            if dic.get(t[i]) == None:
                dic[t[i]] = [i]
            else:
                dic[t[i]].append(i)
        index = 0
        for char in s:
            if dic.get(char) == None:
                return False
            index = left_bound(dic[char], index)
            if index == -1:
                return False
            index = dic[char][index] + 1
        return True
```