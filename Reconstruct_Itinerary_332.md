# 332. Reconstruct Itinerary 解题记录
## 题目描述：
Given a list of airline tickets represented by pairs of departure and arrival airports [from, to], reconstruct the itinerary in order. All of the tickets belong to a man who departs from JFK. Thus, the itinerary must begin with JFK.    

Note:    

1. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string. For example, the itinerary ["JFK", "LGA"] has a smaller lexical order than ["JFK", "LGB"].  
2. All airports are represented by three capital letters (IATA code).  
3. You may assume all tickets form at least one valid itinerary.

**Example 1:**  
```
Input: tickets = [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
Output: ["JFK", "MUC", "LHR", "SFO", "SJC"]
```    
**Example 2:**
```
Input: tickets = [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
Output: ["JFK","ATL","JFK","SFO","ATL","SFO"]
Explanation: Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"]. But it is larger in lexical order.
```
## 解题思路：
先将票用map存起来变成有向图，然后再用递归到达最底层，往上返回路径。
## 代码：
``` C
class Solution {
public:
    vector<string> findItinerary(vector<pair<string, string>> tickets) {
        unordered_map<string, multiset<string>> m;
        vector<string> res;
        if (tickets.size() == 0) {
            return res;
        }
        for (pair<string, string> p: tickets) {
            m[p.first].insert(p.second);

        }
        stack<string> s;
        s.push("JFK");
        while (!s.empty()) {
            string next = s.top();
            if (m[next].empty()) {
                res.push_back(next);
                s.pop();
            } else {
                s.push(*m[next].begin());
                m[next].erase(m[next].begin());
            }
        }
        reverse(res.begin(), res.end());
        return res;
    }
};
```