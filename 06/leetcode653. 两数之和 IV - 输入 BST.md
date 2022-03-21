- 非迭代中序遍历
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
