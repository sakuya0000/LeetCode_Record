# 134. Gas Station �����¼
## ��Ŀ������
There are N gas stations along a circular route, where the amount of gas at station i is `gas[i]`.  
  
You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from station i to its next station (*i*+1). You begin the journey with an empty tank at one of the gas stations.  
  
Return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1.  
  
**Note:**  
  
- If there exists a solution, it is guaranteed to be unique.  
- Both input arrays are non-empty and have the same length.  
- Each element in the input arrays is a non-negative integer.  
  
**Example 1:**  
  
> <strong>Input:</strong>
gas  = [1,2,3,4,5]
cost = [3,4,5,1,2]
	
> <strong>Output:</strong> 3
	
> <strong>Explanation:</strong>
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4  
Travel to station 4. Your tank = 4 - 1 + 5 = 8  
Travel to station 0. Your tank = 8 - 2 + 1 = 7  
Travel to station 1. Your tank = 7 - 3 + 2 = 6  
Travel to station 2. Your tank = 6 - 4 + 3 = 5  
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.  
Therefore, return 3 as the starting index.  

  
**Example 2:**  
  
> <strong>Input: </strong>
gas  = [2,3,4]
cost = [3,4,3]
	
> <strong>Output:</strong> -1
	
> <strong>Explanation:</strong>
You can't start at station 0 or 1, as there is not enough gas to travel to the next station.  
Let's start at station 2 and fill up with 4 unit of gas. Your tank = 0 + 4 = 4  
Travel to station 0. Your tank = 4 - 3 + 2 = 3  
Travel to station 1. Your tank = 3 - 3 + 3 = 3  
You cannot travel back to station 2, as it requires 4 unit of gas but you only have 3.  
Therefore, you can't travel around the circuit once no matter where you start.  

## ����˼·��
���ȱ���һ�������ÿ�ξ�������վgas�ĵ�ʧ�������¼����������ļ�¼�����ǰ�ÿ��վ�ĵ�ʧ��¼���������ǰ�`��ͬ��ʧ`��վ��¼������
Ҳ���ǰ�ʧȥgas�������ڵ�����վʧȥ��gas�����һ�𣬵õ�һ����¼����֮��Ȼ����Ϊ��Ŀ���ص���gas�е��±꣬����Ҫ��һ����������¼
�±ꡣ  
  
������ʱ��˳����һ������¼�������ĺ��������Ƿ������һ��ѭ����������������������С��0ֱ�ӷ���-1��  
  
Ȼ����ٱ���һ���¼�����飬�Ӽ�¼Ϊ��������ʼ���������������Ա���������ĩβ��ֱ�ӷ��ظ�����gas�е��±꼴�ɡ�  
## ���룺
``` C
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int n = gas.size();
        vector<int> count;
        int sum = gas[0]-cost[0], all = gas[0]-cost[0];
        bool flag = (gas[0]-cost[0])<0?0:1;  //�����������������Ǹ�
        if(flag)
            gas[0] = 0;  //���±�ֱ�Ӽ�¼��gas��
        for(int i = 1; i < n; i++){
            int t = gas[i]-cost[i];
            all += t;  //���м�¼�ĺ�
            if(t > 0){
                if(flag)
                    sum += t;  //Ϊ�����䣬������
                else{
                //�����䣬��Ӽ�¼����ʼ�µ�����
                    count.push_back(sum);
                    gas[count.size()] = i;
                    sum = t;
                }
                flag = true;
            }
            if(t < 0){
                if(flag){
                //Ϊ�����䣬��Ӽ�¼����ʼ�µ�����
                    count.push_back(sum);
                    sum = t;
                }
                else
                //Ϊ�����䣬������
                    sum += t;
                flag = false;
            }
        }
        if(all < 0)  //�����Ƿ������һ��ѭ��
            return -1;
        count.push_back(sum);
        int len = count.size();
        for(int i = 0; i < len; i++){
        //��ʼ�Ӽ�¼������Ѱ���±�
            if(count[i] >= 0){
                int tsum = count[i], j = i+1;
                while(j != len){
                    tsum += count[j++];
                    if(tsum < 0)
                        break;
                }
                if(j == len){
                //�����������β
                    return gas[i];
                }
            }
        }
        return -1;
    }
};
```