# Merge Two Sorted Lists (LeetCode)
Link: https://leetcode.com/problems/jump-game-ii/description/

Solution - 
## Approach 1: Iterative Approach
- Time Complexity: O(n+m)
 - Space Complexity: O(1)
```C++
ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
    ListNode* dummyNode = new ListNode(-1);
    ListNode* temp = dummyNode;
    ListNode* h1 = list1, *h2 = list2;
    while(h1 && h2) {
        if(h1 -> val >= h2 -> val) {
            temp -> next = h2;
            h2 = h2 -> next;
        }
        else {
            temp -> next = h1;
            h1 = h1 -> next;
        }
        temp = temp -> next;
    }
    while(h1) {
        temp -> next = h1;
        h1 = h1 -> next;
        temp = temp -> next;
    }
    while(h2) {
        temp -> next = h2;
        h2 = h2 -> next;
        temp = temp -> next;
    }
    return dummyNode -> next;
}
```

## Approach 2: Recusrive Approach
- Time Complexity: O(n+m)
- Space Complexity: O(1)
```C++
ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
    ListNode* dummyNode = new ListNode(-1);
    ListNode* temp = dummyNode;
    ListNode* h1 = list1, *h2 = list2;
    while(h1 && h2) {
        if(h1 -> val >= h2 -> val) {
            temp -> next = h2;
            h2 = h2 -> next;
        }
        else {
            temp -> next = h1;
            h1 = h1 -> next;
        }
        temp = temp -> next;
    }
    if(h1) {
        temp -> next = h1;
    }
    if(h2) {
        temp -> next = h2;
    }
    return dummyNode -> next;
}
```