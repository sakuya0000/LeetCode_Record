# 304. Range Sum Query 2D - Immutable �����¼
## ��Ŀ������
Given a 2D matrix matrix, find the sum of the elements inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).    
**Example:**
```
Given matrix = [
  [3, 0, 1, 4, 2],
  [5, 6, 3, 2, 1],
  [1, 2, 0, 1, 5],
  [4, 1, 0, 1, 7],
  [1, 0, 3, 0, 5]
]

sumRegion(2, 1, 4, 3) -> 8
sumRegion(1, 1, 2, 2) -> 11
sumRegion(1, 2, 2, 4) -> 12
```
## ����˼·��
���������һ�����飬�ٸ�����һ���������ϽǺ����½ǵ�λ�ã����ؾ������������ĺ͡�    
���Դ���һ���µ����飬�洢��(0, 0)����λ�õľ���͡�����������һ�������λ�õ�ʱ��ֻҪ��3�μӼ��������ˡ�    
��ʼ���������ʱ������ö�̬�滮�����
## ���룺
``` C
class NumMatrix {
    vector<vector<int>> newMatrix;
public:
    NumMatrix(vector<vector<int>> matrix) {
        int row = matrix.size();
        if(row == 0)
            return;
        int col = matrix[0].size();
        if(col == 0)
            return;
        vector<vector<int>> temp(row+1, vector<int>(col+1, 0));  //���������һ��һ�У����ص�ʱ�����ж��Ƿ��ǵ�һ�е�һ�е����
        newMatrix = temp;
        int sum = 0;
        for(int i = 0; i < col; i++){  //��ʼ����һ��
            sum += matrix[0][i];
            newMatrix[1][i+1] = sum;
        }
        for(int i = 1; i < row; i++){  //�ӵڶ��п�ʼ����
            sum = 0;
            for(int j = 0; j < col; j++){
                sum += matrix[i][j];
                newMatrix[i+1][j+1] = sum + newMatrix[i][j+1];
            }
        }
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        return newMatrix[row2+1][col2+1]-newMatrix[row2+1][col1]-newMatrix[row1][col2+1]+newMatrix[row1][col1];  //����ʱ�Ӽ�
    }
};

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix obj = new NumMatrix(matrix);
 * int param_1 = obj.sumRegion(row1,col1,row2,col2);
 */
```