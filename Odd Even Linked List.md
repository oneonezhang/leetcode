#Odd Even Linked List
##Problem:
Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

Example:
Given 1->2->3->4->5->NULL,  
return 1->3->5->2->4->NULL.  

Note:
The relative order inside both the even and odd groups should remain as it was in the input. 
The first node is considered odd, the second node even and so on ...
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
    ListNode* oddEvenList(ListNode* head) {
        if(head==NULL||head->next==NULL) return head;
        ListNode* oddNode=head;
        ListNode* evenHead=head->next;
        ListNode* evenNode=evenHead;
        ListNode* current=evenHead->next;
        int n=2;
        while(current)
        {
            n++;
            if(n%2) 
            {
                oddNode->next=current;
                oddNode=current;
            }
            else 
            {
                evenNode->next=current;
                evenNode=current;
            }
            current=current->next;
        }
        oddNode->next=evenHead;
        evenNode->next=NULL;
        return head;
    }
};
```
##To Study:
Each time judge two nodes.
```cpp
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        if(head)
        {
            ListNode* oddNode=head;
            ListNode* evenHead=head->next;
            ListNode* evenNode=evenHead;
            while(evenNode&&evenNode->next)
            {
                oddNode->next=evenNode->next;
                oddNode=oddNode->next;
                evenNode->next=oddNode->next;
                evenNode=evenNode->next;
            }
            oddNode->next=evenHead;
        }
        return head;
    }
};
```