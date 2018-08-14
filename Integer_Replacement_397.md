# 397. Integer Replacement 解题记录
## 题目描述：
Given a positive integer n and you can do operations as follow:     

1. If *n* is even, replace *n* with *`n`*`/2`.
2. If *n* is odd, you can replace *n* with either *`n`* `+ 1` or *`n`* `- 1`.

What is the minimum number of replacements needed for n to become 1?     

**Example 1:**  
```
Input:
8

Output:
3

Explanation:
8 -> 4 -> 2 -> 1
```    
**Example 2:**  
```
Input:
7

Output:
4

Explanation:
7 -> 8 -> 4 -> 2 -> 1
or
7 -> 6 -> 3 -> 2 -> 1
```
## 解题思路：
模拟过程，暴力破解。
## 代码：
``` C
class Solution {
    int func(unsigned int n) {
        if(n == 1) return 0;
        if(n % 2 == 0)
            return func(n/2)+1;
        return min(func(n-1), func(n+1)) + 1;
    }
public:
    int integerReplacement(int n) {
        return func(n);
    }
    
};
```