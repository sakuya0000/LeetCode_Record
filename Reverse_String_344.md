# 344. Reverse String �����¼
## ��Ŀ������
Write a function that takes a string as input and returns the string reversed.    
Example:  
Given s = "hello", return "olleh".   
## ����˼·��
�������ӡ�
## ���룺
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