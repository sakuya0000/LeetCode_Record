# 279. Perfect Squares �����¼
## ��Ŀ������
Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.  
  **Example 1:**  
```
Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
```
  **Example 2:**
```
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```
## ����˼·��
��������õ���̬�滮�ķ�������Ϊÿһ������ƽ��������**һ����ͨ��** + **��һ������ƽ�����õ�** �������е��ƹ�ʽ**dp[i + j * j] = min(dp[i + j * j], dp[i]+1);**  
## ���룺
``` C
class Solution {
public:
    int numSquares(int n) {
        int temp = 0, tempSquare = 0;
        vector<int> dp(n+1, INT_MAX);
        while(tempSquare <= n){  //��ʼ��
            dp[tempSquare] = 1;
            temp++;
            tempSquare = temp*temp;
        }
        if(tempSquare == n)
            return 1;
        for(int i = 1; i <= n; i++){
            for(int j = 1; i + j * j <= n; j++){
                dp[i + j * j] = min(dp[i + j * j], dp[i]+1);
            }
        }
        return dp[n];
    }
};
```