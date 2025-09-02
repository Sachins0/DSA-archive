# House Robber (LeetCode)
Link: https://leetcode.com/problems/house-robber/description/

Solution - 
## Approach 1: Recursion
- **Time Complexity:** O(2^n) **Space Complexity:** O(n)
```C++
int robUtil(vector<int>& nums, int i) {
    if(i >= nums.size()) return 0;
    return max((nums[i] + robUtil(nums, i + 2)), 
    robUtil(nums, i + 1));
}
```

## Approach 2: Recursion with Memoization
- **Time Complexity**: O(n)  **Space Complexity**: O(n)
```C++
vector<int> dp;
int robUtil(vector<int>& nums, int i) {
    if(i >= nums.size()) return 0;
    if(dp[i] != -1) return dp[i];
    return dp[i] = max((nums[i] + robUtil(nums, i + 2)), 
    robUtil(nums, i + 1));
}
int rob(vector<int>& nums) {
    int n = nums.size();
    dp.resize(n+1, -1);
    return robUtil(nums, 0);
}
```
## Approach 3: Dynamic Programming (Bottom-Up)
- **Time Complexity**: O(n)  **Space Complexity**: O(n)
```C++
vector<int> dp;
int rob(vector<int>& nums) {
    int n = nums.size();
    dp.resize(n+1, 0);
    dp[n-1] = nums[n-1];
    for(int i = n-2; i >= 0; i--) {
        dp[i] = max((nums[i] + dp[i + 2]), dp[i + 1]);
    }
    return dp[0];
}
```

## Approach 4: Dynamic Programming with Space Optimization
- **Time Complexity**: O(n)  **Space Complexity**: O(q)
```C++
int rob(vector<int>& nums) {
    int n = nums.size();
    int prev2 = 0;
    int prev1 = nums[n-1];
    int next = 0;
    for(int i = n-2; i >= 0; i--) {
        next = max((nums[i] + prev2), prev1);
        prev2 = prev1;
        prev1 = next;
    }
    return prev1;
}
```