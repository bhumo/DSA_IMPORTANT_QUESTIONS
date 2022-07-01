# Linked List basic operations

In linked list, we have a node.

Each node has one data member, and one Node\* next pointer which stores the address of the next node. If there's no next node then it will have NULL stored.&#x20;

<img src=".gitbook/assets/file.drawing (12).svg" alt="Visual representation of singly linked list" class="gitbook-drawing">

Node:

<img src=".gitbook/assets/file.drawing (4).svg" alt="" class="gitbook-drawing">

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
```



**Insertion**

Insertion can be done in three ways

* Insert at head
* Insert at tail
* Insert at position

**Insert at Head**

```
void insertAtHead(Node* &head,int data){
    //step:1 Creation of new node;
    Node *newNode = new Node(data);
    
    //step2 assign the head as the next node for the new node
    newNode->next = head;
    
    //step3 point head to newNode
    head = newNode;
    
    return;
    }
```

**Insert at tail**

```
void insertAtTail(Node* &tail,int data){
    //Step 1 :creation of node
    Node *newNode = new Node(data);
    
    //Step 2 : assign the current tail-> next node to the new node
    
    tail->next = newNode;
    
    //Step3: tail update
    
    tail = newNode;
    
    return;
    }
```

**Insert at position**

<img src=".gitbook/assets/file.drawing (6).svg" alt="explanation for the case where position asks to insert at tail" class="gitbook-drawing">

```
void insertAtPosition(Node* &head, Node* &tail, int data,int pos){
    //Step 1: Create the newNode
            
    
    //Edge Case: When the head and tail both are empty as in empty list
    if(head==NULL){
        Node *newNode = new Node(data);
        head = newNode;
        tail = newNode;
        // this means we have only one node hence, our head and tail will point to one node only
    return;
    }
    
    // if the control reaches here that means we have more than one node in linked list
    
    // now if the pos = 1 then we will be inserting at the head of the list 
    if(pos==1){
       insertAtHead(head,data); 
       return;
    }else{
        // here we will haddle case for insert at middle and tail
        
        Node* temp = head;
        int remaingPositions = pos-1; //pos -1 bcuz we are already at Node 1 
        int i=1;
        Node *prev = NULL;
        Node *newNode = new Node(data);
        while(i<=remaingPositions){
            if(temp==NULL){
                cout<<"Invalid position"<<endl;
                return;
            }
            prev= temp;
            temp = temp->next;
            i++;
        }
        prev->next = newNode;
        newNode->next = temp;
        
        if(temp==NULL){
            tail = newNode;
        }
        
    }
    
```

**DELETE**

```
void deleteNode(Node* &head, Node* &tail, int data){
    
    //Edge case: empty list
    if(head == NULL){
        cout<<"Empty list hence can not delete node with data: "<<data<<endl;
        return;
    }
    
    // The data to delete is actually found at head
    if(head->data == data){
        Node *temp = head;
        head = head->next;
        delete temp;
        return;
    }
    
    // now deletion can occur in the middle of the linked list or at the end or there's no such node
    Node *prev = NULL;
    Node *temp = head;
    bool found  = false;
    while(temp!=NULL ){
        if(temp->data == data){
            found = true;
            break;
        }
        prev = temp;
        temp = temp->next;
    }
    if(found){    
    prev->next = temp->next;
    if(temp->next == NULL){
    // for the last node the next pointer will point to NULL
        tail = prev;
    }
    temp->next = NULL;
    delete temp;
    }
    else{
        cout<<"No such data found"<<endl;
        return;
    }
    
    
}
```
