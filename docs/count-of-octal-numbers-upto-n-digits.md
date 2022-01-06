# 八进制数计数至 N 位数

> 原文:[https://www . geesforgeks . org/八进制数-最多 n 位数/](https://www.geeksforgeeks.org/count-of-octal-numbers-upto-n-digits/)

给定一个整数 **N** ，任务是找到自然八进制数的计数，直到 **N** 位数。

> **例:**
> **输入:** N = 1
> **输出:** 7
> **说明:**
> 1、2、3、4、5、6、7 均为 1 位数自然八进制数。
> **输入:** N = 2
> **输出:** 63
> **说明:**
> 共有 56 个两位八进制数和 7 个一位八进制数。因此，56 + 7 = 63。

**进场:**仔细观察，形成一个几何级数【**7 56 448 3584 28672 229376……**】，第一项为 **7** ，共同比值为 **8** 。
因此，

```
Nth term = Number of Octal numbers of N digits = 7 * 8N - 1
```

最后，所有八进制数(最多 N 位)的计数可以通过从 1 到 N 的循环迭代并使用上述公式计算项的和来计算出来。
以下是上述方法的实现:

## C++

```
// C++ program to find the count of
// natural octal numbers upto N digits

#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// natural octal numbers upto N digits
int count(int N)
{
    int sum = 0;

    // Loop to iterate from 1 to N
    // and calculating number of
    // octal numbers for every 'i'th digit.
    for (int i = 1; i <= N; i++) {
        sum += 7 * pow(8, i - 1);
    }
    return sum;
}

// Driver code
int main()
{
    int N = 4;
    cout << count(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// natural octal numbers upto N digits

public class GFG {

    // Function to return the count of
    // natural octal numbers upto N digits
    static int count(int N)
    {
        int sum = 0;

        // Loop to iterate from 1 to N
        // and calculating number of
        // octal numbers for every 'i'th digit.
        for (int i = 1; i <= N; i++) {
            sum += 7 * Math.pow(8, i - 1);
        }
        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 4;
        System.out.println(count(N));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the count of
# natural octal numbers upto N digits

# Function to return the count of
# natural octal numbers upto N digits
def count(N) :

    sum = 0;

    # Loop to iterate from 1 to N
    # and calculating number of
    # octal numbers for every 'i'th digit.
    for i in range(N + 1) :
        sum += 7 * (8 **(i - 1));

    return int(sum);

# Driver code
if __name__ == "__main__" :

    N = 4;
    print(count(N));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the count of
// natural octal numbers upto N digits
using System;

class GFG
{

    // Function to return the count of
    // natural octal numbers upto N digits
    static int count(int N)
    {
        int sum = 0;

        // Loop to iterate from 1 to N
        // and calculating number of
        // octal numbers for every 'i'th digit.
        for (int i = 1; i <= N; i++)
        {
            sum += (int)(7 * Math.Pow(8, i - 1));
        }
        return sum;
    }

    // Driver code
    public static void Main ()
    {
        int N = 4;
        Console.WriteLine(count(N));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to find the count of
// natural octal numbers upto N digits

// Function to return the count of
// natural octal numbers upto N digits
function count(N)
{
    var sum = 0;

    // Loop to iterate from 1 to N
    // and calculating number of
    // octal numbers for every 'i'th digit.
    for (var i = 1; i <= N; i++) {
        sum += 7 * Math.pow(8, i - 1);
    }
    return sum;
}

// Driver code
 var N = 4;
 document.write(count(N));

</script>
```

**Output:** 

```
4095
```

**时间复杂度:** O(N)