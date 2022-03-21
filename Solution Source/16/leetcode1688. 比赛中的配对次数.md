### 解题思路
- 数学归纳法：
    - 当`n=1`时，`ans=0`
    - 当`n=2`时，`ans=1`
    - 当`n=3`时，`ans=2`
- 不妨设：
    - 当`n=N`时，`ans=N-1`
- 对于：
    - 当`n=N+1`时，`ans=(N-1)+1=N`
- 所以
    - `numberOfMatches(n)=n-1`

### 代码

```cpp
class Solution {
public:
    int numberOfMatches(int n) {
        return n-1;
    }
};
```
### 暴力验证
```cpp
class Solution {
public:
    int numberOfMatches(int n) {
        int count=0;
        while(n>1)count+=n/2,n-=n/2;
        return count;
    }
};
```
- 根据题意，写出暴力
- 注意到 $n/2$ 多次出现
    - 令 $x=n/2$
    - $\therefore$ $\Delta count$+$\Delta n$$=x+(-x)=0$
    - $\therefore count=\Sigma\Delta count=-\Sigma\Delta n=n-1$
