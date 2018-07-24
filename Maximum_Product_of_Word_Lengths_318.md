# 318. Maximum Product of Word Lengths �����¼
## ��Ŀ������
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
## ����˼·��
��ÿ���ַ�����һ��26λ�����ֱ�ʾ��ÿһλ��ʾ��ǰλ���������ĸ�Ƿ���ڡ����磺
> abcd  
> 00 0000 0000 0000 0000 0000 1111
Ȼ�����&�������ܵ�֪�����ַ����Ƿ�����ͬ����ĸ��
## ���룺
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