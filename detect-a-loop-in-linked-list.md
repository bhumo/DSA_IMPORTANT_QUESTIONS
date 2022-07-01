# Detect a Loop in Linked List

**Problem: Given a linked list, find if there exists a loop inside it.**

&#x20;

<img src=".gitbook/assets/file.drawing (15).svg" alt="input/output" class="gitbook-drawing">

**Approach: Floyd Cycle Detection Algorithm**

**Step1 : Move slow pointer one step**

**Step2: Move fast pointer two steps**

**Step 3 :**

**Now, if the linked does not contain a cycle, in that scenario, The Fast Pointer will become NULL**&#x20;

**In an scenario the linked list contains a cycle then at that time the slow == fast and we can conclude that the given linked list has a cycle.**

****

**Dry Run**

<img src=".gitbook/assets/file.drawing (18).svg" alt="DRY RUN for floyd cycle detection algorithm" class="gitbook-drawing">

**Code**

```
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
        if(head==NULL) return false;
        if(head->next == NULL) return false; 
     ListNode *slow,*fast;
        slow = head;
        fast = head;
        while(fast!=NULL && fast->next!=NULL){
            slow = slow->next;
            fast = fast->next->next;
            if(slow==fast){
                break;
            }
        }
        
        if(slow==fast){
            return true;
        }
        
        return false;
        
    }
};
```

**Proof why floyd cycle detection works**

<img src=".gitbook/assets/file.drawing (5).svg" alt="PROOF of Floyds Cycle Detection Algorithm that slow and fast will meet for sure" class="gitbook-drawing">

**Space Complexity : O(1)**

**Time Complexity: O(n)**

<img src=".gitbook/assets/file.drawing (9).svg" alt="" class="gitbook-drawing">
