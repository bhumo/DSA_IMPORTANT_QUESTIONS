# Merge 2 Sorted Linked List

**Approach**

**Step 1: Create a dummy node and keep appending to it which ever is smaller element as compared to L1 or L2**

**Step 2: If any of element in L1 or L2 is remaining add that to the DummyList**

**Step 3: head = dummy->next and then free the memory for dummy node and return head**&#x20;

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
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
     ListNode *temp1,*temp2;
        temp1 = list1;
        temp2 = list2;
        ListNode *dummy = new ListNode(-1);
        ListNode *dummyNode = dummy;
        
        
        // Step 1: Create a dummy node and keep 
        //appending to it which ever is smaller element as compared to L1 or L2
        
        while(temp1!=NULL && temp2!=NULL){
            
            if(temp1->val <= temp2->val){
                dummyNode->next = temp1;
                dummyNode = temp1;
                temp1 = temp1->next;
            }else{
                dummyNode->next= temp2;
                dummyNode = temp2;
                temp2 = temp2->next;
            }
            dummyNode->next = NULL;
        }
        
        //Step 2: If any of element in L1 or L2 is remaining 
        //add that to the DummyList
        if(temp1){
            dummyNode->next = temp1;
        }
        
        if(temp2){
            dummyNode->next = temp2;
        }
        //Step 3: head = dummy->next and then free the memory for dummy node 
        //and return head
        ListNode *head = dummy->next;
        dummy->next=  NULL;
        delete dummy;
        return head;
        
    }
};
```
