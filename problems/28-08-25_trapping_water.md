# Trapping Rain Water (LeetCode)
Link: https://leetcode.com/problems/trapping-rain-water/description/

Solution - 
## Approach 1 - Brute Force
### TC - O(n^2) SC - O(1)
```C++
int trap(vector<int>& height) {
    int n = height.size();
    int totalSum = 0;
    for(int i = 0; i < n; i++) {
        int lMax = 0, rMax = 0;
        for(int l = 0; l <= i; l++) {
            lMax = max(lMax, height[l]);
        }
        for(int r = i; r < n; r++) {
            rMax = max(rMax, height[r]);
        }
        totalSum += min(lMax, rMax) - height[i];
    }
    return totalSum;
}
```

## Approach 2 - Optimized with Dynamic Programming Arrays
### TC - O(n) SC - O(n)
```C++
int trap(vector<int>& height) {
    int n = height.size();
    int totalSum = 0;
    vector<int> lMax(n, 0);
    lMax[0] = height[0];
    for(int i = 1; i <n; i++) {
        lMax[i] = max(lMax[i-1], height[i]);
    }
    vector<int> rMax(n, 0);
    rMax[n-1] = height[n-1];
    for(int i = n-2; i >= 0; i--) {
        rMax[i] = max(rMax[i+1], height[i]);
    }
    for(int i = 0; i < n; i++) {
        totalSum += min(lMax[i], rMax[i]) - height[i];
    }
    return totalSum;
}
```
```C++
int trap(vector<int>& height) {
    int n = height.size();
    int totalSum = 0;
    vector<int> rMax(n, 0);
    rMax[n-1] = height[n-1];
    for(int i = n-2; i >= 0; i--) {
        rMax[i] = max(rMax[i+1], height[i]);
    }
    int lMax = 0;
    for(int i = 0; i < n; i++) {
        lMax = max(lMax, height[i]);
        totalSum += min(lMax, rMax[i]) - height[i];
    }
    return totalSum;
}
```
## Approach 3 - Two Pointers Technique
### TC - O(n) SC - O(1)
```C++
int trap(vector<int>& height) {
    int n = height.size();
    int totalSum = 0;
    int left = 0, right = n-1;
    int lMax = 0, rMax = 0;
    while(left < right) {
        if(height[left] < height[right]) {
            if(height[left] >= lMax) lMax = height[left];
            else totalSum += lMax - height[left];
            left++;
        }else {
            if(height[right] >= rMax) rMax = height[right];
            else totalSum += rMax - height[right];
            right--;
        }
    }
    return totalSum;
}
```


