## 舞蹈链
### Java
```java
class DLX {
    int n,m,si;//n行数m列数si目前有的节点数
    int[] U,D,L,R,Row,Col;//结点信息 [MAXNODE]
    int[] H,ans;int ansd;//H[r] 第r行头指针 ans[d]记录答案，当前搜索（深度）行 [MAXN]
    int[] S;//S[c] 第c列存在结点数 [MAXM]
    public DLX(int n){
        int maxn=n*n*n+10;
        int maxm=n*n*4+10;
        int maxnode=maxn*4+maxm;
        L=new int[maxnode];R=new int[maxnode];Col=new int[maxnode];
        U=new int[maxnode];D=new int[maxnode];Row=new int[maxnode];
        H=new int[maxn];ans=new int[maxn];
        S=new int[maxm];
    }

    public void init(int n,int m){  //初始化空表
        this.n=n;
        this.m=m;
        for(int i=0;i<=m;i++){ //初始化第一横行（表头）            
            S[i]=0;U[i]=D[i]=i;//目前纵向的链是空的
            L[i]=i-1;R[i]=i+1; //横向的连起来
        }
        R[m]=0;L[0]=m;
        si=m;
        for(int i=1;i<=n;i++)H[i]=-1;
    }

    public void link(int r,int c){    //插入点(r,c)
        ++S[Col[++si]=c];Row[si]=r;
        D[si]=D[c]; U[D[c]]=si; U[si]=c; D[c]=si;//核心代码.1上下连表
        if(H[r]==-1)H[r]=L[si]=R[si]=si;
        else{R[si]=R[H[r]]; L[R[H[r]]]=si; L[si]=H[r]; R[H[r]]=si;}
        //核心代码.2左右连表
    }

    public void remove(int c){//列表中删掉c列
        L[R[c]]=L[c];//表头操作
        R[L[c]]=R[c];
        for(int i=D[c];i!=c;i=D[i])
            for(int j=R[i];j!= i;j=R[j]){
                U[D[j]]=U[j];
                D[U[j]]=D[j];
                --S[Col[j]];
            }
    }

    public void resume(int c){//恢复c列
        for(int i=U[c];i!=c;i=U[i])
            for(int j=L[i];j!=i;j=L[j])
                ++S[Col[U[D[j]]=D[U[j]]=j]];
        L[R[c]]=R[L[c]]=c;
    }

    public boolean dance(int d){ //选取了d行
        if(R[0]==0){ansd=d;return true;}//全部覆盖了
        int c=R[0];
        for(int i=R[0];i!=0;i=R[i])if(S[i]<S[c])c=i;
        remove(c);
        for(int i=D[c];i!=c;i=D[i]){
            ans[d]=Row[i];
            for(int j=R[i];j!= i;j=R[j])remove(Col[j]);
            if(dance(d+1))return true;
            for(int j=L[i];j!=i;j=L[j])resume(Col[j]);
        }
        resume(c);
        return false;
    }
}

public class Solution{

    public int[] encode(int i,int j,int k){
        int r=(i*9+j)*9+k;
        int c1=81*0+i*9+j+1;
        int c2=81*1+i*9+k;
        int c3=81*2+j*9+k;
        int c4=81*3+((i/3)*3+(j/3))*9+k;
        return new int[]{r,c1,c2,c3,c4};
    }

    public void solveSudoku(char[][] board){
        DLX dlx=new DLX(9);
        dlx.init(9*9*9,9*9*4);
        int[]code;
        for(int i=0;i<9;i++)
            for(int j=0;j<9;j++)
                for(int k=1;k<=9;k++)
                    if(board[i][j]=='.' || board[i][j]=='0'+k){
                        code=encode(i,j,k);
                        dlx.link(code[0],code[1]);
                        dlx.link(code[0],code[2]);
                        dlx.link(code[0],code[3]);
                        dlx.link(code[0],code[4]);
                    }
        dlx.dance(0);
        int v,x,y;
        for(int i=0;i<dlx.ansd;i++){
            v=(dlx.ans[i]-1)%9+1;//+1
            x=(dlx.ans[i]-1)/9/9;
            y=(dlx.ans[i]-1)/9%9;
            board[x][y]=(char)('0'+v);
        }

    }
}
```

