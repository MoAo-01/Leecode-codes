## 滑动窗口
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int[]next=new int[512];
        int ans=0;
        for(int l=0,r=0;r<s.length();r++) {
            l=Math.max(l,next[s.charAt(r)]);
            next[s.charAt(r)]=r+1;
            ans=Math.max(ans,r-l+1);
        }
        return ans;
    }
}
```
