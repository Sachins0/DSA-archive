# Best Time to Buy and Sell Stock (LeetCode)
Link: https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/

Solution - 
```C++
int maxProfit(vector<int>& prices) {
    int maxProfit = 0;       
    int minPrice = INT_MAX;  
    for (int price : prices) {
        if (price < minPrice) {
            minPrice = price;
        } 
        else {
            maxProfit = max(maxProfit, price - minPrice);
        }
    }
    return maxProfit;
}
```