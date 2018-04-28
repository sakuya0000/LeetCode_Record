# 134. Gas Station 解题记录
## 题目描述：
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

## 解题思路：
首先遍历一遍数组把每次经过加油站gas的得失算出来记录下来，这里的记录并不是把每个站的得失记录下来，而是把`相同得失`的站记录下来。
也就是把失去gas的区间内的所有站失去的gas相加在一起，得到一个记录，反之亦然。因为题目返回的是gas中的下标，所以要用一个数组来记录
下标。  
  
遍历的时候顺便用一个数记录所有数的和来检验是否能完成一次循环，如果遍历结束后这个数小于0直接返回-1。  
  
然后把再遍历一遍记录的数组，从记录为正的数开始往后遍历，如果可以遍历到数组末尾，直接返回该数在gas中的下标即可。  
## 代码：
``` C
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int n = gas.size();
        vector<int> count;
        int sum = gas[0]-cost[0], all = gas[0]-cost[0];
        bool flag = (gas[0]-cost[0])<0?0:1;  //区别区间内数是正是负
        if(flag)
            gas[0] = 0;  //把下标直接记录在gas中
        for(int i = 1; i < n; i++){
            int t = gas[i]-cost[i];
            all += t;  //所有记录的和
            if(t > 0){
                if(flag)
                    sum += t;  //为正区间，继续加
                else{
                //负区间，添加记录，开始新的区间
                    count.push_back(sum);
                    gas[count.size()] = i;
                    sum = t;
                }
                flag = true;
            }
            if(t < 0){
                if(flag){
                //为正区间，添加记录，开始新的区间
                    count.push_back(sum);
                    sum = t;
                }
                else
                //为负区间，继续加
                    sum += t;
                flag = false;
            }
        }
        if(all < 0)  //检验是否能完成一次循环
            return -1;
        count.push_back(sum);
        int len = count.size();
        for(int i = 0; i < len; i++){
        //开始从记录数组中寻找下标
            if(count[i] >= 0){
                int tsum = count[i], j = i+1;
                while(j != len){
                    tsum += count[j++];
                    if(tsum < 0)
                        break;
                }
                if(j == len){
                //遍历到数组结尾
                    return gas[i];
                }
            }
        }
        return -1;
    }
};
```