# Symmetric Tree (LeetCode)
Link: https://leetcode.com/problems/symmetric-tree/description/

Solution - 
## Approach 1: Recursive Solution (DFS)
- Time Complexity: O(n)
- Space Complexity: O(h)
```C++
class Solution {
private:
    bool isMirror(TreeNode* n1, TreeNode* n2) {
        if(!n1 && !n2) return true;
        if(!n1 || !n2) return false;
        return (n1 -> val == n2 -> val)
            && isMirror(n1 -> left, n2 -> right)
            && isMirror(n1 -> right, n2 -> left);
    }
public:
    bool isSymmetric(TreeNode* root) {
        return isMirror(root, root);
    }
};
```

## Approach 2: Iterative Solution (BFS using Queue)
- Time Complexity: O(n)
 - Space Complexity: O(n)
```C++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        queue<TreeNode*> qu;
        qu.push(root);
        qu.push(root);

        while(!qu.empty()) {
            TreeNode* t1 = qu.front(); qu.pop();
            TreeNode* t2 = qu.front(); qu.pop();
            if(!t1 && !t2) continue;
            if(!t1 || !t2 || t1 -> val != t2 -> val) return 
                false;
            qu.push(t1 -> left);
            qu.push(t2 -> right);
            qu.push(t1 -> right);
            qu.push(t2 -> left);
        }
        return true;
    }
};
```