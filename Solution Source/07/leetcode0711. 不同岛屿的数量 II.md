### 代码

```cpp [c++ - 代码]
using P = pair<double, double>;
const double EPS=1e-6;

class Solution {
public:
    int numDistinctIslands2(vector<vector<int>>& grid) {
        n = grid.size(), m  = grid[0].size();
        int ans = 0;
        for (int x = 0; x < n; x++)
            for (int y = 0; y < m; y++)
                if (grid[x][y]) {
                    vector<P> component;
                    dfs(grid, x, y, component);
                    ans += isUnique(get_hash(component));
                }
        return ans; 
    }

private:
    int n,m;

    bool inGrid(int&x,int&y) { return (0 <= x && x < n) && (0 <= y && y < m); }

    vector<double> hashs;

    double distance(P& a, P& b) {
        const double dx = a.first  - b.first, dy = a.second - b.second;
        return sqrt(dx * dx + dy * dy);
    }

    P gravityCenter(vector<P>& component){
        const double n=component.size();
        P o=P(0.0,0.0);
        for(P&p:component)o.first+=p.first/n, o.second+=p.second/n;
        return o;
    }

    double get_hash(vector<P>& component) {
        auto o=gravityCenter(component);
        double sum = 0.0;
        for(P&p:component)sum+=distance(p,o);
        return sum;
    }

    bool isUnique(double h) {
        for(auto&hash:hashs)if(fabs(hash-h)<EPS)return false;
        hashs.push_back(h);
        return true;
    }
    
    const vector<vector<int>>ds{{-1, 0}, {1, 0}, {0, -1}, {0, 1}};

    void dfs(vector<vector<int>>& grid, int x, int y, vector<P>& component) {
        if (!inGrid(x,y) || !grid[x][y]) return;
        grid[x][y] = 0;
        component.emplace_back(x, y);
        for(auto&d:ds)dfs(grid, x + d[0], y + d[1], component);
    }
};
```
```cpp [c++ - 部分数据点]
/*
[
    [@ @ @   @   @   @ @ @ @      ] 
    [          @             @    ] 
    [  @ @   @ @     @ @ @     @  ] 
    [@ @ @   @     @   @     @   @] 
    [      @ @     @ @ @ @ @ @ @  ] 
    [@   @   @   @       @   @    ] 
    [@   @ @ @ @         @ @ @   @] 
    [@         @   @ @ @   @      ] 
    [@ @     @ @     @   @   @    ] 
    [  @     @ @ @ @ @ @   @      ]
]

[
    [    @ @         @ @ @ @ @   @] 
    [    @     @     @   @ @ @    ] 
    [@       @ @ @ @   @          ] 
    [@ @ @   @   @       @ @   @ @] 
    [  @   @               @ @ @  ] 
    [@   @ @ @   @   @       @ @  ] 
    [@     @         @ @          ] 
    [  @       @     @       @ @ @] 
    [  @   @     @ @   @ @        ] 
    [@   @ @   @   @   @ @ @   @  ]
]
*/
```
