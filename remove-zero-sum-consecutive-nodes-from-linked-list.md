---
description: >-
  https://leetcode.com/problems/remove-zero-sum-consecutive-nodes-from-linked-list/
---

# Remove zero sum consecutive Nodes from Linked List

Given the `head` of a linked list, we repeatedly delete consecutive sequences of nodes that sum to `0` until there are no such sequences.

After doing so, return the head of the final linked list.  You may return any such answer.

&#x20;

(Note that in the examples below, all sequences are serializations of `ListNode` objects.)

**Example 1:**

```
Input: head = [1,2,-3,3,1]
Output: [3,1]
Note: The answer [1,2,1] would also be accepted.
```

**Example 2:**

```
Input: head = [1,2,3,-3,4]
Output: [1,2,4]
```

**Example 3:**

```
Input: head = [1,2,3,-3,-2]
Output: [1]
```

**Example 4:**

```
Input: head = [-1,2,3,-3,1]
Output: [-1,2,1]
```

**Approach 1: With Dummy List**

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
    ListNode* solve(ListNode* head,bool &isChanged){
        if(head==NULL){
            return head;
        }
        int sum = 0;
        ListNode *temp =head;
        while(temp!=NULL){
            sum = sum + temp->val;
            if(sum==0){
                isChanged = true;
                break;
            }
            temp=temp->next;
        }
        if(temp==NULL) return temp;
        return temp->next;
    }
    ListNode* removeZeroSumSublists(ListNode* head) {
        if(head == NULL){
            return head;
        }
         ListNode *dummy = new ListNode(-1);
         dummy->next = head;
         ListNode* temp = dummy;
        ListNode *temp2 = head;
        while(temp2!=NULL){
            bool isChanged = false;
            ListNode *nextNode = solve(temp2,isChanged);
            if(isChanged){
                temp->next = nextNode;
                temp2=nextNode;
                continue;
            }
            temp->next = temp2;
            temp = temp2;
            temp2 = temp2->next;
        }
        return dummy->next;
    }
};
```

**Approach 2: Without dummy list**

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
    ListNode* solve(ListNode* head,bool &isChanged){
        if(head==NULL){
            return head;
        }
        int sum = 0;
        ListNode *temp =head;
        while(temp!=NULL){
            sum = sum + temp->val;
            if(sum==0){
                isChanged = true;
                return temp->next;
            }
            temp=temp->next;
        }
        head->next = solve(head->next,isChanged);
        return head;
    }
    ListNode* removeZeroSumSublists(ListNode* head) {
        if(head == NULL){
            return head;
        }
         ListNode *dummy = new ListNode(-1);
         dummy->next = head;
         ListNode* temp = dummy;
        ListNode *temp2 = head;
        while(true){
            bool isChanged = false;
            head = solve(head,isChanged);
            if(head == NULL || isChanged==false){
                break;
            }
            
        }
        return head;
    }
};
```
