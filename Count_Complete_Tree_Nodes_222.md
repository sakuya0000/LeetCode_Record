# 222. Count Complete Tree Nodes �����¼
## ��Ŀ������
Given a complete binary tree, count the number of nodes.  
  
**Example:**  
```
Input: 
    1
   / \
  2   3
 / \  /
4  5 6

Output: 6
```
## ����˼·��
��ȫ�������ض�����һ��������������һ����ȫ�����������Կ������õݹ���������⡣
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
    int countNodes(TreeNode* root) {
        if(!root) 
            return 0;
        int l = getLeft(root) + 1;
        int r = getRight(root) + 1;
        if(l==r) {
            return (2<<(l-1)) - 1;
        } 
        else {
            return countNodes(root->left) + countNodes(root->right) + 1;
        }
    }
    int getLeft(TreeNode* root) {
        int count = 0;
        while(root->left!=NULL) {
            root = root->left;
            ++count;
        }
        return count;
    }
    int getRight(TreeNode* root) {
        int count = 0;
        while(root->right!=NULL) {
            root = root->right;
            ++count;
        }
        return count;
    }
};
```