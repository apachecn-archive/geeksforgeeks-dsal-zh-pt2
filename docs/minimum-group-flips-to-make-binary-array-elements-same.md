# 最小组翻转使二进制数组元素相同

> 原文:[https://www . geesforgeks . org/minimum-group-flips-to-make-binary-array-elements-same/](https://www.geeksforgeeks.org/minimum-group-flips-to-make-binary-array-elements-same/)

给定一个二进制数组，我们需要将这个数组转换为包含全 1 或全 0 的数组。我们需要使用最小数量的组翻转来完成。

示例:

> **输入** : arr[] = {1，1，0，0，0，1}
> 输出:从 2 到 4
> **解释**:我们有两个选择，我们做全 0 或者做全 1。我们需要做两个组翻转来使所有元素为 0，一个组翻转来使所有元素为 1。因为制作所有元素 1 需要最少的组翻转，所以我们这样做。
> **输入** : arr[] = {1，0，0，0，1，0，0，1，1}
> **输出** :
> 从 1 到 3
> 从 5 到 6
> 从 8 到 8
> **输入** : arr[] = {0，0，0 }
> T21】输出 :
> **解释**:输出为空 1}
> **输出** :
> **解释**:输出为空，我们不需要做任何改动
> **输入** : arr[] = {0，1}
> **输出** :
> 从 0 到 0
> **或者**
> 从 1 到 1
> **解释**:这里的空翻次数是一样的要么我们把所有元素都做成 1 要么

一个**天真的解决方案**是遍历数组做两次遍历。我们首先遍历，找出 0 的组数和 1 的组数。我们找到这两者的最小值。然后我们遍历数组，如果 1 的组较少，就翻转 1。否则，我们翻转 0。

**数组一次遍历怎么做？**

一个**有效的解决方案**基于以下事实:

*   组只有两种类型(0 组和 1 组)
*   两组的计数要么相同，要么计数之差最多为 1。例如，在{1，1，0，1，0，0}中，有两组 0 和两组 1。例如，{1，1，0，0，0，1，0，0，1，1}组的计数比 0 的计数多一个。

基于以上事实，我们可以得出结论，如果我们总是翻转第二组和与第二组相同类型的其他组，我们总是会得到正确的答案。在第一种情况下，当组数相同时，我们翻转哪个组类型并不重要，因为两者都会得到正确的答案。在第二种情况下，当有一个额外的时，通过忽略第一组并从第二组开始，我们将这种情况转换为第一种情况(对于从第二组开始的子阵列)，并得到正确的答案。

## C++

```
// C++ program to find the minimum
// group flips in a binary array
#include <iostream>
using namespace std;

void printGroups(bool arr[], int n) {

  // Traverse through all array elements
  // starting from the second element
  for (int i = 1; i < n; i++) {

    // If current element is not same
    // as previous
    if (arr[i] != arr[i - 1]) {

      // If it is same as first element
      // then it is starting of the interval
      // to be flipped.
      if (arr[i] != arr[0])
        cout << "From " << i << " to ";

      // If it is not same as previous
      // and same as first element, then
      // previous element is end of interval
      else
        cout << (i - 1) << endl;
    }
  }

  // Explicitly handling the end of
  // last interval
  if (arr[n - 1] != arr[0])
    cout << (n - 1) << endl;
}

int main() {
  bool arr[] = {0, 1, 1, 0, 0, 0, 1, 1};
  int n = sizeof(arr) / sizeof(arr[0]);
  printGroups(arr, n);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// group flips in a binary array
import java.io.*;
import java.util.*;

class GFG {

static void printGroups(int arr[], int n)
{

    // Traverse through all array elements
    // starting from the second element
    for(int i = 1; i < n; i++)
    {

       // If current element is not same
       // as previous
       if (arr[i] != arr[i - 1])
       {

           // If it is same as first element
           // then it is starting of the interval
           // to be flipped.
           if (arr[i] != arr[0])
               System.out.print("From " + i + " to ");

           // If it is not same as previous
           // and same as first element, then
           // previous element is end of interval
           else
               System.out.println(i - 1);
       }
    }

    // Explicitly handling the end of
    // last interval
    if (arr[n - 1] != arr[0])
        System.out.println(n - 1);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {0, 1, 1, 0, 0, 0, 1, 1};
    int n = arr.length;

    printGroups(arr, n);
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# group flips in a binary array

def printGroups(arr, n):

    # Traverse through all array elements
    # starting from the second element
    for i in range(1, n):

        # If current element is not same
        # as previous
        if (arr[i] != arr[i - 1]):

            # If it is same as first element
            # then it is starting of the interval
            # to be flipped.
            if (arr[i] != arr[0]):
                print("From", i, "to ", end = "")

            # If it is not same as previous
            # and same as the first element, then
            # previous element is end of interval
            else:
                print(i - 1)

    # Explicitly handling the end of
    # last interval
    if (arr[n - 1] != arr[0]):
        print(n - 1)

# Driver Code
if __name__ == '__main__':

    arr = [ 0, 1, 1, 0, 0, 0, 1, 1 ]
    n = len(arr)

    printGroups(arr, n)

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program to find the minimum
// group flips in a binary array
using System;

class GFG{

static void printGroups(int []arr, int n)
{

    // Traverse through all array elements
    // starting from the second element
    for(int i = 1; i < n; i++)
    {

       // If current element is not same
       // as previous
       if (arr[i] != arr[i - 1])
       {

           // If it is same as first element
           // then it is starting of the interval
           // to be flipped.
           if (arr[i] != arr[0])
               Console.Write("From " + i + " to ");

           // If it is not same as previous
           // and same as first element, then
           // previous element is end of interval
           else
               Console.WriteLine(i - 1);
       }
    }

    // Explicitly handling the end
    // of last interval
    if (arr[n - 1] != arr[0])
        Console.WriteLine(n - 1);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 0, 1, 1, 0, 0, 0, 1, 1 };
    int n = arr.Length;

    printGroups(arr, n);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript program to find the minimum
// group flips in a binary array

function printGroups(arr, n) {

  // Traverse through all array elements
  // starting from the second element
  for (var i = 1; i < n; i++) {

    // If current element is not same
    // as previous
    if (arr[i] != arr[i - 1]) {

      // If it is same as first element
      // then it is starting of the interval
      // to be flipped.
      if (arr[i] != arr[0])
        document.write( "From " + i + " to ");

      // If it is not same as previous
      // and same as first element, then
      // previous element is end of interval
      else
        document.write(i - 1 + "<br>");
    }
  }

  // Explicitly handling the end of
  // last interval
  if (arr[n - 1] != arr[0])
    document.write(n - 1 + "<br>");
}

var arr = [0, 1, 1, 0, 0, 0, 1, 1];
var n = arr.length;
printGroups(arr, n);

</script>
```

**Output**

```
From 1 to 2
From 6 to 7
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)