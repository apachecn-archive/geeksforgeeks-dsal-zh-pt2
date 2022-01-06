# 所有可能的 N 长度平衡二进制字符串的计数

> 原文:[https://www . geeksforgeeks . org/count-of-all-可能性-n-length-balanced-binary-strings/](https://www.geeksforgeeks.org/count-of-all-possible-n-length-balanced-binary-strings/)

给定一个数字 **N** ，任务是找到长度为 **N** 的平衡二进制字符串的总数。如果满足以下条件，则称二进制字符串是平衡的:

*   每个二进制字符串中 0 和 1 的数量相等
*   二进制字符串的任何前缀中 0 的计数总是大于或等于 1 的计数
*   例如:01 是长度为 2 的平衡二进制字符串，但 10 不是。

**示例:**

> **输入:** N = 4
> **输出:** 2
> **解释:**可能的平衡二进制字符串有:0101，0011
> 
> **输入:**N = 5
> T3】输出: 0

**方法:**给定的问题可以通过以下方式解决:

1.  如果 **N** 为奇数，则不可能有平衡的二进制字符串，因为 0 和 1 相等计数的条件将失败。
2.  如果 **N** 为偶数，那么 N 长度的二进制串将有 **N/2** 平衡的 0 和 1 对。
3.  所以，现在试着创建一个公式，得到 **N** 为偶数时的平衡弦数。

> 所以如果 **N = 2** ，那么可能的平衡二进制串将只是**“01”**，因为“00”和“11”没有相同的 0 和 1 的计数，“10”没有 0 的计数> =前缀【0，1】中的 1 的计数。
> 同样，如果 **N=4** ，则可能的平衡二进制串为**“0101”**、**“0011”**
> 对于 **N = 6** ，则可能的平衡二进制串为**“010101”**、**“010011”**、**“01101”**、 计数(4) =计数(0)*计数(2) +计数(2)*计数(0) = 1*1 + 1*1 = 2
> 对于 N=6，计数(6) =计数(0)*计数(4) +计数(2)*计数(2) +计数(4)*计数(0) = 1*2 + 1*1 + 2*1 = 5
> 对于 N=8，计数(8) =计数(0)*计数(6) +计数(2)*计数(4) +计数
> 。
> 。
> **对于 N=N，count(N)= count(0)* count(N-2)+count(2)* count(N-4)+count(4)* count(N-6)+…。+count(N-6)* count(4)+count(N-4)* count(2)+count(N-2)* count(0)**
> 这不过是[的加泰罗尼亚数字](https://www.geeksforgeeks.org/program-nth-catalan-number/)。

1.  因此对于任何偶数 **N** 返回加泰罗尼亚语数字为 **(N/2)** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

#define MAXN 500
#define mod 1000000007

// Vector to store catalan number
vector<long long int> cat(MAXN + 1, 0);

// Function to get the Catalan Number
void catalan()
{
    cat[0] = 1;
    cat[1] = 1;

    for (int i = 2; i < MAXN + 1; i++) {
        long long int t = 0;
        for (int j = 0; j < i; j++) {
            t += ((cat[j] % mod)
                  * (cat[i - 1 - j] % mod)
                  % mod);
        }
        cat[i] = (t % mod);
    }
}

int countBalancedStrings(int N)
{
    // If N is odd
    if (N & 1) {
        return 0;
    }

    // Returning Catalan number
    // of N/2 as the answer
    return cat[N / 2];
}

// Driver Code
int main()
{
    // Precomputing
    catalan();

    int N = 4;
    cout << countBalancedStrings(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    public static int MAXN = 500;
    public static int mod = 1000000007;

    // Vector to store catalan number
    public static int[] cat = new int[MAXN + 1];

    // Function to get the Catalan Number
    public static void catalan() {
        cat[0] = 1;
        cat[1] = 1;

        for (int i = 2; i < MAXN + 1; i++) {
            int t = 0;
            for (int j = 0; j < i; j++) {
                t += ((cat[j] % mod)
                        * (cat[i - 1 - j] % mod)
                        % mod);
            }
            cat[i] = (t % mod);
        }
    }

    public static int countBalancedStrings(int N)
    {

        // If N is odd
        if ((N & 1) > 0) {
            return 0;
        }

        // Returning Catalan number
        // of N/2 as the answer
        return cat[N / 2];
    }

    // Driver Code
    public static void main(String args[])
    {

        // Precomputing
        catalan();

        int N = 4;
        System.out.println(countBalancedStrings(N));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python3 program for the above approach
MAXN = 500
mod = 1000000007

# Vector to store catalan number
cat = [0 for _ in range(MAXN + 1)]

# Function to get the Catalan Number
def catalan():

    global cat

    cat[0] = 1
    cat[1] = 1

    for i in range(2, MAXN + 1):
        t = 0
        for j in range(0, i):
            t += ((cat[j] % mod) *
                  (cat[i - 1 - j] % mod) % mod)

        cat[i] = (t % mod)

def countBalancedStrings(N):

    # If N is odd
    if (N & 1):
        return 0

    # Returning Catalan number
    # of N/2 as the answer
    return cat[N // 2]

# Driver Code
if __name__ == "__main__":

    # Precomputing
    catalan()

    N = 4
    print(countBalancedStrings(N))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG
{
    public static int MAXN = 500;
    public static int mod = 1000000007;

    // Vector to store catalan number
    public static int[] cat = new int[MAXN + 1];

    // Function to get the Catalan Number
    public static void catalan()
    {
        cat[0] = 1;
        cat[1] = 1;

        for (int i = 2; i < MAXN + 1; i++)
        {
            int t = 0;
            for (int j = 0; j < i; j++)
            {
                t += ((cat[j] % mod)
                        * (cat[i - 1 - j] % mod)
                        % mod);
            }
            cat[i] = (t % mod);
        }
    }

    public static int countBalancedStrings(int N)
    {

        // If N is odd
        if ((N & 1) > 0)
        {
            return 0;
        }

        // Returning Catalan number
        // of N/2 as the answer
        return cat[N / 2];
    }

    // Driver Code
    public static void Main()
    {

        // Precomputing
        catalan();

        int N = 4;
        Console.Write(countBalancedStrings(N));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>

    // JavaScript Program to implement
    // the above approach
    let MAXN = 500
    let mod = 1000000007

    // Vector to store catalan number
    let cat = new Array(MAXN + 1).fill(0);

    // Function to get the Catalan Number
    function catalan() {
        cat[0] = 1;
        cat[1] = 1;

        for (let i = 2; i < MAXN + 1; i++) {
            let t = 0;
            for (let j = 0; j < i; j++) {
                t += ((cat[j] % mod)
                    * (cat[i - 1 - j] % mod)
                    % mod);
            }
            cat[i] = (t % mod);
        }
    }

    function countBalancedStrings(N)
    {

        // If N is odd
        if (N & 1) {
            return 0;
        }

        // Returning Catalan number
        // of N/2 as the answer
        return cat[Math.floor(N / 2)];
    }

    // Driver Code

    // Precomputing
    catalan();
    let N = 4;
    document.write(countBalancedStrings(N));

// This code is contributed by Potta Lokesh
</script>
```

**Output**

```
2
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)