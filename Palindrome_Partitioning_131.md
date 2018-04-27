# 131. Palindrome Partitioning ����˼·
## ��Ŀ������
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
## ����˼·��
���õݹ飬���ַ��������ҵ���һ���ӻ��ģ�������������ӻ���֮��Ѱ��ʣ�µĻ��ģ��Դ��ҵ����л��ġ�
## ���룺
``` C
class Solution {
public:
    bool isPalindrome(string s){
    //�����Ƿ�Ϊ����
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
        //��ֹ����
            ret.push_back(arr);
            return;
        }
        for(int i = beg; i < len; i++){
            if(isPalindrome(s.substr(beg, i-beg+1))){
            //�ҵ��ӻ���
                arr.push_back(s.substr(beg, i-beg+1));
                add(ret, arr, s, i+1);  //������Ѱ�Ҹ�λ��֮��Ļ���
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