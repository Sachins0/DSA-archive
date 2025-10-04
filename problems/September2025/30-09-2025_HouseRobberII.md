# House Robber II (LeetCode)
Link: https://leetcode.com/problems/house-robber-ii/description/

Solution - 
## Approach 1: Brute-force(Recursion)
### Complexity
- Time Complexity: O(2^n)
- Space Complexity: O(n)
```C++
class Solution {
private:
    int robUtil(vector<int>& nums, int i, int n) {
        if(i >= n) return 0;
        int loot = nums[i]+robUtil(nums, i+2, n);
        int leave = robUtil(nums, i+1, n);
        return max(loot, leave);
    }
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n == 1) return nums[0];
        return max(robUtil(nums, 0, n-1), robUtil(nums, 1, n));
    }
};
```

## Approach 2: Dynamic Programming with Memoization
### Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)
```C++
class Solution {
private:
    int robUtil(vector<int>& nums, int i, int n, vector<int>& dp) {
        if(i > n) return 0;
        if(dp[i] != -1) return dp[i];
        int loot = nums[i]+robUtil(nums, i+2, n, dp);
        int leave = robUtil(nums, i+1, n, dp);
        dp[i] = max(loot, leave);
        return dp[i];
    }
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n == 1) return nums[0];
        vector<int> dp1(n, -1);
        vector<int> dp2(n, -1);
        return max(robUtil(nums, 0, n-2, dp1), 
                    robUtil(nums, 1, n-1, dp2));
    }
};
```

## Approach 3: Dynamic Programming with Tabulation
### Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)
```C++
class Solution {
private:
    int robUtil(vector<int>& nums, int idx, int n, vector<int>& dp) {
        for(int i = n; i >= idx; i--) {
            int loot = nums[i]+dp[i+2];
            int leave = dp[i+1];
            dp[i] = max(loot, leave);
        }
        
        return dp[idx];
    }
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n == 1) return nums[0];
        vector<int> dp1(n+2, 0);
        vector<int> dp2(n+2, 0);
        return max(robUtil(nums, 0, n-2, dp1), 
                    robUtil(nums, 1, n-1, dp2));
    }
};
```

## Approach 4: Optimized Dynamic Programming
### Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)
```C++
class Solution {
private:
    int robUtil(vector<int>& nums, int idx, int n) {
        int prev1 = 0, prev2 = 0;
        for(int i = n; i >= idx; i--) {
            int loot = nums[i]+prev2;
            int leave = prev1;
            int next = max(loot, leave);
            prev2 = prev1;
            prev1 = next;
        }
        
        return prev1;
    }
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n == 1) return nums[0];
        return max(robUtil(nums, 0, n-2), 
                    robUtil(nums, 1, n-1));
    }
};
```
