# Middle of the Linked List (LeetCode)
Link: https://leetcode.com/problems/valid-parentheses/description/

Solution - 
```C++
bool isValid(string s) {
    stack<int> st;
    for(char ch : s) {
        if(ch == '(' || ch == '[' || ch == '{') st.push(ch);
        else {
            if(!st.empty()) {
                if(st.top() == '(' && ch == ')') st.pop();
                else if(st.top() == '{' && ch == '}') st.pop();
                else if(st.top() == '[' && ch == ']') st.pop();
                else return false;
            }
            else return false;
        }
    }
    return st.empty();
}
```
