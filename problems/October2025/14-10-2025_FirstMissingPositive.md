# First Missing Positive (LeetCode)
Link: https://leetcode.com/problems/first-missing-positive/description/
Solution - 
## Brute Force Approach
**Time Complexity**: O(n^2)
**Space Complexity**: O(1)
```C++
int firstMissingPositive(vector<int>& nums) {
    int n = nums.size();
    for (int i = 1; i <= n + 1; ++i) {
        bool found = false;
        for (int num : nums) {
            if (i == num) {
                found = true;
                break;
            }
        }
        if (!found) {
            return i;
        }
    }
    return 1;
}
```

## HashSet Approach
**Time Complexity**: O(n)
**Space Complexity**: O(n)
```C++
int firstMissingPositive(vector<int>& nums) {
    unordered_set<int> numSet(nums.begin(), nums.end());
    for (int i = 1; i <= nums.size() + 1; ++i) {
        if (numSet.find(i) == numSet.end()) {
            return i;
        }
    }
    return 1; 
}
```

##  Cyclic Sort Approach
**Time Complexity**: O(n)
**Space Complexity**: O(1)
```C++
int firstMissingPositive(vector<int>& nums) {
    int n = nums.size();
    for (int i = 0; i < n; ++i) {
        while (nums[i] > 0 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
            swap(nums[i], nums[nums[i] - 1]);
        }
    }
    for (int i = 0; i < n; ++i) {
        if (nums[i] != i + 1) {
            return i + 1;
        }
    }
    
    return n + 1;
}
```