# Binary Tree Inorder Traversal (LeetCode)
Link: https://leetcode.com/problems/binary-tree-inorder-traversal/description/

Solution - 
## Approach 1: Recursive Inorder Traversal
### TC - O(n) SC - O(n)
```C++
void inorder(TreeNode* node,vector<int> &res) {
    if(!node) return ;
    inorder(node -> left, res);
    res.push_back(node -> val);
    inorder(node -> right, res);
}

vector<int> inorderTraversal(TreeNode* root) {
    vector<int> res;
    inorder(root, res); 
    return res;
}
```

## Approach 2: Iterative Inorder Traversal using Stack
### TC - O(n) SC - O(n)
```C++
vector<int> inorderTraversal(TreeNode* root) {
    stack<TreeNode*> st;
    vector<int> inorder;
    while(true){
        if(root!=NULL){
            st.push(root);
            root=root->left;
        }
        else{
            if(st.empty()) break;
            root=st.top();
            st.pop();
            inorder.push_back(root->val);
            root=root->right;
        }
    }
    return inorder;
}

```
## Approach 3: Morris Inorder Traversal (Threaded Binary Tree)
### TC - O(n) SC - O(1)
```C++
void inorderMorris(TreeNode* root,vector<int> &res) {
    if(!root) return;
    TreeNode* curr = root;
    while(curr) {
        if(!curr -> left) {
            res.push_back(curr -> val);
            curr = curr -> right;
        }else {
            TreeNode* prev = curr -> left;
            while(prev ->right && prev -> right != curr) prev = prev -> right;
            if(!prev -> right) {
                prev -> right = curr;
                curr = curr -> left;
            }else {
                prev -> right = NULL;
                res.push_back(curr -> val);
                curr = curr -> right;
            }
        }
    }
}

vector<int> inorderTraversal(TreeNode* root) {
    vector<int> res;
    inorderMorris(root, res); 
    return res;
}

```
