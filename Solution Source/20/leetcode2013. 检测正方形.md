### 解题思路
- 枚举边长 `d`
- 对于给定点 `p` 的: 左下、右上、左上、右下 $4$ 个方向统计

### 代码

```cpp
class DetectSquares {
public:
    int map[1001][1001],dx[4]={-1,1,-1,1},dy[4]={-1,-1,1,1};

    DetectSquares(){memset(map,0,sizeof(map));}
    void add(vector<int> p){map[p[0]][p[1]]++;}

    int count(int d,int x,int y){
        int ans=0;
        for(int i=0;i<4;i++){
            int nx=x+dx[i]*d,ny=y+dy[i]*d;
            ans+=(0<=nx&&nx<=1000 && 0<=ny&&ny<=1000)?map[nx][y]*map[x][ny]*map[nx][ny]:0;
        }
        return ans;
    }    

    int count(vector<int> p) {
        int ans=0,&x=p[0],&y=p[1];
        for(int d=1;d<=1000;d++)ans+=count(d,x,y);
        return ans;
    }
};
```
