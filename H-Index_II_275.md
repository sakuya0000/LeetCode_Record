# 275. H-Index II 解题记录
## 题目描述：
Given an array of citations sorted in ascending order (each citation is a non-negative integer) of a researcher, write a function to compute the researcher's h-index.  
  **Example:**
```
Input: citations = [0,1,3,5,6]
Output: 3 
Explanation: [0,1,3,5,6] means the researcher has 5 papers in total and each of them had 
             received 0, 1, 3, 5, 6 citations respectively. 
             Since the researcher has 3 papers with at least 3 citations each and the remaining 
             two with no more than 3 citations each, her h-index is 3.
```
## 解题思路：
和上一题一样的思路。
## 代码：
``` C
class Solution {
public:
    int hIndex(vector<int>& citations) {
        int n = citations.size();
        if(n == 0)
            return 0;
        int result = 0;
        for(int i = 1; i <= n; i++){
            if(citations[n - i] >= i)
                result = i;
            else 
                break;
        }
        return result;
    }
};
```