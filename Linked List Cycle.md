#Linked List Cycle
#Problem:
Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?
##Idea:
`Two Pointers`
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
    bool hasCycle(ListNode *head) {
        if(!head||!head->next) return 0;
        ListNode* slow=head->next;
        ListNode* fast=head->next->next;
        while(fast&&slow!=fast)
        {
            slow=slow->next;
            if(!fast->next) return 0;
            fast=fast->next->next;
        }
        if(slow==fast) return 1;
        else return 0;
    }
};
```
##To Study:
It's more clear:
```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode* slow=head;
        ListNode* fast=head;
        while(fast&&fast->next)
        {
            slow=slow->next;
            fast=fast->next->next;
            if(slow==fast) return 1;
        }
        return 0;
    }
};
```