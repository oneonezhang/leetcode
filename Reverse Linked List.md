#Reverse Linked List
##Problem:
Reverse a singly linked list.
##Idea:
`recursion`
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(!head) return NULL; 
        ListNode* newHead;
        ListNode* nextNode=head->next;
        if(nextNode)
        {
            newHead=reverseList(nextNode);
            nextNode->next=head;
        }
        else
        {
            newHead=head;
        }
        head->next=NULL;
        return newHead;
    }
};
```
`iteration`
```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* left = NULL;
        ListNode* middle = head;
        ListNode* right;
        while(middle)
        {
            right=middle->next;
            middle->next=left;
            left=middle;
            middle=right;
        }
        return left;
    }
};
```