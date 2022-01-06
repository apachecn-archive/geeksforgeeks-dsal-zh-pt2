# 通过增加/减少元素或保持不变来最大化不同的元素

> 原文:[https://www . geeksforgeeks . org/通过递增-递减元素或保持不变来最大化不同元素/](https://www.geeksforgeeks.org/maximize-distinct-elements-by-incrementing-decrementing-an-element-or-keeping-it-same/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是通过对数组的每个元素执行以下任一给定操作来最大化数组中不同元素的数量:

*   要么将元素增加 1
*   或者将元素减少 1
*   或者保持元素原样。

**注意:**任何元素都不能小于等于 0。

**示例:**

> **输入:** arr = [4，4，5，5，5，6，6]
> **输出:** 5
> **解释:**以三种可能的方式中的任何一种修改数组的每个元素后， **arr[] = [3，4，5，5，5，5，6，7]** 。这里不同的元素是 5。
> 
> **输入:** arr = [1，1，1，8，8，8，9，9]
> **输出:** 6
> **解释:**以三种可能的方式中的任何一种修改数组的每个元素后， **arr[] = [1，1，2，7，8，8，9，10]。**这里明显的元素是 6。

**方法:**思路是先给定数组排序，这样通过与相邻元素的比较，可以很容易地检查出元素，如果它是不同的。

1.  首先，对数组的所有元素进行排序。
2.  初始化变量**计数**和**将**设为 0。(分别存储不同元素和前一个元素的计数。)
3.  之后，使用 **prev** 变量跟踪前一个元素。
4.  迭代排序的数组。
5.  将当前元素的值减少 1，并检查前一个元素是否小于减少的值。如果较小，则增加**计数**，并将当前值分配给**前一个**。
6.  如果当前元素的减少值不大于前一个元素，则保持当前元素不变，并检查前一个元素是否小于当前元素。如果较小，则增加**计数**，并将当前值分配给**前一个**。
7.  如果当前值不大于前一个元素，则将当前值增加 1，并检查前一个元素是否小于增加的当前元素。如果较小，则增加**计数**，并将当前值分配给**前一个**。
8.  如果当前元素的增量值不小于前一个值，则跳过该元素。

下面是上述方法的实现:

## C++

```
// C++ program to Maximize distinct
// elements by incrementing/decrementing
// an element or keeping it same

#include <bits/stdc++.h>
using namespace std;

// Function that Maximize
// the count of distinct
// element
int max_dist_ele(int arr[],
                 int n)
{

    // sort thr array
    sort(arr, arr + n);

    int ans = 0;

    // keeping track of
    // previous change
    int prev = 0;

    for (int i = 0;
         i < n; i++) {

        // check the
        // decremented value
        if (prev < (arr[i] - 1)) {

            ans++;
            prev = arr[i] - 1;
        }

        // check the current
        // value
        else if (prev < (arr[i])) {

            ans++;
            prev = arr[i];
        }

        // check the
        // incremented value
        else if (prev < (arr[i] + 1)) {

            ans++;
            prev = arr[i] + 1;
        }
    }
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 1, 8,
                  8, 8, 9, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << max_dist_ele(arr, n)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Maximize
// the count of distinct element

import java.util.*;

public class GFG {

    // Function that Maximize
    // the count of distinct element
    static int max_dist_ele(
        int arr[], int n)
    {
        // sort thr array
        Arrays.sort(arr);

        int ans = 0;

        // keeping track of
        // previous change
        int prev = 0;

        for (int i = 0;
             i < n; i++) {

            // decrement is possible
            if (prev < (arr[i] - 1)) {

                ans++;
                prev = arr[i] - 1;
            }

            // remain as it is
            else if (prev < (arr[i])) {

                ans++;
                prev = arr[i];
            }
            // increment is possible
            else if (prev < (arr[i] + 1)) {
                ans++;
                prev = arr[i] + 1;
            }
        }

        return ans;
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 1, 1, 1, 8,
                      8, 8, 9, 9 };
        int n = arr.length;

        System.out.println(max_dist_ele(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to Maximize 
# the count of distinct element
def max_dist_ele(arr, n):

    # Sort thr list
    arr.sort()

    ans = 0

    # Keeping track of 
    # previous change
    prev = 0

    for i in range(n):

        # Decrement is possible
        if prev < (arr[i] - 1):
            ans += 1;
            prev = arr[i] - 1

        # Remain as it is
        elif prev < (arr[i]):
            ans += 1
            prev = arr[i]

        # Increment is possible
        elif prev < (arr[i] + 1):
            ans += 1
            prev = arr[i] + 1

    return ans

# Driver Code
arr = [ 1, 1, 1, 8, 8, 8, 9, 9 ]
n = len(arr)

print(max_dist_ele(arr, n))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to maximize the 
// count of distinct element
using System;

class GFG{

// Function that maximize the 
// count of distinct element
static int max_dist_ele(int []arr, int n)
{

    // Sort thr array
    Array.Sort(arr);

    int ans = 0;

    // Keeping track of
    // previous change
    int prev = 0;

    for(int i = 0; i < n; i++)
    {

       // Decrement is possible
       if (prev < (arr[i] - 1))
       {
           ans++;
           prev = arr[i] - 1;
       }

       // Remain as it is
       else if (prev < (arr[i]))
       {
           ans++;
           prev = arr[i];
       }

       // Increment is possible
       else if (prev < (arr[i] + 1))
       {
           ans++;
           prev = arr[i] + 1;
       }
    }
    return ans;
}

// Driver Code
public static void Main(String []args)
{
    int []arr = { 1, 1, 1, 8,
                  8, 8, 9, 9 };
    int n = arr.Length;

    Console.WriteLine(max_dist_ele(arr, n));
}
}

// This code is contributed by Amit Katiyar
```

**Output:**

```
6

```

 ***时间复杂度:** O(N*logN)*