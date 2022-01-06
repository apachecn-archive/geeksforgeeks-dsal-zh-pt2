# 从 1 到 n 对所有数字中的总设定位进行计数|设定 2

> 原文:[https://www . geesforgeks . org/count-total-set-bit-in-all-numbers-from-1-n-set-2/](https://www.geeksforgeeks.org/count-total-set-bits-in-all-numbers-from-1-to-n-set-2/)

给定一个正整数 **N** ，任务是计算从 **1** 到 **N** 的所有数字的二进制表示中的设定位数之和。
**举例:**

> **输入:** N = 3
> **输出:** 4
> 
> <figure class="table">
> 
> | 小数 | 二进制的 | 设置位数 |
> | --- | --- | --- |
> | one | 01 | one |
> | Two | Ten | one |
> | three | Eleven | Two |
> 
> 1 + 1 + 2 = 4
> **输入:** N = 16
> **输出:** 33
> 
> </figure>

**方法:**其他一些解决这个问题的方法已经讨论过了[这里](https://www.geeksforgeeks.org/count-total-set-bits-in-all-numbers-from-1-to-n/)。本文讨论了另一种时间复杂度为 0 的方法。
检查下表中从 1 到 N 的数字的二进制表示模式:

<figure class="table">

| 小数 | E | D | C | B | A |
| --- | --- | --- | --- | --- | --- |
| Zero | Zero | Zero | Zero | Zero | Zero |
| one | Zero | Zero | Zero | Zero | one |
| Two | Zero | Zero | Zero | one | Zero |
| three | Zero | Zero | Zero | one | one |
| four | Zero | Zero | one | Zero | Zero |
| five | Zero | Zero | one | Zero | one |
| six | Zero | Zero | one | one | Zero |
| seven | Zero | Zero | one | one | one |
| eight | Zero | one | Zero | Zero | Zero |
| nine | Zero | one | Zero | Zero | one |
| Ten | Zero | one | Zero | one | Zero |
| Eleven | Zero | one | Zero | one | one |
| Twelve | Zero | one | one | Zero | Zero |
| Thirteen | Zero | one | one | Zero | one |
| Fourteen | Zero | one | one | one | Zero |
| Fifteen | Zero | one | one | one | one |
| Sixteen | one | Zero | Zero | Zero | Zero |

注意，

1.  A 中的每一个交替位都被设置。
2.  B 中每 2 个交替位设置一次。
3.  C 中每 4 个交替位设置一次。
4.  D 中每 8 个交替位设置一次。
5.  …..
6.  这将继续重复每 2 的幂。

所以，我们将迭代直到数字中的位数。我们不需要迭代从 1 到 n 范围内的每个数字。
我们将执行以下操作来获得期望的结果。

*   ，首先，我们将在数字上加上 1，以补偿 0。因为二进制数字系统从 0 开始。所以现在 n = n + 1。
*   我们将跟踪到目前为止遇到的设置位的数量。我们将用 n/2 初始化它。
*   我们将保留一个 2 的幂的变量，以便跟踪我们正在计算的位。
*   我们将迭代直到 2 的幂变得大于 n。
*   我们可以通过将 n 除以当前的 2 次方，得到所有数字在当前位中的 0 和 1 对的数量。
*   现在我们必须将设置的位数相加。我们可以用 0 和 1 对的数量除以 2，得到 1 对的数量，然后乘以 2 的当前幂，得到组中 1 的数量。
*   现在可能有一个机会，我们得到一个数作为对的数目，它在组中间的某个地方，即在那个特定的组中，1 的数目小于 2 的当前幂。因此，我们将找到模数，并将其添加到集合位的计数中，借助于一个示例，这将是清楚的。

**例:**考虑 N = 14
从上表可知，从 1 到 14 总共会有 28 个设置位。
我们将考虑 2 <sup>0</sup> 作为 A，2 <sup>1</sup> 作为 B，2 <sup>2</sup> 作为 C，2 <sup>3</sup> 作为 D
首先我们将在数字 N 上加 1，所以现在我们的 N = 14 + 1 = 15。
^代表升到次方，而不是异或。

2^3 的意思是 2 加 3。

*   A 的计算(2<sup>0</sup>= 1)
    15/2 = 7
    A 中的设定位数= 7——>(I)
*   计算 B (2^1 = 2)
    15/2 = 7 = >有 7 组 0 和 1
    现在，为了只计算组集位数，我们必须将其除以 2。
    所以，7/2 = 3。共有 3 个设置位组。
    并且这些组将包含等于 2 的幂的设置位，这一次是 2。因此，我们将设置的位组数乘以 2 的幂
    = > 3*2 = 6 — > (2i)
    加上
    这可能会有一些额外的 1，因为不考虑第 4 组，因为这种除法只会给我们整数值。所以我们也要补充一点。注意:–只有当 0 和 1 的组数为奇数时，才会出现这种情况。
    15% 2 = 1—>(2ii)
    2i+2ii =>6+1 = 7—>(ii)
*   c 的计算(2^2 = 4)
    15/4 = 3 = >有 3 组 0 和 1
    设置位组的数量= 3/2 = 1
    这些组中设置位的数量= 1*4 = 4 — > (3i)
    由于 3 是奇数，我们必须在组中添加不被考虑的位
    因此，15% 4 = 3—>(3i)
    3i+3i = 4+3 = 7——————
*   计算 D (2^3 = 8)
    15/8 = 1 = >有 1 组 0 和 1。在这种情况下，只有一个组，而那个组也只有 0。
    设置位组数= 1/2 = 0
    这些组中的设置位数= 0 * 8 = 0 — > (4i)
    由于组数为奇数，
    所以，15% 8 = 7—>(4ii)
    4i+4ii = 0+7 = 7—>(iv)

此时，我们的 2 的幂变得大于数字，在我们的例子中是 15。(2 的幂= 16 和 16 > 15)。所以循环在这里终止。
最终输出= i + ii + iii + iv = 7 + 7 + 7 + 7 = 28
从 1 到 14 的设定位数为 28。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the sum of the count
// of set bits in the integers from 1 to n
int countSetBits(int n)
{

    // Ignore 0 as all the bits are unset
    n++;

    // To store the powers of 2
    int powerOf2 = 2;

    // To store the result, it is initialized
    // with n/2 because the count of set
    // least significant bits in the integers
    // from 1 to n is n/2
    int cnt = n / 2;

    // Loop for every bit required to represent n
    while (powerOf2 <= n) {

        // Total count of pairs of 0s and 1s
        int totalPairs = n / powerOf2;

        // totalPairs/2 gives the complete
        // count of the pairs of 1s
        // Multiplying it with the current power
        // of 2 will give the count of
        // 1s in the current bit
        cnt += (totalPairs / 2) * powerOf2;

        // If the count of pairs was odd then
        // add the remaining 1s which could
        // not be groupped together
        cnt += (totalPairs & 1) ? (n % powerOf2) : 0;

        // Next power of 2
        powerOf2 <<= 1;
    }

    // Return the result
    return cnt;
}

// Driver code
int main()
{
    int n = 14;

    cout << countSetBits(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the sum of the count
// of set bits in the integers from 1 to n
static int countSetBits(int n)
{

    // Ignore 0 as all the bits are unset
    n++;

    // To store the powers of 2
    int powerOf2 = 2;

    // To store the result, it is initialized
    // with n/2 because the count of set
    // least significant bits in the integers
    // from 1 to n is n/2
    int cnt = n / 2;

    // Loop for every bit required to represent n
    while (powerOf2 <= n)
    {

        // Total count of pairs of 0s and 1s
        int totalPairs = n / powerOf2;

        // totalPairs/2 gives the complete
        // count of the pairs of 1s
        // Multiplying it with the current power
        // of 2 will give the count of
        // 1s in the current bit
        cnt += (totalPairs / 2) * powerOf2;

        // If the count of pairs was odd then
        // add the remaining 1s which could
        // not be groupped together
        cnt += (totalPairs % 2 == 1) ?
                      (n % powerOf2) : 0;

        // Next power of 2
        powerOf2 <<= 1;
    }

    // Return the result
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int n = 14;

    System.out.println(countSetBits(n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum of the count
# of set bits in the integers from 1 to n
def countSetBits(n) :

    # Ignore 0 as all the bits are unset
    n += 1;

    # To store the powers of 2
    powerOf2 = 2;

    # To store the result, it is initialized
    # with n/2 because the count of set
    # least significant bits in the integers
    # from 1 to n is n/2
    cnt = n // 2;

    # Loop for every bit required to represent n
    while (powerOf2 <= n) :

        # Total count of pairs of 0s and 1s
        totalPairs = n // powerOf2;

        # totalPairs/2 gives the complete
        # count of the pairs of 1s
        # Multiplying it with the current power
        # of 2 will give the count of
        # 1s in the current bit
        cnt += (totalPairs // 2) * powerOf2;

        # If the count of pairs was odd then
        # add the remaining 1s which could
        # not be groupped together
        if (totalPairs & 1) :
            cnt += (n % powerOf2)
        else :
            cnt += 0

        # Next power of 2
        powerOf2 <<= 1;

    # Return the result
    return cnt;

# Driver code
if __name__ == "__main__" :

    n = 14;

    print(countSetBits(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the sum of the count
// of set bits in the integers from 1 to n
static int countSetBits(int n)
{

    // Ignore 0 as all the bits are unset
    n++;

    // To store the powers of 2
    int powerOf2 = 2;

    // To store the result, it is initialized
    // with n/2 because the count of set
    // least significant bits in the integers
    // from 1 to n is n/2
    int cnt = n / 2;

    // Loop for every bit required to represent n
    while (powerOf2 <= n)
    {

        // Total count of pairs of 0s and 1s
        int totalPairs = n / powerOf2;

        // totalPairs/2 gives the complete
        // count of the pairs of 1s
        // Multiplying it with the current power
        // of 2 will give the count of
        // 1s in the current bit
        cnt += (totalPairs / 2) * powerOf2;

        // If the count of pairs was odd then
        // add the remaining 1s which could
        // not be groupped together
        cnt += (totalPairs % 2 == 1) ?
                      (n % powerOf2) : 0;

        // Next power of 2
        powerOf2 <<= 1;
    }

    // Return the result
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int n = 14;

    Console.WriteLine(countSetBits(n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript implementation of the approach// Function to return the sum of the count
// of set bits in the integers from 1 to n
function countSetBits(n)
{

    // Ignore 0 as all the bits are unset
    n++;

    // To store the powers of 2
    var powerOf2 = 2;

    // To store the result, it is initialized
    // with n/2 because the count of set
    // least significant bits in the integers
    // from 1 to n is n/2
    var cnt = n / 2;

    // Loop for every bit required to represent n
    while (powerOf2 <= n)
    {

        // Total count of pairs of 0s and 1s
        var totalPairs = n / powerOf2;

        // totalPairs/2 gives the complete
        // count of the pairs of 1s
        // Multiplying it with the current power
        // of 2 will give the count of
        // 1s in the current bit
        cnt += (totalPairs / 2) * powerOf2;

        // If the count of pairs was odd then
        // add the remaining 1s which could
        // not be groupped together
        cnt += (totalPairs % 2 == 1) ?
                      (n % powerOf2) : 0;

        // Next power of 2
        powerOf2 <<= 1;
    }

    // Return the result
    return cnt;
}

// Driver code
var n = 14;

document.write(countSetBits(n));

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
28
```

时间复杂度:0(对数 n)

辅助空间:0(1)

</figure>