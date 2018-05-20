# 227. Basic Calculator II �����¼
## ��Ŀ������
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
## ����˼·��
��Ϊ`*`��`/`�������ȼ������Բ��ܽ��������ļ��㣬Ҫ��һ��ֵ�ݴ����ֵ��ֱ������`+`��`-`�ٽ��м��㡣
## ���룺
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