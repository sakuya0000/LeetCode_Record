# 338. Counting Bits 解题记录
## 题目描述：
Given a non negative integer number num. For every numbers i in the range **0 ≤ i ≤ num** calculate the number of 1's in their binary representation and return them as an array.     
Example:  
For `num = 5` you should return `[0,1,1,2,1,2]`.   
## 解题思路：
这题可以用动态规划来完成，递推公式为f(a)=f(2<sup>n</sup>)+f(b)，(b<=2<sup>n</sup>)。
## 代码：
``` C
class Solution {
public:
    vector<int> countBits(int num) {
        if(num == 0) return vector<int>(1, 0);
        vector<int> ret(num+1, 1);
        ret[0] = 0;
        for(int t = 2; t < num; t *= 2){
            for(int i = 1; i < t && t+i <= num; i++){
                ret[i+t] = ret[t] + ret[i];
            }
        }
        return ret;
    }
};
```