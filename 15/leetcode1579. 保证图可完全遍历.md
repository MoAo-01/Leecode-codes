### 解题思路
并查集:
没什么好说的，一般来说为了保证复杂度稳定在哈弗曼常数下;
需要采取:   路径压缩(find)+按秩合并(union);

### 代码

```java

class UnionFind {// 并查集模板
    int setCount;// 当前连通分量数目
    int[] fa;
    int[] sz;
    int n;
    public boolean united(int x, int y) { x = find(x);y = find(y);return x==y; }
    public int find(int x) { return fa[x] == x ? x : (fa[x] = find(fa[x])); }
    private void swap(int x, int y) { x=x^y;y=x^y;x=x^y; }
    public UnionFind(int n) {//构造函数+初始化
        this.sz = new int[n];for (int i = 0; i < n; i++)sz[i] = 1;
        this.fa = new int[n];for (int i = 0; i < n; i++)fa[i] = i;
        this.setCount = n;
        this.n = n;
    }
    public boolean union(int x, int y) {
        x = find(x);
        y = find(y);
        if (x == y) return false;
        if (sz[x] < sz[y])swap(x,y);//按秩合并保证 sz[x]>=sz[y]
        sz[x] += sz[y];//把秩小的unite到大的上
        fa[y] = x;
        --setCount;
        return true;
    }
}

class Solution {
    public int maxNumEdgesToRemove(int n, int[][] edges) {
        UnionFind ufa = new UnionFind(n);//初始化 Alice 森林
        UnionFind ufb = new UnionFind(n);//初始化 Bob 森林
        int ans = 0;
        for (int[] e : edges) { --e[1];--e[2]; }// 节点编号改为从 0 开始
        for (int[] e : edges)
            if (e[0] == 3)// 公共边
                if(ufa.united(e[1],e[2]))ans++;
                else {
                    ufa.union(e[1], e[2]);
                    ufb.union(e[1], e[2]);
                }
        for (int[] e : edges) {// 独占边
            if (e[0] == 1) if (!ufa.union(e[1], e[2])) ans++;// Alice 独占边
            if (e[0] == 2) if (!ufb.union(e[1], e[2])) ans++;// Bob 独占边
        }
        if (ufa.setCount != 1 || ufb.setCount != 1) return -1;
        return ans;
    }
}
```
