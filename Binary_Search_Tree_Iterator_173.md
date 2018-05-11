# 173. Binary Search Tree Iterator �����¼
## ��Ŀ������
Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.  
  
Calling `next()` will return the next smallest number in the BST.  
  
Note: `next()` and `hasNext()` should run in average O(1) time and uses O(h) memory, where h is the height of the tree.   
## ����˼·��
��BST���������һ�������У�Ȼ��Զ��н��в��������ˡ����������п���ͨ����������õ���
## ���룺
``` C
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class BSTIterator {
private:
    queue<TreeNode *> inOrderNodes;

    void inOrder(TreeNode *root, queue<TreeNode *> &inOrderNodes)
    //��������õ�����
    {
        if (!root)
            return;
        if (root->left)
            inOrder(root->left, inOrderNodes);

        inOrderNodes.push(root);

        if (root->right)
            inOrder(root->right, inOrderNodes);
    }
public:
    BSTIterator(TreeNode *root) {
        inOrder(root, inOrderNodes);
    }

    /** @return whether we have a next smallest number */
    bool hasNext() {
        if(inOrderNodes.empty())
            return false;
        return true;
    }

    /** @return the next smallest number */
    int next() {
        TreeNode *node = inOrderNodes.front();
        inOrderNodes.pop();
        return node->val;
    }

};

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = BSTIterator(root);
 * while (i.hasNext()) cout << i.next();
 */
```