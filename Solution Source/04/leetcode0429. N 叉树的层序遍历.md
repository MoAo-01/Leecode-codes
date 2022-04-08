```cpp
#include <bits/stdc++.h>
using namespace std;

// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};

class Solution {
public:
    vector<vector<int>> levelOrder(Node* root) {
        vector<vector<int>>ans;
        if(!root)return ans;
        queue<Node*>q;
        q.push(root);
        while(!q.empty()){
            int sz=q.size();
            vector<int>level;
            while(sz--){
                Node *node=q.front();
				q.pop();
                level.push_back(node->val);
                for(Node* child:node->children)
                    q.push(child);            
            }
            ans.push_back(level);
        }
        return ans;
    }
};


int main(){
	Solution sol;
	Node* leaf1=new Node(5);
	Node* leaf2=new Node(6);
	
	Node* son1=new Node(3);
	Node* son2=new Node(2);
	Node* son3=new Node(4);
	
	Node* root=new Node(1);
	
	son1->children.push_back(leaf1);
	son1->children.push_back(leaf2);
	
	root->children.push_back(son1);
	root->children.push_back(son2);
	root->children.push_back(son3);
	
	vector<vector<int>>ans=sol.levelOrder(root);
	
	for(auto row:ans){
		cout<<"";
		for(auto val:row){
			cout<<val<<" ";
		}		
		cout<<""<<endl;
	}	
	return 0;
}
```
