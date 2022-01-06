# 在一行中制作给定的二进制数组，大小为 2 到全 0

> 原文:[https://www . geeksforgeeks . org/make-给定二进制数组大小-单行二到全 0/](https://www.geeksforgeeks.org/make-given-binary-array-of-size-two-to-all-0s-in-a-single-line/)

给定大小为 2 的二进制数组**arr【N】**(其中 **N = 2** )至少有一个元素为零。任务是编写一个单行函数，将数组的两个元素都设置为零。编写函数有一个限制。不能使用三元运算符和元素的直接赋值。

> 根据问题约束，只有三种阵列元素组合是可能的:
> 
> 1.  **arr[0] = 1 和 arr[1] = 0**
> 2.  **arr[0] = 0 和 arr[1] = 1**
> 3.  **arr[0] = 0 和 arr[1] = 0**

本文讨论以下方法:

1.  **仅使用赋值运算符。**
2.  **使用赋值运算符两次。**
3.  **否定(！)运算符(逻辑非)。**

让我们开始详细讨论这些方法。

**1。仅使用赋值运算符:**

赋值操作符可用于将给定二进制数组的两个元素都设置为 0，但在这种方法中，不直接使用索引。

**进场:**

有三种方法可以实现这一点:

> **1。arr[arr[1]] = arr[arr[0]]**
> 如果 arr={0，1}，那么 arr[0]将被分配给 arr[1]。
> 如果 arr={1，0}，那么 arr[1]将被分配给 arr[0]。
> 
> **2。arr[arr[1]] = 0**
> 如果 arr[1]=0，那么 arr[0]将是 1，所以 arr[arr[1]]将使 arr[0]=0。
> 如果 arr[1]=1，那么 arr[1]将为 1，所以 arrT5【arr[1]】将使 arr[1]=0。
> 
> **3。arr[1–arr[0]]= arr[1–arr[1]]**
> 如果 arr[1]=0 且 arr[0]=1，则 1-arr[1]将为 1，因此 arr[1]将被分配给 arr[0]。
> 如果 arr[1]=1 且 arr[0]=0，那么 1-arr[1]将为 0，因此 arr[0]将被分配给 arr[1]。

下面是实现该方法的 C++代码:

## C++

```
// C++ program to set both elements
// to 0 in binary array[2].
#include <iostream>
using namespace std;

void MakeBothZeros(int arr[])
{
    arr[arr[1]] = arr[arr[0]];

    // Two other approaches to solve
    // the problem
    // arr[arr[1]] = 0;
    // arr[1 - arr[0]] = arr[1 - arr[1]];
}

// Driver code
int main()
{
    int First_Arr[] = {0, 1};
    MakeBothZeros(First_Arr);
    cout << First_Arr[0] << " " <<
            First_Arr[1] << endl;

    int Second_Arr[] = {1, 0};
    MakeBothZeros(Second_Arr);
    cout << Second_Arr[0] << " " <<
            Second_Arr[1] << endl;

    int Thrd_Arr[] = {0, 0};
    MakeBothZeros(Thrd_Arr);
    cout << Thrd_Arr[0] << " " <<
            Thrd_Arr[1] << endl;

    return 0;
}
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      function MakeBothZeros(arr) {
          arr[arr[1]] = arr[arr[0]];

          // Two other approaches to solve
          // the problem
          // arr[arr[1]] = 0;
          // arr[1 - arr[0]] = arr[1 - arr[1]];
      }

      // Driver code

      let First_Arr = [0, 1];
      MakeBothZeros(First_Arr);
      document.write(First_Arr[0] + " " +
          First_Arr[1] + "<br>");

      let Second_Arr = [1, 0];
      MakeBothZeros(Second_Arr);
      document.write(Second_Arr[0] + " " +
          Second_Arr[1] + '<br>');

      let Thrd_Arr = [0, 0];
      MakeBothZeros(Thrd_Arr);
      document.write(Thrd_Arr[0] + " " +
          Thrd_Arr[1] + '<br>');

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
0 0
0 0
0 0
```

**2。使用赋值运算符两次:**

如约束下所列，不允许直接分配。因此，arr[0]=0 和 arr[1]=0 不是有效的语句。赋值运算符将被使用两次来将两个元素都设置为零。

**进场:**

有三种方法可以实现这一点:

> **1。arr[0]= arr[1]= arr[0]&arr[1]**
> 如果任一元素为 1。
> 1 和 0 的“与”总是 0。所以，两者都取值 0。
> 
> **2。arr[0] = arr[1] -= arr[1]**
> 如果 arr[1]=1，那么 arr[1]得到 1-1=0，那么两者都变成 0。
> 
> **3。arr[1] = arr[0] -= arr[0]**
> 如果 arr[0]=1，那么 arr[0]得到 1-1=0。
> 否则 arr[0]= 0-0 = 0。所以，两者都变成了 0。

下面是实现该方法的 C++程序:

## C++

```
// C++ program to set both elements
// to 0 in binary array[2].
#include <iostream>
using namespace std;

void MakeBothZeros(int arr[])
{
    arr[0] = arr[1] = arr[0] & arr[1];

    // Two other approaches to solve
    // the problem
    // arr[0] = arr[1] -= arr[1];
    // arr[1] = arr[0] -= arr[0];
}

// Driver code
int main()
{
    int First_Arr[] = {0, 1};
    MakeBothZeros(First_Arr);
    cout << First_Arr[0] << " " <<
            First_Arr[1] << endl;

    int Second_Arr[] = {1, 0};
    MakeBothZeros(Second_Arr);
    cout << Second_Arr[0] << " " <<
            Second_Arr[1] << endl;

    int Thrd_Arr[] = {0, 0};
    MakeBothZeros(Thrd_Arr);
    cout << Thrd_Arr[0] << " " <<
            Thrd_Arr[1] << endl;

    return 0;
}
```

**Output**

```
0 0
0 0
0 0
```

**注意:**
时间复杂度为 O(1)，因为只使用了一个语句。

**3。通过使用否定(！)运算符(逻辑非):**

在这种方法中，赋值运算符与否定运算符一起使用，使给定数组的两个元素在单行代码中均为 0。

**进场:**

有三种方法可以做到这一点:

> **1。arr[!arr[0]] = arr[arr[0]]**
> 如果 arr={0，1}，则索引 1 被赋予索引 0 值。
> 如果 arr={1，0}，则索引 0 被赋予索引 1 的值。
> 
> **2。arr[arr[1]] = arr[！arr[1]]**
> 如果 arr={0，1}，则索引 0 的值被分配给索引 1。
> 如果 arr={1，0}，则索引 1 的值被分配给索引 0。
> 
> **3。arr[!arr[0]] = arr[！arr[1]]**
> 如果 arr={0，1}，因为 1 是索引 1 的值，所以索引 0 的值再次为 0，
> 将被赋给索引 1，使数组充满零。
> 如果 arr={1，0}，则索引 1 的值被分配给索引 0。

下面是实现该方法的 C++程序:

## C++

```
// C++ program to set both elements
// to 0 in binary array[2].
#include <iostream>
using namespace std;

void MakeBothZeros(int arr[])
{
    arr[!arr[0]] = arr[arr[0]];

    // Two other approaches to solve
    // the problem
    // arr[arr[1]] = arr[!arr[1]]
    // arr[!arr[0]] = arr[!arr[1]]
}

// Driver code
int main()
{
    int First_Arr[] = {0, 1};
    MakeBothZeros(First_Arr);
    cout << First_Arr[0] << " " <<
            First_Arr[1] << endl;

    int Second_Arr[] = {1, 0};
    MakeBothZeros(Second_Arr);
    cout << Second_Arr[0] << " " <<
            Second_Arr[1] << endl;

    int Thrd_Arr[] = {0, 0};
    MakeBothZeros(Thrd_Arr);
    cout << Thrd_Arr[0] << " " <<
            Thrd_Arr[1] << endl;

    return 0;
}
```

**Output**

```
0 0
0 0
0 0
```