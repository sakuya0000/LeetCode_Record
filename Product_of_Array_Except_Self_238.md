# 238. Product of Array Except Self
## ��Ŀ������
Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].  
Solve it *without division* and in *O(n)*.  
For example, given *[1,2,3,4]*, return **`[24,12,8,6]`**.  
## ����˼·��
�������ǿ����ȴ���һ������ret����ret�ĵ�һ����Ϊ1��Ȼ����ѭ����ret�����дӵڶ���Ԫ�ؿ�ʼ��ֵ��������`��һ��Ԫ��`��`nums�еĶ�ӦԪ��`��  
��˵�һ�α���������Եõ�ret�е�Ԫ�طֲ�Ϊ
> [1, nums[0], nums[0]*nums[1],����, ��nums[i](i<amp;n-1)]��  
������������һ������nums�����ĩβ��ʼ�ˣ�ÿһ�γ˺�Ҫ��ret�Ķ�ӦԪ�س��������`����ret��ǰԪ��δ�˵Ĳ���`��ֱ���˵�nums[1]��
## ���룺
``` C
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> ret(n, 1);
        for(int i = 1; i < n; i++){
        //��һ�α���
            ret [i] = nums[i-1] * ret[i-1];
        }
        for(int i = n - 1; i > 1; i--){
        //�ڶ��α���
            ret[0] *= nums[i];
            ret[i-1] *= ret[0];
        }
        ret[0] *= nums[1];  //�������ͬ����
        return ret;
    }
};
```