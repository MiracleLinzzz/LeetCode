## Add Binary

### 模拟 竖式运算

```
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        index1 = len(a) - 1
        index2 = len(b) - 1
        carry = 0
        result = ""
        while index1 >= 0 or index2 >= 0 or carry > 0:
            carry += (int(a[index1]) if index1 >=0 else 0) + (int(b[index2]) if index2 >=0 else 0)
            result = str(carry % 2) + result
            carry = carry // 2
            index1 -= 1
            index2 -= 1
        return result 
```


### 位运算
