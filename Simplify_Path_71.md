# 71. Simplify Path
## ��Ŀ������
Given an absolute path for a file (Unix-style), simplify it.  
> For example,  
> **path** = "/home/", => "/home"  
> **path** = "/a/./b/../../c/", => "/c"  

Corner Cases:  
- Did you consider the case where path = "/../"?  
	In this case, you should return "/".  
- Another corner case is the path might contain multiple slashes '/' together, such as "/home//foo/".  
	In this case, you should ignore redundant slashes and return "/home/foo".  
## ����˼·��
�����������������������'/'�ַ���"../"�ַ�����"./"�ַ�����������ڱ�����ʱ��ֱ���Թ�'/'����������飬�ٽ��õ�����������".."��"."�Ƚϣ�ÿ�αȽ���յõ����ַ�����  
## ���룺
``` C
class Solution {
public:
    string simplifyPath(string path) {
        string ret, temp;
        int n = path.length();
        for (int i = 0; i < n; i++) {
            if (path[i] == '/') {
                        //��'/'Ϊ����������
                if (temp.empty())
                                //tempΪ�մ�
                    continue;
                if (temp == ".") {
                                //tempΪ'.'
                    temp.clear();
                    continue;
                }
                if (temp == "..") {
                                //tempΪ".."
                    int next = ret.rfind("/");
                    if (next > 0)
                                        //��ֹretΪ�մ���nextΪ-1�����
                        ret.erase(ret.begin() + next, ret.end());
                    else
                        ret.clear();
                    temp.clear();
                }
                else {
                                //���
                    ret = ret + '/' + temp;
                    temp.clear();
                }
            }
            else
                temp += path[i];
        }
        if (temp == ".." && ret.length()>1) {
                //��Ϊ��'/'Ϊ������������ܻ��������һ���ַ�����'/'��������������Ҫ�ٱȽ�һ��
            ret.erase(ret.begin() + ret.rfind("/"), ret.end());
        }
        if (temp != "." && temp != ".." && !temp.empty())
            ret = ret + '/' + temp;
        if (ret.empty())
            ret = "/";
        return ret;
    }
};
```