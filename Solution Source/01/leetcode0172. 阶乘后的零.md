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


```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    vector<int>fives{
        (int)pow(5,1),
        (int)pow(5,2),
        (int)pow(5,3),
        (int)pow(5,4),
        (int)pow(5,5),
        (int)pow(5,6),
        (int)pow(5,7),
        (int)pow(5,8),
        (int)pow(5,9),
        (int)pow(5,10),
        (int)pow(5,11)
    };

    int sum(int&n){
        int ans=0;
        for(auto&five:fives)ans+=n/five;
        return ans;
    }

    int trailingZeroes(int n) {
        return sum(n);
    }
};
```
