# Course Schedule II �����¼
## ��Ŀ������
There are a total of n courses you have to take, labeled from `0` to `n-1`.    
Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`    
Given the total number of courses and a list of prerequisite **pairs**, return the ordering of courses you should take to finish all courses.    
There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.    
**Example 1:**
> **Input:** 2, [[1,0]]  
> **Output:** [0,1]  
> **Explanation:** There are a total of 2 courses to take. To take course 1 you should have finished  
>             course 0. So the correct course order is [0,1] .  

**Example 2:**
> **Input:** 4, [[1,0],[2,0],[3,1],[3,2]]  
> **Output:** [0,1,2,3] or [0,2,1,3]  
> **Explanation:** There are a total of 4 courses to take. To take course 3 you should have finished both  
>             courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.   
>             So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3] .  
## ����˼· 1��
�������207��û�ж��ı仯��Ψһ��ͬ���Ƿ��ص��ǿγ����򡣵����ĵ�˼·����һģһ���ģ�����DFS�����
## ����(DFS)��
``` C
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<pair<int, int>>& prerequisites) {
        vector<vector<int> > graph(numCourses, vector<int>(0));  //����ͼ���ɺ��޿�ָ�����޿�
        vector<int> visit(numCourses, 0);  //����״̬
        vector<int> ret;  //��������
        stack<int> pre;  //�洢�����޿εĿγ�
        for(vector<pair<int, int>>::iterator i = prerequisites.begin(); i != prerequisites.end(); i++){  //��ʼ������ͼ
            graph[(*i).first].push_back((*i).second);
            pre.push((*i).first);
        }
        while(!pre.empty()){  //����������޿εĿγ�
            int i = pre.top();
            pre.pop();
            if(!searchPreCourse(graph, visit, ret, i)) return vector<int>();
        }
        for(int i = 0; i < numCourses; i++){  //�������Щû�����޿���û�з��ʹ��Ŀγ�
            if(graph[i].size() == 0 && visit[i] == 0)
                ret.push_back(i);
        }
        return ret;
    }
    bool searchPreCourse(vector<vector<int> > &graph, vector<int> &visit, vector<int> &ret, int cur){
        if(visit[cur] == -1) return false;
        if(visit[cur] == 1) return true;
        visit[cur] = -1;
        for(int i = 0; i < graph[cur].size(); i++){
            if(!searchPreCourse(graph, visit, ret, graph[cur][i])){
                return false;
            }
        }
        visit[cur] = 1;
        ret.push_back(cur);
        return true;
    }
};
```
## ����˼· 2��
ͬ����Ҳ����BFS�������˼·Ҳ��һ���ġ�
## ����(BFS)��
``` C
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<pair<int, int>>& prerequisites) {
        vector<vector<int> > graph(numCourses, vector<int>(0));  //����ͼ�������޿�ָ����޿�
        vector<int> degree(numCourses, 0);  //�γ̵����޿θ���
        vector<int> ret;  //��������
        for(vector<pair<int, int>>::iterator i = prerequisites.begin(); i != prerequisites.end(); i++){  //��ʼ������ͼ����¼�γ����޸���
            graph[(*i).second].push_back((*i).first);
            degree[(*i).first]++;
        }
        stack<int> pre;
        for(int i = 0; i < degree.size(); i++){  //�ҵ�û�����޵Ŀγ̣���ӽ�ջ
            if(degree[i] == 0) pre.push(i);
        }
        while(!pre.empty()){  //����ջ��Ԫ�أ���ӿγ�
            int temp = pre.top();
            ret.push_back(temp);
            pre.pop();
            for(int i = 0; i < graph[temp].size(); i++){
                if(--degree[graph[temp][i]] == 0){
                    pre.push(graph[temp][i]);
                }
            }
        }
        for(int i = 0; i < degree.size(); i++){  //����Ƿ������
            if(degree[i]){
                return vector<int>();
            }
        }
        return ret;
    }
};
```