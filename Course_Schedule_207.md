# 207.Course Schedule �����¼
## ��Ŀ������
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

## ����˼· 1��
���������DFS��ʵ�֣�����һ������ͼgraph����¼�γ̣�������ͼ**�ɺ��޿�ָ�����޿�**����һ��ջpre����¼**��**���޿εĿγ̣�
��һ������visit����¼�γ̵�״̬���Ƿ�����ɣ���Ȼ�����õݹ�鿴�γ��Ƿ������ꡣ    
���õݹ������˼·�ǣ��Ƚ��ÿγ���Ϊ�������꣬��visit[cur]=-1��Ȼ����graph���α����ÿγ̵����޿Σ����������꣬�򽫸ÿγ���Ϊ�����꣬
��1������**true**����������һ���������꣬��ֱ�ӷ���**false**��  
��������ײ������Ϊ�ÿγ�û�����޿λ���ǰ���Ѿ���������������**(visit[cur]=1)**��  
����������ײ������Ϊ�γ�֮��Χ�ɻ�**(visit[cur]=-1)**��
## ����(DFS)��
``` C
class Solution {
public:
    bool canFinish(int numCourses, vector<pair<int, int>>& prerequisites) {
        vector<vector<int> > graph(numCourses, vector<int>(0));
        vector<int> visit(numCourses, 0);  //��¼�γ�״̬
        stack<int> pre;  //��¼�����޿εĿγ�
        for(vector<pair<int, int> >::iterator i = prerequisites.begin(); i != prerequisites.end(); ++i){  //����ͼ�����޿�ָ�����޿�
            graph[(*i).first].push_back((*i).second);
            pre.push((*i).first);
        }
        while(!pre.empty()){  //����
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
## ����˼· 2��
���⻹������BFS�İ취�������һ������ͼgraph��¼�γ�**�����޿�ָ����޿Σ�**����һ��ջpre�洢**û��**���޿εĿγ̣�
��һ������degree����¼�����޿ογ̵����޿θ�����    
**Ȼ��**���α���ջpre��Ԫ�أ��������޿���graph�в��Һ��޿Σ�Ȼ�󽫺��޿ε����޿θ�����1��Ҳ����degree-1��
����Ҫע�����������û�����޵ĺ��޿�Ҳ����ջ�� �� 
**���**����degree��ȫ��0��˵��������ɣ����򲻿��ԡ�
## ����(BFS)��
``` C
class Solution {
public:
    bool canFinish(int numCourses, vector<pair<int, int>>& prerequisites) {
        vector<vector<int> > graph(numCourses, vector<int>(0));
        vector<int> degree(numCourses, 0);  //��¼���޿θ���
        for(vector<pair<int, int> >::iterator i = prerequisites.begin(); i != prerequisites.end(); ++i){  //����ͼ�����޿�ָ����޿�
            graph[(*i).second].push_back((*i).first);
            degree[(*i).first]++;
        }
        stack<int> pre;  //��¼û�����޿εĿγ�
        for(int i = 0; i < numCourses; i++){
            if(degree[i] == 0)
                pre.push(i);
        }
        while(!pre.empty()){
            int preCourse = pre.top();
            pre.pop();
            for(int i = 0; i < graph[preCourse].size(); i++){  //����û�����޿εĿγ��Һ��޿�
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