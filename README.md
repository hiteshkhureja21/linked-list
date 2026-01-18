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
