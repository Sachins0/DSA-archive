# Single Number (LeetCode)
Link: https://leetcode.com/problems/single-number/description/
Solution - 
## Approach 1: Brute Force Using Nested Loops 
**Time Complexity**: O(n^2)
**Space Complexity**: O(1)
```C++
int singleNumber(vector<int>& nums) {
    for(int i = 0; i < nums.size(); i++) {
        bool found = false;
        for(int j = 0; j < nums.size(); j++) {
            if (i != j && nums[i] == nums[j]) {
                found = true;
                break;
            }
        }
        if (!found) {
            return nums[i];
        }
    }
    return -1; 
}
```

## Approach 2: Using Sorting
**Time Complexity**: O(nlogn)
**Space Complexity**: O(1)
```C++
int singleNumber(vector<int>& nums) {
    sort(nums.begin(), nums.end()); 
    for(int i = 0; i < nums.size() - 1; i += 2) {
        if(nums[i] != nums[i+1]) {
            return nums[i];
        }
    }
    return nums.back();
}
```

## Approach 3: Using Hash Table
**Time Complexity**: O(n)
**Space Complexity**: O(n)
```C++
int singleNumber(vector<int>& nums) {
    unordered_map<int, int> countMap;
    for(int num : nums) {
        countMap[num]++;
    }
    for(auto& pair : countMap) {
        if(pair.second == 1) {
            return pair.first;
        }
    }
    return -1; 
}
```

## Approach 4: Bit Manipulation (Optimal Solution)
**Time Complexity**: O(n)
**Space Complexity**: O(1)
```C++
int singleNumber(vector<int>& nums) {
    int result = 0;
    for(int num : nums) {
        result ^= num; 
    }
    return result;
}
```