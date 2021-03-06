# 309. Best Time to Buy and Sell Stock with Cooldown 解题记录
## 题目描述：
Say you have an array for which the ith element is the price of a given stock on day i.    
Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:    
- You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).  
- After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)

    **Example:**
```
Input: [1,2,3,0,2]
Output: 3 
Explanation: transactions = [buy, sell, cooldown, buy, sell]
```
## 解题思路：
动态规划，维护buy和sell的信息。
## 代码：
``` C
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int buy = INT_MIN, pre_buy = 0, sell = 0, pre_sell = 0;
        for (int price : prices) {
            pre_buy = buy;
            buy = max(pre_sell - price, pre_buy);
            pre_sell = sell;
            sell = max(pre_buy + price, pre_sell);
        }
        return sell;
    }
};
```