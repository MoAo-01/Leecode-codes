### 解题思路
#### 朴素法
1. 递归
> 对于到达n级台阶的方案数（记为`f(n)`）
> 则`f(n)=f(n-1)+f(n-2)`(从一级前/两级前跳过来)
> 考虑递归出口：`f(0)=f(1)=1`

 复杂度：
- 时间:$O(N^2)$
- 空间:$O(N^2)$（系统消耗栈堆的空间）
- 代码：略。

2. 动态规划
> 基于递归（自顶向下）
> 改为（自底向上）
> 任然是考虑：`f(n)=f(n-1)+f(n-2)`基于`f(0)=f(1)=1`
> 从前往后递推，`f(2),f(3),...`

复杂度：
- 时间:$O(N)$
- 空间:$O(N)$
- 代码：略。



3. 记忆化搜索
> 改良递归，进行剪枝
> 额外开辟O(n)空间记录搜索过的状态
> 若下一次搜索到相同状态，直接返回

复杂度：
- 时间:$O(N)$
- 空间:$O(N)$
- 代码：略。

#### 进阶法

4. 矩阵快速幂
- 能否继续加速计算呢？答案是可以！
> 让我们揭露一下这个题目的本质
> 实际上就是快速计算对于一个递推式`f(n)=f(n-1)+f(n-2)`的通项`f(n)`
> 这其实和斐波拉契数列是本质相同的
> `PS:`数学好的同学应该知道这是可以直接求出通项公式的
- 这里，让我们自己推一个公式吧
> 由于起始条件为：`f(0)=f(1)=1`，每次我们要求出下一项
> 比较自然的想法：将前后两次的结果放入矩阵中，如下`x,y,z,w`均待定

![MommyTalk1627094825004](https://user-images.githubusercontent.com/83717535/126855380-1f67d147-f672-4e03-9e6d-b033c6733a3d.png)


> 由此，我们得到了:对于第$n$个通项(矩阵)，$A_n=[f_n,f_{n+1}]$
> $\therefore A_n=A_0·B·B·B···(n个矩阵B)$
> $\therefore A_n=A_0·(B^n)$

- 加速（快速幂:求$A^n$）
> 将$n$按照二进制位拆开，运算乘法，来求幂
> 我们可以知道，在二进制下n相邻的两位，对应$A$(底数)的倍增
> 即：`A=A*A;`
> 这样，我们只需遍历n对应的二进制数的长度次，即可计算出$A^n$
> 代入矩阵，进行矩阵乘法/求幂运算

复杂度：
- 时间：$O(logN)$
- 空间：$O(1)$

- 代码（C++）

```cpp
typedef long long ll;

class Solution {
private:
    struct Matrix{
        const static int N=2;
        const static ll MOD=1e9+7;
        ll a[N][N];
        Matrix(bool x){for(int i=0;i<N;i++)for(int j=0;j<N;j++)a[i][j]=x?i==j:0;}
        Matrix operator*(Matrix&b){
            Matrix C=Matrix(0);
            for(int k=0;k<N;k++)
                for(int i=0;i<N;i++)
                    for(int j=0;j<N;j++)
                        C.a[i][j]=(C.a[i][j]+a[i][k]*b.a[k][j])%MOD;
            return C;
        }
        Matrix operator^(int n){
            Matrix C=Matrix(1);
            Matrix A=Matrix(0);
            for(int i=0;i<N;i++)for(int j=0;j<N;j++)A.a[i][j]=a[i][j];
            for(;n;n>>=1,A=A*A)if(n&1)C=C*A;
            return C;
        }

        void show(){puts("");for(int i=0;i<N;i++){for(int j=0;j<N;j++)cout<<a[i][j]<<" ";puts("");}}
    };


public:
    int numWays(int n) {
        Matrix A0=Matrix(0);
        A0.a[0][0]=1,A0.a[0][1]=1;
        A0.a[1][0]=0,A0.a[1][1]=0;
        //A0.show();
        Matrix B=Matrix(0);
        B.a[0][0]=0,B.a[0][1]=1;
        B.a[1][0]=1,B.a[1][1]=1;
        //B.show();
        Matrix C=B^n;
        //C=A0*C;
        //C.show();        
        return (A0*C).a[0][0];
    }
};
```
