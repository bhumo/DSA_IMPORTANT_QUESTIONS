# Double Linked List

**Node**

```
class Node{
  public:
    int data;
    Node *prev;
    Node *next;
    
    Node(int data){
        this->data = data;
        this->prev = NULL;
        this->next = NULL;
    }
};

```

**Insert At Head**

```
void insertAtHead(Node* &head,int data)
{
    //step:1 Node creation
    
    Node* newNode = new Node(data);
    
    //step2: link the next of newNode to head
    
    newNode->next = head;
    
    //step:3 link the previous of head to newNode
    
    head->prev = newNode;
    
    //step:4 update the head
    head = newNode;
    return;
}
```

**Insert at tail**

```
void insertAtTail(Node* &tail, int data){
    
    //Step:1 Node creation
    
    Node* newNode = new Node(data);
    if(tail==NULL){

        tail = newNode;
        return;
    }
    //step2: link the next of tail to newNode
    
    tail->next = newNode;
    // step3: update the previous of newNode
    
    newNode->prev = tail; 
    
    //step4: update the tail
}
```

**Insert at position**

```
void insertAtPosition(Node* &head, Node* &tail, int data,int pos){
    //edge case: empty list
    if(head==NULL){
        Node* newNode = new Node(data);
        head = newNode;
        tail = newNode;
        return;
    }
    
    // insertAtHead
    
    if(pos==1){
        insertAtHead(head,data);
        return;
    }
    Node* newNode = new Node(data);
    int i=1;
    Node *prev = head;
    Node *temp = head;
    // traverse till the position
    // prev ==> pos-1 node
    // temp ==> pos node
    // temp will be NULL if pos is (length of DLL)+1 in this case 
    // we must update tail pointer as well
    
    while(i<=pos-1){
        if(temp==NULL){
            cout<<"Invalid positon"<<endl;
            return;
        }
        prev = temp;
        temp = temp->next;
        i++;
    }
    newNode->next = temp;
    newNode->prev = prev;
    if(temp){
        temp->prev = newNode;
    }
    else{
        
        tail = newNode;
    }
    prev->next = newNode;
    
    return;
}
```

**Delete Node**

```
void deleteNode(Node* &head, Node* &tail, int data){
    //Edge case: List is empty
    if(head == NULL){
        cout<<"Empty List"<<endl;
        return;
    }
    
    //if target data to delete is found at head node
    // in this case we will update the head
    if(head->data == data){
        Node* temp = head;
        head = head->next;
        temp->next=NULL;
        delete temp;
        return;
    }
    // If control reaches here there following scenarios are possible
    // 1. Node to delete in somewhere in between the DLL
    // 2. Node to delete is present at tail && requires us to update tail pointer
    // 3. Node doesn't exists
    Node *prev = NULL;
    Node *temp = head;
    while(temp && temp->data!=data){
        prev= temp;
        temp=temp->next;
    }
    //the node to delete is in temp && if data is not found then temp will be null
    if(temp==NULL){
        cout<<"No node with data "<<data<<endl;
        return;
    }
    prev->next=temp->next;
            // temp->next will be null if we are at the tail of DLL hence the needed check
        // if temp->next is not null we will assign temp->next->prev = prev
    if(temp->next){

       temp->next->prev =prev;
    }else{
        tail=prev;
    }
    temp->prev = NULL;
    temp->next = NULL;
    delete temp;
}
```
