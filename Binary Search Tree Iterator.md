#Binary Search Tree Iterator
##Problem:
Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

Calling next() will return the next smallest number in the BST.

Note: next() and hasNext() should run in average O(1) time and uses O(h) memory, where h is the height of the tree.
##Idea:
`Inorder Traversal`
```cpp
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class BSTIterator {
public:
    BSTIterator(TreeNode *root) {
        TreeNode* smaller = root;
        while(smaller)
        {
            BSTStack.push(smaller);
            smaller=smaller->left;
        }
    }

    /** @return whether we have a next smallest number */
    bool hasNext() {
        return !BSTStack.empty();
    }

    /** @return the next smallest number */
    int next() {
        TreeNode* nextNode=BSTStack.top();
        BSTStack.pop();
        TreeNode* smaller = nextNode->right;
        while(smaller)
        {
            BSTStack.push(smaller);
            smaller=smaller->left;
        }
        return nextNode->val;
    }
private:
    stack<TreeNode*> BSTStack;
};

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = BSTIterator(root);
 * while (i.hasNext()) cout << i.next();
 */
 ```