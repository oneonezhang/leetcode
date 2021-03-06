#Invert Binary Tree
##Problem:
Invert a binary tree.

```     
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```
to
```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```
##Idea:
1.DFS
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
    TreeNode* invertTree(TreeNode* root) {
        if (root!=NULL)
        {
            invertTree(root->left);
            invertTree(root->right);
            TreeNode* temp;
            temp=root->left;
            root->left=root->right;
            root->right=temp;
        }
        return root;
    }
};
```
2.BFS
```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(root!=NULL)
        {
            queue<TreeNode*> treeNodeQueue;
            treeNodeQueue.push(root);
            while(!treeNodeQueue.empty())
            {
                int length=treeNodeQueue.size();
                for(int i=0;i<length;i++)
                {
                    TreeNode* first=treeNodeQueue.front();
                    treeNodeQueue.pop();
                    TreeNode* temp=first->left;
                    first->left=first->right;
                    first->right=temp;
                    if(first->left!=NULL) treeNodeQueue.push(first->left);
                    if(first->right!=NULL) treeNodeQueue.push(first->right);
                }
            }
            return root;
        }
    }
};
```