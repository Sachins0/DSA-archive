# Spiral Matrix (LeetCode)
Link: https://leetcode.com/problems/spiral-matrix/description/

Solution - 
## Approach 1: Layer-by-Layer Traversal
- **Time Complexity**: O(m*n)
- **Space Complexity**: O(1)
```C++
vector<int> spiralOrder(vector<vector<int>>& matrix) {
    int m = matrix.size();
    int n = matrix[0].size();
    vector<int> res;
    int left = 0, right = n-1, top = 0, bottom = m-1;
    while(top <= bottom && left <= right) {
        //top row
        for(int i = left; i <= right; i++) {
            res.push_back(matrix[top][i]);
        }
        top++;
        //right col
        for(int j = top; j <= bottom ; j++) {
            res.push_back(matrix[j][right]);
        }
        right--;
        //bottom row
        if(top <= bottom) {
            for(int i = right; i >= left; i--) {
            res.push_back(matrix[bottom][i]);
        }
        bottom--;
        }
        //left col
        if(left <= right) {
            for(int j = bottom; j >= top ; j--) {
            res.push_back(matrix[j][left]);
        }
        left++;
        }
    }
    return res;
}
```
