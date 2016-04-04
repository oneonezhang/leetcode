#Same Tree
##Problem:
Given two binary trees, write a function to check if they are equal or not.

Two binary trees are considered equal if they are structurally identical and the nodes have the same value.
##Idea:
`recursion && DFS`
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
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(p==NULL&&q==NULL) return 1;
        else if(p==NULL||q==NULL) return 0;
        else
        {
            return (p->val==q->val)&&isSameTree(p->left,q->left)&&isSameTree(p->right,q->right);
        }
    }
};
```