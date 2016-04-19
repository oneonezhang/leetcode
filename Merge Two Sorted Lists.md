#Merge Two Sorted Lists
##Problem:
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
##Idea:
1.like `Merge` in merge sort
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1==NULL) return l2;
        else if(l2==NULL) return l1;
        else
        {
            ListNode* head;
            if(l1->val<=l2->val)
            {
                head=l1;
                l1=l1->next;
            }
            else
            {
                head=l2;
                l2=l2->next;
            }
            ListNode* current=head;
            while(l1&&l2)
            {
                if(l1->val<=l2->val)
                {
                    current->next=l1;
                    l1=l1->next;
                    current=current->next;
                }
                else
                {
                    current->next=l2;
                    l2=l2->next;
                    current=current->next;
                }
            }
            if(l1) current->next=l1;
            else if(l2) current->next=l2;
            return head;
        }
    }
};
```
2.`recursion`
```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(!l1) return l2;
        if(!l2) return l1;
        if(l1->val<=l2->val)
        {
            l1->next=mergeTwoLists(l1->next,l2);
            return l1;
        }
        else
        {
            l2->next=mergeTwoLists(l1,l2->next);
            return l2;
        }
    }
};
```
##To Study:
`use dummy head`
```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode dummy(0);
        ListNode* current=&dummy;
        while(l1&&l2)
        {
            if(l1->val<=l2->val)
            {
                current->next=l1;
                l1=l1->next;
            }
            else
            {
                current->next=l2;
                l2=l2->next;
            }
            current=current->next;
        }
        if(l1) current->next=l1;
        else if(l2) current->next=l2;
        return dummy.next;
    }
};
```