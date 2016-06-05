#Binary Tree Level Order Traversal
##Problem:
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
return its level order traversal as:
```
[
  [3],
  [9,20],
  [15,7]
]
```
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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        queue<TreeNode*> levelQueue;
        if(root) levelQueue.push(root);
        while(!levelQueue.empty())
        {
            int n=levelQueue.size();
            vector<int> currentLevel(n);
            for(int i=0;i<n;i++)
            {
                TreeNode* top=levelQueue.front();
                levelQueue.pop();
                currentLevel[i]=top->val;
                if(top->left) levelQueue.push(top->left);
                if(top->right) levelQueue.push(top->right);
            }
            result.push_back(currentLevel);
        }
        return result;
    }
};
```
##To Study:
`DFS` preorder traversal
```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if(root) helper(result,0,root);
        return result;
    }
private:
    void helper(vector<vector<int>>& result,int level,TreeNode* node)
    {
        if(result.size()<level+1) result.push_back(vector<int>());
        result[level].push_back(node->val);
        if(node->left) helper(result,level+1,node->left);
        if(node->right) helper(result,level+1,node->right);
    }
};
```