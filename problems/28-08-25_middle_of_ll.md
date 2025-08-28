# Middle of the Linked List (LeetCode)
Link: https://leetcode.com/problems/middle-of-the-linked-list/description/

Solution - 
```C++
ListNode* middleNode(ListNode* head) {
    ListNode* slow = head, *fast = head;
    while(fast -> next && fast->next -> next) {
        fast = fast -> next -> next;
        slow = slow -> next;
    }
    return fast -> next ? slow -> next : slow;
}
```
