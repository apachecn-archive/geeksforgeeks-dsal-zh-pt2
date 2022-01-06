# 表示一个数所需的 2 的给定幂的最小数量

> 原文:[https://www . geeksforgeeks . org/最小给定 2 次方数要求代表一个数/](https://www.geeksforgeeks.org/minimum-number-of-given-powers-of-2-required-to-represent-a-number/)

给定一个整数 **x** 和一个数组 **arr[]** ，每个元素都是 2 的幂。任务是从数组中找出 2 的最小整数次幂，相加后得到 **x** 。如果无法用给定的数组元素表示 **x** ，则打印 **-1** 。
**举例:**

> **输入:** arr[] = {2，4，8，2，4}，x = 14
> **输出:** 3
> 14 可以写成 8 + 4 + 2
> **输入:** arr[] = {2，4，8，2，4}，x = 5
> **输出:** -1
> 5 不能表示为给定数组中任何元素的和。

**方法:**对于 2 的每次幂，让我们计算给定数组中元素的数量，值等于这个。姑且称之为 **cnt** 。显而易见，我们可以贪婪地获得 x 值(因为元素的所有较小值都是元素的所有较大值的除数)。
现在让我们迭代 2 从 **30** 到 **0** 的所有**次方。让**度**成为当前度。我们可以取 **min(x / 2 <sup>deg</sup> ，cnt <sub>deg</sub> )** 元素，取值等于 **2 <sup>deg</sup>** 。让它被弯曲。答案加 cur，从 **x** 中减去 **2 <sup>度</sup> * cur** 。重复该过程，直到 **x** 不能再减少。如果迭代所有次幂后，x 仍然非零，则打印 **-1** 。否则，打印答案。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of given integer powers of 2 required
// to represent a number as sum of these powers
int power_of_two(int n, int a[], int x)
{

    // To store the count of powers of two
    vector<int> cnt(31);

    for (int i = 0; i < n; ++i) {

        // __builtin_ctz(a[i]) returns the count
        // of trailing 0s in a[i]
        ++cnt[__builtin_ctz(a[i])];
    }

    int ans = 0;
    for (int i = 30; i >= 0 && x > 0; --i) {

        // If current power is available
        // in the array and can be used
        int need = min(x >> i, cnt[i]);

        // Update the answer
        ans += need;

        // Reduce the number
        x -= (1 << i) * need;
    }

    // If the original number is not reduced to 0
    // It cannot be represented as the sum
    // of the given powers of 2
    if (x > 0)
        ans = -1;

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 4, 4, 8 }, x = 6;
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << power_of_two(n, arr, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// __builtin_ctz(a[i]) returns the count
// of trailing 0s in a[i]
static int __builtin_ctz(int a)
{
    int count = 0;
    for(int i = 0; i < 40; i++)
    if(((a >> i) & 1) == 0)
    {
        count++;
    }
    else
        break;
    return count;
}

// Function to return the minimum number
// of given integer powers of 2 required
// to represent a number as sum of these powers
static int power_of_two(int n, int a[], int x)
{

    // To store the count of powers of two
    Vector<Integer> cnt = new Vector<Integer>();

    for (int i = 0; i < 31; ++i)
        cnt.add(0);

    for (int i = 0; i < n; ++i)
    {

        // __builtin_ctz(a[i]) returns the count
        // of trailing 0s in a[i]

        cnt.set(__builtin_ctz(a[i]),
        (cnt.get(__builtin_ctz(a[i]))==null) ?
        1 : cnt.get(__builtin_ctz(a[i]))+1);
    }

    int ans = 0;
    for (int i = 30; i >= 0 && x > 0; --i)
    {

        // If current power is available
        // in the array and can be used
        int need = Math.min(x >> i, cnt.get(i));

        // Update the answer
        ans += need;

        // Reduce the number
        x -= (1 << i) * need;
    }

    // If the original number is not reduced to 0
    // It cannot be represented as the sum
    // of the given powers of 2
    if (x > 0)
        ans = -1;

    return ans;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 2, 2, 4, 4, 8 }, x = 6;
    int n = arr.length;
    System.out.println(power_of_two(n, arr, x));
}
}

