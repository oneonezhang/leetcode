#Binary Tree Inorder Traversal
##Problem:
Given a binary tree, return the inorder traversal of its nodes' values.

For example:
Given binary tree {1,#,2,3},
```
   1
    \
     2
    /
   3
```
return [1,3,2].

Note: Recursive solution is trivial, could you do it iteratively?
##Idea:
1.`Recursive solution`  
2.`Morris Traversal`
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
    vector<int> inorderTraversal(TreeNode* root) {
        TreeNode* current=root;
        vector<int> nodes;
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
                    current=current->left;
                }
                else
                {
                    predecessor->right=NULL;
                    nodes.push_back(current->val);
                    current=current->right;
                }
            }
        }
        return nodes;
    }
};
```
3.`Stack`
```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        stack<TreeNode*> treeNodeStack;
        vector<int> nodes;
        if(root) treeNodeStack.push(root);
        while(!treeNodeStack.empty())
        {
            TreeNode* current=treeNodeStack.top();
            treeNodeStack.pop();
            if(current->right) treeNodeStack.push(current->right);
            if(current->left)
            {
                TreeNode* copy = new TreeNode(current->val);//local variable doesn't work
                treeNodeStack.push(copy);
                treeNodeStack.push(current->left);
            }
            else
            {
                nodes.push_back(current->val);
            }
        }
        return nodes;
    }
};
```
**new创建出的内存空间代码块结束后不会被销毁——堆**   
**局部变量会被销毁——栈**
##To Study:
用new动态内存分配会导致Memory Leak  
1.`栈顶为当前节点作为左子树成分的最近根节点`
```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        TreeNode* current = root;
        vector<int> nodes;
        stack<TreeNode*> treeNodeStack;
        while(current||!treeNodeStack.empty())
        {
            if(current)
            {
                treeNodeStack.push(current);
                current=current->left;
            }
            else
            {
                current = treeNodeStack.top();
                treeNodeStack.pop();
                nodes.push_back(current->val);
                current=current->right;
            }
        }
        return nodes;
    }
};
```
2.也可以用哈希表记录每一个节点的左子树有没有被访问过
