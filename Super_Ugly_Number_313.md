# 313. Super Ugly Number 解题记录
## 题目描述：
Write a program to find the `nth` super ugly number.    
Super ugly numbers are positive numbers whose all prime factors are in the given prime list `primes` of size `k`.    
**Example:**
```
Input: n = 12, primes = [2,7,13,19]
Output: 32 
Explanation: [1,2,4,7,8,13,14,16,19,26,28,32] is the sequence of the first 12 
                    super ugly numbers given primes = [2,7,13,19] of size 4.
```
## 解题思路：
思路和264题丑数2一样，都是记录prime的倍数，用动态规划一个一个找下去。
## 代码：
``` C
class Solution {
public:
    int nthSuperUglyNumber(int n, vector<int>& primes) {
        int len = primes.size();
        vector<int> uglyNums(n, 1), index(len, 0), val(len, 1);
        for(int i = 0; i < n; i++){
            int minNum = val[0];
            for(int j = 1; j < len; j++){
                minNum = min(minNum, val[j]);
            }
            uglyNums[i] = minNum;
            for(int j = 0; j < len; j++){
                if(minNum == val[j]){
                    val[j] = uglyNums[index[j]]*primes[j];
                    index[j]++;
                }
            }
        }
        return uglyNums[n-1];
    }
};
```