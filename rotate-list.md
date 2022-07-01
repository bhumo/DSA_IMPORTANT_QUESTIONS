---
description: https://leetcode.com/problems/rotate-list/
---

# Rotate List



Given the `head` of a linked list, rotate the list to the right by `k` places.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg)

```
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg)

```
Input: head = [0,1,2], k = 4
Output: [2,0,1]
```

&#x20;

**Constraints:**

* The number of nodes in the list is in the range `[0, 500]`.
* `-100 <= Node.val <= 100`
* `0 <= k <= 2 * 109`



**Approach**

**Step 1 : Get the length of the linked list**

**Step 2: Handle Edge Case**

&#x20;**** if n==0: empty list hence no rotation needed

if k==0 then no rotation

if k%n == 0 then also no rotation

&#x20;**Step 3** : k = k%n as k>n sometimes

**Step 4 traverse n-k node** &#x20;

**Step 5 n-k th node = NULL (now we have two LL one LL node 1 to (n-kth )node another (kth node to nth node)**

**Step6: Find the tail of second LL \[k to nth node] then tail->next = head**

**Step 7 return the new head**

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
    int getLength(ListNode *head){
        int length  = 0;
        while(head!=NULL){
            length++;
            head = head->next;
        }
        
        return length;
    }
    ListNode* rotateRight(ListNode* head, int k) {
        //Step1 : Get the length of the liked list
        int n = getLength(head);
        //Edge Cases
        // n == 0: means the list is empty
        // k==0 means no rotation
        // k%n == 0 means no rotation
        if(n==0 || k==0 || k%n == 0) return head;

        // do k mod with n because k>n is possible input 
        k = k%n;
        
        //Step 3: traverse n-k node
        int t = n - k;
        ListNode *temp = head;    
        while(--t){
            temp = temp->next;
        }
        
        //Step 4: Store the kth node(temp->next) as newHead         
        
        ListNode *newHead = temp->next;
        
        //Step5: make the (n-k)th node next null
        temp->next = NULL;
       
        //Step6: Find the tail of the Kth-Nth nodes range
        ListNode* tail = newHead;
        while(tail->next!=NULL){
            tail = tail->next;
        }
        
        //Step7: Link tail with the first LL's head
        tail->next = head;
        
        //Step8: Return the updated head
        return newHead;
    }
};
```
