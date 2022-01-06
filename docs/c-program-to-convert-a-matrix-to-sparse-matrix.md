# 将矩阵转换为稀疏矩阵的 C++程序

> 原文:[https://www . geesforgeks . org/c-program-to-convert-a-matrix-to-sparse-matrix/](https://www.geeksforgeeks.org/c-program-to-convert-a-matrix-to-sparse-matrix/)

给定一个大部分元素为 0 的矩阵，在 C++中将这个矩阵转换成稀疏矩阵
**示例:**

```
Input: Matrix:
0 1 1
1 2 2
2 1 3
3 2 5
4 3 4
Output: Sparse Matrix: 
0 1 0 0 
0 0 2 0 
0 3 0 0 
0 0 5 0 
0 0 0 4
Explanation:
Here the Sparse matrix is represented
in the form Row Column Value

Hence the row 0 1 1 means that the value
of the matrix at row 0 and column 1 is 1
```

**进场:**

1.  得到大部分元素为 0 的矩阵。
2.  创建一个新的 2D 数组来存储只有 3 列(行、列、值)的[稀疏矩阵](https://www.geeksforgeeks.org/sparse-matrix-representation/)。
3.  遍历矩阵，检查元素是否非零。在这种情况下，将该元素插入到[稀疏矩阵](https://www.geeksforgeeks.org/sparse-matrix-representation/)中。
4.  每次插入后，递增可变长度的值(此处为“len”)。这将作为[稀疏矩阵](https://www.geeksforgeeks.org/sparse-matrix-representation/)的行维度
5.  打印[稀疏矩阵](https://www.geeksforgeeks.org/sparse-matrix-representation/)及其元素的维度。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to convert a Matrix
// into Sparse Matrix

#include <iostream>
using namespace std;

// Maximum number of elements in matrix
#define MAX 100

// Array representation
// of sparse matrix
//[][0] represents row
//[][1] represents col
//[][2] represents value
int data[MAX][3];

// total number of elements in matrix
int len;

// insert elements into sparse matrix
void insert(int r, int c, int val)
{
    // insert row value
    data[len][0] = r;

    // insert col value
    data[len][1] = c;

    // insert element's value
    data[len][2] = val;

    // increment number of data in matrix
    len++;
}

// printing Sparse Matrix
void print()
{
    cout << "\nDimension of Sparse Matrix: "
         << len << " x " << 3;
    cout << "\nSparse Matrix: \nRow Column Value\n";

    for (int i = 0; i < len; i++) {

        cout << data[i][0] << " "
             << data[i][1] << " "
             << data[i][2] << "\n";
    }
}

// Driver code
int main()
{
    int i, j;
    int r = 5, c = 4;

    // Get the matrix
    int a[r] = { { 0, 1, 0, 0 },
                    { 0, 0, 2, 0 },
                    { 0, 3, 0, 0 },
                    { 0, 0, 5, 0 },
                    { 0, 0, 0, 4 } };

    // print the matrix
    cout << "\nMatrix:\n";
    for (i = 0; i < r; i++) {
        for (j = 0; j < c; j++) {
            cout << a[i][j] << " ";
        }
        cout << endl;
    }

    // iterate through the matrix and
    // insert every non zero elements
    // in the Sparse Matrix
    for (i = 0; i < r; i++)
        for (j = 0; j < c; j++)
            if (a[i][j] > 0)
                insert(i, j, a[i][j]);

    // Print the Sparse Matrix
    print();

    return 0;
}
```

**Output:** 

```
Matrix:
0 1 0 0 
0 0 2 0 
0 3 0 0 
0 0 5 0 
0 0 0 4 

Dimension of Sparse Matrix: 5 x 3
Sparse Matrix: 
Row Column Value
0 1 1
1 2 2
2 1 3
3 2 5
4 3 4
```