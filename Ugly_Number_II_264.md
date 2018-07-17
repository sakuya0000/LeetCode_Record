# 264. Ugly Number II �����¼
## ��Ŀ������
Write a program to find the `n` -th ugly number.  
Ugly numbers are **positive numbers**whose prime factors only include `2, 3, 5` .   
**Example:**  
```
Input: n = 10
Output: 12
Explanation: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.
```
## ����˼·��
��������������ȫΪ2��3��5����������ֻҪ��1X2��3��5�Ϳɵõ����г�����  
  ��һ����������¼������������������еĳ������Ǵ�ͬһ������X2��X3��X5�õ�������Ҫ��3��������¼X2��X3��X5��һ��������
ÿ�ζ�ȡ3������С������Ȼ����������Ӧ��2��3��5�õ���һ��������  
������3������Ҫ��Ϊ����X2��X3��X5��Ҫ���������������Ҫ��������Ҫ3���±�����¼��3������λ�á�
## ���룺
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