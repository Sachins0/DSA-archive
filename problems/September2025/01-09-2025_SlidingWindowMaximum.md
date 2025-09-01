# Sliding Window Maximum (LeetCode)
Link: https://leetcode.com/problems/sliding-window-maximum/description/

Solution - 
## Optimized Approach using a Deque
```C++
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> dq;
    vector<int> res;
    for(int i = 0; i < nums.size(); i++) {
        while(!dq.empty() && dq.front() <= i-k ) dq.pop_front();
        while(!dq.empty() && nums[i] > nums[dq.back()]) 
            dq.pop_back();
        dq.push_back(i);
        if(i >= k-1) res.push_back(nums[dq.front()]);
    }
    return res;
}
```
