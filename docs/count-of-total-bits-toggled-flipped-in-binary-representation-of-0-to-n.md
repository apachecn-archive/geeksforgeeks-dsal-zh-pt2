# 以 0 到 N 的二进制表示切换/翻转的总位数

> 原文:[https://www . geesforgeks . org/总位数-切换-二进制翻转-表示 0 到 n/](https://www.geeksforgeeks.org/count-of-total-bits-toggled-flipped-in-binary-representation-of-0-to-n/)

给定一个整数 **N** ，任务是找到切换的总位数，依次获得从 **0** 到 **N** 的所有数字。

**示例:**

> **输入:** N = 5
> **输出:** 8
> **解释:**
> 我们用二进制表示从 0 到 5 的数字:
> 000 - > 001 : 1 位切换
> 001 - > 010 : 2 位切换
> 010 - > 011 : 1 位切换
> 011 - > 100 : 3 位切换【T13
> 
> **输入:**N = 1
> T3】输出: 1

**方法:**
按照以下步骤解决问题:

*   需要进行以下观察来解决问题:

> 最右边的位每次切换。
> (00**0**)->(00**1**)->(01**0**)->(01**1**)
> 因此，该位对计数的贡献为 **N** 。
> 每 2 个数字后，下一位切换。
> (0**0**0)—>(0**0**1)—>(0**1**0)—>(0**1**1)—>(1**0**0)
> 因此，该位对计数的贡献为 **N/2** 。

*   因此，我们可以得出结论，第**I**个最低有效位将贡献 **N/(2 <sup>i</sup> )** 给切换计数。
*   因此，我在范围**【0，对数<sub>2</sub>N】**内的 N/(2 <sup>i</sup> 之和给出了所需的答案。
*   因此，初始化一个变量**和**。将 **N** 添加到 **ans** 并将 **N** 更新为 **N/2** 。重复此过程，直到 **N** 变为 0，得到最终结果。

下面是上述方法的实现:

## C++

```
// C++ program to count
// the number of toggles
// required to generate
// all numbers from 0 to N

#include <bits/stdc++.h>
using namespace std;

typedef long long int ll;

// Function to count and print
// the required number of
// toggles
void solve(ll N)
{
    // Store the count
    // of toggles
    ll ans = 0;

    while (N != 0) {

        // Add the contribution
        // of the current LSB
        ans += N;

        // Update N
        N /= 2;
    }
    // Print the result
    cout << ans << endl;
}
// Driver code
int main()
{
    ll N = 5;
    solve(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the
// number of toggles required
// to generate all numbers
// from 0 to N
class GFG{

// Function to count and print
// the required number of
// toggles
static void solve(int N)
{

    // Store the count
    // of toggles
    int ans = 0;

    while (N != 0)
    {

        // Add the contribution
        // of the current LSB
        ans += N;

        // Update N
        N /= 2;
    }

    // Print the result
    System.out.println(ans);
}

// Driver code
public static void main(String []args)
{
    int N = 5;

    solve(N);
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program to count
# the number of toggles
# required to generate
# all numbers from 0 to N

# Function to count and pr
# the required number of
# toggles
def solve(N):

    # Store the count
    # of toggles
    ans = 0

    while (N != 0):

        # Add the contribution
        # of the current LSB
        ans += N

        # Update N
        N //= 2

    # Print the result
    print(ans)

# Driver code
N = 5

solve(N)

# This code is contributed by code_hunt
```

## C#

```
// C# program to count the
// number of toggles required
// to generate all numbers
// from 0 to N
using System;

class GFG{

// Function to count and print
// the required number of
// toggles
static void solve(int N)
{

    // Store the count
    // of toggles
    int ans = 0;

    while (N != 0)
    {

        // Add the contribution
        // of the current LSB
        ans += N;

        // Update N
        N /= 2;
    }

    // Print the result
    Console.Write(ans);
}

// Driver code
public static void Main(string []args)
{
    int N = 5;

    solve(N);
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

// Javascript program to count the
// number of toggles required to
// generate all numbers from 0 to N

// Function to count and print
// the required number of
// toggles
function solve(N)
{

    // Store the count
    // of toggles
    let ans = 0;

    while (N != 0)
    {

        // Add the contribution
        // of the current LSB
        ans += N;

        // Update N
        N = parseInt(N / 2, 10);
    }

    // Print the result
    document.write(ans);
}

// Driver code   
let N = 5;

solve(N);

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
8
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*