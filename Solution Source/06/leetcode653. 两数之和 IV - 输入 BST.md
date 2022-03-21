- DFS非迭代中序遍历
- 哈希表

```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    bool findTarget(TreeNode* root, int k) {
        unordered_set<int>hash;
        stack<TreeNode*>s;
        auto node=root;
        while(!s.empty()||node){            
            if(node){
                s.push(node);
                node=node->left;
            }
            else{
                node=s.top(),s.pop();
                if(hash.count(k-node->val))return true;
                else hash.insert(node->val);
                node=node->right;                
            }
        }
        return false;
    }
};
```
- BFS+hash
```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    bool findTarget(TreeNode* root, int k) {
        unordered_set<int>hash;
        queue<TreeNode*>q;
        q.push(root);
        while(!q.empty()){
            int sz=q.size();
            while(sz--){
                auto node=q.front();q.pop();
                if(hash.count(k-node->val))return true;
                else hash.insert(node->val);
                if(node->left)q.push(node->left);
                if(node->right)q.push(node->right);
            }
        }
        return false;
    }
};
```
