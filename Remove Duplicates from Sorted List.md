#Remove Duplicates from Sorted List
##Problem:
Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,  
Given 1->1->2, return 1->2.  
Given 1->1->2->3->3, return 1->2->3.  
##Idea:
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
    ListNode* deleteDuplicates(ListNode* head) {
        if(head)
        {
            ListNode* current=head;
            while(current->next)
            {
                if(current->val==current->next->val)
                {
                    current->next=current->next->next;
                }
                else 
                {
                    current=current->next;
                }
            }
        }
        return head;
    }
};
```
##To Study:
`recursion`
```cpp
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        if(!head||!head->next) return head;
        else
        {
            ListNode* nextHead=deleteDuplicates(head->next);
            head->next=nextHead;
            return (head->val==nextHead->val)?nextHead:head;
        }
    }
};
```