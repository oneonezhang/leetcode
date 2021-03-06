#Maximum Depth of Binary Tree
##Problem:
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
##Idea:
`recursion`
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
    int maxDepth(TreeNode* root) {
        if (root==NULL)
            return 0;
        else
        {
            int leftDepth=maxDepth(root->left);
            int rightDepth=maxDepth(root->right);
            return (leftDepth>rightDepth)?leftDepth+1:rightDepth+1;
        }
    }
};
```
##To Study:
1.我上面的算法算`Depth-First-Search`  
2.`Breadth-First-Search`
```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root==NULL) return 0;
        queue<TreeNode*> treeNodeQueue;
        treeNodeQueue.push(root);
        int depth=0;
        while(!treeNodeQueue.empty())
        {
            depth++;
            int n=treeNodeQueue.size();
            for(int i=0;i<n;i++)
            {
                TreeNode* pointer=treeNodeQueue.front();
                treeNodeQueue.pop();
                if(pointer->left!=NULL)
                    treeNodeQueue.push(pointer->left);
                if(pointer->right!=NULL)
                    treeNodeQueue.push(pointer->right);
            }
        }
        return depth;
    }
}; 
```
