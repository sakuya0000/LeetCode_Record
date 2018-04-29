# 139. Word Break �����¼
## ��Ŀ������
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
## ����˼·��
��������ö�̬�滮������������**s[j]֮ǰ���ַ����ɱ�����**��**s[j]��s[i-1]���ַ����ɱ����룬
��ôs[i]֮ǰ���ַ������ɱ����룬����һ������dp����ʾ��Ӧ�ַ����Ƿ�ɱ����롣
## ���룺
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