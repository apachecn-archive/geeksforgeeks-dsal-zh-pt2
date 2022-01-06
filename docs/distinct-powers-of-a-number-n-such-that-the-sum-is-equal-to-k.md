# 一个数 N 的不同次方，其和等于 K

> 原文:[https://www . geeksforgeeks . org/distinct-power of-number-n-so-sum 等于-k/](https://www.geeksforgeeks.org/distinct-powers-of-a-number-n-such-that-the-sum-is-equal-to-k/)

给定两个数字 **N** 和 **K** ，任务是打印 **N** 的不同幂，用来得到总和 **K** 。如果不可能，打印 **-1** 。

**示例:**

> **输入:** N = 3，K = 40
> **输出:** 0，1，2，3
> **说明:**
> N 的值为 3。
> 3<sup>0</sup>+3<sup>1</sup>+3<sup>2</sup>+3<sup>3</sup>= 40
> 
> **输入:** N = 4，K = 65
> **输出:** 0，3
> N 的值为 4。
> 4 <sup>0</sup> + 4 <sup>3</sup> = 65
> 
> **输入:** N = 4，K = 18
> **输出:** -1
> **说明:**
> 加 4 的幂不可能得到 18。

**观察:**对于任意一个数 **a** 需要做的一个观察是，如果 a 从 0 到 k-1 的所有乘方最多用一次每个乘方相加，就不可能存在大于 a 的数 <sup>K</sup> 。

**例:**设 a = 3，K = 4。然后:

> 3 <sup>4</sup> = 81。
> 3<sup>0</sup>+3<sup>1</sup>+3<sup>2</sup>+3<sup>3</sup>= 40 小于 81(3 <sup>4</sup> )。

**天真法:**利用上述观察，可以形成天真法。想法是不断从 K 减去不超过 **K** 的 **N** 的最高幂，直到 K 达到 0。如果在任何情况下，K 等于之前已经减去的某个幂，则不可能得到等于 K 的和。因此，使用数组来跟踪已经从 K 减去的幂

下面是上述方法的实现:

## C++

```
// C++ implementation to find distinct
// powers of N that add upto K

#include <bits/stdc++.h>
using namespace std;

// Function to return the highest power
// of N not exceeding K
int highestPower(int n, int k)
{
    int i = 0;
    int a = pow(n, i);

    // Loop to find the highest power
    // less than K
    while (a <= k) {
        i += 1;
        a = pow(n, i);
    }
    return i - 1;
}

// Initializing the PowerArray
// with all 0's.
int b[50] = { 0 };

// Function to print
// the distinct powers of N
// that add upto K
int PowerArray(int n, int k)
{
    while (k) {

        // Getting the highest
        // power of n before k
        int t = highestPower(n, k);

        // To check if the power
        // is being used twice or not
        if (b[t]) {

            // Print -1 if power
            // is being used twice
            cout << -1;
            return 0;
        }

        else
            // If the power is not visited,
            // then mark the power as visited
            b[t] = 1;

        // Decrementing the value of K
        k -= pow(n, t);
    }

    // Printing the powers of N
    // that sum up to K
    for (int i = 0; i < 50; i++) {
        if (b[i]) {
            cout << i << ", ";
        }
    }
}

// Driver code
int main()
{
    int N = 3;
    int K = 40;
    PowerArray(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find distinct
// powers of N that add upto K

class GFG{

// Function to return the highest power
// of N not exceeding K
static int highestPower(int n, int k)
{
    int i = 0;
    int a = (int) Math.pow(n, i);

    // Loop to find the highest power
    // less than K
    while (a <= k) {
        i += 1;
        a = (int) Math.pow(n, i);
    }
    return i - 1;
}

// Initializing the PowerArray
// with all 0's.
static int b[] = new int[50];

// Function to print
// the distinct powers of N
// that add upto K
static int PowerArray(int n, int k)
{
    while (k>0) {

        // Getting the highest
        // power of n before k
        int t = highestPower(n, k);

        // To check if the power
        // is being used twice or not
        if (b[t]>0) {

            // Print -1 if power
            // is being used twice
            System.out.print(-1);
            return 0;
        }

        else
            // If the power is not visited,
            // then mark the power as visited
            b[t] = 1;

        // Decrementing the value of K
        k -= Math.pow(n, t);
    }

    // Printing the powers of N
    // that sum up to K
    for (int i = 0; i < 50; i++) {
        if (b[i] > 0) {
            System.out.print(i+ ", ");
        }
    }
    return 0;
}

// Driver code
public static void main(String[] args)
{
    int N = 3;
    int K = 40;
    PowerArray(N, K);
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation to find distinct
# powers of N that add up to K

from math import pow

# Function to return the highest power
# of N not exceeding K
def highestPower(n,k):
    i = 0
    a = pow(n, i)

    # Loop to find the highest power
    # less than K
    while (a <= k):
        i += 1
        a = pow(n, i)
    return i - 1

# Initializing the PowerArray
# with all 0's.
b = [0 for i in range(50)]

# Function to print
# the distinct powers of N
# that add upto K
def PowerArray(n, k):
    while (k):
        # Getting the highest
        # power of n before k
        t = highestPower(n, k)

        # To check if the power
        # is being used twice or not
        if (b[t]):
            # Print -1 if power
            # is being used twice
            print(-1)
            return 0

        else:
            # If the power is not visited,
            # then mark the power as visited
            b[t] = 1

        # Decrementing the value of K
        k -= pow(n, t)

    # Printing the powers of N
    # that sum up to K
    for i in range(50):
        if (b[i]):
            print(i,end = ', ')

# Driver code
if __name__ == '__main__':
    N = 3
    K = 40
    PowerArray(N, K)

# This code is contributed by Surendra_Gangwar
```

## C#

```

// C# implementation to find distinct
// powers of N that add up to K

using System;

public class GFG{

// Function to return the highest power
// of N not exceeding K
static int highestPower(int n, int k)
{
    int i = 0;
    int a = (int) Math.Pow(n, i);

    // Loop to find the highest power
    // less than K
    while (a <= k) {
        i += 1;
        a = (int) Math.Pow(n, i);
    }
    return i - 1;
}

// Initializing the PowerArray
// with all 0's.
static int []b = new int[50];

// Function to print
// the distinct powers of N
// that add upto K
static int PowerArray(int n, int k)
{
    while (k > 0) {

        // Getting the highest
        // power of n before k
        int t = highestPower(n, k);

        // To check if the power
        // is being used twice or not
        if (b[t] > 0) {

            // Print -1 if power
            // is being used twice
            Console.Write(-1);
            return 0;
        }

        else
            // If the power is not visited,
            // then mark the power as visited
            b[t] = 1;

        // Decrementing the value of K
        k -= (int)Math.Pow(n, t);
    }

    // Printing the powers of N
    // that sum up to K
    for (int i = 0; i < 50; i++) {
        if (b[i] > 0) {
            Console.Write(i+ ", ");
        }
    }
    return 0;
}

// Driver code
public static void Main(String[] args)
{
    int N = 3;
    int K = 40;
    PowerArray(N, K);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation to find distinct
// powers of N that add upto K

// Function to return the highest power
// of N not exceeding K
function highestPower(n, k)
{
    let i = 0;
    let a = Math.pow(n, i);

    // Loop to find the highest power
    // less than K
    while (a <= k) {
        i += 1;
        a = Math.pow(n, i);
    }
    return i - 1;
}

// Initializing the PowerArray
// with all 0's.
let b = Array.from({length: 50}, (_, i) => 0);

// Function to print
// the distinct powers of N
// that add upto K
function PowerArray(n, k)
{
    while (k>0) {

        // Getting the highest
        // power of n before k
        let t = highestPower(n, k);

        // To check if the power
        // is being used twice or not
        if (b[t]>0) {

            // Print -1 if power
            // is being used twice
            document.write(-1);
            return 0;
        }

        else
            // If the power is not visited,
            // then mark the power as visited
            b[t] = 1;

        // Decrementing the value of K
        k -= Math.pow(n, t);
    }

    // Printing the powers of N
    // that sum up to K
    for (let i = 0; i < 50; i++) {
        if (b[i] > 0) {
            document.write(i+ ", ");
        }
    }
    return 0;
}

// Driver Code

    let N = 3;
    let K = 40;
    PowerArray(N, K);

</script>
```

**Output:** 

```
0, 1, 2, 3,
```

***时间复杂度:** O((log N) <sup>2</sup> )*

*   找出功率所花费的时间是 **Log(N)** 。
*   除此之外，另一个对数(N)循环正被用于 **K** 。
*   所以，整体时间复杂度为 **Log(N) <sup>2</sup>**

**辅助空间:** O(50)

**有效方法:**可以做的另一个观察是对于 **K** 为 **N 的**次只能使用一次的幂之和， **K % N** 要么必须为 **1** 要么为 **0** (1 因 N <sup>0</sup> )。所以，( **K % N** )如果出来的不是 0 或者 1，就可以断定不可能得到 **K** 的和。
因此，通过使用上述观察，可以遵循以下步骤来计算答案:

1.  首先，用 0 初始化计数器。
2.  如果 **(K % N) = 0** ，则计数器增加 **1** ，K 更新为 **K/N** 。
3.  如果 **K % N = 1** ，则频率数组 **f【计数】**增加 **1** ，K 更新为**K–1**。
4.  如果在任何一点上，这个 **f【计数】**变成大于 1，那么返回-1(因为同一个幂不能用两次)。

下面是上述方法的实现:

## C++

```
// C++ implementation to find out
// the powers of N that add upto K

#include <bits/stdc++.h>
using namespace std;

// Initializing the PowerArray
// with all 0's
int b[50] = { 0 };

// Function to find the powers of N
// that add up to K
int PowerArray(int n, int k)
{

    // Initializing the counter
    int count = 0;

    // Executing the while
    // loop until K is
    // greater than 0
    while (k) {
        if (k % n == 0) {
            k /= n;
            count++;
        }

        // If K % N == 1,
        // then the power array
        // is incremented by 1
        else if (k % n == 1) {
            k -= 1;
            b[count]++;

            // Checking if any power is
            // occurred more than once
            if (b[count] > 1) {
                cout << -1;
                return 0;
            }
        }

        // For any other value, the sum of
        // powers cannot be added up to K
        else {
            cout << -1;
            return 0;
        }
    }

    // Printing the powers of N
    // that sum up to K
    for (int i = 0; i < 50; i++) {
        if (b[i]) {
            cout << i << ", ";
        }
    }
}

// Driver code
int main()
{
    int N = 3;
    int K = 40;
    PowerArray(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find out
// the powers of N that add upto K
class GFG{

// Initializing the PowerArray
// with all 0's
static int b[] = new int[50];

// Function to find the powers of N
// that add up to K
static int PowerArray(int n, int k)
{

    // Initializing the counter
    int count = 0;

    // Executing the while
    // loop until K is
    // greater than 0
    while (k > 0)
    {
        if (k % n == 0)
        {
            k /= n;
            count++;
        }

        // If K % N == 1,
        // then the power array
        // is incremented by 1
        else if (k % n == 1)
        {
            k -= 1;
            b[count]++;

            // Checking if any power is
            // occurred more than once
            if (b[count] > 1)
            {
                System.out.print(-1);
                return 0;
            }
        }

        // For any other value, the sum of
        // powers cannot be added up to K
        else
        {
            System.out.print(-1);
            return 0;
        }
    }

    // Printing the powers of N
    // that sum up to K
    for(int i = 0; i < 50; i++)
    {
       if (b[i] != 0)
       {
           System.out.print(i + ", ");
       }
    }
    return Integer.MIN_VALUE;
}

// Driver code
public static void main(String[] args)
{
    int N = 3;
    int K = 40;
    PowerArray(N, K);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find out
# the powers of N that add upto K

# Initializing the PowerArray
# with all 0's
b = [0 for i in range(50)]

# Function to find the powers of N
# that add up to K
def PowerArray(n, k):

    # Initializing the counter
    count = 0

    # Executing the while
    # loop until K is
    # greater than 0
    while (k):
        if (k % n == 0):
            k //= n
            count += 1

        # If K % N == 1,
        # then the power array
        # is incremented by 1
        elif (k % n == 1):
            k -= 1
            b[count] += 1

            # Checking if any power is
            # occurred more than once
            if (b[count] > 1):
                print(-1)
                return 0

        # For any other value, the sum of
        # powers cannot be added up to K
        else:
            print(-1)
            return 0

    # Printing the powers of N
    # that sum up to K
    for i in range(50):
        if (b[i]):
            print(i,end = ",")

# Driver code
if __name__ == '__main__':

    N = 3
    K = 40

    PowerArray(N, K)

# This code is contributed by ipg2016107
```

## C#

```
// C# implementation to find out
// the powers of N that add upto K
using System;

class GFG{

// Initializing the PowerArray
// with all 0's
static int []b = new int[50];

// Function to find the powers of N
// that add up to K
static int PowerArray(int n, int k)
{

    // Initializing the counter
    int count = 0;

    // Executing the while loop
    // until K is greater than 0
    while (k > 0)
    {
        if (k % n == 0)
        {
            k /= n;
            count++;
        }

        // If K % N == 1, then
        // the power array is
        // incremented by 1
        else if (k % n == 1)
        {
            k -= 1;
            b[count]++;

            // Checking if any power is
            // occurred more than once
            if (b[count] > 1)
            {
                Console.Write(-1);
                return 0;
            }
        }

        // For any other value, the sum of
        // powers cannot be added up to K
        else
        {
            Console.Write(-1);
            return 0;
        }
    }

    // Printing the powers of N
    // that sum up to K
    for(int i = 0; i < 50; i++)
    {
       if (b[i] != 0)
       {
           Console.Write(i + ", ");
       }
    }
    return int.MinValue;
}

// Driver code
public static void Main(String[] args)
{
    int N = 3;
    int K = 40;

    PowerArray(N, K);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
    // Javascript implementation to find out
    // the powers of N that add upto K

    // Initializing the PowerArray
    // with all 0's
    let b = new Array(50);
    b.fill(0);

    // Function to find the powers of N
    // that add up to K
    function PowerArray(n, k)
    {

        // Initializing the counter
        let count = 0;

        // Executing the while loop
        // until K is greater than 0
        while (k > 0)
        {
            if (k % n == 0)
            {
                k = parseInt(k / n, 10);
                count++;
            }

            // If K % N == 1, then
            // the power array is
            // incremented by 1
            else if (k % n == 1)
            {
                k -= 1;
                b[count]++;

                // Checking if any power is
                // occurred more than once
                if (b[count] > 1)
                {
                    document.write(-1);
                    return 0;
                }
            }

            // For any other value, the sum of
            // powers cannot be added up to K
            else
            {
                document.write(-1);
                return 0;
            }
        }

        // Printing the powers of N
        // that sum up to K
        for(let i = 0; i < 50; i++)
        {
           if (b[i] != 0)
           {
               document.write(i + ", ");
           }
        }
        return Number.MIN_VALUE;
    }

    let N = 3;
    let K = 40;

    PowerArray(N, K);

</script>
```

**Output:** 

```
0, 1, 2, 3,
```

***时间复杂度:**由于每次不查最高功率，所以这个算法的运行时间是 **log(N)** 。*

***辅助空间:**O(50)*T4】