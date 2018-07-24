# 326. Power of Three 解题记录
## 题目描述：
Given an integer, write a function to determine if it is a power of three.    
**Example 1:**
```
Input: 27
Output: true
```  
**Example 2:**
```
Input: 0
Output: false
```
## 解题思路：
让n一直除以3，除到余数不为0的时候跳出循环，最后判断一下n是否等于1。
## 代码：
``` C
class Solution {
public:
    bool isPowerOfThree(int n) {
        if(n == 0) return false;
        while(n%3 == 0){
            n /= 3;
        }
        if(n == 1) return true;
        return false;
    }
};
```