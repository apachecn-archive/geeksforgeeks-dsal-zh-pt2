# 使用运算符重载的矩阵运算

> 原文:[https://www . geesforgeks . org/matrix-operations-use-operator-overloading/](https://www.geeksforgeeks.org/matrix-operations-using-operator-overloading/)

**先决条件:** [运算符重载](https://www.geeksforgeeks.org/operator-overloading-c/)
给定 NxN 维度的两个矩阵 **mat1[][]** 和 **mat2[][]** ，任务是使用[运算符重载](https://www.geeksforgeeks.org/operator-overloading-c/)执行[矩阵运算](https://www.geeksforgeeks.org/different-operation-matrices/)。
**举例:**

> **输入:** arr1[][] = { {1，2，3}，{4，5，6}，{1，2，3}}，arr2[][] = { {1，2，3}，{4，5，16}，{1，2， 3}}
> **输出:**
> 两个给定矩阵相加为:
> 2 4 6
> 8 10 22
> 2 4 6
> 两个给定矩阵相减为:
> 0 0
> 0 0-10
> 0 0
> 两个给定矩阵相乘为:
> 12 18 44
> 30 45 110
> 12 18 44
> **arr2[][] = { {1，2，3}，{41，5，16}，{1，22，3}}
> **输出:**
> 两个给定矩阵相加为:
> 12 4 6
> 45 10 16
> 2 34 6
> 两个给定矩阵相减为:
> 10 0 0 0
> -37 0-16
> 0-10
> 相乘**

**方法:**
要重载 **+** 、**–**、 ***** 运算符，我们将创建一个名为 matrix 的类，然后制作一个公共函数来重载运算符。

*   至霸王符 **'+'** 使用原型:

```
Return_Type classname :: operator +(Argument list)
{
    // Function Body
}
```

*   **例如:**

> 假设有两个相同维度的矩阵 **M1[][]** 和 **M2[][]** 。使用运算符重载 M1[][]和 M2[][]可以添加为 **M1 + M2** 。

> 在上面的语句中，M1 被视为 hai global，而 M2[][]被作为参数传递给函数**“void Matrix::operator+(Matrix x)**”。

> 在上述重载函数中，两个矩阵相加的方法是通过将 M1[][]作为第一个矩阵，将 M2[][]作为第二个矩阵，即矩阵 x(作为自变量)来实现的。

*   至霸王符 **'-'** 使用原型:

```
Return_Type classname :: operator -(Argument list)
{
    // Function Body
}
```

*   **例如:**

> 假设有两个相同维度的矩阵 **M1[][]** 和 **M2[][]** 。使用运算符重载 M1[][]和 M2[][]可以添加为**M1-M2**

> 在上面的语句中，M1 被视为 hai global，而 M2[][]被作为参数传递给函数**“void Matrix::operator-(Matrix x)**”。

> 在上面的重载函数中，两个矩阵的[减法是通过将 M1[][]作为第一个矩阵，将 M2[][]作为第二个矩阵，即矩阵 x(作为自变量)来实现的。](https://www.geeksforgeeks.org/program-subtraction-matices/)

*   给霸王符**' ***使用原型:

```
Return_Type classname :: operator *(Argument list)
{
    // Function Body
}
```

> 假设有两个相同维度的矩阵 **M1[][]** 和 **M2[][]** 。使用运算符重载 M1[][]和 M2[][]可以添加为 **M1 * M2** 。

> 在上面的语句中，M1 被视为 hai global，而 M2[][]被作为参数传递给函数**“void Matrix::operator *(Matrix x)**”。

> 在上述重载函数中，两个矩阵的[相乘的方法是通过将 M1[][]作为第一个矩阵，将 M2[][]作为第二个矩阵，即矩阵 x(作为自变量)来实现的。](https://www.geeksforgeeks.org/c-program-multiply-two-matrices/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
#define rows 50
#define cols 50
using namespace std;

int N;

// Class for Matrix operator overloading
class Matrix {

    // For input Matrix
    int arr[rows][cols];

public:
    // Function to take input to arr[][]
    void input(vector<vector<int> >& A);
    void display();

    // Functions for operator overloading
    void operator+(Matrix x);
    void operator-(Matrix x);
    void operator*(Matrix x);
};

// Functions to get input to Matrix
// array arr[][]
void Matrix::input(vector<vector<int> >& A)
{

    // Traverse the vector A[][]
    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            arr[i][j] = A[i][j];
        }
    }
}

// Function to display the element
// of Matrix
void Matrix::display()
{

    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            // Print the element
            cout << arr[i][j] << ' ';
        }
        cout << endl;
    }
}

// Function for addition of two Matrix
// using operator overloading
void Matrix::operator+(Matrix x)
{
    // To store the sum of Matrices
    int mat[N][N];

    // Traverse the Matrix x
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {

            // Add the corresponding
            // blocks of Matrices
            mat[i][j] = arr[i][j]
                        + x.arr[i][j];
        }
    }

    // Display the sum of Matrices
    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            // Print the element
            cout << mat[i][j] << ' ';
        }
        cout << endl;
    }
}

// Function for subtraction of two Matrix
// using operator overloading
void Matrix::operator-(Matrix x)
{
    // To store the difference of Matrices
    int mat[N][N];

    // Traverse the Matrix x
    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            // Subtract the corresponding
            // blocks of Matrices
            mat[i][j] = arr[i][j]
                        - x.arr[i][j];
        }
    }

    // Display the difference of Matrices
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {

            // Print the element
            cout << mat[i][j] << ' ';
        }
        cout << endl;
    }
}

// Function for multiplication of
// two Matrix using operator
// overloading
void Matrix::operator*(Matrix x)
{
    // To store the multiplication
    // of Matrices
    int mat[N][N];

    // Traverse the Matrix x
    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            // Initialise current block
            // with value zero
            mat[i][j] = 0;

            for (int k = 0; k < N; k++) {
                mat[i][j] += arr[i][k]
                             * (x.arr[k][j]);
            }
        }
    }

    // Display the multiplication
    // of Matrices
    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            // Print the element
            cout << mat[i][j] << ' ';
        }
        cout << endl;
    }
}

// Driver Code
int main()
{

    // Dimension of Matrix
    N = 3;

    vector<vector<int> > arr1
        = { { 1, 2, 3 },
            { 4, 5, 6 },
            { 1, 2, 3 } };

    vector<vector<int> > arr2
        = { { 1, 2, 3 },
            { 4, 5, 16 },
            { 1, 2, 3 } };

    // Declare Matrices
    Matrix mat1, mat2;

    // Take Input to matrix mat1
    mat1.input(arr1);

    // Take Input to matrix mat2
    mat2.input(arr2);

    // For addition of matrix
    cout << "Addition of two given"
         << " Matrices is : \n";
    mat1 + mat2;

    // For subtraction of matrix
    cout << "Subtraction of two given"
         << " Matrices is : \n";
    mat1 - mat2;

    // For multiplication of matrix
    cout << "Multiplication of two"
         << " given Matrices is : \n";
    mat1* mat2;

    return 0;
}
```

**Output**

```
Addition of two given Matrices is : 
2 4 6 
8 10 22 
2 4 6 
Subtraction of two given Matrices is : 
0 0 0 
0 0 -10 
0 0 0 
Multiplication of two given Matrices is : 
12 18 44 
30 45 110 
12 18 44 
```