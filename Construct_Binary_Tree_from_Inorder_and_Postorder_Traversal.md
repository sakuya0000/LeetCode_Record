# 106. Construct Binary Tree from Inorder and Postorder Traversal �����¼
## ��Ŀ������
Given inorder and postorder traversal of a tree, construct the binary tree.  
  
**Note:**  
You may assume that duplicates do not exist in the tree.  
  
For example, given  
```
inorder = [9,3,15,20,7]  
postorder = [9,15,7,20,3]  
```
Return the following binary tree:  
```
    3
   / \
  9  20
    /  \
   15   7
```
## ����˼·��
�����˼·����һ��û�ж������𣬿���˵����Ŀ������һģһ���������postorder���ſ����൱����һ���preorder��
ֻ����������������������������������  
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
    TreeNode* build(vector<int>& in, int inBeg, int inEnd, vector<int>& post, int postBeg, int postEnd){
        if(inBeg>inEnd || postBeg>postEnd)
            return NULL;
        int root_index = inBeg;
        for(; root_index <= inEnd; root_index++){
        //Ѱ�Ҹ��ڵ�
            if(in[root_index] == post[postEnd])
                break;
        }
        TreeNode *root = new TreeNode(in[root_index]);
        int len = root_index - inBeg;
        root->right = build(in, root_index+1, inEnd, post, postBeg+len, postEnd-1);  //�ݹ�Ѱ���ҽڵ�
        root->left = build(in, inBeg, root_index-1, post, postBeg, postBeg+len-1);  //�ݹ�Ѱ����ڵ�
        return root;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        int n = inorder.size()-1;
        return build(inorder, 0, n, postorder, 0, n);
    }
};
```