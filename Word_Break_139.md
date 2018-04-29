# 139. Word Break 解题记录
## 题目描述：
Given a **non-empty** string s and a dictionary wordDict containing a list of **non-empty** words, 
determine if s can be segmented into a space-separated sequence of one or more dictionary words.  
  
**Note:**  
  
- The same word in the dictionary may be reused multiple times in the segmentation.  
- You may assume the dictionary does not contain duplicate words.  
  
**Example 1:**  
  
> <strong>Input:</strong> s = "leetcode", wordDict = ["leet", "code"]  
> <strong>Output:</strong> true  
> <strong>Explanation:</strong> Return true because "leetcode" can be segmented as "leet code".  
  
**Example 2:**  
  
> <strong>Input:</strong> s = "applepenapple", wordDict = ["apple", "pen"]  
> <strong>Output:</strong> true  
> <strong>Explanation:</strong> Return true because "applepenapple" can be segmented as "apple pen apple".  
	             Note that you are allowed to reuse a dictionary word.
## 解题思路：
这题可以用动态规划来解决，如果在**s[j]之前的字符串可被分离**且**s[j]到s[i-1]的字符串可被分离，
那么s[i]之前的字符串都可被分离，可用一个数组dp来表示对应字符串是否可被分离。
## 代码：
``` C
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        int n = s.length();
        int nums = wordDict.size();
        vector<bool> dp(n+1, false);
        dp[0] = true;
        for(int i = 1; i <= n; i++){
            for(int j = i-1; j >= 0; j--){
                if(dp[j] && (find(wordDict.begin(), wordDict.end(), s.substr(j, i-j)) != wordDict.end())){
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[n];
    }
};
```