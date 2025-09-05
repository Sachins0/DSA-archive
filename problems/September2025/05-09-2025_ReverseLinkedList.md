# Reverse Linked List (LeetCode)
Link: https://leetcode.com/problems/reverse-linked-list/description/

Solution - 
## Iterative Approach
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)
```C++
ListNode* reverseList(ListNode* head) {
    if(!head) return NULL;
    ListNode* temp = head, *nextN = NULL, *prev = NULL;
    while(temp) {
        nextN = temp -> next;
        temp -> next = prev;
        prev = temp;
        temp = nextN;
    }
    return prev;
}
```

## Recursive Approach
- **Time Complexity**: O(n)
- **Space Complexity**: O(n)
```C++
 ListNode* reverseList(ListNode* head) {
    if(head==NULL || head->next==NULL) return head;
    ListNode* newhead=reverseList(head->next);
    head->next->next=head;
    head->next=NULL;
    return newhead;
}
```
