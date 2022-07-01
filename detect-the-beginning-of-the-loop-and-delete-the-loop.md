# Detect The Beginning of the Loop & delete the loop

<img src=".gitbook/assets/file.drawing (14).svg" alt="Problem Explanation" class="gitbook-drawing">

Given a linked list return the beginning of the loop if loop exists else return NULL

**Approach**

**Step 1: fast = Detect if the loop is present or not and return fast Pointer**&#x20;

<img src=".gitbook/assets/file.drawing (1).svg" alt="" class="gitbook-drawing">

**Step2: if(fast == NULL) then it means there's no loop therefore return NULL**

**Step3: If fast is present then , set the slow to the head**

<img src=".gitbook/assets/file.drawing (19).svg" alt="" class="gitbook-drawing">

**Step 4: Move both slow and fast pointer one step ahead until slow == fast**

<img src=".gitbook/assets/file.drawing (3).svg" alt="" class="gitbook-drawing">

**Step 5: to delete the loop temp = slow and iterate over temp until temp->next!= slow**

<img src=".gitbook/assets/file.drawing (13).svg" alt="" class="gitbook-drawing">

**Step 6: temp->next = NULL**

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
    ListNode *detectLoop(ListNode *head){
        if(head == NULL) return NULL;
        ListNode *slow = head;
        ListNode *fast = head;
        while(fast!=NULL && fast->next!=NULL ){
            slow = slow->next;
            fast = fast->next->next;
            if(slow == fast){
                return slow;
            }
        }
        
        return NULL;
    }
    ListNode *detectCycle(ListNode *head) {
        ListNode *fast = detectLoop(head);
        if(fast==NULL){
            // there's no cycle found therfore return head;
            return NULL;
        }
        ListNode *slow = head;

        while(slow!=fast){
            slow = slow->next;
            fast = fast->next;
        }
// Below is the code to delete the loop
         ListNode *temp = slow;
         while(temp->next != slow){
             temp = temp->next;
         }
        
         temp->next = NULL;
        
        return slow;
    }
};
```
