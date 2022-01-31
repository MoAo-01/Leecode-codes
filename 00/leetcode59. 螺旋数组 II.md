```java
class Solution {
    public static int tx[]={0,1,0,-1};
    public static int ty[]={1,0,-1,0};

    public static void dfs(int[][] A,int x,int y,int dep,int n,int last){
        if(dep==n*n)return;
        A[x][y]=dep+1;

        int xxx=x+tx[last],yyy=y+ty[last];
        if(0<=xxx&&xxx<n && 0<=yyy&&yyy<n && A[xxx][yyy]==0)
            dfs(A,xxx,yyy,dep+1,n,last);

        for(int i=0;i<4;i++){
            int xx=x+tx[i],yy=y+ty[i];
            if(0<=xx&&xx<n && 0<=yy&&yy<n && A[xx][yy]==0)
                dfs(A,xx,yy,dep+1,n,i);
        }
    }

    public static int[][] generateMatrix(int n) {
        int[][] A=new int[n][n];
        dfs(A,0,0,0,n,0);
        return A;
    }
}
```
```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
    ret=[[0 for _ in range(n)]for _ in range(n)]
    i,j,di,dj=0,0,0,1
    for a in range(n**2):
        ret[i][j]=a+1
        if ret[(i+di)%n][(j+dj)%n]>0:
            di,dj=dj,-di
        i+=di
        j+=dj
    return ret
```
