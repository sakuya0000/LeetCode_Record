# 131. Palindrome Partitioning 解题思路
## 题目描述：
Given a string s, partition s such that every substring of the partition is a palindrome.  
  
Return all possible palindrome partitioning of s.  
  
**Example:**  
```
Input: "aab"
Output:
[
  ["aa","b"],
  ["a","a","b"]
]
```
## 解题思路：
利用递归，在字符串中先找到第一个子回文，接下来在这个子回文之后寻找剩下的回文，以此找到所有回文。
## 代码：
``` C
class Solution {
public:
    bool isPalindrome(string s){
    //检验是否为回文
        int right = s.length()-1, left = 0;
        bool ret = true;
        while(left<right){
            if(s[left++]!=s[right--]){
                ret = false;
                break;
            }
        }
        return ret;
    }
    void add(vector<vector<string>> &ret, vector<string> arr, string& s, int beg){
        int len = s.length();
        if(beg==len){
        //终止条件
            ret.push_back(arr);
            return;
        }
        for(int i = beg; i < len; i++){
            if(isPalindrome(s.substr(beg, i-beg+1))){
            //找到子回文
                arr.push_back(s.substr(beg, i-beg+1));
                add(ret, arr, s, i+1);  //接下来寻找该位置之后的回文
                arr.pop_back();
            }
        }
    }
    vector<vector<string>> partition(string s) {
        vector<vector<string>> ret;
        add(ret, vector<string>(), s, 0);
        return ret;
    }
};
```