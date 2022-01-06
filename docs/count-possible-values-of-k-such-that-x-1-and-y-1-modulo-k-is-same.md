# 计算 K 的可能值，使得 X–1 和 Y–1 模 K 相同

> 原文:[https://www . geeksforgeeks . org/count-k 的可能值-so-x-1 和-y-1-模-k-相同/](https://www.geeksforgeeks.org/count-possible-values-of-k-such-that-x-1-and-y-1-modulo-k-is-same/)

给定两个数字 **X** 和 **Y** ，任务是找出满足等式**(X–1)% K =(Y–1)% K**的整数 K 的个数。

**示例:**

> **输入:** X = 2，Y = 6
> **输出:** 3
> **说明:**
> K = {1，2，4}满足给定方程。因此，计数为 3。
> 
> **输入:** X = 4，Y = 9
> T3】输出: 2

**方法:**按照以下步骤解决问题:

*   想法是找到 **X** 和 **Y** 的**绝对差**。
*   找出计算出的绝对差的除数，并打印出所需答案。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count integers K
// satisfying given equation
int condition(int a, int b)
{
    // Calculate the absoluter
    // difference between a and b
    int d = abs(a - b), count = 0;

    // Iterate till sqrt of the difference
    for (int i = 1; i <= sqrt(d); i++) {
        if (d % i == 0) {
            if (d / i == i)
                count += 1;
            else
                count += 2;
        }
    }

    // Return the count
    return count;
}

// Driver Code
int main()
{

    int x = 2, y = 6;
    cout << condition(x, y) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count integers K
// satisfying given equation
static int condition(int a, int b)
{

    // Calculate the absoluter
    // difference between a and b
    int d = Math.abs(a - b), count = 0;

    // Iterate till sqrt of the difference
    for(int i = 1; i <= Math.sqrt(d); i++)
    {
        if (d % i == 0)
        {
            if (d / i == i)
                count += 1;
            else
                count += 2;
        }
    }

    // Return the count
    return count;
}

// Driver Code
public static void main (String[] args)
{
    int x = 2, y = 6;

    System.out.println(condition(x, y));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count integers K
# satisfying given equation
def condition(a, b):

    # Calculate the absoluter
    # difference between a and b
    d = abs(a - b)
    count = 0

    # Iterate till sqrt of the difference
    for i in range(1, d + 1):
        if i * i > d:
            break
        if (d % i == 0):
            if (d // i == i):
                count += 1
            else:
                count += 2

    # Return the count
    return count

# Driver Code
if __name__ == '__main__':

    x = 2
    y = 6

    print(condition(x, y))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to count
// integers K satisfying
// given equation
static int condition(int a,
                     int b)
{   
  // Calculate the absoluter
  // difference between a and b
  int d = Math.Abs(a - b), count = 0;

  // Iterate till sqrt of
  // the difference
  for(int i = 1;
          i <= Math.Sqrt(d); i++)
  {
    if (d % i == 0)
    {
      if (d / i == i)
        count += 1;
      else
        count += 2;
    }
  }

  // Return the count
  return count;
}

// Driver Code
public static void Main(String[] args)
{
  int x = 2, y = 6;
  Console.WriteLine(condition(x, y));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count integers K
// satisfying given equation
function condition(a, b)
{

    // Calculate the absoluter
    // difference between a and b
    let d = Math.abs(a - b), count = 0;

    // Iterate till sqrt of the difference
    for(let i = 1; i <= Math.sqrt(d); i++)
    {
        if (d % i == 0)
        {
            if (d / i == i)
                count += 1;
            else
                count += 2;
        }
    }

    // Return the count
    return count;
}

// Driver Code

  let x = 2, y = 6;

  document.write(condition(x, y));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(√ABS(X–Y))*
***辅助空间:** O(1)*