# 344. Reverse String 解题记录
## 题目描述：
Write a function that takes a string as input and returns the string reversed.    
Example:  
Given s = "hello", return "olleh".   
## 解题思路：
反过来加。
## 代码：
``` C
class Solution {
public:
    string reverseString(string s) {
        string ret;
        int n = s.length();
        for(int i = n-1; i >= 0; i--){
            ret += s[i];
        }
        return ret;
    }
};
```