# Diameter of Binary Tree (LeetCode)
Link: https://leetcode.com/problems/diameter-of-binary-tree/description/

Solution - 
## Approach 1: Recursive DFS with Calculating Height
- **Time Complexity**: O(n)
- **Space Complexity**: O(h)
```C++
int diamUtil(TreeNode* root, int &diam) {
    if(!root) return 0;
    int leftSide = diamUtil(root -> left, diam);
    int rightSide = diamUtil(root -> right, diam);
    diam = max(diam, leftSide + rightSide);
    return 1 + max(leftSide, rightSide);
}
int diameterOfBinaryTree(TreeNode* root) {
    int diam = 0;
    diamUtil(root, diam);
    return diam;
}
```
