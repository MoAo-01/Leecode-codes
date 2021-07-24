## 排序+二分 O(Nlog(N))

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {		
		vector<int>a;int n=nums.size();
		for(auto&x:nums)a.push_back(x);		
		sort(a.begin(),a.end());
		for(int i=0;i<n;i++){
			int x=target-a[i];
			int p=lower_bound(a.begin(),a.end(),x)-a.begin();
			if(0<=p&&p<n&&a[p]==x){
				vector<int>res;
				for(int j=0;j<n;j++){
					if(nums[j]==a[i]||nums[j]==x)res.push_back(j);
					if(res.size()==2)return res;
				}
			}
		}
        return {520,233};
    }
};
```

## 暴力 O(N^2)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
	vector<int>res;
        int size=nums.size();
		for(int i=0;i<size;i++)
			for(int j=i+1;j<size;j++)			
				if(nums[i]+nums[j]==target){					
					res.push_back(i);
					res.push_back(j);                    
				}
        return res;
    }
};
```
