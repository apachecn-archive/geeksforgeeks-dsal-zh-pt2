# 先找到包含奇数元素的数组中的第 k 个元素，然后找到偶数元素

> 原文:[https://www . geeksforgeeks . org/find-kth-数组中的元素-包含奇数元素-先有后有偶数元素/](https://www.geeksforgeeks.org/find-kth-element-in-an-array-containing-odd-elements-first-and-then-even-elements/)

给定整数数组的长度 **N** 和整数 **K** 。任务是修改数组，使数组首先包含从 1 到 **N** 的所有奇数，然后包含从 1 到 **N** 的所有偶数，然后打印修改后的数组中的 **K <sup>th</sup>** 元素。
**示例:**

> **输入:** N = 8，K = 5
> **输出:** 2
> 数组将为{1，3，5，7，2，4，6，8}
> ，第五个元素为 2。
> **输入:** N = 7，K = 2
> **输出:** 3

**天真的做法:**简单的做法是先存储奇数，一个一个直到 **N** ，然后再一个一个的存储偶数直到 **N** ，然后打印第 kth 个元素。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the kth element
// in the modified array
int getNumber(int n, int k)
{
    int arr[n];

    int i = 0;

    // First odd number
    int odd = 1;
    while (odd <= n) {

        // Insert the odd number
        arr[i++] = odd;

        // Next odd number
        odd += 2;
    }

    // First even number
    int even = 2;
    while (even <= n) {

        // Insert the even number
        arr[i++] = even;

        // Next even number
        even += 2;
    }

    // Return the kth element
    return arr[k - 1];
}

// Driver code
int main()
{
    int n = 8, k = 5;
    cout << getNumber(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the kth element
// in the modified array
static int getNumber(int n, int k)
{
    int []arr = new int[n];

    int i = 0;

    // First odd number
    int odd = 1;
    while (odd <= n)
    {

        // Insert the odd number
        arr[i++] = odd;

        // Next odd number
        odd += 2;
    }

    // First even number
    int even = 2;
    while (even <= n)
    {

        // Insert the even number
        arr[i++] = even;

        // Next even number
        even += 2;
    }

    // Return the kth element
    return arr[k - 1];
}

// Driver code
public static void main(String[] args)
{
    int n = 8, k = 5;
    System.out.println(getNumber(n, k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the kth element
# in the modified array
def getNumber(n, k):
    arr = [0] * n;

    i = 0;

    # First odd number
    odd = 1;
    while (odd <= n):

        # Insert the odd number
        arr[i] = odd;
        i += 1;

        # Next odd number
        odd += 2;

    # First even number
    even = 2;
    while (even <= n):
        # Insert the even number
        arr[i] = even;
        i += 1;

        # Next even number
        even += 2;

    # Return the kth element
    return arr[k - 1];

# Driver code
if __name__ == '__main__':
    n = 8;
    k = 5;
    print(getNumber(n, k));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the kth element
// in the modified array
static int getNumber(int n, int k)
{
    int []arr = new int[n];

    int i = 0;

    // First odd number
    int odd = 1;
    while (odd <= n)
    {

        // Insert the odd number
        arr[i++] = odd;

        // Next odd number
        odd += 2;
    }

    // First even number
    int even = 2;
    while (even <= n)
    {

        // Insert the even number
        arr[i++] = even;

        // Next even number
        even += 2;
    }

    // Return the kth element
    return arr[k - 1];
}

// Driver code
public static void Main(String[] args)
{
    int n = 8, k = 5;
    Console.WriteLine(getNumber(n, k));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// C++ implementation of the approach

// Function to return the kth element
// in the modified array
function getNumber(n, k)
{
    var arr = Array(n).fill(n);

    var i = 0;

    // First odd number
    var odd = 1;
    while (odd <= n) {

        // Insert the odd number
        arr[i++] = odd;

        // Next odd number
        odd += 2;
    }

    // First even number
    var even = 2;
    while (even <= n) {

        // Insert the even number
        arr[i++] = even;

        // Next even number
        even += 2;
    }

    // Return the kth element
    return arr[k - 1];
}

// Driver code
    var n = 8, k = 5;
    document.write(getNumber(n, k));

</script>
```

**Output:** 

```
2
```

**高效的方法:**找到第一个偶数元素将存储在生成的数组中的索引。现在，如果 **k** 的值小于或等于指数，那么期望的数字将是**k * 2–1**否则期望的数字将是**(k–指数)* 2**
下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the kth element
// in the modified array
int getNumber(int n, int k)
{
    int pos;

    // Finding the index from where the
    // even numbers will be stored
    if (n % 2 == 0) {
        pos = n / 2;
    }
    else {
        pos = (n / 2) + 1;
    }

    // Return the kth element
    if (k <= pos) {
        return (k * 2 - 1);
    }
    else

        return ((k - pos) * 2);
}

// Driver code
int main()
{
    int n = 8, k = 5;

    cout << getNumber(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the kth element
// in the modified array
static int getNumber(int n, int k)
{
    int pos;

    // Finding the index from where the
    // even numbers will be stored
    if ((n % 2) == 0)
    {
        pos = n / 2;
    }
    else
    {
        pos = (n / 2) + 1;
    }

    // Return the kth element
    if (k <= pos)
    {
        return (k * 2 - 1);
    }
    else
        return ((k - pos) * 2);
}

// Driver code
public static void main (String[] args)
{
    int n = 8, k = 5;
    System.out.println (getNumber(n, k));
}
}

// This code is contributed by @tushil.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the kth element
# in the modified array
def getNumber(n, k) :

    # Finding the index from where the
    # even numbers will be stored
    if (n % 2 == 0) :
        pos = n // 2;

    else :
        pos = (n // 2) + 1;

    # Return the kth element
    if (k <= pos) :
        return (k * 2 - 1);

    else :
        return ((k - pos) * 2);

# Driver code
if __name__ == "__main__" :
    n = 8; k = 5;

    print(getNumber(n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the kth element
// in the modified array
static int getNumber(int n, int k)
{
    int pos;

    // Finding the index from where the
    // even numbers will be stored
    if ((n % 2) == 0)
    {
        pos = n / 2;
    }
    else
    {
        pos = (n / 2) + 1;
    }

    // Return the kth element
    if (k <= pos)
    {
        return (k * 2 - 1);
    }
    else
        return ((k - pos) * 2);
}

// Driver code
static public void Main ()
{
    int n = 8, k = 5;
    Console.Write(getNumber(n, k));
}
}

// This code is contributed by @ajit.
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the kth element
    // in the modified array
    function getNumber(n, k)
    {
        let pos;

        // Finding the index from where the
        // even numbers will be stored
        if ((n % 2) == 0)
        {
            pos = parseInt(n / 2, 10);
        }
        else
        {
            pos = parseInt(n / 2, 10) + 1;
        }

        // Return the kth element
        if (k <= pos)
        {
            return (k * 2 - 1);
        }
        else
            return ((k - pos) * 2);
    }

    let n = 8, k = 5;
    document.write(getNumber(n, k));

</script>
```

**Output:** 

```
2
```