### C++
```cpp
#define MAXC (81*4+10)
#define MAXR (81*9+10)
#define MAXN ((81*4+10)*(81*9+10)+10)
#define INF 99999999

class Solution {
	public:
		int cnt;
		char s[200];
		int U[MAXN], D[MAXN], L[MAXN], R[MAXN];
		int Col[MAXN], Row[MAXN];//节点所在列与行
		int H[MAXR];//行头指针
		int S[MAXC];//储存每列的元素数量
		int ans[100];

		void init(int n) {
			for (int i = 0; i <= n; i++) {
				U[i] = D[i] = i;
				L[i] = i - 1;
				R[i] = i + 1;
				S[i] = 0;
			}
			R[n] = 0;
			L[0] = n;
			S[0] = INF;//!!!
			cnt = n + 1;
			memset(H, 0, sizeof(H));
		}

		void link(int r, int c) {
			Row[cnt] = r;//记录行列
			Col[cnt] = c;
			U[cnt] = U[c];//上下连接
			D[cnt] = c;
			D[U[c]] = cnt;
			U[c] = cnt;

			if (H[r] == 0)//左右连接
				H[r] = L[cnt] = R[cnt] = cnt;
			else {
				L[cnt] = L[H[r]];
				R[L[H[r]]] = cnt;
				L[H[r]] = cnt;
				R[cnt] = H[r];
			}

			S[c]++;
			cnt++;
		}

		void remove(int c) {
			L[R[c]] = L[c];
			R[L[c]] = R[c];
			for (int i = D[c]; i != c; i = D[i]) {
				for (int j = R[i]; j != i; j = R[j]) {
					U[D[j]] = U[j];
					D[U[j]] = D[j];
					S[Col[j]]--;
				}
			}
		}

		void resume(int c) {
			L[R[c]] = c;
			R[L[c]] = c;
			for (int i = U[c]; i != c; i = U[i]) {
				for (int j = L[i]; j != i; j = L[j]) {
					U[D[j]] = j;
					D[U[j]] = j;
					S[Col[j]]++;
				}
			}
		}

		void write(vector<vector<char>>& s) {
			sort(ans, ans + 81);
			int p = 0;
			for (int i = 0; i < 9; i++)
				for (int j = 0; j < 9; j++) {
					int num = ans[p++];
					num = num - (i * 9 + j) * 9;
					s[i][j]=num+'0';
				}

		}

		bool dance(int k) {
			if (R[0] == 0)return true;
			int c=0;
			for (int i = R[0]; i != 0; i = R[i])
				if (S[i] < S[c])
					c = i;
				

			remove(c);
			for (int i = D[c]; i != c; i = D[i]) {
				ans[k] = Row[i];
				for (int j = R[i]; j != i; j = R[j])remove(Col[j]);
				if (dance(k + 1))return true;
				for (int j = L[i]; j != i; j = L[j])resume(Col[j]);
			}
			resume(c);
			return false;
		}

		int encode(int a,int b,int c) {
			return 81*a+9*b+c;
		}

		void build(vector<vector<char>>& s) {
			init(9*9*4);
			for (int i = 0; i < 9; i++)
				for (int j = 0; j < 9; j++)
					for (int k = 1; k <= 9; k++) {
						int base = (i * 9 + j) * 9;
						if (s[i][j]=='.'||s[i][j]=='0'+k) {
							int r=base+k;
							link(r,encode(0,i,k));
							link(r,encode(1,j,k));
							link(r,encode(2,j/3*3+i/3,k));
							link(r,encode(3,i,j+1));
						}
					}
		}
		void solveSudoku(vector<vector<char>>& board) {
			build(board);
			dance(0);
			write(board);
		}
};
```
