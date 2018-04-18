# 98. Validate Binary Search Tree �����¼
## ��Ŀ������
Given a binary tree, determine if it is a valid binary search tree (BST).  
Assume a BST is defined as follows:  
- The left subtree of a node contains only nodes with keys less than the node's key.  
- The right subtree of a node contains only nodes with keys greater than the node's key.  
- Both the left and right subtrees must also be binary search trees.  
**Example 1:**  
```
    2
   / \
  1   3
```
Binary tree `[2,1,3]`, return **true**.  
**Example 2:**  
```
    1
   / \
  2   3
```
Binary tree `[1,2,3]`, return **false**.  
## ����˼·��
�����Ǽ���һ���������Ƿ���BST���ʺ��õݹ��������  
- �����ҽ��ݹ���ֹ������Ϊ�ڵ�Ϊ��;  
- Ȼ��ÿ�����±�����ʱ�����´�һ������`(minN, maxN)`������һ���ڵ�������������ڷ���false���������������  

������Ĵ��ݹ���Ϊ��  
1. �������Ľڵ����ҽڵ㣬����`(val, maxN)`;  
2. �������Ľڵ�����ڵ㣬����`(minN, val)`;  
## ���룺
``` C
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool judge(TreeNode* root, long long minN, long long maxN){
        if(!root)
        //��ֹ����
            return true;
        if(!(root->val>minN && root->val<maxN))
        //����val�Ƿ���������
            return false;
        return judge(root->left, minN, root->val) && judge(root->right, root->val, maxN);  //���±���
    }
    bool isValidBST(TreeNode* root) {
        return judge(root, -21474836470, 21474836470);  //��Ϊ�ڵ��������ΪINT_MAX��INT_MIN
    }
};
```