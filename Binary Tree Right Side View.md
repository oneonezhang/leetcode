#Binary Tree Right Side View
##Problem:
Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

For example:
Given the following binary tree,
```
   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```
You should return [1, 3, 4].
##Idea:
`BFS`
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> result;
        if(root)
        {
            queue<TreeNode*> treeQueue;
            treeQueue.push(root);
            while(!treeQueue.empty())
            {
                result.push_back(treeQueue.back()->val);
                int n=treeQueue.size();
                for(int i=0;i<n;i++)
                {
                    TreeNode* current=treeQueue.front();
                    treeQueue.pop();
                    if(current->left) treeQueue.push(current->left);
                    if(current->right) treeQueue.push(current->right);
                }
            }
        }
        return result;
    }
};
```
##To Study:
`DFS`
```cpp
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> result;
        helper(root,result,0);
        return result;
    }
private:
    void helper(TreeNode* node,vector<int>& result,int visitedDepth)
    {
        if(node==NULL) return;
        if(visitedDepth==result.size()) result.push_back(node->val);
        helper(node->right,result,visitedDepth+1);
        helper(node->left,result,visitedDepth+1);
    }
};
```