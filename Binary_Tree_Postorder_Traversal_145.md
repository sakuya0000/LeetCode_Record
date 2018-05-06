# 145. Binary Tree Postorder Traversal �����¼
## ��Ŀ������
Given a binary tree, return the postorder traversal of its nodes' values.  
  
**Example:**  
  
```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [3,2,1]
```
  
**Follow up:** Recursive solution is trivial, could you do it iteratively?  
## ����˼·��
һ��ʼû�п����Ǹ�Follow up���õݹ�����һ�飬����д�����ʱ�򿴵��ˣ��������õ�������һ�顣  
  
��Ϊ�ݹ��ʵ�ֺ����ף�˼·Ҳ��ûʲô�ý��ˡ�  
  
�õ�����д�Ļ��Ͳ���ֱ�ӴӶ�������ĩβ��ʼ���ˣ������Ҳ��ôӸ��ڵ㿪ʼ�ӣ�Ȼ���ټ��������������������ķ�����  
����ٷ�ת����Ϳ��Եõ�����ǰ������������ˡ�
## ���루�ݹ飩��
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
    void addElement(TreeNode* cur, vector<int> &ret){
        if(!cur)
            return;
        addElement(cur->left, ret);
        addElement(cur->right, ret);
        ret.push_back(cur->val);
    }
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ret;
        addElement(root, ret);
        return ret;
    }
};
```
## ���루��������
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
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ret;
        stack<TreeNode*> leftNodes;  //��ջ��������ڵ�λ��
        while(root){
            ret.push_back(root->val);
            if(root->right){
            //�Ȳ鿴�ҽڵ��Ƿ����
                if(root->left){
                //������ڵ�������ջ
                    leftNodes.push(root->left);
                }
                root = root->right;
                continue;
            }
            if(root->left){
            //��ڵ㲻���ڣ��ٿ��ҽڵ��Ƿ����
                root = root->left;
                continue;
            }
            if(leftNodes.size()){
            //���������ٿ�ջ���Ƿ���ڽڵ�
                root = leftNodes.top();
                leftNodes.pop();
                continue;
            }
            break;  //���ȫ�������ھ��˳�ѭ��
        }
        reverse(ret.begin(), ret.end());
        return ret;
    }
};
```