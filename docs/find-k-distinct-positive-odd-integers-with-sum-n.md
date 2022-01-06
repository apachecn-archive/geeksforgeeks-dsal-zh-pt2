# 用和 N 求 K 个不同的正奇数

> 原文:[https://www . geeksforgeeks . org/find-k-distinct-正整数-奇数-带和-n/](https://www.geeksforgeeks.org/find-k-distinct-positive-odd-integers-with-sum-n/)

给定两个整数 **N** 和 **K** ，任务是找到 K 个不同的正奇数，使得它们的和等于给定的数 N。
T5】示例:

> **输入:** N = 10，K = 2
> **输出:** 1 9
> **解释:**
> 两个奇数正整数，它们的和为 10，可以是(1，9)或(3，7)。
> **输入:** N = 10，K = 4
> **输出:**否
> **说明:**
> 不存在四个和为 10 的奇数正整数。

**逼近:**
数 **N** 可以表示为 **K** 的正奇数之和只有满足以下两个条件:

1.  如果 K 的平方小于或等于 N，
2.  如果 N 和 K 的和是偶数。

如果满足这些条件，那么存在 K 个奇数正整数，其和为 N.
以生成 K 个这样的奇数:

*   打印从 1 开始的前 K-1 个奇数，即 1、3、5、7、9……。
*   最后一个奇数将是:N –(前 K-1 个奇数正整数的和)

以下是上述方法的实现:

## C++

```
// C++ implementation to find K
// odd positive integers such that
// their sum is equal to given number

#include <bits/stdc++.h>
using namespace std;

#define ll long long int

// Function to find K odd positive
// integers such that their sum is N
void findDistinctOddSum(ll n, ll k)
{
    // Condition to check if there
    // are enough values to check
    if ((k * k) <= n &&
        (n + k) % 2 == 0){
        int val = 1;
        int sum = 0;
        for(int i = 1; i < k; i++){
            cout << val << " ";
            sum += val;
            val += 2;
        }
        cout << n - sum << endl;
    }
    else
        cout << "NO \n";
}

// Driver Code
int main()
{
    ll n = 100;
    ll k = 4;
    findDistinctOddSum(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find K
// odd positive integers such that
// their sum is equal to given number
import java.util.*;

class GFG{

// Function to find K odd positive
// integers such that their sum is N
static void findDistinctOddSum(int n, int k)
{
    // Condition to check if there
    // are enough values to check
    if ((k * k) <= n &&
        (n + k) % 2 == 0){
        int val = 1;
        int sum = 0;
        for(int i = 1; i < k; i++){
            System.out.print(val+ " ");
            sum += val;
            val += 2;
        }
        System.out.print(n - sum +"\n");
    }
    else
        System.out.print("NO \n");
}

// Driver Code
public static void main(String[] args)
{
    int n = 100;
    int k = 4;
    findDistinctOddSum(n, k);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to find K
# odd positive integers such that
# their summ is equal to given number

# Function to find K odd positive
# integers such that their summ is N
def findDistinctOddsumm(n, k):

    # Condition to check if there
    # are enough values to check
    if ((k * k) <= n and (n + k) % 2 == 0):
        val = 1
        summ = 0
        for i in range(1, k):
            print(val, end =  " ")
            summ += val
            val += 2
        print(n - summ)
    else:
        print("NO")

# Driver Code
n = 100
k = 4
findDistinctOddsumm(n, k)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to find K
// odd positive integers such that
// their sum is equal to given number
using System;

public class GFG{

// Function to find K odd positive
// integers such that their sum is N
static void findDistinctOddSum(int n, int k)
{
    // Condition to check if there
    // are enough values to check
    if ((k * k) <= n &&
        (n + k) % 2 == 0){
        int val = 1;
        int sum = 0;
        for(int i = 1; i < k; i++){
            Console.Write(val+ " ");
            sum += val;
            val += 2;
        }
        Console.Write(n - sum +"\n");
    }
    else
        Console.Write("NO \n");
}

// Driver Code
public static void Main(String[] args)
{
    int n = 100;
    int k = 4;
    findDistinctOddSum(n, k);
}
}
// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Function to find K odd positive
// integers such that their sum is N
function findDistinctOddSum(n,k)
{
    // Condition to check if there
    // are enough values to check
    if ((k * k) <= n &&
        (n + k) % 2 == 0){
        var val = 1;
        var sum = 0;
        for(var i = 1; i < k; i++){
            document.write( val+ " ");
            sum += val;
            val += 2;
        }
        document.write( n - sum) ;    }
    else
        document.write( "NO \n");
}

// Driver Code
var n = 100;
    var k = 4;
    findDistinctOddSum(n, k);

</script>
```

**Output**

```
1 3 5 91
```

**业绩分析:**

*   **时间复杂度:**在上面给出的方法中，有一个循环在最坏的情况下花费 O(K)时间。因此，该方法的时间复杂度为 **O(K)** 。
*   **辅助空间:** O(1)