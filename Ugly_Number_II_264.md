# 264. Ugly Number II 解题记录
## 题目描述：
Write a program to find the `n` -th ugly number.  
Ugly numbers are **positive numbers**whose prime factors only include `2, 3, 5` .   
**Example:**  
```
Input: n = 10
Output: 12
Explanation: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.
```
## 解题思路：
丑数是质因数数全为2，3，5的数，所以只要将1X2，3，5就可得到所有丑数。  
  用一个数组来记录升序丑数，因升序排列的丑数不是从同一个丑数X2，X3，X5得到，所以要用3个数来记录X2，X3，X5上一个丑数。
每次都取3个数最小的数，然后将它乘以相应的2，3或5得到下一个丑数。  
而对这3个数的要求为它们X2，X3，X5后要比数组中最大数还要大，所以需要3个下标来记录这3个数的位置。
## 代码：
``` C
class Solution {
public:
    int nthUglyNumber(int n) {
        int index_2 = 0, index_3 = 0, index_5 = 0;
        int val_2 = 2, val_3 = 3, val_5 = 5;
        vector<int> dp(n, 1);
        for(int i = 1; i < n; i++){
            int val = min(min(val_2, val_3), val_5);
            if(val == val_2){
                dp[i] = val_2;
                index_2++;
                val_2 = 2*dp[index_2];
            }
            if(val == val_3){
                dp[i] = val_3;
                index_3++;
                val_3 = 3*dp[index_3];
            }
            if(val == val_5){
                dp[i] = val_5;
                index_5++;
                val_5 = 5*dp[index_5];
            }
        }
        return dp[n-1];
    }
};
```