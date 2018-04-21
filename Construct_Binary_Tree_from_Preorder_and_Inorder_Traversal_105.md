# 105. Construct Binary Tree from Preorder and Inorder Traversal �����¼
## ��Ŀ������
Given preorder and inorder traversal of a tree, construct the binary tree.  
**Note:**  
You may assume that duplicates do not exist in the tree.  
For example, given  
```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```
Return the following binary tree:  
```
    3
   / \
  9  20
    /  \
   15   7
``` C
## ����˼·��
����Ļ���˼·�Ǵ�ǰ������������л�ȡ���ڵ㣬Ȼ��������������������ҵ����ڵ����ڵ�λ�ã���߼�Ϊ�������飬�ұ�Ϊ�������顣  
�õݹ������б�����ÿ�εݹ���С������������ķ�Χ��
## ���룺
```
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
    TreeNode *build(vector<int>& pre, int preBeg, int preEnd, vector<int>& in, int inBeg, int inEnd){
        if(inBeg>inEnd || preBeg>preEnd)
            return NULL;
        int rootIndex = 0;
        for(int i = 0; i <= inEnd; i++)
            if(in[i] == pre[preBeg]){
                rootIndex = i;
                break;
            }
        int len = rootIndex - inBeg;
        TreeNode *root = new TreeNode(pre[preBeg]);
        root->left = build(pre, preBeg+1, preBeg+len, in, inBeg, rootIndex-1);
        root->right = build(pre, preBeg+len+1, preEnd, in, rootIndex+1, inEnd);
        return root;
    }
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int preLen = preorder.size();
        return build(preorder, 0, preLen-1, inorder, 0, preLen-1);
    }
};
```