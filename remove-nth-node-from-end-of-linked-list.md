---
description: https://leetcode.com/problems/remove-nth-node-from-end-of-list/
---

# Remove nth Node from end of Linked List

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/remove\_ex1.jpg)

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

**Example 2:**

```
Input: head = [1], n = 1
Output: []
```

**Example 3:**

```
Input: head = [1,2], n = 1
Output: [1]
```

&#x20;

**Constraints:**

* The number of nodes in the list is `sz`.
* `1 <= sz <= 30`
* `0 <= Node.val <= 100`
* `1 <= n <= sz`

&#x20;

**Follow up:** Could you do this in one pass?

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if(head == NULL) {
            return head;
        }
        



        ListNode *prev = NULL;
        ListNode *slow = head;
        ListNode *fast = head;
        
        int count = 0;
        while(fast!=NULL && count<n){
            fast = fast->next;
            count++;
        }

        while(fast != NULL){
            prev = slow;
            slow = slow->next;
            fast = fast->next; 
        }
        if(prev == NULL){
            ListNode *temp = head->next;
            delete head;
            
            return temp;
            
        }
        prev->next = slow->next;
        slow->next = NULL;
        
        delete slow;
        return head;
        
    }
};
```
