# 152. Maximum Product Subarray �����¼
## ��Ŀ������
Find the contiguous subarray within an array (containing at least one number) which has the largest product.  
For example, given the array **[2,3,-2,4]**,  
the contiguous subarray **[2,3]** has the largest product = **6**. 
## ����˼·��
**�����ɷ�Ϊ���������**  
1. �з�0��Ԫ�أ����ȷ�������������<0��Ԫ�أ��ɷ�Ϊ2�������  
�� 1)����Ϊ`ż��`���������ֻҪ��Ԫ��ȫ��һ��ͻ�õ����ֵ��  
�� 2)����Ϊ`����`�����ȿ�һ������: 
***
`[-1, -2, -3, -4, -5]`  
*��Ϊ��Ŀ��Ҫ�󷵻ص����˻������Կ����ų����õ��������Ϊ��������*  
`[-1, -2, -3, -4]`  
`[-2, -3, -4, -5]`  
***
������ˣ����������ֻ�����ֿ����ԣ��ֱ���`�ӵ�һ��Ԫ�س˵������ڶ�������`��`�ӵڶ��������˵����һ��Ԫ��`��  
������`>0`��Ԫ��û��˿����Ӱ�죬�˹�ȥ���ɡ����㸺���븺�����м����ǰ����Ǻ������������Ҳֻ���������Ľ����  
2.��0��Ԫ�أ������ĸ�����0��Ϊ0������0���൱һ����ֹ������һ�����黮�ֳ��������顣  
## ���룺
``` C
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int maxAll = nums[0], n = nums.size();
        int first = 1, second = 1;
        bool flag = 0; //�Ƿ�����������־
        for(int i = 0; i < n; i++){
            first *= nums[i];
            second *= nums[i];
            maxAll = maxAll>first?maxAll:first;  //�����������ĵ�һ�����
            maxAll = maxAll>second?maxAll:second;  //�����ĵڶ������
            if(nums[i] < 0 && !flag){
            //��һ����������
                second = 1;
                flag = 1;
            }
            if(nums[i] == 0){
            //����0�����
                maxAll = 0>maxAll?0:maxAll;
                flag = 0;-5
                first = 1;
                second = 1;
            }
        }
        return maxAll;
    }
};
```