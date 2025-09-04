# Container With Most Water (LeetCode)
Link: https://leetcode.com/problems/container-with-most-water/description/

Solution - 
## Brute Force Approach
- **Time Complexity**: O(n^2)
- **Space Complexity**: O(1)
```C++
int maxArea(vector<int>& height) {
    int n = height.size();
    int maxArea = -1;
    for(int i = 0; i < n-1; i++) {
        for(int j = i+1; j < n; j++) {
            int h = min(height[i], height[j]);
            int area = h *(j-i);
            maxArea = max(maxArea, area);
        }
    } 
    return maxArea;
}
```

## Two pointers approach
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)
```C++
int maxArea(vector<int>& height) {
    int n = height.size();
    int maxArea = 0;
    int left = 0, right = n-1;
    while( left < right) {
        int h = min(height[left], height[right]);
        int area = h * (right-left);
        maxArea = max(maxArea, area);
        if(height[left] < height[right])left++;
        else right--;
    }
    return maxArea;
}
```
