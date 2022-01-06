# 对不可表示为至少两个连续正整数之和的 N 个数进行计数

> 原文:[https://www . geeksforgeeks . org/count-numbers-up-n-无法表示为至少两个连续正整数的和/](https://www.geeksforgeeks.org/count-numbers-up-to-n-that-cannot-be-expressed-as-sum-of-at-least-two-consecutive-positive-integers/)

给定一个正整数 **N** ，任务是从范围**【1，N】**中找出整数的个数，使得[整数不能表示为两个或多个连续正整数](https://www.geeksforgeeks.org/check-number-can-expressed-sum-consecutive-numbers/)的和。

**示例:**

> **输入:** N = 10
> **输出:** 4
> **说明:**不能表示为两个或两个以上连续整数之和的整数为{1，2，4，8}。因此，整数的计数是 4。
> 
> **输入:**N = 100
> T3】输出: 7

**天真法:**给定的问题可以基于这样的观察来解决:[如果一个数是二的幂](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)，那么它就不能表示为连续数的和。按照以下步骤解决给定的问题:

*   初始化一个变量，比如说**计数**，它存储了不能表示为两个或多个连续整数之和的范围**【1，N】**内的数字计数。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，如果[号 **i** 是 2](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) 的完美幂，则**的值递增 **1** 计数**。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number can
// be expressed as a power of 2
bool isPowerof2(unsigned int n)
{
    // f N is power of
    // two
    return ((n & (n - 1)) && n);
}

// Function to count numbers that
// cannot be expressed as sum of
// two or more consecutive +ve integers
void countNum(int N)
{
    // Stores the resultant
    // count of integers
    int count = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // Check if i is power of 2
        bool flag = isPowerof2(i);

        // Increment the count if i
        // is not power of 2
        if (!flag) {
            count++;
        }
    }

    // Print the value of count
    cout << count << "\n";
}

// Driver Code
int main()
{
    int N = 100;
    countNum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if a number can
// be expressed as a power of 2
static boolean isPowerof2(int n)
{

    // f N is power of
    // two
    return ((n & (n - 1)) > 0 && n > 0);
}

// Function to count numbers that
// cannot be expressed as sum of
// two or more consecutive +ve integers
static void countNum(int N)
{

    // Stores the resultant
    // count of integers
    int count = 0;

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

        // Check if i is power of 2
        boolean flag = isPowerof2(i);

        // Increment the count if i
        // is not power of 2
        if (!flag)
        {
            count++;
        }
    }

    // Print the value of count
    System.out.print(count + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int N = 100;

    countNum(N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a number can
# be expressed as a power of 2
def isPowerof2(n):
    # if N is power of
    # two
    return ((n & (n - 1)) and n)

# Function to count numbers that
# cannot be expressed as sum of
# two or more consecutive +ve integers
def countNum(N):
    # Stores the resultant
    # count of integers
    count = 0

    # Iterate over the range [1, N]
    for i in range(1, N + 1):

        # Check if i is power of 2
        flag = isPowerof2(i)

        # Increment the count if i
        # is not power of 2
        if (not flag):
            count += 1

    # Print the value of count
    print(count)

# Driver Code
if __name__ == '__main__':

    N = 100
    countNum(N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if a number can
// be expressed as a power of 2
static bool isPowerof2(int n)
{

    // f N is power of
    // two
    return ((n & (n - 1)) > 0 && n > 0);
}

// Function to count numbers that
// cannot be expressed as sum of
// two or more consecutive +ve integers
static void countNum(int N)
{

    // Stores the resultant
    // count of integers
    int count = 0;

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

        // Check if i is power of 2
        bool flag = isPowerof2(i);

        // Increment the count if i
        // is not power of 2
        if (!flag)
        {
            count++;
        }
    }

    // Print the value of count
    Console.Write(count + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int N = 100;

    countNum(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if a number can
// be expressed as a power of 2
function isPowerof2(n)
{
    // f N is power of
    // two
    return ((n & (n - 1)) && n);
}

// Function to count numbers that
// cannot be expressed as sum of
// two or more consecutive +ve integers
function countNum(N)
{
    // Stores the resultant
    // count of integers
    let count = 0;

    // Iterate over the range [1, N]
    for (let i = 1; i <= N; i++) {

        // Check if i is power of 2
        let flag = isPowerof2(i);

        // Increment the count if i
        // is not power of 2
        if (!flag) {
            count++;
        }
    }

    // Print the value of count
    document.write(count + "\n");
}

// Driver code

    let N = 100;
    countNum(N);

// This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效法:**上述方法也可以基于以下观察进行优化:除了 **2** 之外，不是 **2** 幂的整数可以表示为两个或多个连续正整数的和。因此，**【1，N】**范围内此类整数的计数由 **(log <sub>2</sub> N + 1)给出。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count numbers that
// cannot be expressed as sum of
// two or more consecutive +ve integers
void countNum(int N)
{
    // Stores the count
// of such numbers
    int ans = log2(N) + 1;

    cout << ans << "\n";
}

// Driver Code
int main()
{
    int N = 100;
    countNum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to count numbers that
    // cannot be expressed as sum of
    // two or more consecutive +ve integers
    static void countNum(int N)
    {

        // Stores the count
        // of such numbers
        int ans = (int)(Math.log(N) / Math.log(2)) + 1;

        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 100;
        countNum(N);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import math

# Function to count numbers that
# cannot be expressed as sum of
# two or more consecutive +ve integers
def countNum(N):

    # Stores the count
        # of such numbers
    ans = int(math.log2(N)) + 1

    print(ans)

# Driver Code
if __name__ == "__main__":

    N = 100
    countNum(N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count numbers that
// cannot be expressed as sum of
// two or more consecutive +ve integers
static void countNum(int N)
{

    // Stores the count
    // of such numbers
    int ans = (int)(Math.Log(N) /
                    Math.Log(2)) + 1;

   Console.WriteLine(ans);
}

// Driver Code
static void Main()
{
    int N = 100;
    countNum(N);
}
}

// This code is contributed by SoumikMondal.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count numbers that
// cannot be expressed as sum of
// two or more consecutive +ve integers
function countNum(N)
{

    // Stores the count
    // of such numbers
    var ans = parseInt(Math.log(N) / Math.log(2)) + 1;

    document.write(ans);
}

// Driver Code
var N = 100;
countNum(N);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*