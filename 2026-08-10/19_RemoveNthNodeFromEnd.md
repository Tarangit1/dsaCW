```cpp
ListNode* removeNthNodeFromEnd(ListNode* root, int n){

    ListNode *ahead = root;
    ListNode *behind = root;

    for(int i = 0 ; i < n ;i++){  // get the fast node to nth node
        ahead = ahead->next;
    }

    if(!ahead) return root->next;  // if the fast pointer is null, it means we need to remove the head node

    while(ahead!=null && ahead->next!=null){ // move both pointers until the fast pointer reaches the end
        ahead = ahead->next;
        behind = behind->next;
    }
    behind->next = behind->next->next; // remove the nth node
    return root;

}
```