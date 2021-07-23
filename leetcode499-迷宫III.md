### 解题思路
- 搜索模板题

### 代码

```cpp
struct node{
    int x,y,d;string path;
    node(int x,int y,int d,string path):x(x),y(y),d(d),path(path){}
    bool operator<(const node&t)const{return(d==t.d)?path>t.path:d>t.d;}
};
class Solution{
public:
    int dx[4]={0,1,0,-1},dy[4]={1,0,-1,0};char ds[4]={'r','d','l','u'};
    string findShortestWay(vector<vector<int>>&maze,vector<int>&ball,vector<int>&hole) {
        priority_queue<node>q;
        int n=maze.size(),m=maze[0].size();
        vector<vector<int>>dis(n,vector<int>(m,1e9));
        auto end=[&](int x,int y){return x==hole[0] && y==hole[1];};        
        auto ok=[&](int x,int y){return 0<=x&&x<n && 0<=y&&y<m && !maze[x][y];};        
        q.push(node(ball[0],ball[1],0,"")),dis[ball[0]][ball[1]]=0;
        while(!q.empty()){
            auto u=q.top();q.pop();
            int x=u.x,y=u.y,d=u.d;string s=u.path;
            if(end(x,y))return s;
            for(int i=0;i<4;i++){
                int nx=x,ny=y,nd=d;string ns=s+ds[i];
                while(ok(nx+dx[i],ny+dy[i])){
                    nx+=dx[i],ny+=dy[i],nd++;
                    if(end(nx,ny))break;
                }
                if(d<nd && nd<=dis[nx][ny])
                    q.push(node(nx,ny,nd,ns)),dis[nx][ny]=nd;                
            }
        }
        return "impossible";
    }
};
```
