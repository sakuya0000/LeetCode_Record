# 142. Linked List Cycle II �����¼
## ��Ŀ������
Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.  
  
**Note:** Do not modify the linked list. 
## ����˼·��
��������ָ��fast��slow����������fastָ����ٶ�Ϊslow�ٶȵ�������
����˾��������һ���������ǵ�λ�þ��뻷��ʼ��λ�ú�headָ�뵽����ʼ��λ�����ڵ�ĸ�����ͬ��
Ȼ����slowָ��Ϊhead���ٴα�����ڶ����������ǻ���ʼ��λ�á�
## ���룺
``` C
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* fast = head, *slow = head;
        while(fast){
            if(!fast->next || !fast->next->next)
	    //��������
                return NULL;
            fast = fast->next->next;
            slow = slow->next;
            if(fast == slow)  //��һ������
                break;
        }
        slow = head;
        while(slow != fast){
        //�ڶ�������
            slow = slow->next;
            fast = fast->next;
        }
        return slow;
    }
};
```