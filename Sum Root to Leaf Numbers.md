#Sum Root to Leaf Numbers
##Problem:
Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path 1->2->3 which represents the number 123.

Find the total sum of all root-to-leaf numbers.

For example,
```
    1
   / \
  2   3
```
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.

Return the sum = 12 + 13 = 25.
##Idea:
`DFS recursion`
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
    int sumNumbers(TreeNode* root) {
        int sum = 0;
        backTrack(root,sum,0);
        return sum;
    }
private:
    void backTrack(TreeNode* current, int& sum, int pathNumBefore)
    {
        if(current == NULL) return;
        int pathNum = pathNumBefore * 10 + current->val;
        if(current->left == NULL && current->right == NULL)
        {
            sum += pathNum;
        }
        else
        {
            backTrack(current->left,sum,pathNum);
            backTrack(current->right,sum,pathNum);
        }
    }
};
```
##To Study:
1.return int and reduce a parameter
```cpp
class Solution {
public:
    int sumNumbers(TreeNode* root) {
        return helper(root,0);
    }
private:
    int helper(TreeNode* current, int pathNumBefore)
    {
        if(current==NULL) return 0;
        int pathNum=pathNumBefore*10+current->val;
        if(current->left==NULL && current->right==NULL)
        {
            return pathNum;
        }
        else
        {
            return helper(current->left,pathNum)+helper(current->right,pathNum); 
        }
    }
};
```
2.iteration
```cpp
class Solution {
public:
    int sumNumbers(TreeNode* root) {
        int sum=0;
        int pathNum=0;
        TreeNode* current=root;
        stack<TreeNode*> nodeStack;
        stack<int> numStack;
        while(current||!nodeStack.empty())
        {
            if(current)
            {
                pathNum=pathNum*10+current->val;
                if(current->left==NULL && current->right==NULL)
                {
                    sum+=pathNum;
                    current=NULL;
                }
                else
                {
                    nodeStack.push(current);
                    numStack.push(pathNum);
                    current=current->left;
                }
            }
            else
            {
                current=nodeStack.top()->right;
                nodeStack.pop();
                pathNum=numStack.top();
                numStack.pop();
            }
        }
        return sum;
    }
};
```

