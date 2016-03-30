#Kth Smallest Element in a BST
##Problem:
Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Note: 
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?
##Idea:
`Inorder Traversal`
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
    int kthSmallest(TreeNode* root, int k) {
        TreeNode* current=root;
        int count=0;
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
                current=treeNodeStack.top();
                treeNodeStack.pop();
                count++;
                if(count==k) return current->val;
                current=current->right;
            }
        }
    }
};
```
##To Study:
1.`recursion`
```cpp
class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        int number;
        int count=k;
        helper(root,count,number);
        return number;
    }
private:
    void helper(TreeNode* node,int &count,int &number)
    {
        if(node->left) helper(node->left,count,number);
        count--;
        if(count==0) number=node->val;
        if(count<=0) return;
        if(node->right) helper(node->right,count,number);
    }
};
```
2.`Binary Search`
```cpp
class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        int number=count(root->left);
        if(k<=number) return kthSmallest(root->left,k);
        else if(k>number+1) return kthSmallest(root->right,k-number-1);
        else return root->val;
        
    }
private:
    int count(TreeNode* root)
    {
        if(!root) return 0;
        else
        return 1+count(root->left)+count(root->right);
    }
};
```
We can keep track of elements in a subtree of any node while building the tree.   
Time:O(height of BST)
