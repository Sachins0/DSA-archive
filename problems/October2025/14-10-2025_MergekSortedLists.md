# Merge k Sorted Lists (LeetCode)
Link: https://leetcode.com/problems/merge-k-sorted-lists/description/
Solution - 
## Approach 1: Brute Force - Collect and Sort
**Time Complexity**: O(nlogn)
**Space Complexity**: O(n)
```C++
ListNode* mergeKLists(vector<ListNode*>& lists) {
    vector<int> nodes;
    for (auto list : lists) {
        while (list) {
            nodes.push_back(list->val);
            list = list->next;
        }
    }
    sort(nodes.begin(), nodes.end());
    ListNode* dummy = new ListNode();
    ListNode* current = dummy;
    for (int val : nodes) {
        current->next = new ListNode(val);
        current = current->next;
    }
    
    return dummy->next;
}
```

## Approach 2: Min-Heap Approach
**Time Complexity**: O(nlogk)
**Space Complexity**: O(k)
```C++
ListNode* mergeKLists(vector<ListNode*>& lists) {
    auto compare = [](ListNode* a, ListNode* b){return a->val > b->val;};
    priority_queue<ListNode*, vector<ListNode*>, decltype(compare)> minH(compare);
    for(auto list : lists) {
        if(list) minH.push(list);
    }
    ListNode* dummy = new ListNode();
    ListNode* curr = dummy;
    while(!minH.empty()) {
        ListNode* temp = minH.top();
        minH.pop();
        curr -> next = temp;
        curr = curr -> next;
        if(temp -> next) minH.push(temp->next);
    }
    return dummy->next;
}
```

## Approach 3: Divide and Conquer
**Time Complexity**: O(nlogk)
**Space Complexity**: O(1)
```C++
class Solution {
private:
    ListNode* mergeTwoLL(ListNode* l1, ListNode* l2) {
        ListNode dummy;
        ListNode* temp = &dummy;
        while(l1 && l2) {
            if(l1 -> val < l2 -> val) {
            temp -> next = l1;
            l1 = l1->next;
            }else {
                temp -> next = l2;
                l2 = l2 -> next;
            }
            temp = temp -> next;
        }
        temp -> next = l1 ? l1 : l2;
        return dummy.next;
    }
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.empty()) return nullptr;
        int n = lists.size();
        int interval = 1;
        while(interval < n) {
            for(int i = 0; i + interval < n; i+= 2*interval) {
            lists[i] = mergeTwoLL(lists[i], lists[i+interval]);
            }
            interval *= 2;
        }
        return lists[0];
    }
};
```

## Alternate Approach 3
```C++
class Solution {
private:
    ListNode* mergeTwoLL(ListNode* l1, ListNode* l2) {
        if(!l1) return l2;
        if(!l2) return l1;
        if(l1 -> val < l2 -> val) {
            l1 -> next = mergeTwoLL(l1->next, l2);
            return l1;
        }else {
            l2 -> next = mergeTwoLL(l1, l2->next);
            return l2;
        }
        return nullptr;
    }

    ListNode* partitionAndMerge(int start, int end, vector<ListNode*>& lists) {
        if(start > end) return nullptr;
        if(start == end) return lists[start];
        int mid = start + (end - start)/2;
        ListNode* l1 = partitionAndMerge(start, mid, lists);
        ListNode* l2 = partitionAndMerge(mid+1, end, lists);
        return mergeTwoLL(l1, l2);
    }
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.empty()) return nullptr;
        int n = lists.size();
        return partitionAndMerge(0, n-1, lists);
    }
};
```