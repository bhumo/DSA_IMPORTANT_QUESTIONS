# Pallindrome Linked list

Given the `head` of a singly linked list, return `true` if it is a palindrome.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

```
Input: head = [1,2,2,1]
Output: true
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg)

```
Input: head = [1,2]
Output: false
```

&#x20;

**Constraints:**

* The number of nodes in the list is in the range `[1, 105]`.
* `0 <= Node.val <= 9`

&#x20;Approach:&#x20;

Step1 : Find the length of the linked list

Step2 : Find the middle of the linked list using slow and fast pointer

If the linked list is of odd size....

<img src=".gitbook/assets/file.drawing (10).svg" alt="" class="gitbook-drawing">

Step3: Reverse linked list 2

Step4 compare the both LL1 && LL2

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        int length = 0;
        ListNode *temp=head;
        while(temp!=NULL){
            length++;
            temp=temp->next;
        }
        
        if(length<=1){
            return true;
        }
        
        ListNode *slow,*fast,*prev,*curr,*next;
        slow = head;
        fast = head;
        
        while(fast!=NULL && fast->next!=NULL){
            slow = slow->next;
            fast= fast->next->next;
        }

        ListNode* head1 = head;
        ListNode *endingNode = slow;
        ListNode* head2 = slow;
        if(length&1){
            //odd case
            //1->2->3->1->2 slow will point to 3
            head2=slow->next;
            endingNode=head2;
        }
        
        //Step2: Revese the @nd part of LL head2
        prev=NULL;
        next=NULL;
        curr=head2;
        
        while(curr!=NULL){
            next=curr->next;
            curr->next=prev;
            prev=curr;
            curr=next;
        }
        head2=prev;
        
        ListNode *temp1,*temp2;
        temp1=head1;
        temp2=head2;
        while(temp1!=endingNode && temp2!=NULL){
            if(temp1->val != temp2->val){
                return false;
            }
            temp1=temp1->next;
            temp2=temp2->next;
        }
        
        return true;
    }
};
```

