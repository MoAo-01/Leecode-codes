- 质因数分解，质因子 $2$ 必然比 $5$ 多
- 所以只需求质因子 $5$ 的个数
- 考虑迭代法

```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    int trailingZeroes(int n) {
        int sum=0;
        while(n>0){
            sum+=n/5;
            n/=5;
        }
        return sum;
    }
};
```
