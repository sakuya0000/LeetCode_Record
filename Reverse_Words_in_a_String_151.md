# 151. Reverse Words in a String �����¼
## ��Ŀ������
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
## ����˼·��
��ת�ַ�������һ���µ��ַ�����¼���ٽ��ɵĵ����µġ�
## ���룺
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