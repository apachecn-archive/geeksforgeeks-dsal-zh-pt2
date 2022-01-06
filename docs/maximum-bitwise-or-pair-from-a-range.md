# 某个范围内的最大位“或”对

> 原文:[https://www . geeksforgeeks . org/最大按位或范围对/](https://www.geeksforgeeks.org/maximum-bitwise-or-pair-from-a-range/)

给定一个范围**【L，R】**，任务是找到一对 **(X，Y)** ，使得 **L ≤ X，Y ≤ R** 和 **(X | Y)** 在所有可能的对中最大，然后打印找到的对的位或。
**举例:**

> **输入:** L = 4，R = 5
> **输出:** 5
> 唯一的一对是(4，5)和(4 | 5) = 5。
> **输入:** L = 14，R = 2500
> **输出:** 4095

**天真的做法:**从 **L** 迭代到 **R** 检查每一个可能的对的按位 OR，最后打印最大值。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <climits>
#include <iostream>
using namespace std;

// Function to return the maximum bitwise OR
// possible among all the possible pairs
int maxOR(int L, int R)
{
    int maximum = INT_MIN;

    // Check for every possible pair
    for (int i = L; i < R; i++)
        for (int j = i + 1; j <= R; j++)

            // Maximum among all (i, j) pairs
            maximum = max(maximum, (i | j));

    return maximum;
}

// Driver code
int main()
{
    int L = 4, R = 5;

    cout << maxOR(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum bitwise OR
// possible among all the possible pairs
static int maxOR(int L, int R)
{
    int maximum = Integer.MIN_VALUE;

    // Check for every possible pair
    for (int i = L; i < R; i++)
        for (int j = i + 1; j <= R; j++)

            // Maximum among all (i, j) pairs
            maximum = Math.max(maximum, (i | j));

    return maximum;
}

// Driver code
public static void main(String []args)
{
    int L = 4, R = 5;

    System.out.println(maxOR(L, R));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum bitwise OR
# possible among all the possible pairs
def maxOR(L, R):
    maximum = -10**9

    # Check for every possible pair
    for i in range(L, R):
        for j in range(i + 1, R + 1):

            # Maximum among all (i, j) pairs
            maximum = max(maximum, (i | j))

    return maximum

# Driver code
L = 4
R = 5

print(maxOR(L, R))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum bitwise OR
// possible among all the possible pairs
static int maxOR(int L, int R)
{
    int maximum = int.MinValue;

    // Check for every possible pair
    for (int i = L; i < R; i++)
        for (int j = i + 1; j <= R; j++)

            // Maximum among all (i, j) pairs
            maximum = Math.Max(maximum, (i | j));

    return maximum;
}

// Driver code
public static void Main(String []args)
{
    int L = 4, R = 5;

    Console.WriteLine(maxOR(L, R));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum bitwise OR
// possible among all the possible pairs
function maxOR(L, R)
{
    let maximum = Number.MIN_VALUE;

    // Check for every possible pair
    for (let i = L; i < R; i++)
        for (let j = i + 1; j <= R; j++)

            // Maximum among all (i, j) pairs
            maximum = Math.max(maximum, (i | j));

    return maximum;
}

// Driver code
    let L = 4, R = 5;

    document.write(maxOR(L, R));

// This code is contributed by shivanisinghss2110

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(n <sup>2</sup>

**辅助空间:**0(1)
**有效方法:**或运算设置 **i <sup>第</sup>T8】位，如果任一操作数设置了 **i <sup>第</sup>T12】位。我们的目标是最大化设置位数。
现在的任务是找到 **B** 中 **L** 和 **R** 不同的最高有效位。 **B <sup>th</sup>** 位将设置在 **R** 中，而不设置在 **L** 中。可以生成的最大或将使所有对比特 **B** 有效的比特与 **L** 和 **R** 相同，并且所有比 **B** 低的比特将被设置，因为它们将包含在该范围内。 **B <sup>第</sup>** 位在或中为 1，因为 1 | 0 为 1。
现在，考虑 **L** 和 **R** 的二进制表示，从最高有效位(MSB)到最低有效位(LSB)。假设第一个 **x** 位对于 **L** 和 **R** 都相同。那么所有可能的 A 和 B 都具有与 **L** 和 **R** 相同的第一 **x** 位，因为即使这些 **x** 位中的单个位发生变化，该值也会移动到不允许的范围**【L，R】**之外。
接下来，将设置所有低于差异位 **B** 的位，包括 **B** 。
考虑下面的例子，
L = 001100010
R = 001100110
前六位对于 **L** 和 **R** 是相同的，因此所有的数字 N，使得 **L≤ N < R** 成立，它们的前六位将与 **L** 相同(或】
现在，忽略第一个 **x** 位，我们发现该位不匹配。在这一点上，可以构造 A，使得不匹配的位不被设置为 A，并且所有比当前位低的位都被设置。类似地，可以构造 B，使得为 B 设置失配位，并且在 B 中不设置所有后续位。
它们的“或”应该具有包括失配位设置在内的所有位。
把这个逻辑应用到我们的例子中，我们有 A = 001100011 和 B = 001100100，它们的 OR 是 001100111，这是最大可能。
以下是上述方法的实施:**** 

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

const int MAX = 64;

// Function to return the maximum bitwise OR
// possible among all the possible pairs
int maxOR(int L, int R)
{

    // If there is only a single value
    // in the range [L, R]
    if (L == R) {
        return L;
    }

    int ans = 0;

    // Loop through each bit from MSB to LSB
    for (int i = MAX - 1; i >= 0; i--) {
        int p, lbit, rbit;
        p = 1 << i;
        lbit = (L >> i) & 1; // bit of left limit
        rbit = (R >> i) & 1; // bit of right limit

        // MSBs where the bits differ,
        // all bits from that bit are set
        if ((rbit == 1) && (lbit == 0)) {
            ans += (p << 1) - 1;
            break;
        }

        // If MSBs are same, then ans
        // bit is same as that of
        // bit of right or left limit
        if (rbit == 1) {
            ans += p;
        }
    }
    return ans;
}

// Driver code
int main()
{
    int L = 4, R = 5;

    cout << maxOR(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int MAX = 64;

// Function to return the maximum bitwise OR
// possible among all the possible pairs
static int maxOR(int L, int R)
{

    // If there is only a single value
    // in the range [L, R]
    if (L == R)
    {
        return L;
    }

    int ans = 0;

    // Loop through each bit from MSB to LSB
    for (int i = MAX - 1; i >= 0; i--)
    {
        int p, lbit, rbit;
        p = 1 << i;
        lbit = (L >> i) & 1; // bit of left limit
        rbit = (R >> i) & 1; // bit of right limit

        // MSBs where the bits differ,
        // all bits from that bit are set
        if ((rbit == 1) && (lbit == 0))
        {
            ans += (p << 1) - 1;
            break;
        }

        // If MSBs are same, then ans
        // bit is same as that of
        // bit of right or left limit
        if (rbit == 1)
        {
            ans += p;
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int L = 4, R = 5;

    System.out.println(maxOR(L, R));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAX = 64;

# Function to return the maximum bitwise OR
# possible among all the possible pairs
def maxOR(L, R) :

    # If there is only a single value
    # in the range [L, R]
    if (L == R) :
        return L;

    ans = 0;

    # Loop through each bit from MSB to LSB
    for i in range(MAX - 1, -1, -1) :
        p = 1 << i;
        lbit = (L >> i) & 1; # bit of left limit
        rbit = (R >> i) & 1; # bit of right limit

        # MSBs where the bits differ,
        # all bits from that bit are set
        if ((rbit == 1) and (lbit == 0)) :
            ans += (p << 1) - 1;
            break;

        # If MSBs are same, then ans
        # bit is same as that of
        # bit of right or left limit
        if (rbit == 1) :
            ans += p;

    return ans;

# Driver code
if __name__ == "__main__" :

    L = 4; R = 5;

    print(maxOR(L, R));

    # This code is contributed by kanugargng
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
static int MAX = 64;

// Function to return the maximum bitwise OR
// possible among all the possible pairs
static int maxOR(int L, int R)
{

    // If there is only a single value
    // in the range [L, R]
    if (L == R)
    {
        return L;
    }

    int ans = 0;

    // Loop through each bit from MSB to LSB
    for (int i = MAX - 1; i >= 0; i--)
    {
        int p, lbit, rbit;
        p = 1 << i;
        lbit = (L >> i) & 1; // bit of left limit
        rbit = (R >> i) & 1; // bit of right limit

        // MSBs where the bits differ,
        // all bits from that bit are set
        if ((rbit == 1) && (lbit == 0))
        {
            ans += (p << 1) - 1;
            break;
        }

        // If MSBs are same, then ans
        // bit is same as that of
        // bit of right or left limit
        if (rbit == 1)
        {
            ans += p;
        }
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int L = 4, R = 5;

    Console.WriteLine(maxOR(L, R));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let MAX = 64;
// Function to return the maximum bitwise OR
// possible among all the possible pairs
function maxOR(L,R)
{
    // If there is only a single value
    // in the range [L, R]
    if (L == R)
    {
        return L;
    }

    let ans = 0;

    // Loop through each bit from MSB to LSB
    for (let i = MAX - 1; i >= 0; i--)
    {
        let p, lbit, rbit;
        p = 1 << i;
        lbit = (L >> i) & 1; // bit of left limit
        rbit = (R >> i) & 1; // bit of right limit

        // MSBs where the bits differ,
        // all bits from that bit are set
        if ((rbit == 1) && (lbit == 0))
        {
            ans += (p << 1) - 1;
            break;
        }

        // If MSBs are same, then ans
        // bit is same as that of
        // bit of right or left limit
        if (rbit == 1)
        {
            ans += p;
        }
    }
    return ans;
}

// Driver code
let L = 4, R = 5;

document.write(maxOR(L, R));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(log <sub>2</sub> (R))，其中 R 为范围上限。

**辅助空间:** O(1)