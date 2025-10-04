# Intersection of Two Linked Lists (LeetCode)
Link: https://leetcode.com/problems/intersection-of-two-linked-lists/description/

Solution - 
## Approach Two Pointers
- Time Complexity: O(N+M)
 - Space Complexity: O(1)
```C++
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* tempA = headA, *tempB = headB;
        while(tempA != tempB) {
            tempA = (tempA == nullptr) ? headB : tempA -> next;
            tempB = (tempB == nullptr) ? headA : tempB -> next;
        }
        return tempA;
    }
```