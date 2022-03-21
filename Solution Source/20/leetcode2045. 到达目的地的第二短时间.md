### 解题思路
- 按照普通版本的迪杰斯特拉算法松弛
- 优先队列带入**三个**属性
- `[t,c,u]=[到达前继结点(u)已用时间, 经过等待到达后继结点(v)用时, 前继结点(u)]`
- **不同点：** 每个结点可以有**两个**可以松弛的属性
- 即，最短距离 `t1` 与次短距离 `t2`

### 代码

```cpp
const int INF=1e9;
typedef tuple<int,int,int> III;

class Solution {
public:
    int secondMinimum(int n, vector<vector<int>>& edges,int time,int change) {
        vector<vector<int>>adj(n);
        for(auto&edge:edges){
            int u=edge[0]-1,v=edge[1]-1;
            adj[u].push_back(v);
            adj[v].push_back(u);
        }        
        vector<int>t1(n,INF),t2(n,INF);//到达下标表示点的第一和第二短的消耗时间
        priority_queue<III,vector<III>,greater<III>>pq;
        pq.emplace(t1[0]=0,0,0);
        while(!pq.empty()){
            auto[t,c,u]=pq.top();pq.pop();
            if(t>t2[u])continue;
            for(int v:adj[u]){
                int tt=c+time;
                int remain=tt%(change*2);
                int cc=(remain>=change)?(tt/(change*2)+1)*(change*2):(tt);
                if(tt<t1[v]){pq.emplace(t1[v]=tt,cc,v);continue;}
                if(t1[v]<tt && tt<t2[v]){pq.emplace(t2[v]=tt,cc,v);continue;}
            }
        }
        return t2[n-1];
    }
};
```
