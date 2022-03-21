### 解题思路
裸的nim游戏变种
不知道为什么放在哈希这块
直接异或和就是答案
### 代码

```java
class Solution {
    public int singleNumber(int[] nums) {
        int ans=0;
        for(int a:nums)ans=ans^a;
        return ans;
    }
}
```
