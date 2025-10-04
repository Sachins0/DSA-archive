# Range Sum Query - Immutable (LeetCode)
Link: https://leetcode.com/problems/range-sum-query-immutable/description/

Solution - 
## Approach 1: Brute Force
- Time Complexity:
Query time complexity is (O(n)) per query, where (n = j - i + 1).
 - Space Complexity:
(O(1))
```C++
class NumArray {
private:
    vector<int> data;
public:
    NumArray(vector<int>& nums) : data(nums) {
    }
    
    int sumRange(int left, int right) {
        int ans = 0;
        for(int i = left; i<= right; i++) {
            ans += data[i];
        }
        return ans;
    }
};
```

## Approach 2: Prefix Sum
- Time Complexity:
Building the prefix sum takes (O(n)).
Query time complexity is (O(1)) per query.
- Space Complexity:
(O(n)) for the prefix sum array.

```C++
class NumArray {
private:
    vector<int> pfixSum;
public:
    NumArray(vector<int>& nums) {
        int n = nums.size();
        pfixSum.resize(n+1, 0);
        for(int i = 0; i < n; i++) {
            pfixSum[i+1] = nums[i]+pfixSum[i];
        }
    }
    
    int sumRange(int left, int right) {
        return pfixSum[right+1] - pfixSum[left]; 
    }
};
```
