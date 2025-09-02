# Reverse Nodes in k-Group (LeetCode)
Link: https://leetcode.com/problems/reverse-nodes-in-k-group/description/

Solution - 
```C++
ListNode* reverseLL(ListNode* head) {
    ListNode* curr = head;
    ListNode* prev = NULL;
    ListNode* nextN;
    while(curr) {
        nextN = curr -> next;
        curr -> next = prev;
        prev = curr;
        curr = nextN;
        
    }
    return prev;
}
ListNode* getkth(ListNode* temp, int k) {
    while(k!=1 && temp) {
        temp = temp -> next;
        k--;
    }
    return temp;
}
ListNode* reverseKGroup(ListNode* head, int k) {
    ListNode* temp = head, *prevLast = NULL;
    while(temp) {
        //get kth node
        ListNode* kthnode = getkth(temp, k);
        // grp smaller than k
        if(!kthnode) {
            if(prevLast){
                prevLast -> next = temp;
            } 
            break;
        }
        ListNode* nextNode = kthnode -> next;
        kthnode -> next = NULL;
        //Reverse the current group `kthnode` is the new head and `temp` is the new tail.
        reverseLL(temp);
        // first grp
        if(temp == head) {
            head = kthnode;
        }else {
            prevLast -> next = kthnode;
        }
        prevLast = temp;
        temp = nextNode;
    }
    return head;
}
```
