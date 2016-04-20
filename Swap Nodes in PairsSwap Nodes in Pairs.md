#Swap Nodes in Pairs
##Problem:
Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given 1->2->3->4, you should return the list as 2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.
##Idea:
Sorry I modify the values in the list
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
    ListNode* swapPairs(ListNode* head) {
        ListNode* first=head;
        while(first&&first->next)
        {
            int temp=first->val;
            first->val=first->next->val;
            first->next->val=temp;
            first=first->next->next;
        }
        return head;
    }
};
```
##To Study:
1.`recursion`——O(n) space 
```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(!head||!head->next) return head;
        else
        {
            ListNode* newHead=head->next;
            head->next=swapPairs(head->next->next);
            newHead->next=head;
            return newHead;
        }
    }
};
```
2.`iteration`
```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode dummy(0);
        ListNode* current=&dummy;
        current->next=head;
        while(current->next&&current->next->next)
        {
            ListNode* first=current->next;
            ListNode* second=first->next;
            first->next=second->next;
            second->next=first;
            current->next=second;
            current=first;
        }
        return dummy.next;
    }
};
```