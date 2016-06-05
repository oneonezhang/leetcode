#Binary Tree Level Order Traversal II
##Problem:
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
return its bottom-up level order traversal as:
```
[
  [15,7],
  [9,20],
  [3]
]
```
##Idea:
1.BFS+reverse
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
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
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
        reverse(result.begin(),result.end());
        return result;
    }
};
```
2.DFS,count the height of the tree
```cpp
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        int h=getHeight(root);
        vector<vector<int>> result(h);
        helper(result,h-1,root);
        return result;
    }
private:
    int getHeight(TreeNode* node)
    {
        if(node==NULL) return 0;
        int left=getHeight(node->left);
        int right=getHeight(node->right);
        return max(left,right)+1;
    }
    void helper(vector<vector<int>>& result,int num,TreeNode* node)
    {
        if(node==NULL) return;
        result[num].push_back(node->val);
        helper(result,num-1,node->left);
        helper(result,num-1,node->right);
    }
};
```