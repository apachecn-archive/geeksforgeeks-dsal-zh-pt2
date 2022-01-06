# 最小化圆形阵列中相邻元素的最大绝对差

> 原文:[https://www . geeksforgeeks . org/最小化圆形数组中相邻元素的最大绝对差/](https://www.geeksforgeeks.org/minimize-the-maximum-absolute-difference-of-adjacent-elements-in-a-circular-array/)

给定一个由 **N** 个整数组成的圆形数组 **arr** ，任务是在不移除任何元素的情况下，最小化数组中相邻元素的最大绝对差。

**示例:**

> **输入:** arr[] = {1，3，10，2，0，9，6}
> **输出:** {0，2，6，10，9，3，1}
> **说明:**在上例中，相邻元素之间的最大差值为 6，介于 9 和 3 之间。其他订单无法进一步减少。
> 
> **输入:** arr[] = {1，2，3，4，5，6}
> **输出:** {1，3，5，6，4，2}
> **示例:**最大差值为(1，3)和(3，5)与(6，4)和(4，2)之间的 2。

**逼近** :
为了解决这个问题，仅仅显示排序后的数组会导致不正确的解决方案，因为它被视为圆形数组。排序后，最后一个和第一个索引元素分别是数组中最高和最低的元素。因此，相邻元件之间的最大差异可以进一步最小化。因此，在排序之后，我们需要对排序后的数组重新排序，使得数组中的偶数索引元素位于奇数索引元素之前，并以相反的顺序排列奇数索引元素。

> **说明:**对于给定的数组 arr[] = {1，3，10，2，0，9，6}，排序后的数组将是{0，1，2，3，6，9，10}。圆形数组中相邻元素之间的最大差值为**| 10–0 | = 10**。基于上述方法对数组重新排序后，我们得到的数组是{0，2，6，10，9，3，1}。因此，最大差异现在最小化至**| 9–3 | = 6**。

下面的代码是上述方法的实现:

## C++

```
// C++ Program to minimize the
// maximum absolute difference
// between adjacent elements
// of the circular array

#include <bits/stdc++.h>
using namespace std;

#define ll long long

// Function to print the reordered array
// which minimizes thee maximum absolute
// difference of adjacent elements
void solve(vector<int>& arr, int N)
{
    // Sort the given array
    sort(arr.begin(), arr.end());
    // Reorder the array
    int fl = 1,k=0;
    for(int i=0;i<=N/2;i++)
    {
        if((i%2 && fl) || !fl)
        {
            int x = arr[i];
            arr.erase(arr.begin() + i);
            arr.insert(arr.begin() + N - 1 - k, x);
            k++;
            fl = 0;
        }
    }
    // Print the new ordering
    for (int i : arr)
        cout << i << " ";
}

// Driver code
int main()
{
    int N = 7;
    vector<int> arr = {1, 3, 10, 2, 0, 9, 6};
    solve(arr, N);

    return 0;
}

// this code is contributed by divyanshu gupta
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to minimize the
// maximum absolute difference
// between adjacent elements
// of the circular array
import java.util.*;

class GFG{

// Function to print the reordered array
// which minimizes thee maximum absolute
// difference of adjacent elements
static void solve(Vector<Integer> arr, int N)
{

    // Sort the given array
    Collections.sort(arr);

    // Reorder the array
    int fl = 1, k = 0;

    for(int i = 0; i <= N / 2; i++)
    {
        if ((i % 2 != 0 && fl != 0) || fl == 0)
        {
            int x = arr.get(i);
            arr.remove(i);
            arr.add( N - 1 - k, x);
            k++;
            fl = 0;
        }
    }

    // Print the new ordering
    for(int i : arr)
        System.out.print(i + " ");
}

// Driver code
public static void main(String[] args)
{
    int N = 7;
    Vector<Integer> arr = new Vector<>();

    arr.add(1);
    arr.add(3);
    arr.add(10);
    arr.add(2);
    arr.add(0);
    arr.add(9);
    arr.add(6);

    solve(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 Program to minimize the
# maximum absolute difference
# between adjacent elements
# of the circular array

# Function to print the reordered array
# which minimizes thee maximum absolute
# difference of adjacent elements
def solve(arr, N):

    # Sort the given array
    arr.sort(reverse = False)

    # Reorder the array
    fl = 1
    k=0
    for i in range(N // 2 + 1):
        if((i % 2 and fl) or fl == 0):
            x = arr[i]
            arr.remove(arr[i])
            arr.insert(N - 1 - k, x)
            k += 1
            fl = 0

    # Print the new ordering
    for i in arr:
        print(i, end = " ")

# Driver code
if __name__ == '__main__':

    N = 7

    arr = [ 1, 3, 10, 2, 0, 9, 6 ]
    solve(arr, N)

# This code is contributed by Samarth
```

## C#

```
// C# program to minimize the
// maximum absolute difference
// between adjacent elements
// of the circular array
using System;
using System.Collections.Generic;
class GFG{

// Function to print the
// reordered array which
// minimizes thee maximum
// absolute difference of
// adjacent elements
static void solve(List<int> arr,
                  int N)
{   
  // Sort the given array
  arr.Sort();

  // Reorder the array
  int fl = 1, k = 0;

  for(int i = 0; i <= N / 2; i++)
  {
    if ((i % 2 != 0 &&
         fl != 0) || fl == 0)
    {
      int x = arr[i];
      arr.RemoveAt(i);
      arr.Insert(N - 1 - k, x);
      k++;
      fl = 0;
    }
  }

  // Print the new ordering
  foreach(int i in arr)
    Console.Write(i + " ");
}

// Driver code
public static void Main(String[] args)
{
  int N = 7;
  List<int> arr = new List<int>();

  arr.Add(1);
  arr.Add(3);
  arr.Add(10);
  arr.Add(2);
  arr.Add(0);
  arr.Add(9);
  arr.Add(6);

  solve(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
0 2 6 10 9 3 1
```