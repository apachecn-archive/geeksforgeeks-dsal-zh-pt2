# 确保每个工人在任何时刻都就座所需的最少椅子数量

> 原文:[https://www . geeksforgeeks . org/最低数量的椅子-需要确保每个员工在任何时候都可以入座/](https://www.geeksforgeeks.org/minimum-number-of-chairs-required-to-ensure-that-every-worker-is-seated-at-any-instant/)

给定一个代表工人进出休息区记录的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** ，其中 **E** 代表进入， **L** 代表离开休息区。每个工人需要一把椅子。任务是找到所需的最低数量的椅子，以便在任何给定的时间都不会缺少椅子。

**示例:**

> **输入:**S = " EELEE "
> T3】输出: 3
> **说明:**
> 第一步:一人进入。因此，目前需要 1 把椅子。
> 第二步:另一个人进入。因此，椅子的数量需要增加到 2 把。
> 第三步:一人离开。因此，不需要增加椅子的数量。
> 第四步:另一个人进入。不过，没有必要增加椅子的数量。
> 第四步:另一个人进入。因此，椅子的数量需要增加到 3 把。
> 因此，至少需要 3 把椅子，这样椅子就不会短缺。
> 
> **输入:**S = " EL "
> T3】输出: 1

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如说**计数**。
*   [使用一个变量迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符，比如说 **i** 。
*   如果 **i** <sup>th</sup> 字符为**【E】**，则增加 **1** 计数，因为需要更多椅子。
*   如果第 i <sup>个</sup>字符是**‘L’**，那么随着其中一把椅子被清空，将计数减少 **1** 。
*   打印任意一步得到的**计数**的最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of chairs required to ensure that
// every worker is seated at any time
int findMinimumChairs(string s)
{
    // Stores the number of
    // chairs required
    int count = 0;

    // Pointer to iterate
    int i = 0;

    // Stores minimum number of
    // chairs required
    int mini = INT_MIN;

    // Iterate over every character
    while (i < s.length()) {

        // If character is 'E'
        if (s[i] == 'E')

            // Increase the count
            count++;

        // Otherwise
        else
            count--;

        // Update maximum value of count
        // obtained at any given time
        mini = max(count, mini);

        i++;
    }

    // Return mini
    return mini;
}

// Driver Code
int main()
{
    // Input

    // Given String
    string s = "EELEE";

    // Function call to find the
    // minimum number of chairs
    cout << findMinimumChairs(s);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG
{

  // Function to find the minimum number
  // of chairs required to ensure that
  // every worker is seated at any time
  static int findMinimumChairs(String s)
  {

    // Stores the number of
    // chairs required
    int count = 0;

    // Pointer to iterate
    int i = 0;

    // Stores minimum number of
    // chairs required
    int mini = Integer.MIN_VALUE;

    // Iterate over every character
    while (i < s.length()) {

      // If character is 'E'
      if (s.charAt(i) == 'E')

        // Increase the count
        count++;

      // Otherwise
      else
        count--;

      // Update maximum value of count
      // obtained at any given time
      mini = Math.max(count, mini);

      i++;
    }

    // Return mini
    return mini;
  }

  // Driver code
  public static void main(String[] args)
  {
    // Input

    // Given String
    String s = "EELEE";

    // Function call to find the
    // minimum number of chairs
    System.out.print(findMinimumChairs(s));
  }
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python 3 implementation of
# the above approach
import sys

# Function to find the minimum number
# of chairs required to ensure that
# every worker is seated at any time
def findMinimumChairs(s):

    # Stores the number of
    # chairs required
    count = 0

    # Pointer to iterate
    i = 0

    # Stores minimum number of
    # chairs required
    mini = -sys.maxsize - 1

    # Iterate over every character
    while (i < len(s)):

        # If character is 'E'
        if (s[i] == 'E'):

            # Increase the count
            count += 1

        # Otherwise
        else:
            count -= 1

        # Update maximum value of count
        # obtained at any given time
        mini = max(count, mini)
        i += 1

    # Return mini
    return mini

# Driver Code
if __name__ == '__main__':

    # Input

    # Given String
    s = "EELEE"

    # Function call to find the
    # minimum number of chairs
    print(findMinimumChairs(s))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{

  // Function to find the minimum number
  // of chairs required to ensure that
  // every worker is seated at any time
  static int findMinimumChairs(string s)
  {

    // Stores the number of
    // chairs required
    int count = 0;

    // Pointer to iterate
    int i = 0;

    // Stores minimum number of
    // chairs required
    int mini = Int32.MinValue;

    // Iterate over every character
    while (i < s.Length) {

      // If character is 'E'
      if (s[i] == 'E')

        // Increase the count
        count++;

      // Otherwise
      else
        count--;

      // Update maximum value of count
      // obtained at any given time
      mini = Math.Max(count, mini);

      i++;
    }

    // Return mini
    return mini;
  }

  // Driver code
  public static void Main()
  {
    // Input

    // Given String
    string s = "EELEE";

    // Function call to find the
    // minimum number of chairs
    Console.WriteLine(findMinimumChairs(s));
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

// Function to find the minimum number
// of chairs required to ensure that
// every worker is seated at any time
function findMinimumChairs(s)
{
    // Stores the number of
    // chairs required
    var count = 0;

    // Pointer to iterate
    var i = 0;

    // Stores minimum number of
    // chairs required
    var mini = -2147483647;

    // Iterate over every character
    while (i < s.length) {

        // If character is 'E'
        if (s[i] == 'E')

            // Increase the count
            count++;

        // Otherwise
        else
            count--;

        // Update maximum value of count
        // obtained at any given time
        mini = Math.max(count, mini);

        i++;
    }

    // Return mini
    return mini;
}

// Driver Code
    // Input

    // Given String
    var s = "EELEE";

    // Function call to find the
    // minimum number of chairs
    document.write(findMinimumChairs(s));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)