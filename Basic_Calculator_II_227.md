# 227. Basic Calculator II 解题记录
## 题目描述：
Implement a basic calculator to evaluate a simple expression string.  
The expression string contains only non-negative integers, `+`, `-`, `*`, `/` operators and empty spaces . The integer division should truncate toward zero.  
  
**Example 1:**  
```
Input: "3+2*2"
Output: 7
```
  
**Example 2:**  
```
Input: " 3/2 "
Output: 1
```
 
**Example 3:**  
```
Input: " 3+5 / 2 "
Output: 5
```
## 解题思路：
因为`*`和`/`具有优先级，所以不能进行立即的计算，要用一个值暂存这个值，直到遇到`+`和`-`再进行计算。
## 代码：
``` C
class Solution {
public:
    int calculate(string s) {
        int tSum = 0, num = 0, res = 0, n = s.length();
        char op = '+';
        for(int i = 0; i < n; i++){
            char c = s[i];
            if(c >= '0'){
                num = num*10 + c-'0';
                continue;
            }
            if(c == ' ')
                continue;
            switch (op) {
                case '+': tSum += num; break;
                case '-': tSum -= num; break;
                case '*': tSum *= num; break;
                case '/': tSum /= num; break;
            }
            if (c == '+' || c == '-') {
                res += tSum;
                tSum = 0;
            }
            op = c;
            num = 0;
        }
        switch (op) {
	        case '+': tSum += num; break;
	        case '-': tSum -= num; break;
	        case '*': tSum *= num; break;
	        case '/': tSum /= num; break;
	    }
	    res += tSum;
        return res;
    }
};
```