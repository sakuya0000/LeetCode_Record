# 357. Count Numbers with Unique Digits �����¼
## ��Ŀ������
Given a non-negative integer n, count all numbers with unique digits, x, where 0 �� x < 10<sup>n</sup>.    

**Example:**  
Given n = 2, return 91. (The answer should be the total numbers in the range of 0 �� x < 100, excluding `[11,22,33,44,55,66,77,88,99]`)  
## ����˼·��
��ͨ������������⣬��������10<sup>n</sup>������λ��ͬ���ֵ���f(n)��Ϊ��

1. ����λ��Ϊ0������λ��ͬ���ֵ�����  
2. ����λΪ0������λ��ͬ���ֵ�����

����2������f(n-1)������1ͨ��������Ͽ�֪Ϊ9\*9\*8\*����\*(10-n+1)����f(n)=f(n-1)+9\*9\*8\*����\*(10-n+1)����֪���ƹ�ʽ������dp������
## ���룺
``` C
class Solution {
public:
    int countNumbersWithUniqueDigits(int n) {
        if(n == 0) return 1;
        if(n == 1) return 10;
        vector<int> nums(n, 10);
        for(int i = 1; i < n; i++){
            int sum = 9;
            for(int j = 0; j < i; j++){
                sum *= (9-j);
            }
            nums[i] = nums[i-1] + sum;
        }
        return nums[n-1];
    }
};
```