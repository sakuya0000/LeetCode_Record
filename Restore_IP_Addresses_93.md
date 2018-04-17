# 93. Restore IP Addresses �����¼
## ��Ŀ������
Given a string containing only digits, restore it by returning all possible valid IP address combinations.  
For example:  
Given `"25525511135"`,  
return `["255.255.11.135", "255.255.111.35"]`. (Order does not matter)  
## ����˼·��
**Ҫ������������Ҫ�˽�IP��ַ����ɣ�**  
1. ÿ����ַ��4��������ɣ���3��'.'�ָ�;  
2. ÿ������С�ڵ���255��  

**������������ǾͿ��Կ�ʼ�����ˣ����������˵ݹ�ķ��������⣺**  
1. ������һ����count����������˼������ֺ�һ����beg����¼��һ�����ֵ���ֹλ�ã����count<3�Ļ��ͱ������£������ĸ��ִ�����IP��ַ��ɵĵڶ������������Ͼͼ����ݹ飬�����Ͼ�ֱ�ӽ�����  
2. ���count==3ʱ��ֱ��ȡ�ַ��������һ���ֽ��бȽϣ�������ӵ����飬�����Ͼͽ�����������������������������  
## ���룺
``` C
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
        vector<string> ret;
        select(s, ret, "", 0, 0, s.size());
        return ret;
    }
    bool substrCheck(string str, string &ret, int count){
    //����ִ��Ƿ����������������Ͼ�˳�������
        unsigned num = 0, len = str.size();
        if(len > 1 && str[0] == '0')
            return false;
        for(int i = 0; i < len; i++){
            num = num * 10 + str[i] - '0';
        }
        if(num <= 255){
            if(count)
                ret += '.' + str;
            else
                ret += str;
            return true;
        }
        return false;
    }
    void select(string &s, vector<string> &ret, string tempS, int count, int beg, int len){
        if(count == 3){
        //��������
            if(substrCheck(s.substr(beg, len-beg), tempS, count)){
                ret.push_back(tempS);
            }
            return;
        }
        for(int i = beg+1; i < len; i++){
        //����Ѱ����һ������
            string t = tempS;
            if(substrCheck(s.substr(beg, i-beg), t, count))
                select(s, ret, t, count+1, i, len);
            else
                break;
        }
    }
};
```