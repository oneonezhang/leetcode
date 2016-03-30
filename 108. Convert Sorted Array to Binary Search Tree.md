#Convert Sorted Array to Binary Search Tree
##Problem:
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.
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
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        if(nums.empty()) return 0;
        return helper(nums,0,(int)nums.size()-1);
    }
private:
    TreeNode* helper(vector<int>& nums,int left,int right)
    {
        int mid = (left+right)/2;
        TreeNode* root = new TreeNode(nums[mid]);
        if(left<mid)
        {
            TreeNode* leftNode = helper(nums,left,mid-1);
            root->left = leftNode;
        }
        if(right>mid)
        {
            TreeNode* rightNode = helper(nums,mid+1,right);
            root->right = rightNode;
        }
        return root;
    }
};
```