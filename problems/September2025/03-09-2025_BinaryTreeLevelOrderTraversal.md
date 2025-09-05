# Binary Tree Level Order Traversal (LeetCode)
Link: https://leetcode.com/problems/binary-tree-level-order-traversal/description/

Solution - 
## Recursive DFS Approach
- **Time Complexity**: O(N)
- **Space Complexity**: O(N)
```C++
vector<vector<int>> res;
void dfs(TreeNode* node, int level) {
    if(!node) return;
    if(level == res.size()) res.push_back(vector<int>());
    res[level].push_back(node -> val);
    dfs(node -> left, level+1);
    dfs(node -> right, level+1);
}
vector<vector<int>> levelOrder(TreeNode* root) {
    if(root == NULL) return {};
    dfs(root, 0);
    return res;
}
```

## Iterative BFS Approach
- **Time Complexity**: O(N)
- **Space Complexity**: O(N)
```C++
 vector<vector<int>> levelOrder(TreeNode* root) {
    if(root == NULL) return {};
    queue<TreeNode*> qu;
    vector<vector<int>> res;
    qu.push(root);
    while(!qu.empty()) {
        vector<int> currLevel;
        int currSize = qu.size();
        for(int i = 0; i < currSize; i++) {
            TreeNode* node = qu.front();
            currLevel.push_back(node -> val);
            qu.pop();
            if(node-> left) qu.push(node -> left);
            if(node-> right) qu.push(node -> right);
        }
        res.push_back(currLevel);
    }
    return res;
}
```
