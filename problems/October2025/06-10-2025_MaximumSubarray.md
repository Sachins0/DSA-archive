# Maximum Subarray (LeetCode)
Link: https://leetcode.com/problems/maximum-subarray/description/

Solution - 
## Approach 1: Brute Force
**Time Complexity**: O(n^2)

**Space Complexity**: O(1)
```C++
int maxSubArray(vector<int>& nums) {
    int n = nums.size();
    int maxSum = nums[0];
    int currSum = 0;
    for(int i = 0; i < n; i++) {
        currSum = 0;
        for(int j = i; j < n; j++) {
            currSum += nums[j];
            if(currSum > maxSum) maxSum = currSum;
        }
    }
    return maxSum;
}
```

## Approach 2: Kadane's Algo
**Time Complexity**: O(n)
**Space Complexity**: O(1)
```C++
int maxSubArray(std::vector<int>& nums) {
    int maxSum = INT_MIN;  
    int currentSum = 0;    
    for (int num : nums) { 
        currentSum += num; 
        if (currentSum > maxSum) { 
            maxSum = currentSum;
        }
        if (currentSum < 0) { 
            currentSum = 0;
        }
    }
    return maxSum;
}
```