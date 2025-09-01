# Generate Parentheses (LeetCode)
Link: https://leetcode.com/problems/generate-parentheses/description/

Solution - 
## Approach 1: Brute Force
### Time Complexity: O(2^(2n) * n) Space Complexity: O(2^(2n) * n) 
```C++
bool isValid(string s) {
    int cnt = 0;
    for(char chars : s) {
        cnt += (chars == '(') ? 1 : -1;
        if(cnt < 0) return false;
    }
    return cnt == 0;
}

void generateParenthesisUtil(string curr, int n, vector<string> &ans) {
    if(curr.length() == 2*n) {
        if(isValid(curr)) {
            ans.push_back(curr);
        }
        return ;
    }
    generateParenthesisUtil(curr + '(', n, ans);
    generateParenthesisUtil(curr + ')', n, ans);
}

vector<string> generateParenthesis(int n) {
    vector<string> ans;
    generateParenthesisUtil("", n, ans);
    return ans;
}

```
## Approach 2: Backtracking
### Time Complexity: O(4^n / sqrt(n)) - Catalan number C(n) as only valid sequences are generated.
### Space Complexity: O(4^n / sqrt(n))
```C++
void generateParenthesisUtil(string curr, int open, int close,
    int max, vector<string> &ans) {
    if(curr.length() == 2*max) {
        ans.push_back(curr);
        return ;
    }
    if(open < max) generateParenthesisUtil(curr + '(', open+1,
        close, max, ans);
    if(close < open) generateParenthesisUtil(curr + ')', open, 
        close +1, max, ans);
}

vector<string> generateParenthesis(int n) {
    vector<string> ans;
    generateParenthesisUtil("", 0, 0, n, ans);
    return ans;
}

```