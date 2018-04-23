# 114. Flatten Binary Tree to Linked List �����¼
## ��Ŀ������
Given a binary tree, flatten it to a linked list in-place.  
  
For example, given the following tree:  
```
    1
   / \
  2   5
 / \   \
3   4   6
```
The flattened tree should look like:  
```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```
## ����˼·��
����Ҫ�Ƚ�������������������λ�ã�ȷ������С�Ľڵ�����ұߣ�����Խڵ���в�����ֵ���Ҳ����ҽڵ㡣  
Ȼ�������Ӹ��ڵ㣬�ҽڵ㡢��ڵ��˳��һֱ�ݹ���Ӵ�������ˡ�  
�����Ŀ��Ҫ���Ƿ�����ڵ�Ļ��Ϳ����������λ�õĲ��裬Ч��Ҳ�����һ�㡣
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
    TreeNode* ListRoot = NULL;  //������¼��ӵ�λ��
    void transform(TreeNode* root){
        if(!root)
            return;
        TreeNode* temp_right =root->right;
        root->right = root->left;
        root->left = temp_right;
        ListRoot->right = root;  //��Ӹ��ڵ�
        ListRoot = ListRoot->right;
        transform(root->right);  //����
        transform(root->left);  //����
        root->left = NULL;  //�ٽ���ڵ����
    }
    void flatten(TreeNode* root) {
        ListRoot = new TreeNode(0);
        transform(root);
    }
};
```