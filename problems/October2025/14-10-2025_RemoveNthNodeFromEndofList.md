# Remove Nth Node From End of List (LeetCode)
Link: https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/
Solution - 
## Approach 1: Two Pass Algorithm
**Time Complexity**: O(l)
**Space Complexity**: O(1)
```C++
ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode *dummy = new ListNode(0, head);
    ListNode *current = head;
    int length = 0;
    while (current != nullptr) {
        length++;
        current = current->next;
    }

    length -= n;
    current = dummy;
    while (length > 0) {
        length--;
        current = current->next;
    }
    current->next = current->next->next;
    return dummy->next;
}
```

## Approach 2: Single Pass Using Two Pointers
**Time Complexity**: O(l)
**Space Complexity**: O(1)
```C++
ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode *dummy = new ListNode(0, head);
    ListNode *fast = dummy;
    ListNode *slow = dummy;

    for (int i = 0; i <= n; i++) {
        fast = fast->next;
    }

    while (fast != nullptr) {
        fast = fast->next;
        slow = slow->next;
    }

    slow->next = slow->next->next;

    return dummy->next;
}
```