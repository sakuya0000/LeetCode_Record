# 347. Top K Frequent Elements �����¼
## ��Ŀ������
Given a non-empty array of integers, return the ***k*** most frequent elements.    
For example,  
Given `[1,1,1,2,2,3]` and k = 2, return `[1,2]`.   
## ����˼·��
����map��¼�������ֵ�Ƶ�ʣ��ٷ�����������У����ȡ������
## ���룺
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