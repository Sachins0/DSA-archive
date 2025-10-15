# Binary Tree Cameras (LeetCode)
Link: https://leetcode.com/problems/binary-tree-cameras/description/
Solution - 
## Greedy DFS approach
**Time Complexity**: O(n)
**Space Complexity**: O(h)
```C++
class Solution {
private:
    int cameras = 0;
    // 0 -> needs camera
    //1 -> covered
    //2 -> has camera
    int dfs(TreeNode* root) {
        if(!root) return 1;
        int left = dfs(root -> left);
        int right = dfs(root -> right);
        if(left == 0 || right == 0) {
            cameras++;
            return 2;
        }
        if(left == 2 || right == 2) return 1;
        return 0;

    }
public:
    int minCameraCover(TreeNode* root) {
        return (dfs(root) == 0 ? 1 : 0)+cameras;
    }
};
```