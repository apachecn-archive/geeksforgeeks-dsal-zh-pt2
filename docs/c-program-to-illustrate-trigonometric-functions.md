# 图解三角函数的 C++程序

> 原文:[https://www . geesforgeks . org/c-程序-图解-三角函数/](https://www.geeksforgeeks.org/c-program-to-illustrate-trigonometric-functions/)

**[数学. h 标题](https://www.geeksforgeeks.org/c-mathematical-functions/)** 包含执行基本数值运算的方法，如初等指数、对数、平方根和三角函数。为了使用这些功能，您需要包含头文件**数学. h** 。
注意:所有的函数都是以弧度而不是度数输入的

下面是可以从 math.h 标题中使用的各种三角函数:

1.  **sin**: This function takes angle (in **radians**) as an argument and returns its sine value that could be verified using a sine curve.

    **示例:**

    ```
    // C++ program to illustrate
    // sin trigonometric function

    #include <iostream>
    #include <math.h>
    using namespace std;

    int main()
    {
        double x = 2.3;
        cout << "Sine value of x = 2.3: "
             << sin(x) << endl;

        return 0;
    }
    ```

    **Output:**

    ```
    Sine value of x = 2.3: 0.745705

    ```