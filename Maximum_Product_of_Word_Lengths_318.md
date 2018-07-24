# 318. Maximum Product of Word Lengths 解题记录
## 题目描述：
Given a string array `words`, find the maximum value of `length(word[i]) * length(word[j])` where the two words do not share common letters. You may assume that each word will contain only lower case letters. If no such two words exist, return 0.    
**Example 1:**
```
Input: ["abcw","baz","foo","bar","xtfn","abcdef"]
Output: 16 
Explanation: The two words can be "abcw", "xtfn".
```    
**Example 2:**
```
Input: ["a","ab","abc","d","cd","bcd","abcd"]
Output: 4 
Explanation: The two words can be "ab", "cd".
```    
**Example 3:**
```
Input: ["a","aa","aaa","aaaa"]
Output: 0 
Explanation: No such pair of words.
```
## 解题思路：
将每个字符串由一个26位的数字表示，每一位表示当前位所代表的字母是否存在。例如：
> abcd  
> 00 0000 0000 0000 0000 0000 1111
然后进行&操作都能得知两个字符串是否有相同的字母。
## 代码：
``` C
class Solution {
public:
    int maxProduct(vector<string>& words) {
        int n = words.size();
        vector<int> nums(n, 0);
        for(int i = 0; i < n; i++){
            for(int j = 0; j < words[i].length(); j++){
                nums[i] |= 1 << (words[i][j]-'a');
            }
        }
        int maxNum = 0;
        for(int i = 0; i < n-1; i++){
            for(int j = i+1; j < n; j++){
                if((nums[i]&nums[j]) == 0){
                    int temp = words[i].length()*words[j].length();
                    maxNum = max(maxNum, temp);
                }
            }
        }
        return maxNum;
    }
};
```