# 95. Unique Binary Search Trees II
## 题目描述：
Given an integer n, generate all structurally unique **BST's** (binary search trees) that store values 1...n.  
For example,  
Given n = 3, your program should return all 5 unique BST's shown below.  
>   1         3     3      2      1
>    \       /     /      / \      \
>     3     2     1      1   3      2
>    /     /       \                 \
>   2     1         2                 3

## 解题思路：
由于这道题的要求是返回所有BST的根节点，因此要从二叉树的末尾开始添加节点，先获取左子树的所有可能性，再获取右子树的所有可能性，然后将两者组合起来。
## 代码：
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
    vector<TreeNode*> addTrees(int beg, int end){
        vector<TreeNode*> ret;
        if(beg > end){
        //子树不存在
            ret.push_back(NULL);
            return ret;
        }
        if(beg == end){
        //子树唯一节点
            TreeNode *p = new TreeNode(beg);
            ret.push_back(p);
            return ret;
        }
        for(int i = beg; i <= end; i++){
        //获取两子树组合的所有可能性，作为这一层子树返回
            vector<TreeNode*> left = addTrees(beg, i-1);  //获取下一层左子树
            vector<TreeNode*> right = addTrees(i+1, end);  //获取下一层右子树
            for(int j = 0; j < left.size(); j++){
                for(int k = 0; k < right.size(); k++){
                //组合
                    TreeNode* root = new TreeNode(i);
                    root->left = left[j];
                    root->right = right[k];
                    ret.push_back(root);
                }
            }
        }
        return ret;
    }
    vector<TreeNode*> generateTrees(int n) {
        if(n < 1)
            return vector<TreeNode*>(NULL);
        return addTrees(1, n);
    }
};
```