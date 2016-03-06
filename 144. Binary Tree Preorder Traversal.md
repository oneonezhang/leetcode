#Binary Tree Preorder Traversal
##Problem:
Given a binary tree, return the preorder traversal of its nodes' values.

For example:
Given binary tree {1,#,2,3},
```
   1
    \
     2
    /
   3
```
return [1,2,3].

Note: Recursive solution is trivial, could you do it iteratively?
##Idea:
`Stack`
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
    vector<int> preorderTraversal(TreeNode* root) {
        stack<TreeNode*> treeNodeStack;
        vector<int> nodes;
        if (root != NULL) treeNodeStack.push(root);
        while(!treeNodeStack.empty())
        {
            TreeNode* currentRoot=treeNodeStack.top();
            treeNodeStack.pop();
            nodes.push_back(currentRoot->val);
            if(currentRoot->right != NULL) treeNodeStack.push(currentRoot->right);
            if(currentRoot->left != NULL) treeNodeStack.push(currentRoot->left);
        }
        return nodes;
    }
};
//T:O(n) S:O(n)
```  
##To Study:
1.`Recursive solution`
```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> nodes;
        preorder(root,nodes);
        return nodes;
    }
private:
    void preorder(TreeNode* root,vector<int>& nodes)
    {
        if(root != NULL)
        {
            nodes.push_back(root->val);
            preorder(root->left,nodes);
            preorder(root->right,nodes);
        }
    }
};
//T:O(n) S:O(n)-function call stack 
```
2.`Morris Traversal`-Threaded Binary Tree
```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> nodes;
        TreeNode* current=root;
        while(current)
        {
            if(!current->left)
            {
                nodes.push_back(current->val);
                current=current->right;
            }
            else
            {
                TreeNode* predecessor=current->left;
                while(predecessor->right&&predecessor->right!=current)
                {
                    predecessor=predecessor->right;
                }
                if(!predecessor->right)
                {
                    predecessor->right=current;
                    nodes.push_back(current->val);
                    current=current->left;
                }
                else
                {
                    predecessor->right=NULL;
                    current=current->right;
                }
            }
        }
        return nodes;
    }
};
//T:O(n) S:O(1)
```