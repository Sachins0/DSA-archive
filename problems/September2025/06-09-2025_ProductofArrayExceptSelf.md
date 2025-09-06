# Product of Array Except Self (LeetCode)
Link: https://leetcode.com/problems/product-of-array-except-self/description/

Solution - 
## Approach 1: Two Passes with Extra Space
- **Time Complexity**: O(n)
- **Space Complexity**: O(n)
```C++
vector<int> productExceptSelf(vector<int>& nums) {
    int n = nums.size();
    vector<int> leftPro(n);
    vector<int> rightPro(n);
    leftPro[0] = 1;
    vector<int> res(n, 0);
    for(int i = 1; i < n; i++) {
        leftPro[i] = nums[i-1]*leftPro[i-1];
    }
    rightPro[n-1] = 1;
    for(int i = n-2; i >= 0; i--) {
        rightPro[i] = nums[i+1]*rightPro[i+1];
    }
    for(int i = 0; i < n; i++) res[i] = leftPro[i]*rightPro[i];
    return res;
}
```

## Approach 2: Two Passes with Constant Space
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)
```C++
vector<int> productExceptSelf(vector<int>& nums) {
    int n = nums.size();
    vector<int> rightPro(n);
    rightPro[n-1] = 1;
    for(int i = n-2; i >= 0; i--) {
        rightPro[i] = nums[i+1]*rightPro[i+1];
    }
    int leftPro = 1;
    for(int i = 1; i < n; i++) {
        leftPro *= nums[i-1];
        rightPro[i] *= leftPro;
    }
    return rightPro;
}
```
