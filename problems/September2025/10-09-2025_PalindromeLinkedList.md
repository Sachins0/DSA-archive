# Palindrome Linked List (LeetCode)
Link: https://leetcode.com/problems/palindrome-linked-list/description/

Solution - 
## Approach 1: Using Stack
```C++
bool isPalindrome(ListNode* head) {
    stack<int>st;
    ListNode* ptr=head;
    while(ptr!=NULL){
        st.push(ptr->val);
        ptr=ptr->next;
    }
    while(head!=NULL && !st.empty()){
        if(head->val!=st.top()) return false;
        else st.pop();
        head=head->next;
    }
    return true;
}
```

## Approach 1: Using reversal
```C++
class Solution {
public:
    ListNode* reversell(ListNode* head2){
        ListNode* ptr1=NULL;
        ListNode* ptr2=head2;
        while(ptr2!=NULL){
            ListNode* ptr3=ptr2->next;
            ptr2->next=ptr1;
            ptr1=ptr2;
            ptr2=ptr3;
        }
        return ptr1;
    }
    bool isPalindrome(ListNode* head) {
        // Floyd’s cycle finding algorithm  
        ListNode* slow=head;
        ListNode* fast=head;
        if(head==NULL || head->next==NULL) return true;
        while(fast->next && fast->next->next){
            slow=slow->next;
            fast=fast->next->next;
        }
        ListNode* revhead=reversell(slow->next);
        ListNode* p1=head;
        ListNode* p2=revhead;
        while(p2){
            if(p1->val!=p2->val){
                reversell(revhead);
                 return false;
            }
            p1=p1->next;
            p2=p2->next;
        }
        reversell(revhead);
        return true;
    }
};
```
