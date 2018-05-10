# 165. Compare Version Numbers �����¼
## ��Ŀ������
Compare two version numbers version1 and version2.  
If `version1 > version2` return `1`; if `version1 < version2` return `-1`;otherwise return `0`.  
  
You may assume that the version strings are non-empty and contain only digits and the `.` character.  
The `.` character does not represent a decimal point and is used to separate number sequences.  
For instance, `2.5` is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.  
  
**Example 1:**  
```
Input: version1 = "0.1", version2 = "1.1"
Output: -1
```
  
**Example 2:**  
```
Input: version1 = "1.0.1", version2 = "1"
Output: 1
```
## ����˼·��
�����˼·���Ǵӿ�ͷһ��һ������ȥ��û��ʲô���õİ취��ֻҪС��һЩ���ݾ����ˣ�
> *version1* = "1.0", *version2* = "1"  
> *version1* = "1.01", *version2* = "1.1"  
���������ݵķ��ؽ������`0`��
## ���룺
``` C
class Solution {
public:
    int getVal(string& str, int& index){
    //��ȡ��Ӧ����
        int t = index;
        for(int i = index; i < str.length();i++){
            if(str[i] == '.'){
            //���� '.' ��������
                index = i;  //��i������index���� '.' ����λ���±꣬�����ظ���ȡ����
                return atoi(str.substr(t, i - t).c_str());
            }
        }
        index = str.length();
        return atoi(str.substr(t, str.length() - t).c_str());  //����β��������
    }
    int compareVersion(string version1, string version2) {
        for(int i = 0, j = 0; i < version1.length() || j < version2.length(); i++, j++){
            if(i >= version1.length())
                version1 += ".0";  //�������ȼ���0�����Ƚ�
            if(j >= version2.length())
                version2 += ".0";  //ͬ��
            int num1 = getVal(version1, i), num2 = getVal(version2, j);
            if(num1 > num2)
                return 1;
            if(num1 < num2)
                return -1;
        }
        return 0;
    }
};
```