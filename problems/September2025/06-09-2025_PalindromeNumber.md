# Palindrome Number (LeetCode)
Link: https://leetcode.com/problems/palindrome-number/description/

Solution - 
## Approach 1: Converting to string
```C++
 bool isPalindrome(int x) {
    string str = to_string(x);
    int i = 0, j = str.size()-1;
    while(i <= j) {
        if(str[i] != str[j]) return false;
        i++;
        j--;
    }
    return true;
}
```
## Approach 2: Reversing and comparing
```C++
bool isPalindrome(int x) {
    long revNo = 0;
    int num = x;
    while(num) {
        revNo *= 10;
        revNo += abs(num % 10);
        num /= 10;
    }
    return revNo == x;
}
```
