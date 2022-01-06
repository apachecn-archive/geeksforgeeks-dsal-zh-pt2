# 在 1 到 N 的范围内对(A，B)进行计数，使得 A 的最后一位等于 B 的第一位

> 原文:[https://www . geeksforgeeks . org/成对计数-a-b 范围-1 到-n-这样-a 的最后一位等于 b 的第一位/](https://www.geeksforgeeks.org/count-of-pairs-a-b-in-range-1-to-n-such-that-last-digit-of-a-is-equal-to-the-first-digit-of-b/)

给定一个数字 **N** ，任务是在范围**【1，N】**内找到对的数量 **(A，B)** ，使得 **A** 的最后一位等于 **B** 的第一位， **A** 的第一位等于 **B** 的最后一位。
**举例:**

> **输入:** N = 25
> **输出:** 17
> **解释:**
> 配对为:
> (1，1)，(1，11)，(2，2)，(2，22)，(3，3)，(4，4)，(5，5)，(6，6)，(7，7)，(8，8)，(9，9)，(11，1)，(11，11)，(12，21)，(21，12)，(22，2)，(22，22)

**逼近:**对于每一对整数 **(i，j)(0 ≤ i，j ≤ 9)** ，我们定义 **c <sub>i，j</sub> (1 ≤ k ≤ N)** ，即 **k** 的第一位数字的个数等于 **i** ，最后一位数字等于 **j** 。通过使用 **c <sub>i，j</sub>** ，可以通过**∑<sub>I = 0</sub><sup>9</sup>∑<sub>j = 0</sub><sup>9</sup>c<sub>I，j</sub> * c <sub>j，i</sub>** 计算出问题的答案。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to implement the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to Count of pairs (A, B) in range 1 to N
int pairs(int n)
{
    vector<vector<int> > c(10, vector<int>(10, 0));

    int tmp = 1;

    // count C i, j
    for (int i = 1; i <= n; i++) {
        if (i >= tmp * 10)
            tmp *= 10;
        c[i / tmp][i % 10]++;
    }

    // Calculate number of pairs
    long long ans = 0;
    for (int i = 1; i < 10; i++)
        for (int j = 1; j < 10; j++)
            ans += (long long)c[i][j] * c[j][i];

    return ans;
}

// Driver code
int main()
{
    int n = 25;

    // Function call
    cout << pairs(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach

class GFG{

// Function to Count of pairs (A, B) in range 1 to N
static int pairs(int n)
{
    int [][]c = new int[10][10];

    int tmp = 1;

    // count C i, j
    for (int i = 1; i <= n; i++) {
        if (i >= tmp * 10)
            tmp *= 10;
        c[i / tmp][i % 10]++;
    }

    // Calculate number of pairs
    int ans = 0;
    for (int i = 1; i < 10; i++)
        for (int j = 1; j < 10; j++)
            ans += c[i][j] * c[j][i];

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 25;

    // Function call
    System.out.print(pairs(n));

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement the above approach

# Function to Count of pairs (A, B) in range 1 to N
def pairs(n):
    c = [[0 for i in range(10)] for i in range(10)]

    tmp = 1

    # count C i, j
    for i in range(1, n + 1):
        if (i >= tmp * 10):
            tmp *= 10
        c[i // tmp][i % 10] += 1

    # Calculate number of pairs
    ans = 0
    for i in range(1, 10):
        for j in range(1, 10):
            ans += c[i][j] * c[j][i]

    return ans

# Driver code
if __name__ == '__main__':
    n = 25

    # Function call
    print(pairs(n))

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program to implement the above approach
using System;

class GFG{

// Function to Count of pairs (A, B) in range 1 to N
static int pairs(int n)
{
    int [,]c = new int[10, 10];

    int tmp = 1;

    // count C i, j
    for (int i = 1; i <= n; i++) {
        if (i >= tmp * 10)
            tmp *= 10;
        c[i / tmp, i % 10]++;
    }

    // Calculate number of pairs
    int ans = 0;
    for (int i = 1; i < 10; i++)
        for (int j = 1; j < 10; j++)
            ans += c[i, j] * c[j, i];

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int n = 25;

    // Function call
    Console.Write(pairs(n));

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to Count of pairs (A, B) in range 1 to N
function pairs(n)
{
    let c = new Array(10);
    for (var i = 0; i < c.length; i++) {
    c[i] = new Array(2);
    }
    for (var i = 0; i < c.length; i++) {
    for (var j = 0; j < c.length; j++) {
    c[i][j] = 0;
    }
    }

    let tmp = 1;

    // count C i, j
    for (let i = 1; i <= n; i++) {
        if (i >= tmp * 10)
            tmp *= 10;
        c[Math.floor(i / tmp)][i % 10]++;
    }

    // Calculate number of pairs
    let ans = 0;
    for (let i = 1; i < 10; i++)
        for (let j = 1; j < 10; j++)
            ans += c[i][j] * c[j][i];

    return ans;
}

// Driver code

         let n = 25;

    // Function call
    document.write(pairs(n));

</script>
```

**Output:** 

```
17
```

**时间复杂度:** O(N)

**辅助空间:** O(10*10)