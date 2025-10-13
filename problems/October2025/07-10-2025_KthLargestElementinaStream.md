# Kth Largest Element in a Stream(LeetCode)
Link: https://leetcode.com/problems/kth-largest-element-in-a-stream/description/

Solution - 
## Approach 1: Naive Approach: Sorting Each Time
**Time Complexity**: O(nlogn)
**Space Complexity**: O(n)
```C++
class KthLargest {
public:
    KthLargest(int k, vector<int>& nums) : k(k), nums(nums) {
        sort(this->nums.begin(), this->nums.end(), greater<int>());
    }
    
    int add(int val) {
        nums.push_back(val);
        sort(nums.begin(), nums.end(), greater<int>());
        return nums[k - 1];  // Return the k-th largest element
    }

private:
    int k;
    vector<int> nums;
};
```

## Approach 2: Optimized Approach with Min-Heap
**Time Complexity**: O(logk)
**Space Complexity**: O(k)
```C++
class KthLargest {
private:
    int k;  
    priority_queue<int, vector<int>, greater<int>> pq;
public:
    KthLargest(int k, vector<int>& nums) : k(k) {
        for(int num : nums) add(num);
    }
    
    int add(int val) {
        pq.push(val);
        if(pq.size() > k) pq.pop();
        return pq.top();
    }
};
```