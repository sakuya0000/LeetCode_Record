# 151. Reverse Words in a String 解题记录
## 题目描述：
Given an input string, reverse the string word by word.  
  
**Example:**  
```
Input: "the sky is blue",
Output: "blue is sky the".
```
  
**Note:**  
- A word is defined as a sequence of non-space characters.  
- Input string may contain leading or trailing spaces. However, your reversed string should not contain leading or trailing spaces.  
- You need to reduce multiple spaces between two words to a single space in the reversed string.  
## 解题思路：
反转字符串，用一个新的字符串记录，再将旧的等于新的。
## 代码：
```  C
class Solution {
public:
    void reverseWords(string &s) {
        string str;
        int end = s.length()-1, beg = end;
        for(int i = end; i >= 0; i--){
            if(s[i] == ' '){
                if(end - beg != 0)
                    str += s.substr(beg + 1, end - beg) + ' ';
                end = beg = i-1;
            }
            else
                beg--;
        }
        if(s[0] == ' '){
            if(str.length() != 0)
                str.erase(str.length()-1, 1);
        }
        else{
            str += s.substr(0, end + 1);
        }
        s = str;
    }
};
```