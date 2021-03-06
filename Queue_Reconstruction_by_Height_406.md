# 406. Queue Reconstruction by Height 解题记录
## 题目描述：
Suppose you have a random list of people standing in a queue. Each person is described by a pair of integers `(h, k)`, where `h` is the height of the person and `k` is the number of people in front of this person who have a height greater than or equal to `h`. Write an algorithm to reconstruct the queue.    

**Note:**    
The number of people is less than 1,100.    


**Example**
```
Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```
## 解题思路：
先对所有人进行身高排序，高的在前面，矮的在后面，身高相同再比较第二个数，小的在前面。然后再把排序好的数组按顺序插入第二个数的位置。
## 代码：
``` C
class Solution {
    static bool cmp(pair<int, int> &a, pair<int, int> &b){
        return a.first > b.first || (a.first == b.first && a.second < b.second);
    }
public:
    vector<pair<int, int>> reconstructQueue(vector<pair<int, int>>& people) {
        vector<pair<int, int>> ret;
        sort(people.begin(), people.end(), cmp);
        for(int i = 0; i < people.size(); i++){
            ret.insert(ret.begin() + people[i].second, people[i]);
        }
        return ret;
    }
};
```
