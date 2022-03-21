### 解题思路
单项扫描，移动指针cnt读入

### 代码

```java
class Solution {
    public int removeElement(int[] nums, int val) {
	int cnt=0;
	for(int num:nums)if(num!=val)nums[cnt++]=num;		
	return cnt;
    }
}
```
