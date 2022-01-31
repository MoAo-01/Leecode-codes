### 解题思路
自用DFS模板，还算条理清晰吧

### 代码

```java [sol-Java模板]
class Solution {
    List<List<Integer>> res=new ArrayList<List<Integer>>();
    int[] vis=new int[20];
    int[] ans=new int[20];
    int n;
    void dfs(int dep,int[]nums){
        if(dep==n){
            List<Integer> a=new ArrayList<Integer>();
            for(int i=0;i<n;i++)a.add(nums[ans[i]]);
            res.add(a);
        }
        for(int i=0;i<n;i++)
            if(vis[i]==0){
                vis[i]=1; ans[dep]=i;
                dfs(dep+1,nums);
                vis[i]=0; ans[dep]=0;
            }
    }

    public List<List<Integer>> permute(int[] nums) {
        n=nums.length;
        dfs(0,nums);
        return res;
    }
}
```
```cpp [sol-C++ STL版本]
class Solution {
public:    
    vector<vector<int>> permute(vector<int>&nums) {
        vector<vector<int>>ans;
        sort(nums.begin(),nums.end());
        do ans.push_back(nums);
        while(next_permutation(nums.begin(),nums.end()));
        return ans;
    }
};
```
