# Middle Element of Linked List





Given the `head` of a singly linked list, return _the middle node of the linked list_.

If there are two middle nodes, return **the second middle** node.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

```
Input: head = [1,2,3,4,5]
Output: [3,4,5]
Explanation: The middle node of the list is node 3.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg)

```
Input: head = [1,2,3,4,5,6]
Output: [4,5,6]
Explanation: Since the list has two middle nodes with values 3 and 4, we return the second one.
```

&#x20;

**Constraints:**

* The number of nodes in the list is in the range `[1, 100]`.
* `1 <= Node.val <= 100`

<img src=".gitbook/assets/file.drawing (17).svg" alt="" class="gitbook-drawing">

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
    ListNode* middleNode(ListNode* head) {
        
        ListNode *slow =head;
        ListNode *fast = head;
        
        while(fast!=NULL && fast->next!=NULL){
            // hey i am slow like turtle and i will walk one step at a time....
            slow = slow->next;
            // hey i am super fast so i am gonna walk twice steps everytime because i lost to turtle last time as i fell asleep in the middle of the race..... 
            fast = fast->next->next;
        }
        
        //sadly rabit still lost as it went too fast and missed middle element LOL
        
        
        //HEY TUTRLE WON by doing just n/4 steps unlike rabbit who walked n/2 steps cool yeah!!!
        return slowly;
    }
};
```
