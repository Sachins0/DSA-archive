# Invert Binary Tree (LeetCode)
Link: https://leetcode.com/problems/invert-binary-tree/description/

Solution - 
## Approach 1: Recursive Depth-First Search (DFS)
- **Time Complexity**: O(n)  **Space Complexity**: O(h)
```C++
TreeNode* invertTree(TreeNode* root) {
    if(!root) return NULL;
    TreeNode* node = root -> left;
    root -> left = root -> right;
    root -> right = node;
    invertTree(root -> right);
    invertTree(root -> left);
    return root;
}
```

## Approach 2: Iterative Breadth-First Search (BFS) using a Queue
- **Time Complexity**: O(n)  **Space Complexity**: O(n)
```C++
TreeNode* invertTree(TreeNode* root) {
    if(!root) return NULL;
    queue<TreeNode*> qu;
    qu.push(root);
    while(!qu.empty()) {
        TreeNode* node = qu.front();
        qu.pop();
        TreeNode* temp = node -> left;
        node -> left = node -> right;
        node -> right = temp;
        if(node -> left) qu.push(node -> left);
        if(node-> right) qu.push(node -> right);
    }
    return root;
}
```
## Approach 3: Iterative Depth-First Search (DFS) using a Stack
- **Time Complexity**: O(n)  **Space Complexity**: O(h)
```C++
TreeNode* invertTree(TreeNode* root) {
    if(!root) return NULL;
    stack<TreeNode*> st;
    st.push(root);
    while(!st.empty()) {
        TreeNode* node = st.top();
        st.pop();
        TreeNode* temp = node -> left;
        node -> left = node -> right;
        node -> right = temp;
        if(node -> left) st.push(node -> left);
        if(node-> right) st.push(node -> right);
    }
    return root;
}
```
```