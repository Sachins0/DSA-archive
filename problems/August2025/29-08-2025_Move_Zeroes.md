# Move Zeroes (LeetCode)
Link: https://leetcode.com/problems/move-zeroes/description/

Solution - 
## Approach 1
```C++
void moveZeroes(vector<int>& nums) {
    int lastNonZero = 0;
    for(int i = 0; i < nums.size(); i++) {
        if(nums[i]!= 0) {
            swap(nums[lastNonZero], nums[i]);
            lastNonZero++;
        }
    }
}
```

## Approach 2
```C++
void moveZeroes(vector<int>& nums) {
    int lastNonZero = 0;
    for(int i = 0; i < nums.size(); i++) {
        if(nums[i] != 0) nums[lastNonZero++] = nums[i];
    }
    for(int i = lastNonZero; i < nums.size(); i++) {
        nums[i] = 0;
    }
}

```
