# 207.Course Schedule 解题记录
## 题目描述：
There are a total of n courses you have to take, labeled from `0` to `n-1`.
Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`
Given the total number of courses and a list of prerequisite **pairs**, is it possible for you to finish all courses?
  
**Example 1:**
> **Input:** 2, [[1,0]]  
> **Output:** true  
> **Explanation:** There are a total of 2 courses to take.   
>                         To take course 1 you should have finished course 0. So it is possible.  

**Example 2:**
> **Input:** 2, [[1,0],[0,1]]  
> **Output:** false  
> **Explanation:** There are a total of 2 courses to take.   
>                        To take course 1 you should have finished course 0, and to take course 0 you should  
>                        also have finished course 1. So it is impossible.  

## 解题思路 1：
本题可以用DFS来实现，先用一个有向图graph来记录课程，该有向图**由后修课指向先修课**，用一个栈pre来记录**有**先修课的课程，
用一个数组visit来记录课程的状态（是否能完成）。然后利用递归查看课程是否能修完。    
利用递归检索的思路是：先将该课程设为不可修完，即visit[cur]=-1。然后由graph依次遍历该课程的先修课，若都能修完，则将该课程设为能修完，
即1，返回**true**；若其中有一个不能修完，则直接返回**false**。  
能修完最底层的条件为该课程没有先修课或是前面已经检索过了能修完**(visit[cur]=1)**；  
不能修完最底层的条件为课程之间围成环**(visit[cur]=-1)**。
## 代码(DFS)：
``` C
class Solution {
public:
    bool canFinish(int numCourses, vector<pair<int, int>>& prerequisites) {
        vector<vector<int> > graph(numCourses, vector<int>(0));
        vector<int> visit(numCourses, 0);  //记录课程状态
        stack<int> pre;  //记录有先修课的课程
        for(vector<pair<int, int> >::iterator i = prerequisites.begin(); i != prerequisites.end(); ++i){  //有向图，后修课指向先修课
            graph[(*i).first].push_back((*i).second);
            pre.push((*i).first);
        }
        while(!pre.empty()){  //检索
            int i = pre.top();
            pre.pop();
            if(!searchPreCourse(graph, visit, i)){
                return false;
            }
        }
        return true;
    }
    bool searchPreCourse(vector<vector<int>> &graph, vector<int> &visit, int cur){
        if(visit[cur] == -1) return false;
        if(visit[cur] == 1 || graph[cur].size() == 0) return true;
        visit[cur] = -1;
        for(int i = 0; i < graph[cur].size(); i++){
            if(!searchPreCourse(graph, visit, graph[cur][i])){
                return false;
            }
        }
        visit[cur] = 1;
        return true;
    }
};
```
## 解题思路 2：
本题还可以用BFS的办法解决，用一个有向图graph记录课程**（先修课指向后修课）**，用一个栈pre存储**没有**先修课的课程，
用一个数组degree来记录有先修课课程的先修课个数。    
**然后**依次遍历栈pre中元素，根据先修课再graph中查找后修课，然后将后修课的先修课个数减1，也就是degree-1。
不过要注意减掉个数后没有先修的后修课也加入栈中 。 
**最后**遍历degree，全是0就说明可以完成，否则不可以。
## 代码(BFS)：
``` C
class Solution {
public:
    bool canFinish(int numCourses, vector<pair<int, int>>& prerequisites) {
        vector<vector<int> > graph(numCourses, vector<int>(0));
        vector<int> degree(numCourses, 0);  //记录先修课个数
        for(vector<pair<int, int> >::iterator i = prerequisites.begin(); i != prerequisites.end(); ++i){  //有向图，先修课指向后修课
            graph[(*i).second].push_back((*i).first);
            degree[(*i).first]++;
        }
        stack<int> pre;  //记录没有先修课的课程
        for(int i = 0; i < numCourses; i++){
            if(degree[i] == 0)
                pre.push(i);
        }
        while(!pre.empty()){
            int preCourse = pre.top();
            pre.pop();
            for(int i = 0; i < graph[preCourse].size(); i++){  //根据没有先修课的课程找后修课
                if(--degree[graph[preCourse][i]] == 0)
                    pre.push(graph[preCourse][i]);
            }
        }
        for(int i = 0; i < degree.size(); i++){
            if(degree[i] != 0)
                return false;
        }
        return true;
    }
};
```