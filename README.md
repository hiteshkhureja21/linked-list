# linked-list
singly ll
code for deletion and insertion
#include <iostream>
using namespace std;

class Node{
    public:
    int data ;
    Node* next;
    //constructor
    Node(int d){
        this->data = d;
        this->next = NULL;
    }
    ~Node(){
        int value = this->data;
        cout << "Destructor called for node: " << data << endl;
    }
};
void insertathead(Node* &head,int d){
    Node* temp = new Node(d);
    temp->next = head;
    head = temp;
}
void insertattail(Node* &tail,int d){
    Node* temp = new Node(d);
    tail->next = temp;
    tail = temp;
}
void insertatmid(Node* &head,Node* &tail,int pos,int d){
    Node* temp = head;
    int count = 1;
    while(count<pos -1 ){
        temp = temp->next;
        count++;
    }
    Node *insert = new Node(d);
    insert->next = temp->next;
    temp->next = insert;
    if(pos == 1){
        insertathead(head,d);
        return;
    }
    if(temp->next==NULL){
        insertattail(tail,d);
        return;
    }
}
void deletion(Node* &head,int pos){
    if(pos == 1){
        Node *temp = head;
        head = head -> next;
        delete temp;
    }else{
        Node *curr = head;
        Node *prev = NULL;
        int count = 1;
        while(count<pos){
            prev = curr;
            curr = curr->next;
            count++;
        }
        prev->next = curr->next;
        curr->next = NULL;
    }
}
void print(Node * &head){
    Node* temp = head;
    while(temp!=NULL){
        cout<<temp->data<<" ";
        temp = temp->next;
    }
    cout<<endl;
}
int main() {
    Node *node1 = new Node(12);
    Node* head = node1;
    head->next = new Node(10);
    Node* tail = head->next;
    print(head);
    insertathead(head,17);
    print(head);
    insertattail(tail,19);
    print(head);
    insertatmid(head,tail,2,100);
    print(head);
    cout<<"here is call for delection"<<endl;
    deletion(head,3);
    print(head);
    return 0;
}
// doubly linked list
#include <iostream>
using namespace std;

class Node{
    public:
    int data;
    Node* prev;
    Node* next;
    //constructor
    Node(int d){
        this->data = d;
        this->prev = NULL;
        this->next = NULL;
    }
    //destructor
    ~Node(){
        cout<<"destructor calling"<<endl;
    }
};
void insertathead(Node * &head ,int d){
    Node *temp = new Node(d);
    temp->next = head;
    head->prev = temp;
    head = temp;
}
void insertattail(Node * &tail ,int d){
    Node *temp = new Node(d);
    tail->next = temp;
    temp->prev = tail;
    tail = temp;
}
void insert(Node * &head,Node * &tail,int pos ,int d){
    Node*temp = head;
    if(pos == 1){
        insertathead(head,d);
        return;
    }
    if(temp->next == NULL){
        insertattail(tail,d);
        return ;
    }
    int count = 1;
    while(count<pos-1){
        temp = temp->next;
        count++;
    }
    Node *insert = new Node(d);
    insert->next = temp->next;
    temp->next->prev = insert;
    temp->next = insert;
    insert->prev = temp;

}
void print(Node* &head){

    Node *temp = head;
    while(temp!=NULL){
        cout<<temp->data<<" ";
        temp = temp->next;
    }
    cout<<endl;
}
void delection(Node* &head,int d){
    Node*temp = head;
    if(d == 1){
        temp->next->prev = NULL;
        head = temp->next;
        temp -> next = NULL;
        delete temp;
    }else{
        Node*curr = head;
        Node*prev = NULL;
        int count = 1;
        while(count<d){
            prev = curr;
            curr = curr->next;
            count++;
        }
        curr->prev = NULL;
        prev->next = curr->next;
        curr->next = NULL;
        delete curr;
    }
}
int main(){
    Node *node1 = new Node(10);
    Node*head = node1;
    print(head);
    Node*tail = node1;
    insertathead(head,8);
    insertathead(head,18);
    insertattail(tail,28);
    print(head);
    insert(head,tail,2,100);
    print(head);
    delection(head,3);
    print(head);
}
for circular linked list
#include <iostream>
using namespace std;

class Node{
    public:
    int data;
    Node*next;
    //contructor
    Node(int data){
        this->data = data;
        this->next = NULL;
    }
    ~Node(){
        cout<<"destructor"<<endl;
    }
};
void insert(Node* &tail,int element,int d){
    if(tail == NULL){
        Node* newnode = new Node(d);
        tail = newnode;
        newnode->next = newnode;
    }else{
        Node *curr = tail;
        while(curr->data!=element){
            curr = curr->next;
        }
        Node *temp = new Node(d);
        temp->next = curr->next;
        curr->next = temp;
    }
}
void print(Node * &tail){
    Node *temp = tail;
    do{
        cout<<tail->data<<" ";
        tail = tail->next;
    }while(tail!=temp);
    cout<<endl;
}
void delection(Node * &tail,int value){
    if(tail==NULL){
        cout<<"Empty list"<<endl;
    }else{
        Node *prev = tail;
        Node *curr = prev->next;
        while(curr->data!=value){
            prev = curr;
            curr = curr->next;
        }
        prev -> next= curr->next;
        if(tail == curr){
            tail = prev;
        }
        curr->next = NULL;
        if(curr == prev){
            tail = NULL;
        }
        delete curr;
    }
}
int main(){
    //Node *node1 = new Node(10);
    //Node*tail = node1;
    Node*tail = NULL;
    insert(tail,3,10);
    print(tail);
    insert(tail,10,3);
    print(tail);
    delection(tail,3);
    print(tail);
}
