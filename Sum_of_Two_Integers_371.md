# 371. Sum of Two Integers 解题记录
## 题目描述：
Calculate the sum of two integers *a* and *b*, but you are **not allowed** to use the operator `+` and `-`.    
**Example:**  
Given *a* = 1 and *b* = 2, return 3. 
## 解题思路：
本题不允许用加减号，所以只能考虑位运算。a^b表示a+b的相应位相加，但没有考虑进位，也就是说19^1的结果为10。而a&b表示a+b的进位
，也就是说19&1的结果为1。所以一直循环a^b，用b来储存进位就可以得到最后的结果了。
## 代码：
``` C
class Solution {
public:
    int getSum(int a, int b) {
        while(b){
            int t = a ^ b;  //相应位相加
            b = (a & b) << 1;  //进位
            a = t;
        }
        return a;
    }
};
```