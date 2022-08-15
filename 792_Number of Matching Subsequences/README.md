## Number of Matching Subsequences


还有其他思路
```
class Solution:
    def numMatchingSubseq(self, s: str, words: List[str]) -> int:
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
        for i in range(len(s)):
            if dic.get(s[i]) == None:
                dic[s[i]] = [i]
            else:
                dic[s[i]].append(i)
        
        count = 0
        for word in words:
            index = 0
            n = len(word)
            i = 0
            while i < n:
                if dic.get(word[i]) == None:
                    break
                index = left_bound(dic[word[i]], index)
                if index == -1:
                    break
                index = dic[word[i]][index] + 1  
                i += 1
            if i == n:
                count += 1
        return count
```