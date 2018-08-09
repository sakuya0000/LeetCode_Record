# 392. Is Subsequence 解题记录
## 题目描述：
Given a string **s** and a string **t**, check if s is subsequence of **t**. 
You may assume that there is only lower case English letters in both **s** and **t**. **t** is potentially a very long (length ~= 500,000) string, and **s** is a short string (<=100).     
A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ace" is a subsequence of "abcde" while "aec" is not).     
**Example 1:**  
s = `"abc"`, t = `"ahbgdc"`     
Return true.     
**Example 2:**  
s = `"axc"`, t = `"ahbgdc"`     
Return `false`.   
## 解题思路：
遍历t字符串一个个比对s字符串中的字符。
## 代码：
``` C
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int index = 0, s_len = s.length(), t_len = t.length();
        if(s_len == 0) return true;
        for(int i = 0; i < t_len; i++){
            if(t[i] == s[index]) index++;
            if(index == s_len) return true;
        }
        return false;
    }
};
```