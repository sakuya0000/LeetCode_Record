# 150. Evaluate Reverse Polish Notation 解题记录
## 题目描述：
Evaluate the value of an arithmetic expression in Reverse Polish Notation.  
  
Valid operators are `+, -, *, /.` Each operand may be an integer or another expression.  
  
**Note:**  
  
- Division between two integers should truncate toward zero.
- The given RPN expression is always valid. That means the expression would always evaluate to a result and there won't be any divide by zero operation.  
  
**Example 1:**  
```
Input: ["2", "1", "+", "3", "*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```
  
**Example 2:**  
```
Input: ["4", "13", "5", "/", "+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```
  
**Example 3:**
```
Input: ["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
Output: 22
Explanation: 
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```
## 解题思路：
逆波兰表达式，思路很明显是运用栈的思想，可以用递归也可以用迭代。这里我用了迭代。
## 代码：
``` C
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> s; 
        int i;
        int result = 0;
        for (i=0;i<tokens.size();i++)
        {
            if(tokens[i].length() > 1){
                s.push(atoi(tokens[i].c_str()));
                continue;
            }
            if (tokens[i][0] == '+')
            {
                int num1 = s.top();
                s.pop();
                int num2 = s.top();
                s.pop();
                result = num1 + num2;
                s.push(result);
            }
            else if (tokens[i][0] == '-')
            {
                int num1 = s.top();
                s.pop();
                int num2 = s.top();
                s.pop();
                result = num2 - num1;
                s.push(result);
            }
            else if (tokens[i][0] == '*')
            {
                int num1 = s.top();
                s.pop();
                int num2 = s.top();
                s.pop();
                result = num2 * num1;
                s.push(result);
            }
            else if (tokens[i][0] == '/')
            {
                int num1 = s.top();
                s.pop();
                int num2 = s.top();
                s.pop();
                result = num2 / num1;
                s.push(result);
            }else
                s.push(atoi(tokens[i].c_str()));
        }
        return s.top();
    }
};
```