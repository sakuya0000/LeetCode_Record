# 347. Top K Frequent Elements 解题记录
## 题目描述：
Given a non-empty array of integers, return the ***k*** most frequent elements.    
For example,  
Given `[1,1,1,2,2,3]` and k = 2, return `[1,2]`.   
## 解题思路：
先用map记录出现数字的频率，再放入排序队列中，最后取出来。
## 代码：
``` C
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> mp;
        for(int i = 0; i < nums.size(); i++){
            mp[nums[i]]++;
        }
        priority_queue<pair<int, int> > q;
        for(unordered_map<int, int>::iterator i = mp.begin(); i != mp.end(); i++){
            q.push(make_pair((*i).second, (*i).first));
        }
        vector<int> ret;
        while(k-- > 0){
            ret.push_back(q.top().second);
            q.pop();
        }
        return ret;
    }
};
```