# 用可被 3 整除的和最大化给定 0、1 和 2s 的组数

> 原文:[https://www . geesforgeks . org/最大化给定 0-1 和-2 的组数，其和可被 3 整除/](https://www.geeksforgeeks.org/maximize-count-of-groups-from-given-0s-1s-and-2s-with-sum-divisible-by-3/)

给定三个整数， **C0，C1 和 C2** 在一个[组](https://www.geeksforgeeks.org/group-in-cpp-stl/)T4 中 0，1 和 2s 的频率。任务是找出**和可被 3** 整除的最大组数，条件是**和(S)** 可被 3 整除，所有组的[并集](https://www.geeksforgeeks.org/union-c/)必须等于 **S**

***例:***

> ***输入*** : C0 = 2，C1 = 4，C2 = 1
> ***输出*** : 4
> ***解释*** :它可以将组 S = {0，0，1，1，1，1，1，2}分成四组{0}、{0}、{1，1，1}、{1，2}。可以证明 4 是最大可能的答案。
> 
> ***输入*** : C0 = 250，C1 = 0，C2 = 0
> ***输出*** : 250

**方法:**这个问题可以使用 [**贪婪算法**](https://www.geeksforgeeks.org/greedy-algorithms/) 来解决。按照下面给出的步骤解决问题。

*   初始化一个变量 **maxAns** ，比如说 0，来存储最大组数。
*   将 **C0 加到 maxAns** 上，因为每个 **{0}** 可以是一个组，这样总和**可以被 3** 整除。
*   初始化一个变量 **k** ，说 **min(C1，C2)** ，加到 maxAns，因为至少可以创建 **k** 、 **{1，2}** 组。
*   将 **abs(C1-C2) /3 加到 maxAns** 上，将剩余的 **1s 或 2s** 贡献出来。
*   返回 **maxAns。**

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

int maxGroup(int c0, int c1, int c2)
{

    // Initializing to store maximum number of groups
    int maxAns = 0;

    // Adding C0
    maxAns += c0;

    // Taking Minimum of c1, c2 as minimum number of
    // pairs must be minimum of c1, c2
    int k = min(c1, c2);
    maxAns += k;

    // If there is any remaining element in c1 or c2
    // then it must be the absolute difference of c1 and
    // c2 and dividing it by 3 to make it one pair
    maxAns += abs(c1 - c2) / 3;

    return maxAns;
}

int main()
{
    int C0 = 2, C1 = 4, C2 = 1;
    cout << maxGroup(C0, C1, C2);
    return 0;
}

// This code is contributed by maddler
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach

import java.io.*;

class GFG {

    // Function to calculate maximum number of groups
    public static int maxGroup(int c0, int c1, int c2)
    {

        // Initializing to store maximum number of groups
        int maxAns = 0;

        // Adding C0
        maxAns += c0;

        // Taking Minimum of c1, c2 as minimum number of
        // pairs must be minimum of c1, c2
        int k = Math.min(c1, c2);
        maxAns += k;

        // If there is any remaining element in c1 or c2
        // then it must be the absolute difference of c1 and
        // c2 and dividing it by 3 to make it one pair
        maxAns += Math.abs(c1 - c2) / 3;

        return maxAns;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Input
        int C0 = 2, C1 = 4, C2 = 1;

        // Function Call
        System.out.println(maxGroup(C0, C1, C2));
    }
}
```

## 蟒蛇 3

```
# python 3 program for above approach
def maxGroup(c0, c1, c2):

    # Initializing to store maximum number of groups
    maxAns = 0

    # Adding C0
    maxAns += c0

    # Taking Minimum of c1, c2 as minimum number of
    # pairs must be minimum of c1, c2
    k = min(c1, c2)
    maxAns += k

    # If there is any remaining element in c1 or c2
    # then it must be the absolute difference of c1 and
    # c2 and dividing it by 3 to make it one pair
    maxAns += abs(c1 - c2) // 3

    return maxAns

  # Driver code
if __name__ == '__main__':
    C0 = 2
    C1 = 4
    C2 = 1
    print(maxGroup(C0, C1, C2))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to calculate maximum number of groups   
public static int maxGroup(int c0, int c1, int c2)
{

    // Initializing to store maximum number
    // of groups
    int maxAns = 0;

    // Adding C0
    maxAns += c0;

    // Taking Minimum of c1, c2 as minimum number
    // of pairs must be minimum of c1, c2
    int k = Math.Min(c1, c2);
    maxAns += k;

    // If there is any remaining element
    // in c1 or c2 then it must be the
    // absolute difference of c1 and c2
    // and dividing it by 3 to make it one pair
    maxAns += Math.Abs(c1 - c2) / 3;

    return maxAns;
}

// Driver Code
static public void Main()
{

    // Given Input
    int C0 = 2, C1 = 4, C2 = 1;

    // Function Call
    Console.WriteLine(maxGroup(C0, C1, C2));
}
}

// This code is contributed by maddler
```

## java 描述语言

```
<script>

       // JavaScript program for the above approach;
       function maxGroup(c0, c1, c2)
       {

           // Initializing to store maximum number of groups
           let maxAns = 0;

           // Adding C0
           maxAns += c0;

           // Taking Minimum of c1, c2 as minimum number of
           // pairs must be minimum of c1, c2
           let k = Math.min(c1, c2);
           maxAns += k;

           // If there is any remaining element in c1 or c2
           // then it must be the absolute difference of c1 and
           // c2 and dividing it by 3 to make it one pair
           maxAns += Math.abs(c1 - c2) / 3;

           return maxAns;
       }

       let C0 = 2, C1 = 4, C2 = 1;
       document.write(maxGroup(C0, C1, C2));

  // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
4
```

***时间复杂度:*** O(1)
***辅助空间:*** O(1)