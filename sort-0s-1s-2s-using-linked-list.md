# Sort 0's 1's 2's using Linked List

<img src=".gitbook/assets/file.drawing (16).svg" alt="I/P and expected output" class="gitbook-drawing">

**Problem**

**Given a linked list, we have to sort it. The linked list will only contain 0's 1's 2's as it's value**

**Approach:**&#x20;

**Step1: Create dummy node for zero,one,two therefore, we will storing three lists**

zeroHead,oneHead,twoHead and there corresponding tails (zeroTail, oneTail,twoTail)



**Step 2: Traverse the List and update in the corresponding dummy list as per as value**

**Step 3: Connect the three dummy list** and return zeroHead->next;

<img src=".gitbook/assets/file.drawing (11).svg" alt="" class="gitbook-drawing">

```
class Node{
    public:
    int data;
    Node* next;
    Node(int data){
        this->data = data;
        this->next = NULL;
    }
};
void insertAtTail(Node* &tail,int data){
    //Step 1 :creation of node
    Node *newNode = new Node(data);
    
    //Step 2 : assign the current tail-> next node to the new node
    
    tail->next = newNode;
    
    //Step3: tail update
    
    tail = newNode;
    
    return;
}

void traverse(Node* &head){
    Node *temp=head;
    while(temp!=NULL){
        cout<<temp->data<<" ";
        temp = temp ->next;
    }
    cout<<endl;
}
Node* sort012(Node *head){
    Node* zeroHead,*zeroTail,*oneHead,*oneTail,*twoHead,*twoTail,*temp;
    temp = head;
    zeroHead = new Node(-1);
    zeroTail = zeroHead;
    
    oneHead = new Node(-1);
    oneTail = oneHead;
    
    twoHead = new Node(-1);
    twoTail = twoHead;
    
    while(temp!=NULL){
        Node *next = temp->next;
        if(temp->data == 0){
            zeroTail->next = temp;
            zeroTail=temp;
        }else if(temp->data == 1){
            oneTail->next = temp;
            oneTail = temp;
        }else if(temp->data ==2){
            twoTail->next = temp;
            twoTail = temp;
        }
        temp->next = NULL;
        temp = next;
    }
    twoTail->next = NULL;
    oneTail->next = twoHead->next;
    zeroTail->next = oneHead->next;

    return zeroHead->next;
}
int main() {
    Node* head = new Node(0);
    Node *tail = head;
    insertAtTail(tail,1);
    insertAtTail(tail,2);
    insertAtTail(tail,2);
    insertAtTail(tail,1);
    insertAtTail(tail,0);
    insertAtTail(tail,1);
    traverse(head);
    head = sort012(head);
    traverse(head);
  return 0;
}
```
