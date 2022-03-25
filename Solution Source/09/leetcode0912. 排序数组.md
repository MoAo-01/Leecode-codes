- 随机化 + 快速排序


```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    void quick_sort(vector<int>&a){
        if(a.size()<=1)return;
        vector<int>l_a;
        vector<int>r_a;
        int p=a.back(); a.pop_back();

        for(auto&v:a)
            (v<=p)?
                l_a.push_back(v):
                r_a.push_back(v);        

        quick_sort(l_a);
        quick_sort(r_a);
        
        a.clear();

        for(auto&v:l_a)a.push_back(v);
        a.push_back(p);
        for(auto&v:r_a)a.push_back(v);
    }


    vector<int> sortArray(vector<int>& nums) {
        random_shuffle(begin(nums),end(nums));
        quick_sort(nums);
        return nums;
    }
};
```
