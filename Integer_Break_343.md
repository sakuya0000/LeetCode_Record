# 343. Integer Break �����¼
## ��Ŀ������
Given a positive integer n, break it into the sum of at least two positive integers and maximize the product of those integers. Return the maximum product you can get.     
For example, given n = 2, return 1 (2 = 1 + 1); given n = 10, return 36 (10 = 3 + 3 + 4).     
Note: You may assume that n is not less than 2 and not larger than 58.     
## ����˼·��
���ݾ�ֵ����ʽ��֪��n�ֳ���ͬ���������ǵĳ˻�����ٹ۲췢�ֳַ�3�ĳ˻������ģ����еĲ���3�ı���������Ҫ����3.
## ���룺
``` C
class Solution {
public:
    int integerBreak(int n) {
        if(n == 2)
            return 1;
        else if(n == 3)
            return 2;
        else if(n%3 == 0)
            return pow(3, n/3);
        else if(n%3 == 1)
            return 2 * 2 * pow(3, (n - 4) / 3);
        else 
            return 2 * pow(3, n/3);
    }
};
```