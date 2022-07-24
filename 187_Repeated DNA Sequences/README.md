## Repeated DNA Sequences


Rabin-Karp字符串匹配算法  
有点是原本进行字符串匹配时的复杂度是O(NL)，N是字符串长度，L是匹配字符串长度。现在的复杂度是O(N)，因为比对目标字符串时，运用哈希值优化使得复杂度变为了O(1)

```
/* 在最低位添加一个数字 */
// number 的进制
int R = 4;
// 想在 number 的最低位添加的数字
int appendVal = 0~3 中的任意数字;
// 运算，在最低位添加一位
number = R * number + appendVal;

/* 在最高位删除一个数字 */
// number 的进制
int R = 4;
// number 最高位的数字
int removeVal = 0~3 中的任意数字;
// 此时 number 的位数
int L = ?;
// 运算，删除最高位数字
number = number - removeVal * R^(L-1);
```
算法模板：
```
// 文本串
String txt;
// 模式串
String pat;


// 需要寻找的子串长度为模式串 pat 的长度
int L = pat.length();
// 仅处理 ASCII 码字符串，可以理解为 256 进制的数字
int R = 256;
// 存储 R^(L - 1) 的结果
int RL = (int) Math.pow(R, L - 1);
// 维护滑动窗口中字符串的哈希值
int windowHash = 0;
// 计算模式串的哈希值
long patHash = 0;
for (int i = 0; i < pat.length(); i++) {
    patHash = R * patHash + pat.charAt(i);
}

// 滑动窗口代码框架
int left = 0, right = 0;
while (right < txt.length()) {
    // 扩大窗口，移入字符（在最低位添加数字）
    windowHash = R * windowHash + txt[right];
    right++;

    // 当子串的长度达到要求
    if (right - left == L) {
        // 根据哈希值判断窗口中的子串是否匹配模式串 pat
        if (patHash == windowHash) {
            // 找到模式串
            print("找到模式串，起始索引为", left);
            return left;
        }
        
        // 缩小窗口，移出字符（删除最高位数字）
        windowHash = windowHash - txt[left] * RL;
        left++;
    }
}
// 没有找到模式串
return -1;
```


Code：
```
class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        maps = {'A':0, 'C':1, 'G':2, 'T':3}
        seen = {}
        result = set()
        L = 10
        R = 4
        RL = R**(L-1)
        windowHash = 0
        left, right = 0,0
        while right < len(s):
            windowHash = R*windowHash + maps[s[right]]
            right += 1

            if right - left == L:
                if seen.get(windowHash):
                    result.add(s[left:right])
                else:
                    seen[windowHash] = 1
                
                windowHash = windowHash - maps[s[left]] * RL
                left += 1

        return list(result)
``` 