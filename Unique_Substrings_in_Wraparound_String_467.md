# 467. Unique Substrings in Wraparound String
## 题目描述：
Consider the string **s** to be the infinite wraparound string of "abcdefghijklmnopqrstuvwxyz", so s will look like this: 
"...zabcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyzabcd....".  

Now we have another string **p**. Your job is to find out how many unique non-empty substrings of **p** are present in **s**. In particular, your input is the string **p** and you need to output the number of different non-empty substrings of **p** in the string **s**.  

**Note:** **p** consists of only lowercase English letters and the size of p might be over 10000.  
  
**Example 1:**
```
Input: "a"
Output: 1

Explanation: Only the substring "a" of string "a" is in the string s.
```
  
**Example 2:**
```
Input: "cac"
Output: 2
Explanation: There are two substrings "a", "c" of string "cac" in the string s.
```
  
**Example 3:**
```
Input: "zab"
Output: 6
Explanation: There are six substrings "z", "a", "b", "za", "ab", "zab" of string "zab" in the string s.
```
## 解题思路：
用dp记录到当前字符的最大连续字符数，遍历数组不断更新dp数组，
最后把所有字母的最大连续字符数加起来就是答案了。
## 代码：
``` C
class Solution {
public:
    int findSubstringInWraproundString(string p) {
        int cnt[26] = {0};
        int n = p.length();
        int num = 0, res = 0;
        for(int i = 0; i < n; i++){
            if(i>0&&((p[i-1]-'a')+1)%26 == p[i]-'a'){
                num++;
            }
            else num = 1;
            cnt[p[i]-'a'] = max(num, cnt[p[i]-'a']);
        }
        for(int i = 0; i < 26; i++){
            res += cnt[i];
        }
        return res;
    }
};
```
