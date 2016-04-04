#House Robber III
##Problem:
The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.

Example 1:
```
     3
    / \
   2   3
    \   \ 
     3   1
```
Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
Example 2:
```
     3
    / \
   4   5
  / \   \ 
 1   3   1
 ```
Maximum amount of money the thief can rob = 4 + 5 = 9.
#Idea:
`recursion`//very very slow
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
    int rob(TreeNode* root) {
        if(!root) return 0;
        if(root->left==0&&root->right==0) return root->val;
        else if(root->left==0) return max(rob(root->right),rob(root->right->left)+rob(root->right->right)+root->val);
        else if(root->right==0) return max(rob(root->left),rob(root->left->left)+rob(root->left->right)+root->val);
        else return max(rob(root->left)+rob(root->right),rob(root->left->left)+
                        rob(root->left->right)+rob(root->right->left)+rob(root->right->right)+root->val);
    }
};
```
##To Study:
1.`overlapping of subproblems`->`dynamic programming`
`Hash Table`
```cpp
class Solution {
public:
    int rob(TreeNode* root) {
        unordered_map<TreeNode*,int> sub;
        return robSub(root,sub);
    }
private:
    int robSub(TreeNode* root, unordered_map<TreeNode*,int> &sub)
    {
        if(!root) return 0;
        if(sub.find(root)!=sub.end()) return sub[root]; 
        else
        {
            int money=0;
            if(root->left) money += robSub(root->left->left,sub)+robSub(root->left->right,sub);
            if(root->right) money += robSub(root->right->left,sub)+robSub(root->right->right,sub);
            sub[root] = max(money+root->val,robSub(root->left,sub)+robSub(root->right,sub));
            return sub[root];
        }
    }
};
```
2.`return 2 values: rob(1) or not rob(0) for each subproblem`
```cpp
class Solution {
public:
    int rob(TreeNode* root) {
        vector<int> temp=robSub(root);
        return max(temp[0],temp[1]);  
    }
private:
    vector<int> robSub(TreeNode* root)
    {
        vector<int> result={0,0};
        if(root)
        {
            vector<int> left=robSub(root->left);
            vector<int> right=robSub(root->right);
            result[1]=left[0]+right[0]+root->val;
            result[0]=max(left[0],left[1])+max(right[0],right[1]);
        }
        return result;
    }
};
```