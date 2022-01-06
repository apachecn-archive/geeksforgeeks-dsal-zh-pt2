# c++中访问数组元素的不同方式

> 原文:[https://www . geesforgeks . org/不同的访问方式-cpp 中的数组元素/](https://www.geeksforgeeks.org/different-ways-of-accessing-array-elements-in-cpp/)

在本文中，下面将讨论从[数组](https://www.geeksforgeeks.org/array-data-structure/)而不是传统的**arr【I】**表达式中访问元素的两种独特且不同的方式。

*   使用[指针](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/) ***(arr+1)**
*   使用一点操作**我【arr】**来使用数组及其背后的原因。

编译 [C++](https://www.geeksforgeeks.org/c-plus-plus/) 程序时，同时生成[符号表](https://www.geeksforgeeks.org/symbol-table-compiler/)。它的形成是为了存储程序中使用的所有变量的地址的相应值。

让我们考虑一个 C++程序，看看相应程序的符号表是什么:

## C++

```
// C++ program for the above concepts

#include <iostream>
using namespace std;

// Driver Code
int main()
{
    // Assigning a value to a
    int a = 5;

    // Printing the value of a
    cout << "Value of a: " << a;

    // Printing the address of a
    cout << "\nAddress of a: " << &a;

    return 0;
}
```

**Output:** 

```
Value of a: 5
Address of a: 0x7ffe25768fa4
```