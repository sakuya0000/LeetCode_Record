# 307. Range Sum Query - Mutable �����¼
## ��Ŀ������
Given an integer array nums, find the sum of the elements between indices i and j (i �� j), inclusive.    
The update(i, val) function modifies nums by updating the element at index i to val.    
**Example:**
```
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```
## ����˼·��
�����ҵ�˼·�Ǵ���һ���������洢��0λ�õ�Ԫ��λ�õ��������ĺ͡�Ȼ����i��j�͵�ʱ��ֻҪ��һ�¾Ϳ����ˡ������µ�Ч�ʺ�����ô�ߡ�
## ���룺
``` C
class NumArray {
    vector<int> newNums;
public:
    NumArray(vector<int> nums) {
        int n = nums.size();
        vector<int> temp(n+1, 0);
        newNums = temp;
        for(int i = 1; i < n+1; i++){
            newNums[i] = newNums[i-1] + nums[i-1];
        }
    }
    
    void update(int i, int val) {
        int minusNum = newNums[i+1] - newNums[i];
        i++;
        for(; i < newNums.size(); i++){
            newNums[i] -= minusNum;
            newNums[i] += val;
        }
    }
    
    int sumRange(int i, int j) {
        return newNums[j+1] - newNums[i];
    }
};

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * obj.update(i,val);
 * int param_2 = obj.sumRange(i,j);
 */
```