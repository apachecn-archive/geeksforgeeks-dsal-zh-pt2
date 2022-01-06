# 矩阵中从给定源到目的地的所有唯一路径的计数

> 原文:[https://www . geeksforgeeks . org/矩阵中从给定源到目标的所有唯一路径计数/](https://www.geeksforgeeks.org/count-of-all-unique-paths-from-given-source-to-destination-in-a-matrix/)

给定一个大小为 **n*m** 的 **2D 矩阵**，一个源 **s** 和一个目的地 **d** ，打印从给定的 **s** 到 **d** 的所有**唯一路径**的计数。从每个单元格中，您可以只向右移动**或向下移动**。****

******示例**:****

> ******输入** : arr[][] = { {1，2，3}，{4，5，6} }，s = {0，0}，d = {1，2}
> **输出** : 3
> **解释**:从源到目的地的所有可能路径为:****
> 
> *   ****1 -> 4 -> 5 -> 6****
> *   ****1 -> 2 -> 5 -> 6****
> *   ****1 -> 2 -> 3 -> 6****
> 
> ******输入** : arr[][] = { {1，2}，{3，4} }，s = {0，1}，d = {1，1}
> **输出** : 1****

******逼近**:使用[递归](http://www.geeksforgeeks.org/recursion/)先将**右移**&再将**下移**从矩阵路径中的每个像元开始，从**源**开始**。如果到达**目的地****，**增加****计数可能的**路径的**。**********

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// count of all possible paths
int countPaths(int i, int j, int count,
               int p, int q)
{
    // Destination is reached
    if (i == p || j == q) {
        count++;
        return count;
    }

    // Move right
    count = countPaths(i, j + 1,
                       count, p, q);

    // Move down
    count = countPaths(i + 1, j,
                       count, p, q);
    return count;
}

// Driver program to test above functions
int main()
{
    vector<vector<int> > mat = { { 1, 2, 3 },
                                 { 4, 5, 6 } };
    vector<int> s = { 0, 0 };
    vector<int> d = { 1, 2 };
    cout << countPaths(s[0], s[1], 0,
                       d[0], d[1]);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find the
    // count of all possible paths
    static int countPaths(int i, int j, int count,
            int p, int q) {

        // Destination is reached
        if (i == p || j == q) {
            count++;
            return count;
        }

        // Move right
        count = countPaths(i, j + 1,
                count, p, q);

        // Move down
        count = countPaths(i + 1, j,
                count, p, q);
        return count;
    }

    // Driver program to test above functions
    public static void main(String args[]) {
        int[] s = { 0, 0 };
        int[] d = { 1, 2 };
        System.out.println(countPaths(s[0], s[1], 0, d[0], d[1]));
    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the
# count of all possible paths
def countPaths(i, j, count, p, q):

    # Destination is reached
    if (i == p or j == q):
        count += 1
        return count

    # Move right
    count = countPaths(i, j + 1, count, p, q)

    # Move down
    count = countPaths(i + 1, j, count, p, q)
    return count

# Driver program to test above functions
if __name__ == "__main__":

    mat = [[1, 2, 3],
           [4, 5, 6]]
    s = [0, 0]
    d = [1, 2]
    print(countPaths(s[0], s[1], 0, d[0], d[1]))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach

using System;
class GFG {

    // Function to find the
    // count of all possible paths
    static int countPaths(int i, int j, int count, int p, int q) {

        // Destination is reached
        if (i == p || j == q) {
            count++;
            return count;
        }

        // Move right
        count = countPaths(i, j + 1,
                count, p, q);

        // Move down
        count = countPaths(i + 1, j,
                count, p, q);
        return count;
    }

    // Driver program to test above functions
    public static void Main() {
        int[] s = { 0, 0 };
        int[] d = { 1, 2 };
        Console.Write(countPaths(s[0], s[1], 0, d[0], d[1]));
    }
}

// This code is contributed by gfgking.
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to find the
       // count of all possible paths
       function countPaths(i, j, count,
           p, q)
       {

           // Destination is reached
           if (i == p || j == q) {
               count++;
               return count;
           }

           // Move right
           count = countPaths(i, j + 1,
               count, p, q);

           // Move down
           count = countPaths(i + 1, j,
               count, p, q);
           return count;
       }

       // Driver program to test above functions
       let mat = [[1, 2, 3],
                   [4, 5, 6]];
       let s = [0, 0];
       let d = [1, 2];
       document.write(countPaths(s[0], s[1], 0,
           d[0], d[1]));

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
3
```

***时间复杂度*** : O(n+m)
***辅助空间*** : O(1)