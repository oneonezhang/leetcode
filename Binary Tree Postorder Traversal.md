#Binary Tree Postorder Traversal
##Problem:
Given a binary tree, return the postorder traversal of its nodes' values.

For example:
Given binary tree {1,#,2,3},
```
   1
    \
     2
    /
   3
```
return [3,2,1].

Note: Recursive solution is trivial, could you do it iteratively?
##Idea:
1.递归  
2.`Hash Table`+`Stack`
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
    vector<int> postorderTraversal(TreeNode* root) {
        unordered_map<TreeNode*,bool> visited;
        stack<TreeNode*> treeNodeStack;
        vector<int> nodes;
        if(root) treeNodeStack.push(root);
        while(!treeNodeStack.empty())
        {
            TreeNode* current = treeNodeStack.top();
            if(visited[current])
            {
                nodes.push_back(current->val);
                treeNodeStack.pop();
            }
            else
            {
                if(current->right) treeNodeStack.push(current->right);
                if(current->left) treeNodeStack.push(current->left);
                visited[current]=1;
            }
        }
        return nodes;
    }
};
```
##To Study:
1.`reverse preorder traversal`  
root-left-right(preorder)=>root-right-left=>left-right-root(postorder)
```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> nodes;
        stack<TreeNode*> treeNodeStack;
        if(root) treeNodeStack.push(root);
        while(!treeNodeStack.empty())
        {
            TreeNode* current=treeNodeStack.top();
            treeNodeStack.pop();
            nodes.push_back(current->val);
            if(current->left) treeNodeStack.push(current->left);
            if(current->right) treeNodeStack.push(current->right);
        }
        reverse(nodes.begin(),nodes.end());
        return nodes;
    }
};
```
2.`Morris Traversal`  
> (cited from http://www.cnblogs.com/AnnieKim/archive/2013/06/15/MorrisTraversal.html)   
  需要建立一个临时节点dump，令其左孩子是root。并且还需要一个子过程，就是倒序输出某两个节点之间路径上的各个节点。  
  步骤：  
  当前节点设置为临时节点dump。
  1. 如果当前节点的左孩子为空，则将其右孩子作为当前节点。
  2. 如果当前节点的左孩子不为空，在当前节点的左子树中找到当前节点在中序遍历下的前驱节点。
   a) 如果前驱节点的右孩子为空，将它的右孩子设置为当前节点。当前节点更新为当前节点的左孩子。
   b) 如果前驱节点的右孩子为当前节点，将它的右孩子重新设为空。倒序输出从当前节点的左孩子到该前驱节点这条路径上的所有节点。当前节点更新为当前节点的右孩子。
  3. 重复以上1、2直到当前节点为空。
  
```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> nodes;
        stack<TreeNode*> treeNodeStack;
        
        TreeNode* dump = new TreeNode(0);
        dump->left=root;
        TreeNode* current = dump;
        while(current)
        {
            if(current->left)
            {
                TreeNode* predecessor = current->left;
                while(predecessor->right&&predecessor->right!=current)
                {
                    predecessor=predecessor->right;
                }
                if(!predecessor->right)
                {
                    predecessor->right=current;//connected
                    current=current->left;
                }
                else
                {
                    stack<TreeNode*> toAdd;
                    TreeNode* temp=current->left;
                    while(temp != predecessor)
                    {
                        toAdd.push(temp);
                        temp=temp->right;
                    }
                    toAdd.push(predecessor);
                    while(!toAdd.empty())
                    {
                        nodes.push_back(toAdd.top()->val);
                        toAdd.pop();
                    }//left subtree has been traversed
                    predecessor->right=NULL;
                    current=current->right;
                }
            }
            else
            {
                current=current->right;
            }
        }
        delete dump;
        return nodes;
    }
};
```  
3.`a universal idea for preorder traversal inorder traversal and postorder traversal`  
>For each node N, we process it as follows:  
------- push N in stack -> push left tree of N in stack -> pop left tree of N -> push right tree of N in stack -> pop right tree of N -> pop N---------   
For preorder traversal, we visit a node when pushing it in stack. For inorder traversal, we visit a node when pushing its right child in stack. for postorder traversal, we visit a node when popping it.   
lastpop represents the node which is popped the last time. For the top node in stack, it has three choices, pushing its left child in stack, or pushing its right child in stack, or being popped. If lastpop != top->left or top->right, meaning that its left tree has not been pushed in stack, then we push its left child. If last_pop == top->left, we push its right child. Otherwise, we pop the top node.

```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        stack<TreeNode*> treeNodeStack;
        vector<int> nodes;
        TreeNode* lastPop=root;
        if(root) treeNodeStack.push(root);
        while(!treeNodeStack.empty())
        {
            TreeNode* top = treeNodeStack.top();
            if(top->left!=lastPop&&top->right!=lastPop&&top->left)
            {
                treeNodeStack.push(top->left);
            }
            else if(top->right!=lastPop&&top->right&&(top->left==NULL||top->left==lastPop))
            {
                treeNodeStack.push(top->right);
            }
            else
            {
                treeNodeStack.pop();
                nodes.push_back(top->val);
                lastPop=top;
            }
        }
        return nodes;
    }
};
```  
PS:二叉树的这几个遍历终于弄完了啊啊啊！有种走火入魔的感觉X﹏X
