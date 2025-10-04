# Largest Rectangle in Histogram (LeetCode)
Link: https://leetcode.com/problems/largest-rectangle-in-histogram/description/

Solution - 
## Approach 1: Brute Force
- Time Complexity: O(n^2)
 - Space Complexity: O(1)
```C++
int largestRectangleAreaBruteForce(vector<int>& heights) {
    int maxArea = 0;
    int n = heights.size();
    for (int i = 0; i < n; i++) {
        int minHeight = heights[i];
        for (int j = i; j < n; j++) {
            minHeight = min(minHeight, heights[j]); // Find the smallest bar in the current range
            maxArea = max(maxArea, minHeight * (j - i + 1)); // Calculate the area and update maxArea
        }
    }
    return maxArea;
}
```

## Approach 2: Most Optimal Approach - Stack
- Time Complexity: O(n)
- Space Complexity: O(n)

```C++
int largestRectangleArea(vector<int>& heights) {
    stack<int> st;
    int maxArea = 0;
    int nse = 0, pse = 0;
    int ele;
    for(int i = 0; i < heights.size(); i++) {
        while(!st.empty() && heights[st.top()] >= heights[i]) {
            ele = st.top();
            st.pop();
            nse = i, pse = st.empty() ? -1 : st.top();
            maxArea = max(maxArea, heights[ele] * (nse - pse - 1));
        }
        st.push(i);
    }
    while(!st.empty()) {
        nse = heights.size();
        ele = st.top();
        st.pop();
        pse = st.empty() ? -1 : st.top();
        maxArea = max(maxArea, heights[ele] * (nse - pse - 1));
    }
    return maxArea;
}
```