// This code is contributed by Arnab Kundu
```

## 大蟒

```
# Python3 implementation of the approach

# Function to return the minimum number
# of given eger powers of 2 required
# to represent a number as sum of these powers
def power_of_two( n, a, x):

    # To store the count of powers of two
    cnt=[0 for i in range(31)]

    for i in range(n):
        # __builtin_ctz(a[i]) returns the count
        # of trailing 0s in a[i]
        count = 0
        xx = a[i]
        while ((xx & 1) == 0):
            xx = xx >> 1
            count += 1

        cnt[count]+=1

    ans = 0
    for i in range(30,-1,-1):
        if x<=0:
            continue

        # If current power is available
        # in the array and can be used
        need = min(x >> i, cnt[i])

        # Update the answer
        ans += need

        # Reduce the number
        x -= (1 << i) * need

    # If the original number is not reduced to 0
    # It cannot be represented as the sum
    # of the given powers of 2
    if (x > 0):
        ans = -1

    return ans

# Driver code

arr=[2, 2, 4, 4, 8 ]
x = 6
n = len(arr)

print(power_of_two(n, arr, x))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// __builtin_ctz(a[i]) returns the count
// of trailing 0s in a[i]
static int __builtin_ctz(int a)
{
    int count = 0;
    for(int i = 0; i < 40; i++)
    if(((a >> i) & 1) == 0)
    {
        count++;
    }
    else
        break;
    return count;
}

// Function to return the minimum number
// of given integer powers of 2 required
// to represent a number as sum of these powers
static int power_of_two(int n, int []a, int x)
{

    // To store the count of powers of two
    int[] cnt = new int[32];

    for (int i = 0; i < n; ++i)
    {

        // __builtin_ctz(a[i]) returns the count
        // of trailing 0s in a[i]

        cnt[__builtin_ctz(a[i])] =
        cnt[__builtin_ctz(a[i])] ==
        0?1 : cnt[__builtin_ctz(a[i])] + 1;
    }

    int ans = 0;
    for (int i = 30; i >= 0 && x > 0; --i)
    {

        // If current power is available
        // in the array and can be used
        int need = Math.Min(x >> i, cnt[i]);

        // Update the answer
        ans += need;

        // Reduce the number
        x -= (1 << i) * need;
    }

    // If the original number is not reduced to 0
    // It cannot be represented as the sum
    // of the given powers of 2
    if (x > 0)
        ans = -1;

    return ans;
}

// Driver code
static void Main()
{
    int []arr = { 2, 2, 4, 4, 8 };
    int x = 6;
    int n = arr.Length;
    Console.WriteLine(power_of_two(n, arr, x));
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
// Function to return the minimum number
// of given integer powers of 2 required
// to represent a number as sum of these powers
function power_of_two( n, a, x)
{

    // To store the count of powers of two
    let cnt = [];
    for(let i = 0;i<31;i++)
        cnt.push(0);
    for (let i = 0; i < n; ++i) {

        // __builtin_ctz(a[i]) returns the count
        // of trailing 0s in a[i]
        let count = 0;
        let xx = a[i];
        while ((xx & 1) == 0){
            xx = xx >> 1
            count += 1
        }
        cnt[count]+=1;
    }

    let ans = 0;
    for (let i = 30; i >= 0 && x > 0; --i) {

        // If current power is available
        // in the array and can be used
        let need = Math.min(x >> i, cnt[i]);

        // Update the answer
        ans += need;

        // Reduce the number
        x -= (1 << i) * need;
    }

    // If the original number is not reduced to 0
    // It cannot be represented as the sum
    // of the given powers of 2
    if (x > 0)
        ans = -1;

    return ans;
}

// Driver code
let arr = [ 2, 2, 4, 4, 8 ], x = 6;
let n = arr.length;
document.write( power_of_two(n, arr, x));

</script>
```

**Output**

```
2
```

**时间复杂度:** O(N)

**辅助空间:** O(32)