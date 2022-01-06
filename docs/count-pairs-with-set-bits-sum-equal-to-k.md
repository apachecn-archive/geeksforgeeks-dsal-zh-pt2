# 计数设定位总和等于 K 的对

> 原文:[https://www . geesforgeks . org/count-pairs-with-set-bits-sum-equal-to-k/](https://www.geeksforgeeks.org/count-pairs-with-set-bits-sum-equal-to-k/)

给定一个数组**arr【】**和一个整数 **K** ，任务是对设置位之和为 **K**
**的对进行计数。示例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 4
> **输出:** 1
> (3，5)是唯一有效的对，因为整数{1，2，3，4，5}
> 中设置位的计数
> 分别为{1，1，2，1，2}。
> **输入:** arr[] = {5，42，35，22，7}，K = 6
> **输出:** 6

**简单方法:**初始化**计数= 0** 并运行两个嵌套循环，检查所有可能的对，并检查计数位之和是否为 **K** 。如果是，则增加**计数**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of set bits in n
unsigned int countSetBits(int n)
{
    unsigned int count = 0;
    while (n) {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Function to return the count
// of required pairs
int pairs(int arr[], int n, int k)
{

    // To store the count
    int count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Sum of set bits in both the integers
            int sum = countSetBits(arr[i])
                      + countSetBits(arr[j]);

            // If current pair satisfies
            // the given condition
            if (sum == k)
                count++;
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;
    cout << pairs(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count
// of set bits in n
static int countSetBits(int n)
{
    int count = 0;
    while (n > 0)
    {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Function to return the count
// of required pairs
static int pairs(int arr[], int n, int k)
{

    // To store the count
    int count = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {

            // Sum of set bits in both the integers
            int sum = countSetBits(arr[i])
                    + countSetBits(arr[j]);

            // If current pair satisfies
            // the given condition
            if (sum == k)
                count++;
        }
    }
    return count;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = arr.length;
    int k = 4;
    System.out.println(pairs(arr, n, k));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of set bits in n
def countSetBits(n) :

    count = 0;
    while (n) :

        n &= (n - 1);
        count += 1

    return count;

# Function to return the count
# of required pairs
def pairs(arr, n, k) :

    # To store the count
    count = 0;
    for i in range(n) :
        for j in range(i + 1, n) :

            # Sum of set bits in both the integers
            sum = countSetBits(arr[i]) + countSetBits(arr[j]);

            # If current pair satisfies
            # the given condition
            if (sum == k) :
                count += 1 ;

    return count;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4, 5 ];

    n = len(arr);
    k = 4;

    print(pairs(arr, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
public class GFG
{

// Function to return the count
// of set bits in n
static int countSetBits(int n)
{
    int count = 0;
    while (n > 0)
    {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Function to return the count
// of required pairs
static int pairs(int []arr, int n, int k)
{

    // To store the count
    int count = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {

            // Sum of set bits in both the integers
            int sum = countSetBits(arr[i])
                    + countSetBits(arr[j]);

            // If current pair satisfies
            // the given condition
            if (sum == k)
                count++;
        }
    }
    return count;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int n = arr.Length;
    int k = 4;
    Console.WriteLine(pairs(arr, n, k));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to return the count
// of set bits in n
function countSetBits(n)
{
    var count = 0;
    while (n > 0)
    {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Function to return the count
// of required pairs
function pairs(arr , n , k)
{

    // To store the count
    var count = 0;
    for (i = 0; i < n; i++)
    {
        for (j = i + 1; j < n; j++)
        {

            // Sum of set bits in both the integers
            var sum = countSetBits(arr[i])
                    + countSetBits(arr[j]);

            // If current pair satisfies
            // the given condition
            if (sum == k)
                count++;
        }
    }
    return count;
}

// Driver code

var arr = [ 1, 2, 3, 4, 5 ];
var n = arr.length;
var k = 4;
document.write(pairs(arr, n, k));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(n <sup>2</sup> )
**高效方法:**假设每个整数都可以用 32 位来表示，创建一个大小为 32 的频率数组 **freq[]** ，其中 **freq[i]** 将存储设置位等于 **i** 的数字计数。现在在这个频率数组上运行两个嵌套循环，如果 **i + j = K** ，那么对于所有这样的 **i** 和 **j** ，对的计数将是 **freq[i] * freq[j]** 。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 32

// Function to return the count
// of set bits in n
unsigned int countSetBits(int n)
{
    unsigned int count = 0;
    while (n) {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Function to return the count
// of required pairs
int pairs(int arr[], int n, int k)
{

    // To store the count
    int count = 0;

    // Frequency array
    int f[MAX + 1] = { 0 };
    for (int i = 0; i < n; i++)
        f[countSetBits(arr[i])]++;

    for (int i = 0; i <= MAX; i++) {
        for (int j = i; j <= MAX; j++) {

            // If current pair satisfies
            // the given condition
            if (i + j == k) {

                // (arr[i], arr[i]) cannot be a valid pair
                if (i == j)
                    count += ((f[i] * (f[i] - 1)) / 2);
                else
                    count += (f[i] * f[j]);
            }
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;
    cout << pairs(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int MAX = 32;

// Function to return the count
// of set bits in n
static int countSetBits(int n)
{
    int count = 0;
    while (n > 0)
    {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Function to return the count
// of required pairs
static int pairs(int arr[], int n, int k)
{

    // To store the count
    int count = 0;

    // Frequency array
    int []f = new int[MAX + 1];
    for (int i = 0; i < n; i++)
        f[countSetBits(arr[i])]++;

    for (int i = 0; i <= MAX; i++)
    {
        for (int j = i; j <= MAX; j++)
        {

            // If current pair satisfies
            // the given condition
            if (i + j == k)
            {

                // (arr[i], arr[i]) cannot be a valid pair
                if (i == j)
                    count += ((f[i] * (f[i] - 1)) / 2);
                else
                    count += (f[i] * f[j]);
            }
        }
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = arr.length;
    int k = 4;
    System.out.println(pairs(arr, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of the approach
MAX = 32

# Function to return the count
# of set bits in n
def countSetBits(n) :
    count = 0;
    while (n):
        n &= (n - 1);
        count += 1;

    return count;

# Function to return the count
# of required pairs
def pairs(arr, n, k):

    # To store the count
    count = 0;

    # Frequency array
    f = [0 for i in range(MAX + 1)]

    for i in range(n):
        f[countSetBits(arr[i])] += 1;

    for i in range(MAX + 1):
        for j in range(1, MAX + 1):

            # If current pair satisfies
            # the given condition
            if (i + j == k):

                # (arr[i], arr[i]) cannot be a valid pair
                if (i == j):
                    count += ((f[i] * (f[i] - 1)) / 2);
                else:
                    count += (f[i] * f[j]);

    return count;

# Driver code
arr = [ 1, 2, 3, 4, 5 ]
n = len(arr)
k = 4

print (pairs(arr, n, k))

# This code is contributed by CrazyPro
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MAX = 32;

// Function to return the count
// of set bits in n
static int countSetBits(int n)
{
    int count = 0;
    while (n > 0)
    {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Function to return the count
// of required pairs
static int pairs(int []arr, int n, int k)
{

    // To store the count
    int count = 0;

    // Frequency array
    int []f = new int[MAX + 1];
    for (int i = 0; i < n; i++)
        f[countSetBits(arr[i])]++;

    for (int i = 0; i <= MAX; i++)
    {
        for (int j = i; j <= MAX; j++)
        {

            // If current pair satisfies
            // the given condition
            if (i + j == k)
            {

                // (arr[i], arr[i]) cannot be a valid pair
                if (i == j)
                    count += ((f[i] * (f[i] - 1)) / 2);
                else
                    count += (f[i] * f[j]);
            }
        }
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int n = arr.Length;
    int k = 4;
    Console.WriteLine(pairs(arr, n, k));
}
}
/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// javascript implementation of the approach
var MAX = 32;

// Function to return the count
// of set bits in n
function countSetBits(n)
{
    var count = 0;
    while (n > 0)
    {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Function to return the count
// of required pairs
function pairs(arr , n , k)
{

    // To store the count
    var count = 0;

    // Frequency array
    var f = Array.from({length: MAX + 1}, (_, i) => 0);
    for (i = 0; i < n; i++)
        f[countSetBits(arr[i])]++;

    for (i = 0; i <= MAX; i++)
    {
        for (j = i; j <= MAX; j++)
        {

            // If current pair satisfies
            // the given condition
            if (i + j == k)
            {

                // (arr[i], arr[i]) cannot be a valid pair
                if (i == j)
                    count += ((f[i] * (f[i] - 1)) / 2);
                else
                    count += (f[i] * f[j]);
            }
        }
    }
    return count;
}

// Driver code
var arr = [ 1, 2, 3, 4, 5 ];
var n = arr.length;
var k = 4;
document.write(pairs(arr, n, k));

// This code contributed by Princi Singh
</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(n)