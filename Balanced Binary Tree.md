#Balanced Binary Tree
##Problem:
Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
##Idea:
`Recursion`(DFS)  
assign height=-1 to indicate the tree is not balanced  
Time Complexity:O(n)
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
    bool isBalanced(TreeNode* root) {
        return height(root)!=-1;
    }
private:
    int height(TreeNode* node)
    {
        if(node==NULL) return 0;
        else
        {
            int left=height(node->left);
            if(left==-1) return -1;
            int right=height(node->right);
            if(right==-1) return -1;
            if(abs(right-left)>1) return -1;
            return max(left,right)+1;
        }
    }
};
```

##PS:
How many nodes at least in a n-layer balanced binary tree?  
F(n)=F(n-1)+F(n-2)+1  
The first n-2 layers may not be full.