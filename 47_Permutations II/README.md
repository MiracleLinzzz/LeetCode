## Permutations II


### 回溯问题三要素
把和 46.全排列 的区别--重复，考虑了之后，这道题就是和我们之前写过的思考过程一样了，依然是回到老三样：

#### 有效结果
仍然是当前结果的长度==列表的长度，即为找到了一个有效结果

```
if len(sol) == len(nums):
            self.res.append(sol)
```


#### 回溯范围及答案更新
仍然是全部遍历，因为每一层都要考虑全部元素
答案更新仍然是在修改 check 之后回溯内部累加更新 sol

```
for i in range(len(nums)):
    check[i] = 1
    self.backtrack(sol+[nums[i]], nums, check)
    check[i] = 0
```

#### 剪枝条件
在之前的 剪枝条件1：用过的元素不能再使用之外，又添加了一个新的剪枝条件，也就是我们考虑重复部分思考的结果，于是 剪枝条件2：当当前元素和前一个元素值相同（此处隐含这个元素的 index>0 ），并且前一个元素还没有被使用过的时候，我们要剪枝

```
# 防止当前数字重复
if check[i] == 1:
    continue
# 防止出现重复结果 并且 不会漏掉结果
if i > 0 and nums[i] == nums[i-1] and check[i-1] == 0:
    continue
```

### 提速注意点
- int和bool转换需要时间 
- 内部函数和外部函数没什么差别
  
### 代码
```
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:

        def backtrack(permutation: List[int], used: List[int]):
            if len(permutation) == size:
                permutations.append(permutation[:])
                return 
            
            for idx in range(size):
                if used[idx] == 1:
                    continue
                if idx > 0 and nums[idx] == nums[idx-1] and used[idx-1] == 0:
                    continue
                used[idx] = 1
                backtrack(permutation + [nums[idx]], used)
                used[idx] = 0

        
        size = len(nums)
        used = [0] * size
        permutations = []
        nums.sort()
        
        backtrack([], used)

        return permutations
```