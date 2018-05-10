# 165. Compare Version Numbers 解题记录
## 题目描述：
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
## 解题思路：
这题的思路就是从开头一个一个比下去，没有什么更好的办法。只要小心一些数据就行了：
> *version1* = "1.0", *version2* = "1"  
> *version1* = "1.01", *version2* = "1.1"  
这两个数据的返回结果都是`0`。
## 代码：
``` C
class Solution {
public:
    int getVal(string& str, int& index){
    //获取对应数字
        int t = index;
        for(int i = index; i < str.length();i++){
            if(str[i] == '.'){
            //碰到 '.' 返回数字
                index = i;  //让i的引用index等于 '.' 所在位置下标，避免重复获取数字
                return atoi(str.substr(t, i - t).c_str());
            }
        }
        index = str.length();
        return atoi(str.substr(t, str.length() - t).c_str());  //到结尾返回数字
    }
    int compareVersion(string version1, string version2) {
        for(int i = 0, j = 0; i < version1.length() || j < version2.length(); i++, j++){
            if(i >= version1.length())
                version1 += ".0";  //超出长度加上0继续比较
            if(j >= version2.length())
                version2 += ".0";  //同上
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