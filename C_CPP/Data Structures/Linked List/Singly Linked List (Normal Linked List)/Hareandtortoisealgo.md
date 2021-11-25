# Question based on Floyd's Algorithm

- Traverse linked list using two pointers.
Move one pointer(fast) by two and another pointer(slow) by one.
If these pointers meet at the same node then there is a cycle. If pointers do not meet then linked list doesn’t have a cycle.

- Complexity Analysis

- Time Complexity - O(n)
- Space Complexity - O(1)
 
```CPP
#include<iostream>
using namespace std;

class node{
    public:
    int data;
    node* next;

    node(int val){
        data=val;
        next=NULL;
    }
};

void insertattail(node* &head, int val){

    node* n = new node(val);
    if(head==NULL){
        head=n;
        return;
    }

    node* temp=head;
    while(temp->next!=NULL){
        temp=temp->next;
    }
    temp->next =n;
}

void display(node* head){
    node* temp=head;
    while(temp!=NULL){
        cout<<temp->data<<"->";
        temp=temp->next;
    }
    cout<<"NULL"<<endl;
}

void makecycle(node* &head,int pos){
    node* temp=head;
    node* startnode;

    int count=1;
    while(temp->next!=NULL){
        if(count==pos){
            startnode=temp;
        }
        temp=temp->next;
        count++;
    }
    temp->next=startnode;
}


bool detectcycle(node* &head){
    node* slow=head;
    node* fast=head;

    while(fast!=NULL && fast->next!=NULL){
        slow=slow->next;
        fast=fast->next->next;

        if(fast==slow){
            return true;
        }
    }
    return false;
}

int main(){
    node* head=NULL;
    insertattail(head,1);
    insertattail(head,2);
    insertattail(head,3);
    insertattail(head,4);
    insertattail(head,5);
    insertattail(head,6);
    display(head);
    makecycle(head,3);//We will make cycle by using this function
    cout<<detectcycle(head)<<endl;//If cycle is there it will give 1 otherwise 0
    return (0);
}
```

## OUTPUT
```CPP
 1->2->3->4->5->6->NULL
 1
```
