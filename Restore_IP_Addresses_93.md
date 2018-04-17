# 93. Restore IP Addresses 解题记录
## 题目描述：
Given a string containing only digits, restore it by returning all possible valid IP address combinations.  
For example:  
Given `"25525511135"`,  
return `["255.255.11.135", "255.255.111.35"]`. (Order does not matter)  
## 解题思路：
**要解决这道题首先要了解IP地址的组成：**  
1. 每个地址由4个部分组成，由3个'.'分割;  
2. 每个部分小于等于255。  

**清楚这两点我们就可以开始解题了，这题我用了递归的方法来解题：**  
1. 首先用一个数count来计数添加了几个部分和一个数beg来记录上一个部分的终止位置，如果count<3的话就遍历往下，看看哪个字串符合IP地址组成的第二个条件，符合就继续递归，不符合就直接结束。  
2. 最后当count==3时，直接取字符串的最后一部分进行比较，符合添加到数组，不符合就结束程序。这样就满足了两个条件。  
## 代码：
``` C
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
        vector<string> ret;
        select(s, ret, "", 0, 0, s.size());
        return ret;
    }
    bool substrCheck(string str, string &ret, int count){
    //检查字串是否符合添加条件，符合就顺便添加了
        unsigned num = 0, len = str.size();
        if(len > 1 && str[0] == '0')
            return false;
        for(int i = 0; i < len; i++){
            num = num * 10 + str[i] - '0';
        }
        if(num <= 255){
            if(count)
                ret += '.' + str;
            else
                ret += str;
            return true;
        }
        return false;
    }
    void select(string &s, vector<string> &ret, string tempS, int count, int beg, int len){
        if(count == 3){
        //结束条件
            if(substrCheck(s.substr(beg, len-beg), tempS, count)){
                ret.push_back(tempS);
            }
            return;
        }
        for(int i = beg+1; i < len; i++){
        //遍历寻找下一个部分
            string t = tempS;
            if(substrCheck(s.substr(beg, i-beg), t, count))
                select(s, ret, t, count+1, i, len);
            else
                break;
        }
    }
};
```