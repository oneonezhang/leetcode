#Symmetric Tree
##Problem:
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
But the following [1,2,2,null,3,null,3] is not:
```
    1
   / \
  2   2
   \   \
   3    3
```
Note:
Bonus points if you could solve it both recursively and iteratively.
##Idea:
1.`BFS`  
level order traversal and judge if every level is symmetric  
push too many NULL nodes into the queue and Memory Limit Exceeded!  
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
    bool isSymmetric(TreeNode* root) {
        if(root==NULL) return true;
        queue<TreeNode*> treeQueue;
        treeQueue.push(root);
        bool goOn=true;
        while(goOn)
        {
            goOn=false;
            int n=treeQueue.size();
            vector<TreeNode*> currentLayer(n);
            for(int i=0;i<n;i++)
            {
                TreeNode* top=treeQueue.front();
                treeQueue.pop();
                currentLayer[i]=top;
                if(top)
                {
                    treeQueue.push(top->left);
                    treeQueue.push(top->right);
                    if(top->left||top->right) goOn=true;
                }
                else 
                {
                    treeQueue.push(NULL);
                    treeQueue.push(NULL);
                }
            }
            for(int i=0;i<n/2;i++)
            {
                if(currentLayer[i]==NULL&&currentLayer[n-1-i]==NULL) continue;
                else if(currentLayer[i]==NULL||currentLayer[n-1-i]==NULL) return false;
                else if(currentLayer[i]->val==currentLayer[n-1-i]->val) continue;
                else return false;
            }
        }
        return true;
    }
};
```
2.`DFS`,`recursion`
```cpp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(root==NULL) return true;
        else return isMirror(root->left,root->right);
    }
private:
    bool isMirror(TreeNode* left,TreeNode* right)
    {
        if(left==NULL&&right==NULL) return true;
        else if(left==NULL||right==NULL) return false;
        else return isMirror(left->left,right->right)&&isMirror(left->right,right->left)&&left->val==right->val;
    }
};
```
##To Study:
`iteration`
```cpp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(root==NULL) return true;
        stack<TreeNode*> leftStack;
        stack<TreeNode*> rightStack;
        leftStack.push(root->left);
        rightStack.push(root->right);           
        while(!leftStack.empty())
        {
            TreeNode* leftTop=leftStack.top();
            TreeNode* rightTop=rightStack.top();
            leftStack.pop();
            rightStack.pop();
            if(leftTop==NULL&&rightTop==NULL) continue;
            else if(leftTop==NULL||rightTop==NULL) return false;
            else if(leftTop->val!=rightTop->val) return false;
            else
            {
                leftStack.push(leftTop->right);    
                leftStack.push(leftTop->left);
                rightStack.push(rightTop->left);
                rightStack.push(rightTop->right);
            }
        }
        return true;
    }
};
```
It also works with BFS.  
We can also merge the two stacks into one.
