# 通过反复将其面积减少一半来最大化纸张数量

> 原文:[https://www . geeksforgeeks . org/通过反复将纸张面积减少一半来最大化纸张数量/](https://www.geeksforgeeks.org/maximize-count-of-sheets-possible-by-repeatedly-reducing-its-area-to-half/)

给定两个整数 **A** 和 **B** ，代表一张纸的长度和宽度，任务是通过反复将面积减少到一半，直到不能被 **2** 整除，来找到能够从其生成的最大**张纸数量**。

**示例:**

> **输入** : A = 5，B = 10
> **输出** : 2
> **说明:**
> 
> *   初始面积= 5 * 10。计数= 0。
> *   面积/ 2 = 5 * 5。计数= 2。
>     
> 
> **输入** : A = 1，B = 8
> **输出** : 8

**方法:**按照以下步骤解决问题:

*   计算提供的初始纸张的总面积。
*   现在，继续用 **2** 分割纸张的面积，直到变成奇数。
*   每次除法后，将计数增加到其值的两倍。
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// maximum number of sheets
// possible by given operations
int maxSheets(int A, int B)
{
    int area = A * B;

    // Initial count of sheets
    int count = 1;

    // Keep dividing the
    // sheets into half
    while (area % 2 == 0) {

        // Reduce area by half
        area /= 2;

        // Increase count by twice
        count *= 2;
    }

    return count;
}

// Driver Code
int main()
{

    int A = 5, B = 10;
    cout << maxSheets(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to calculate the
  // maximum number of sheets
  // possible by given operations
  static int maxSheets(int A, int B)
  {
    int area = A * B;

    // Initial count of sheets
    int count = 1;

    // Keep dividing the
    // sheets into half
    while (area % 2 == 0)
    {

      // Reduce area by half
      area /= 2;

      // Increase count by twice
      count *= 2;
    }
    return count;
  }

  // Driver Code
  public static void main(String args[])
  {
    int A = 5, B = 10;
    System.out.println(maxSheets(A, B));
  }
}

// This code is contributed by jana_sayantan.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate the
# maximum number of sheets
# possible by given operations
def maxSheets( A, B):
    area = A * B

    # Initial count of sheets
    count = 1

    # Keep dividing the
    # sheets into half
    while (area % 2 == 0):

        # Reduce area by half
        area //= 2

        # Increase count by twice
        count *= 2
    return count

# Driver Code
A = 5
B = 10
print(maxSheets(A, B))

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to calculate the
    // maximum number of sheets
    // possible by given operations
    static int maxSheets(int A, int B)
    {
        int area = A * B;

        // Initial count of sheets
        int count = 1;

        // Keep dividing the
        // sheets into half
        while (area % 2 == 0)
        {

            // Reduce area by half
            area /= 2;

            // Increase count by twice
            count *= 2;
        }

        return count;
    }

    // Driver Code
    public static void Main()
    {
        int A = 5, B = 10;
        Console.WriteLine(maxSheets(A, B));
    }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to calculate the
    // maximum number of sheets
    // possible by given operations
    function maxSheets(A, B)
    {
        let area = A * B;

        // Initial count of sheets
        let count = 1;

        // Keep dividing the
        // sheets into half
        while (area % 2 == 0) {

            // Reduce area by half
            area /= 2;

            // Increase count by twice
            count *= 2;
        }

        return count;
    }
    // Driver Code

     let A = 5, B = 10;
    document.write(maxSheets(A, B));

</script>

```

**Output:** 

```
2
```

***时间复杂度:**O(log<sub>2</sub>(A * B))*
***辅助空间:** O(1)*