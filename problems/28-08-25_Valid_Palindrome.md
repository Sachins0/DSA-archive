# Valid Palindrome (LeetCode)
Link: https://leetcode.com/problems/valid-palindrome/description/

Solution - 
```C++
bool isPalindrome(string s) {
    int n = s.length();
    int i = 0, j = n-1;
    while(i < j) {
        while(i < j && !isalnum(s[i])) i++;
        while(i < j && !isalnum(s[j])) j--;
        if(tolower(s[i]) != tolower(s[j])) {
            return false;
        }
        else i++, j--;
    }
    return true;
}
```
