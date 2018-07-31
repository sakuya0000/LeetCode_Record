# 357. Count Numbers with Unique Digits 解题记录
## 题目描述：
Given a non-negative integer n, count all numbers with unique digits, x, where 0 ≤ x < 10<sup>n</sup>.    

**Example:**  
Given n = 2, return 91. (The answer should be the total numbers in the range of 0 ≤ x < 100, excluding `[11,22,33,44,55,66,77,88,99]`)  
## 解题思路：
普通的排列组合问题，将求所有10<sup>n</sup>内所有位不同数字的数f(n)分为：

1. 求首位不为0的所有位不同数字的数；  
2. 求首位为0的所有位不同数字的数；

问题2就是求f(n-1)，问题1通过排列组合可知为9\*9\*8\*……\*(10-n+1)。得f(n)=f(n-1)+9\*9\*8\*……\*(10-n+1)。已知递推公式所以用dp来做。
## 代码：
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