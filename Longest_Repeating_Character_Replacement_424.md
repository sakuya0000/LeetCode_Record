# 424. Longest Repeating Character Replacement 解题记录
## 题目描述：
Given a string that consists of only uppercase English letters, you can replace any letter in the string with another letter at most k times. Find the length of a longest substring containing all repeating letters you can get after performing the above operations.    

**Note:**  
Both the string's length and k will not exceed 104.    

**Example 1:**  
```
Input:
s = "ABAB", k = 2

Output:
4

Explanation:
Replace the two 'A's with two 'B's or vice versa.
```

**Example 2:**  

```
Input:
s = "AABABBA", k = 1

Output:
4

Explanation:
Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
```
## 解题思路：
这题主要利用移动窗口，记录窗口中每个字母的数量，然后再用一个most记录最多的数量。然后从零开始遍历字符串，比较窗口的长度与most+k：若大于，移动窗口左侧；若小于，则将返回结果与窗口大小比较。
## 代码：
``` C
class Solution {
public:
    int characterReplacement(string s, int k) {
        int n = s.length();
        if(n == 0) return 0;
        vector<int> map(91, 0);
        int ret = 1, left = 0, most = 0;
        for(int right = 0; right < n; right++){
            most = max(most, ++map[s[right]]);
            if(right - left >= most + k)
                map[s[left++]]--;
            else
                ret = max(ret, right - left + 1);
        }
        return ret;
    }
};
```