```java
class Union {// 并查集模板
    int[]fa;int[]sz;int Count;// 当前连通分量数目
    public boolean united(int x,int y){x=find(x);y=find(y);return x==y;}
    public int find(int x){return fa[x]==x?x:(fa[x]=find(fa[x]));}
    public Union(int n) {//构造函数+初始化
        this.sz=new int[n];for(int i=0;i<n;i++)sz[i]=1;
        this.fa=new int[n];for(int i=0;i<n;i++)fa[i]=i;
        this.Count=0;
    }
    public void union(int x,int y) {
        x=find(x);y=find(y);
        if(sz[x]<sz[y]){x^=y;y^=x;x^=y;}//按秩合并保证 sz[x]>=sz[y]
        sz[x]+=sz[y];fa[y]=x;--Count;//把秩小的unite到大的上
    }
}

class Solution {

    public boolean G(int x,int m,int y,int n){return 0<=x&&x<m&&0<=y&&y<n;}
    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        Union set=new Union(m*n);
        int[] vis=new int[m*n];
        List<Integer>ans=new ArrayList<>();
        for(int[] p:positions){
            int i=n*p[0]+p[1],nx=p[0],ny=p[1],x=0,y=0;
            if(vis[i]==1){ans.add(set.Count);continue;}
            set.Count++;vis[i]=1;
            x=nx;y=ny+1;if(G(x,m,y,n)&&vis[i+1]==1&&!set.united(i,i+1))set.union(i,i+1);
            x=nx;y=ny-1;if(G(x,m,y,n)&&vis[i-1]==1&&!set.united(i,i-1))set.union(i,i-1);
            x=nx+1;y=ny;if(G(x,m,y,n)&&vis[i+n]==1&&!set.united(i,i+n))set.union(i,i+n);
            x=nx-1;y=ny;if(G(x,m,y,n)&&vis[i-n]==1&&!set.united(i,i-n))set.union(i,i-n);
            ans.add(set.Count);
        }
        return ans;
    }
}
```
