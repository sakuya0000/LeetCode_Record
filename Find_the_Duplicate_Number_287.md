# 287. Find the Duplicate Number �����¼
## ��Ŀ������
Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.  
**Example 1:**  
```
Input: [1,3,4,2,2]
Output: 2
```
**Example 2:**
```
Input: [3,1,3,4,2]
Output: 3
```
## ����˼·��
������142. Linked List Circle2 �ı��Σ�һ����˼·��
## ���룺
```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = nums[0], fast = nums[nums[0]];
        while(slow != fast){
            slow = nums[slow];
            fast = nums[nums[fast]];
        }
        fast = 0;
        while(slow != fast){
            slow = nums[slow];
            fast = nums[fast];
        }
        return fast;
    }
};
```