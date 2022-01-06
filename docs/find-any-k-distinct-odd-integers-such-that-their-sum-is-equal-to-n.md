# 找出任意 K 个不同的奇数，使得它们的和等于 N

> 原文:[https://www . geesforgeks . org/find-any-k-distinct-奇数-整数-这样-它们的和等于-n/](https://www.geeksforgeeks.org/find-any-k-distinct-odd-integers-such-that-their-sum-is-equal-to-n/)

给定两个整数 **N** 和 **K** ，任务是找到任意 **K** 个不同的奇数，使得它们的和等于 **N** 。如果不存在这样的整数，打印-1。
**举例:**

> **输入:** N = 10，K = 2
> **输出:** 1，9
> **解释:**
> 有两个可能不同的奇数，这样它们的和等于 N.
> 可能的 K 个整数可以是–{(1，9)，(3，7)}
> **输入:** N = 5，K = 4
> **输出:** -1
> **解释:**

**进场:**

*   这个问题的关键观察是，如果 N 和 K 具有不同的[奇偶性](https://www.geeksforgeeks.org/program-to-find-parity/)，那么就不可能找到 K 个这样不同的整数，使得它们的和等于 N，
*   否则这样的**K–1**整数将由**第一个 K-1 奇数正整数**组成
*   第 **K <sup>个</sup>奇数**将等于**(N-第(K-1)个奇数的和)**

```
Kth Odd number  = N - sum of first K-1 integer
```

以下是上述方法的实现:

## C++

```
// C++ implementation to find k
// odd integers such that their sum is N

#include <bits/stdc++.h>
using namespace std;

// Function to find K odd integers
// such that their sum is N
void oddIntegers(int n, int k)
{
    // Condition to check if there
    // exist such K integers
    if (n % 2 != k % 2) {
        cout << "-1"
             << "\n";
        return;
    }

    int sum = 0;
    int i = 1;
    int j = 1;

    // Loop to find first K-1
    // distinct odd integers
    while (j < k) {
        sum = sum + i;
        cout << i << " ";
        i = i + 2;
        j++;
    }

    // Final Kth odd number
    int finalOdd = n - sum;

    cout << finalOdd << "\n";
}

// Driver code
int main()
{
    int n = 10;
    int k = 2;

    oddIntegers(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find k
// odd integers such that their sum is N
class GFG
{

// Function to find K odd integers
// such that their sum is N
static void oddIntegers(int n, int k)
{
    // Condition to check if there
    // exist such K integers
    if (n % 2 != k % 2) {
        System.out.println("-1");
        return;
    }

    int sum = 0;
    int i = 1;
    int j = 1;

    // Loop to find first K-1
    // distinct odd integers
    while (j < k) {
        sum = sum + i;
        System.out.print(i+" ");
        i = i + 2;
        j++;
    }

    // Final Kth odd number
    int finalOdd = n - sum;

    System.out.println(finalOdd);
}

// Driver code
public static void main (String[] args)
{
    int n = 10;
    int k = 2;

    oddIntegers(n, k);
}
}

// This code is contributed by shubhamsingh
```

## 蟒蛇 3

```
# Python3 implementation to find k
# odd integers such that their sum is N

# Function to find K odd integers
# such that their sum is N
def oddIntegers(n, k) :

    # Condition to check if there
    # exist such K integers
    if (n % 2 != k % 2) :
        print("-1");

        return;

    sum = 0;
    i = 1;
    j = 1;

    # Loop to find first K-1
    # distinct odd integers
    while (j < k) :
        sum += i;
        print(i,end= " ");
        i += 2;
        j += 1;

    # Final Kth odd number
    finalOdd = n - sum;

    print(finalOdd);

# Driver code
if __name__ == "__main__" :

    n = 10;
    k = 2;

    oddIntegers(n, k);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find k
// odd integers such that their sum is N
using System;

class GFG
{

// Function to find K odd integers
// such that their sum is N
static void oddints(int n, int k)
{
    // Condition to check if there
    // exist such K integers
    if (n % 2 != k % 2) {
        Console.WriteLine("-1");
        return;
    }

    int sum = 0;
    int i = 1;
    int j = 1;

    // Loop to find first K-1
    // distinct odd integers
    while (j < k) {
        sum = sum + i;
        Console.Write(i+" ");
        i = i + 2;
        j++;
    }

    // Final Kth odd number
    int finalOdd = n - sum;

    Console.WriteLine(finalOdd);
}

// Driver code
public static void Main(String[] args)
{
    int n = 10;
    int k = 2;

    oddints(n, k);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation to find k
// odd integers such that their sum is N   

// Function to find K odd integers
// such that their sum is N
    function oddIntegers(n , k)
    {
        // Condition to check if there
        // exist such K integers
        if (n % 2 != k % 2) {
            document.write("-1");
            return;
        }

        var sum = 0;
        var i = 1;
        var j = 1;

        // Loop to find first K-1
        // distinct odd integers
        while (j < k) {
            sum = sum + i;
            document.write(i + " ");
            i = i + 2;
            j++;
        }

        // Final Kth odd number
        var finalOdd = n - sum;

        document.write(finalOdd);
    }

    // Driver code

        var n = 10;
        var k = 2;

        oddIntegers(n, k);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
1 9
```

**业绩分析:**

*   **时间复杂度:**和上面的方法一样，有一个寻找这种 K 个奇数的循环，在最坏的情况下需要 O(K)个时间。因此时间复杂性将是 **O(K)** 。
*   **辅助空间复杂度:**和上面的方法一样，没有使用额外的空间。因此辅助空间的复杂性将是 **O(1)** 。