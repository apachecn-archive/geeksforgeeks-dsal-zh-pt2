# N 的二进制表示中两个 1 之间的最大距离

> 原文:[https://www . geeksforgeeks . org/n 的二进制表示中两个 1 之间的最大距离/](https://www.geeksforgeeks.org/maximum-distance-between-two-1s-in-binary-representation-of-n/)

给定一个数字 N，任务是找出给定 N 的二进制表示中两个 1 之间的最大距离。如果二进制表示包含少于两个 1，则打印-1。
**示例:**

```
Input: N = 131
Output: 6
131 in binary = 10000011.
The maximum distance between two 1's = 6.

Input: N = 8
Output: -1
8 in binary = 01000.
It contains less than two 1's.
```

**进场:**

*   首先[找到 N 的二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)。
*   对于计算的每个位，检查它是否为“1”。
*   存储在 first_1 中找到的第一个“1”和在 last_1 中找到的最后一个“1”的索引
*   然后检查 last_1 是否小于或等于 first_1。当 N 是 2 的幂时就会是这种情况。因此在这种情况下是 print -1。
*   在任何其他情况下，找出 last_1 和 first_1 之间的差异。这将是所需的距离。

以下是上述方法的实现:

## C++

```
// C++ program to find the
// Maximum distance between two 1's
// in Binary representation of N

#include <bits/stdc++.h>
using namespace std;

int longest_gap(int N)
{

    int distance = 0, count = 0,
        first_1 = -1, last_1 = -1;

    // Compute the binary representation
    while (N) {

        count++;

        int r = N & 1;

        if (r == 1) {
            first_1 = first_1 == -1
                          ? count
                          : first_1;
            last_1 = count;
        }

        N = N / 2;
    }

    // if N is a power of 2
    // then return -1
    if (last_1 <= first_1) {
        return -1;
    }
    // else find the distance
    // between the first position of 1
    // and last position of 1
    else {
        distance = (last_1 - first_1 - 1);
        return distance;
    }
}

// Driver code
int main()
{
    int N = 131;
    cout << longest_gap(N) << endl;

    N = 8;
    cout << longest_gap(N) << endl;

    N = 17;
    cout << longest_gap(N) << endl;

    N = 33;
    cout << longest_gap(N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// Maximum distance between two 1's
// in Binary representation of N
class GFG
{
    static int longest_gap(int N)
    {
        int distance = 0, count = 0,
            first_1 = -1, last_1 = -1;

        // Compute the binary representation
        while (N != 0)
        {
            count++;

            int r = N & 1;

            if (r == 1)
            {
                first_1 = first_1 == -1 ?
                                  count : first_1;
                last_1 = count;
            }
            N = N / 2;
        }

        // if N is a power of 2
        // then return -1
        if (last_1 <= first_1)
        {
            return -1;
        }

        // else find the distance
        // between the first position of 1
        // and last position of 1
        else
        {
            distance = (last_1 - first_1 - 1);
            return distance;
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 131;
        System.out.println(longest_gap(N));

        N = 8;
        System.out.println(longest_gap(N));

        N = 17;
        System.out.println(longest_gap(N));

        N = 33;
        System.out.println(longest_gap(N));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the
# Maximum distance between two 1's
# in Binary representation of N
def longest_gap(N):

    distance = 0
    count = 0
    first_1 = -1
    last_1 = -1

    # Compute the binary representation
    while (N > 0):
        count += 1

        r = N & 1

        if (r == 1):
            if first_1 == -1:
                first_1 = count
            else:
                first_1 = first_1

            last_1 = count

        N = N // 2

    # if N is a power of 2
    # then return -1
    if (last_1 <= first_1):
        return -1

    # else find the distance
    # between the first position of 1
    # and last position of 1
    else:
        distance = last_1 - first_1 - 1
        return distance

# Driver code
N = 131
print(longest_gap(N))

N = 8
print(longest_gap(N))

N = 17
print(longest_gap(N))

N = 33
print(longest_gap(N))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find the
// Maximum distance between two 1's
// in Binary representation of N
using System;

class GFG
{
    static int longest_gap(int N)
    {
        int distance = 0, count = 0,
            first_1 = -1, last_1 = -1;

        // Compute the binary representation
        while (N != 0)
        {
            count++;

            int r = N & 1;

            if (r == 1)
            {
                first_1 = first_1 == -1 ?
                                  count : first_1;
                last_1 = count;
            }
            N = N / 2;
        }

        // if N is a power of 2
        // then return -1
        if (last_1 <= first_1)
        {
            return -1;
        }

        // else find the distance
        // between the first position of 1
        // and last position of 1
        else
        {
            distance = (last_1 - first_1 - 1);
            return distance;
        }
    }

    // Driver code
    public static void Main (String []args)
    {
        int N = 131;
        Console.WriteLine(longest_gap(N));

        N = 8;
        Console.WriteLine(longest_gap(N));

        N = 17;
        Console.WriteLine(longest_gap(N));

        N = 33;
        Console.WriteLine(longest_gap(N));
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
// Javascript program to find the
// Maximum distance between two 1's
// in Binary representation of N

function longest_gap(N)
{

    let distance = 0, count = 0,
        first_1 = -1, last_1 = -1;

    // Compute the binary representation
    while (N) {

        count++;

        let r = N & 1;

        if (r == 1) {
            first_1 = first_1 == -1
                          ? count
                          : first_1;
            last_1 = count;
        }

        N = parseInt(N / 2);
    }

    // if N is a power of 2
    // then return -1
    if (last_1 <= first_1) {
        return -1;
    }
    // else find the distance
    // between the first position of 1
    // and last position of 1
    else {
        distance = (last_1 - first_1 - 1);
        return distance;
    }
}

// Driver code
    let N = 131;
    document.write(longest_gap(N) + "<br>");

    N = 8;
    document.write(longest_gap(N) + "<br>");

    N = 17;
    document.write(longest_gap(N) + "<br>");

    N = 33;
    document.write(longest_gap(N) + "<br>");

</script>
```

**Output:** 

```
6
-1
3
4
```

时间复杂度:0(对数 N)

辅助空间:0(1)