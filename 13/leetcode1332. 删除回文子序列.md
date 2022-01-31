### 解题思路
- 首先，对于回文串，答案为 `1`
- 其次，由于字符串仅由 `a` 或 `b` 组成
- 所以我们一定可以用两次删除，分别取出所有 `a` 和 `b`
- 满足条件，此时答案为 `2`

### 代码
```cpp [1-C++ 简洁版]
class Solution {
public:
    int removePalindromeSub(string s) {
        return string(rbegin(s),rend(s))==s?1:2;
    }
};
```

```python [1-Python3]
class Solution:
    def removePalindromeSub(self, s: str) -> int:
        return 1 if s==s[::-1]else 2
```
```java [1-Java]
class Solution {
    public int removePalindromeSub(String s) {
        return (s.equals(new StringBuilder(s).reverse().toString())?1:2);
    }
}
```
```cpp [1-C++ 原版]
class Solution {
public:
    int removePalindromeSub(string s) {
        auto palindrome=[](string&s)->bool{
            string s0=s;
            reverse(begin(s),end(s));
            return s==s0;
        };
        return palindrome(s)?1:2;
    }
};
```
