# 324. Wiggle Sort II �����¼
## ��Ŀ������
Given an unsorted array `nums`, reorder it such that `nums[0] < nums[1] > nums[2] < nums[3]...`.    
**Example 1:**
```
Input: nums = [1, 5, 1, 1, 6, 4]
Output: One possible answer is [1, 4, 1, 5, 1, 6].
```    
**Example 2:**
```
Input: nums = [1, 3, 2, 2, 3, 1]
Output: One possible answer is [2, 3, 1, 3, 1, 2].
```
## ����˼·��
�Ƚ���������Ȼ�������Ϊ�������֣�ÿ�δ�ǰ�벿�ֵ�ĩβȡһ�����ٴӺ�벿�ֵ�ĩβȡһ����
## ���룺
``` C
class Solution {
public:
	void wiggleSort(vector<int>& nums) {
		int len = nums.size();
		int i = (len + 1) / 2;
		int j = len;
		vector<int> tmp = nums;
		sort(tmp.begin(), tmp.end());
		for (int k = 0; k < len; k++){
			nums[k] = (k & 1) == 1 ? tmp[--j] : tmp[--i];
		}
	}
};
```