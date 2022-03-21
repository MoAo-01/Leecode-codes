## 叉积
```cpp
class Solution {
public:
    double largestTriangleArea(vector<vector<int>>& points) {
        vector<pair<int,int>>P;
        for(auto&point:points)
            P.push_back(make_pair(point[0],point[1]));
        double ans=-1.0;
        for(int i=0;i<P.size();i++)
            for(int j=i+1;j<P.size();j++)
                for(int k=j+1;k<P.size();k++){
                    int a=P[i].first-P[j].first,b=P[i].second-P[j].second;
                    int c=P[k].first-P[j].first,d=P[k].second-P[j].second;
                    ans=max(ans,fabs(a*d-b*c)*0.5);
                }
        return ans;              
    }
};
```
