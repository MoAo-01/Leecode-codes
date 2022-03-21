```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    int ans=0;
    int diameterOfBinaryTree(TreeNode* root) {        
        dfs(root);
        return ans;
    }
    int dfs(TreeNode*rt){
        if(rt==NULL)return-1;
        int ldepth=dfs(rt->left);
        int rdepth=dfs(rt->right);
        ans=max(ans,ldepth+rdepth+2);
        return max(ldepth,rdepth)+1;
    }
};
```
