# 为 X 选择的值的计数，使得 N 在给定操作后减少到 0

> 原文:[https://www . geeksforgeeks . org/为 x-so-n 选择的值的计数在给定操作后减少到 0/](https://www.geeksforgeeks.org/count-of-values-chosen-for-x-such-that-n-is-reduced-to-0-after-given-operations/)

给定一个正整数 **N** ，任务是找到整数 **X** 的个数，以便在执行以下操作序列后将 **N** 的值减少到 **0** 。

*   从 **N** 中减去 **X** 的值。
*   如果 X 是一个一位数的整数，则停止应用操作。
*   将 **X** 的值更新为 **X** 的位数之和。

**示例:**

> ***输入:**N =**T5】9940
> ***输出:** 1*
> ***说明:***
> 考虑到 X 的值为 9910，N 的值可以简化为 0 为:***
> 
> 1.  ****操作 1:** 将 N 更新为 N–X，N = 9939–9910 = 30，将 X 更新为 X 的位数之和，X = 9 + 9 + 1 + 0 = 19。**
> 2.  ****操作 2:** 将 N 更新为 N–X，N = 30–19 = 11，将 X 更新为 X 的位数之和，X = 9 + 1 = 10。**
> 3.  ****操作 3:** 将 N 更新为 N–X，N = 11–10 = 1，将 X 更新为 X 的位数之和，X = 1 + 0 = 1。**
> 4.  ****操作 4:** 将 N 更新为 N–X，N = 1–1 = 0，停止应用操作。**
> 
> **因此，X 只有一个值为 1。**
> 
>  ****输入:**N = 9939
> T3】输出: 3**

****方法:**给定的问题可以使用 [**贪婪方法**](https://www.geeksforgeeks.org/greedy-algorithms/) 来解决，该方法基于以下观察:**

*   **可以观察到，选择 **X** 大于 **N** 的值并不会将 **N** 降低到 **0** 。**
*   **可以肯定的说，如果 **N** 中的位数是 **K** ，那么 **X** 的值没有一个小于**(N–10 * K *(K+1)/2)**，可以将 **N** 转换为 **0** 。**

**从上面的观察来看，想法是迭代范围**[N–10 * K *(K+1)/2，N]** ，并在执行给定操作后，计算该范围内能够将 **N** 转换为 **0** 的那些值。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the value of X
// reduces N to 0 or not
bool check(int x, int N)
{

    while (1) {

       // Update the value of N as N-x
        N -= x;

      // Check if x is a single digit integer
        if (x < 10)
            break;

        int temp2 = 0;
        while (x) {
            temp2 *= 10;
            temp2 += (x % 10);
            x /= 10;
        }
        x = temp2;
    }
    if ((x < 10) && (N == 0)) {
        return 1;
    }
    return 0;
}

// Function to find the number of values
// X such that N can be reduced to 0
// after performing the given operations
int countNoOfsuchX(int N)
{

  // Number of digits in N
    int k = ceil(log10(N));

    // Stores the count of value of X
    int count = 1;

    // Iterate over all possible value
    // of X
    for (int x =( N - (k * (k + 1) * 5)); x < N; x++) {
      // Check if x follow the conditions
        if (check(x, N)) {
            count += 1;
        }
    }

  // Return total count
    return count;
}

// Driver code
int main()
{
    int N = 9399;
    cout << countNoOfsuchX(N);
    return 0;
}

// This code is contributed by maddler.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG {

// Function to check if the value of X
// reduces N to 0 or not
static boolean check(int x, int N)
{

    while (true) {

       // Update the value of N as N-x
        N -= x;

      // Check if x is a single digit integer
        if (x < 10)
            break;

        int temp2 = 0;
        while (x>0) {
           // temp2 *= 10;
            temp2 += (x % 10);
            x = (int)x/10;
        }
        x = temp2;
    }
    if ((x < 10) && (N == 0)) {
        return true;
    }
    return false;
}

// Function to find the number of values
// X such that N can be reduced to 0
// after performing the given operations
static int countNoOfsuchX(int N)
{

  // Number of digits in N
    int k = (int)(Math.log10(N))+1;

    // Stores the count of value of X
    int count = 1;

    // Iterate over all possible value
    // of X
    for (int x =( N - (k * (k + 1) * 5)); x <= N; x++) {

      // Check if x follow the conditions
        if (check(x, N)) {
            count += 1;
        }
    }

  // Return total count
    return count;
}

    // Driver Code
    public static void main(String[] args)
    {
         int N = 9399;
        System.out.println(countNoOfsuchX(N));
    }
}

// This code is contributed by sanjoy_2.
```

## **蟒蛇 3**

```
# Python program for the above approach

# Function to check if the value of X
# reduces N to 0 or not
def check(x, N):

    while True:

        # Update the value of N as N-x
        N -= x

        # Check if x is a single digit integer
        if len(str(x)) == 1:
            break

        # Update x as sum digit of x
        x = sum(list(map(int, str(x))))

    if len(str(x)) == 1 and N == 0:

        return 1

    return 0

# Function to find the number of values
# X such that N can be reduced to 0
# after performing the given operations
def countNoOfsuchX(N):

    # Number of digits in N
    k = len(str(N))

    # Stores the count of value of X
    count = 0

    # Iterate over all possible value
    # of X
    for x in range(N - k*(k + 1)*5, N + 1):
        # Check if x follow the conditions
        if check(x, N):
            count += 1

    # Return the total count
    return count

# Driver Code
N = 9939
print(countNoOfsuchX(N))
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if the value of X
// reduces N to 0 or not
static bool check(int x, int N)
{

    while (true) {

       // Update the value of N as N-x
        N -= x;

      // Check if x is a single digit integer
        if (x < 10)
            break;

        int temp2 = 0;
        while (x>0) {
           // temp2 *= 10;
            temp2 += (x % 10);
            x = (int)x/10;
        }
        x = temp2;
    }
    if ((x < 10) && (N == 0)) {
        return true;
    }
    return false;
}

// Function to find the number of values
// X such that N can be reduced to 0
// after performing the given operations
static int countNoOfsuchX(int N)
{

  // Number of digits in N
    int k = (int)(Math.Log10(N))+1;

    // Stores the count of value of X
    int count = 1;

    // Iterate over all possible value
    // of X
    for (int x =( N - (k * (k + 1) * 5)); x <= N; x++) {

      // Check if x follow the conditions
        if (check(x, N)) {
            count += 1;
        }
    }

  // Return total count
    return count;
}

// Driver code
public static void Main()
{
    int N = 9399;
    Console.Write(countNoOfsuchX(N));
}
}

// This code is contributed by ipg2016107.
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to check if the value of X
// reduces N to 0 or not
function check(x, N)
{

    while (true) {

       // Update the value of N as N-x
        N -= x;

      // Check if x is a single digit leteger
        if (x < 10)
            break;

        let temp2 = 0;
        while (x>0) {
           // temp2 *= 10;
            temp2 += (x % 10);
            x = Math.floor(x / 10);
        }
        x = temp2;
    }
    if ((x < 10) && (N == 0)) {
        return true;
    }
    return false;
}

// Function to find the number of values
// X such that N can be reduced to 0
// after performing the given operations
function countNoOfsuchX(N)
{

  // Number of digits in N
    let k = Math.floor(Math.log10(N)) + 1;

    // Stores the count of value of X
    let count = 1;

    // Iterate over all possible value
    // of X
    for (let x =( N - (k * (k + 1) * 5)); x <= N; x++) {

      // Check if x follow the conditions
        if (check(x, N)) {
            count += 1;
        }
    }

  // Return total count
    return count;
}

// Driver Code
     let N = 9399;
     document.write(countNoOfsuchX(N));

// This code is contributed by avijitmondal1998.
</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:** O(log N)*
***辅助空间:** O(log N)***