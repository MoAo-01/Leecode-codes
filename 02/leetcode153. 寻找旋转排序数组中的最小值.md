## O(N)

```java
class Solution {
    public int findMin(int[] nums) {
        int num=nums[0];
        for(int i=0;i+1<nums.length;i++)if(nums[i]>nums[i+1]){num=nums[i+1];break;}
        return num;
    }
}
```

## 伪O(log(N))
```java
class Solution {
    public int findMin(int[] nums) {
        int r=nums.length-1;  
        if(r<5){
            int ans=nums[0];
            for(int num:nums)if(nums[0]>num){ans=num;break;}
            return ans;
        }
        int l=0;
        while(l<r){
            int mid=(l+r)>>1;
            if(nums[mid]<nums[r])return findMin(Arrays.copyOfRange(nums,l,(mid)+1));
            else if(nums[mid]>nums[r])return findMin(Arrays.copyOfRange(nums,mid+1,(r)+1));
            else return findMin(Arrays.copyOfRange(nums,l,(r-1)+1));//可能被卡成O(n)
        }
        return nums[l];
    }
}
```
## 结合，伪O(Nlog(N))
```java
class Solution {
    public int comp(int[] nums){
        int ans=nums[0];
        for(int num:nums)if(nums[0]>num){ans=num;break;}
        return ans;
    }

    public int findMin(int[] nums) {
        int l=0,r=nums.length-1;
        if(r<5)return comp(nums);
        while(l<r){
            int mid=(l+r)>>1;
            if(nums[mid]<nums[r])return findMin(Arrays.copyOfRange(nums,l,(mid)+1));
            else if(nums[mid]>nums[r])return findMin(Arrays.copyOfRange(nums,mid+1,(r)+1));
            else return findMin(Arrays.copyOfRange(nums,l,(r-1)+1));//可能被卡成O(n)
        }
        return nums[l];
    }
}
```
