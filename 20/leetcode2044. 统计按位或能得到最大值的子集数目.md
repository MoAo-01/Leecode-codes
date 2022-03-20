### 解题思路
- 话不多说，抛弃`DFS`吧
- 01枚举，我们直接上位运算

### 代码

```cpp
class Solution {
public:
    int countMaxOrSubsets(vector<int>& nums) {
        int maxOr=INT_MIN,cnt=0;
        int n=nums.size();
        for(int mask=1;mask<(1<<n);mask++){
            int sum=0;
            for(int i=0;i<n;i++){
                if(mask&(1<<i)){
                    sum|=nums[i];
                }
            }
            if(sum==maxOr)cnt++;
            else if(sum>maxOr){
                maxOr=sum;
                cnt=1;
            }
        }
        return cnt;
    }
};
```
### 相关题表
|  题目   | 题解  | 难度|
|  -------  | ----  | ---- |
| [22. 括号生成](https://leetcode-cn.com/problems/generate-parentheses/)  | [题解](https://leetcode-cn.com/problems/generate-parentheses/solution/mo-ao-wei-yun-suan-01mei-ju-by-moao-s4fa/) |🤣🤣|
| [2044. 统计按位或能得到最大值的子集数目](https://leetcode-cn.com/problems/count-number-of-maximum-bitwise-or-subsets/)  | [题解](https://leetcode-cn.com/problems/count-number-of-maximum-bitwise-or-subsets/solution/mo-ao-by-moao-mzok/)|🤣🤣|
| [320. 列举单词的全部缩写](https://leetcode-cn.com/problems/generalized-abbreviation/)  | [题解](https://leetcode-cn.com/problems/generalized-abbreviation/solution/mo-ao-01mei-ju-zhuang-tai-ya-suo-you-ya-c03j9/) |🤣🤣|
|[1723. 完成所有工作的最短时间](https://leetcode-cn.com/problems/find-minimum-time-to-finish-all-jobs/)|[题解](https://leetcode-cn.com/problems/find-minimum-time-to-finish-all-jobs/solution/mo-ao-zhuang-ya-dp-by-moao-0926/)|🤣🤣🤣🤣|
|[1681. 最小不兼容性](https://leetcode-cn.com/problems/minimum-incompatibility/)|[题解](https://leetcode-cn.com/problems/minimum-incompatibility/solution/mo-ao-zhuang-ya-dp-by-moao-akqa/)|🤣🤣🤣🤣🤣|
