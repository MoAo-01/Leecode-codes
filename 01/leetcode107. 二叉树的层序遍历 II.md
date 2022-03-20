### 解题思路
- BFS

### 代码

```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<TreeNode*>>level(2000);
        queue<TreeNode*>q;
        if(root)q.push(root);
        int depth=0;
        while(!q.empty()){
            int sz=q.size();
            while(sz--){
                auto p=q.front();q.pop();
                level[depth].push_back(p);
                if(p->left)q.push(p->left);
                if(p->right)q.push(p->right);
            }
            depth++;
        }
        vector<vector<int>>ans(depth);
        int idx=0;
        while(depth--){
            for(const auto&p:level[depth]){
                ans[idx].push_back(p->val);
            }
            idx++;
        }
        return ans;
    }
};
```
