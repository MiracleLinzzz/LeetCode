## Combination Sum


combinations.append(combination[:])  
和  
combinations.append(combination)  
区别在哪？


变量 path 所指向的列表 在深度优先遍历的过程中只有一份 ，深度优先遍历完成以后，回到了根结点，成为空列表。

在 Java 中，参数传递是 值传递，对象类型变量在传参的过程中，复制的是变量的地址。这些地址被添加到 res 变量，但实际上指向的是同一块内存地址，因此我们会看到 66 个空的列表对象。解决的方法很简单，在 res.add(path); 这里做一次拷贝即可。



```
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:

        def backtrack(combination, start, Sum):
            if Sum == target:
                combinations.append(combination[:])
                # print(combinations, combination)
                return
            
            if Sum > target:
                return
            
            for idx in range(start, len(candidates)):
                combination.append(candidates[idx])
                # print(combination)
                Sum += candidates[idx]
                backtrack(combination, idx, Sum)
                Sum -= candidates[idx]
                combination.pop()

        combination = []
        combinations = []
        backtrack(combination, 0, 0)
        return combinations
```