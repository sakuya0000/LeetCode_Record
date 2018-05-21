# 228. Summary Ranges 解题记录
## 题目描述：
Given a sorted integer array without duplicates, return the summary of its ranges.  
  
**Example 1:**  
```
Input:  [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
Explanation: 0,1,2 form a continuous range; 4,5 form a continuous range.
```
  
**Example 2:**
```
Input:  [0,2,3,4,6,8,9]
Output: ["0","2->4","6","8->9"]
Explanation: 2,3,4 form a continuous range; 8,9 form a continuous range.
```
## 解题思路：
用一个符号记录是否连续，然后遍历得到字符串数组。
## 代码：
``` C
class Solution {
public:
    vector<string> summaryRanges(vector<int>& nums) {
        if(nums.size() == 0)
            return vector<string>();
        bool isC = false;
        vector<string> ret;
        string tStr = to_string(nums[0]);
        for(int i = 1; i < nums.size(); i++){
            if(nums[i] == nums[i-1]+1 && !isC){
                isC = true;
                tStr +="->";
            }
            if(nums[i] != nums[i-1]+1){
                if(isC){
                    tStr += to_string(nums[i-1]);
                }
                ret.push_back(tStr);
                tStr = to_string(nums[i]);
                isC = false;
            }
        }
        if(isC){
            tStr += to_string(*nums.rbegin());
        }
        ret.push_back(tStr);
        return ret;
    }
};
```