# Reverse Linked List in K groups

Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return _the modified list_.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse\_ex1.jpg)

```
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse\_ex2.jpg)

```
Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]
```

&#x20;

**Constraints:**

* The number of nodes in the list is `n`.
* `1 <= k <= n <= 5000`
* `0 <= Node.val <= 1000`

&#x20;

**Follow-up:** Can you solve the problem in `O(1)` extra memory space?

Approach: Recursive solution

Step 1: Let us check if we have k nodes or not, in case less than k nodes return head&#x20;

Step 2: If k nodes found reverse them&#x20;

Step3: head will be our last node after reversal therefore, head->next = Recursive Call

Step 4 return prev

<img src=".gitbook/assets/file.drawing (2).svg" alt="Explanation" class="gitbook-drawing">

TC: O(N)

SC: O(N)

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
    ListNode* reverseKGroup(ListNode* head, int k) {
       //Edge Case or base case
       if(head == NULL){
           return head;
       } 
        int count = 0;
        ListNode *prev,*curr,*next;
        prev = NULL;
        next = NULL;
        curr = head;
        ListNode *temp = head;
        
        // Step1: Count if K Nodes exists or not
        while(temp!=NULL && count!=k){
            count++;
            temp=temp->next;
        }
        // Return head if the k nodes does not exits 
        if(count<k) return head;
        count=0;
        // Step2 Reverse the K Nodes
        while(curr!=NULL && count<k){
            next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
            count++;
        }   
        // Step3 Connect the swapped list and LL from the recusive call
        
         head->next = reverseKGroup(curr,k);
        
        //Step 4 return the head of the reverse list which will be found at prev
        return  prev;
    }
};
```
