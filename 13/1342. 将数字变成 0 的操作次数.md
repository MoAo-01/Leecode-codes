### 解题思路
- 位数 + 数码 `1` 的个数 - `1`

### 代码

```cpp
class Solution {
public:
    int numberOfSteps(int num) {
        return num?(32-__builtin_clz(num))+__builtin_popcount(num)-1:0;
    }
};
```
### 思路相同
```cpp
class Solution {
public:
    int numberOfSteps(int num) {
        return num?(int)(ceil(log(num+1)/log(2)))+bitset<32>(num).count()-1:0;
    }
};
```
