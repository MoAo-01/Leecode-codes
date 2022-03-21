### 解题思路
dfs板子题，没有优化的写法，只需维护横竖撇捺四个方向的数字用于记录出现的皇后位置即可
每次从搜索的当前位置再往后搜索即可，之前的位置必不可能放下之后的皇后。

### 代码

```java
class Solution {
    String[][] q =new String[10][10];
    List<List<String>>ans =new ArrayList();
    int[] r=new int[10];//row=n
    int[] c=new int[10];//column=n
    int[] a=new int[20];//a=x-y+n
    int[] b=new int[20];//b=x+y
    int n;
    boolean check(int x,int y){//x row, y col
        if(r[x]==1||c[y]==1||a[x-y+n]==1||b[x+y]==1)return false;
        return true;
    }

    void addResultToAns(){
        ArrayList<String> res=new ArrayList();
        for(int i=1;i<=n;i++) {
            String line="";
            for(int j=1;j<=n;j++)line+=q[i][j];
            res.add(line);
        }
        ans.add(res);
    }

    void dfs(int last_i,int last_j,int dep){
        if(dep==n){
            addResultToAns();
            return;
        }
        for(int i=last_i;i<=n;i++)
            for(int j=i==last_i?last_j+1:1;j<=n;j++){
                if(check(i,j)){
                    r[i]=1;c[j]=1;a[i-j+n]=1;b[i+j]=1;
                    q[i][j]="Q";dfs(i,j,dep+1);q[i][j]=".";
                    r[i]=0;c[j]=0;a[i-j+n]=0;b[i+j]=0;
                }
            }
    }

    public List<List<String>> solveNQueens(int n) {
        this.n=n;
        for(int i=1;i<=n;i++)for(int j=1;j<=n;j++)q[i][j]=".";
        dfs(1,0,0);
        return ans;
    }
}
```
