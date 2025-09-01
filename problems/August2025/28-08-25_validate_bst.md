# Validate Binary Search Tree
Link: https://leetcode.com/problems/validate-binary-search-tree/description/

Solution - 
## Approach 1 - Recursive Range Check 
### TC - O(n) SC - O(n)
```C++
bool isValidBSTUtil(TreeNode* node, long maxVal, long minVal) {
    if(!node) return true;
    if(node -> val >= maxVal || node -> val <= minVal) return false;
    return isValidBSTUtil(node -> left, node -> val, minVal) &&
            isValidBSTUtil(node -> right, maxVal, node -> val);
}

bool isValidBST(TreeNode* root) {
    return isValidBSTUtil(root, LONG_MAX, LONG_MIN);
}
```

## Approach 2 - Inorder Recursive
### TC - O(n) SC - O(n)
```C++
bool isBST(TreeNode* root,TreeNode* &prev){
    if(root==NULL) return true;
    if(!isBST(root->left,prev)) return false;//left subtree
    if(prev && root->val<=prev->val) return false;//root
    prev=root;
    return isBST(root->right,prev);//right subtree
}
bool isValidBST(TreeNode* root) {
    TreeNode* prev=NULL;
    return isBST(root,prev);
}
```
## Approach 3 - Morris Traversal - Inorder Iterative
### TC - O(n) SC - O(1)
```C++
bool isValidBST(TreeNode* root) {
    long long prevVal = LLONG_MIN;
    bool is_bst = true;
    TreeNode* curr = root;
    while(curr != NULL) {
        if(curr -> left == NULL) {
            if(curr -> val <= prevVal) is_bst = false;
            prevVal = curr -> val;
            curr = curr -> right;
        }
        else {
            TreeNode* prev = curr -> left;
            while(prev -> right && prev -> right != curr) prev = prev -> right;
            if(prev -> right == NULL) {
                prev -> right = curr;
                curr = curr -> left;
            }
            else {
                prev -> right = NULL;
                if(curr -> val <= prevVal) is_bst = false;
                prevVal = curr -> val;
                curr = curr -> right;
            }
        }
    }
    return is_bst;
}
```

