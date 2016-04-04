#Populating Next Right Pointers in Each Node
##Problem:
Given a binary tree

    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

Note:

You may only use constant extra space.
You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).
For example,
Given the following perfect binary tree,
```
         1
       /  \
      2    3
     / \  / \
    4  5  6  7
```
After calling your function, the tree should look like:
```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL
```
##Idea:
```cpp
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        if(root)
        {
            root->next=NULL;
            TreeLinkNode* father=root;
            TreeLinkNode* start=root->left;
            TreeLinkNode* end=root->right;
            while(start)
            {
                TreeLinkNode* current=start;
                while(current!=end)
                {
                    if(current==father->left)
                    {
                        current->next=father->right;
                    }
                    else
                    {
                        father=father->next;
                        current->next=father->left;
                    }
                    current=current->next;
                }
                current->next=NULL;
                father=start;
                start=start->left;
                end=end->right;
            }
        }
    }
};
```
##To Study:
1.`iteration with 2 additional pointers`
```cpp
class Solution {
public:
    void connect(TreeLinkNode *root) {
        if(root)
        {
            TreeLinkNode* current = root;
            TreeLinkNode* nextLine=root->left;
            while(nextLine)
            {
                while(current)
                {
                    current->left->next=current->right;
                    if(current->next) current->right->next=current->next->left;
                    current=current->next;
                }
                current=nextLine;
                nextLine=nextLine->left;
            }
        }
    }
};
```
2.`Queue`-O(n) space
```cpp
class Solution {
public:
    void connect(TreeLinkNode *root) {
        if(!root) return;
        queue<TreeLinkNode*> treeQueue;
        treeQueue.push(root);
        while(!treeQueue.empty())
        {
            treeQueue.push(NULL);
            TreeLinkNode* current=treeQueue.front();
            treeQueue.pop();
            while(current)
            {
                current->next=treeQueue.front();
                if(current->left) treeQueue.push(current->left);
                if(current->right) treeQueue.push(current->right);
                current=current->next;
                treeQueue.pop();
            }
        }
        
    }
};
```
3.`recursion`,`DFS`-stack O(logn) space
```cpp
class Solution {
public:
    void connect(TreeLinkNode *root) {
        if(!root||!root->left) return;
        root->left->next=root->right;
        if(root->next) root->right->next=root->next->left;
        connect(root->left);
        connect(root->right);
    }
};
```