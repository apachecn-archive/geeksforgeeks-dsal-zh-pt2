# 按位“与”为正的前 N 个自然数的最大集合数

> 原文:[https://www . geeksforgeeks . org/从第一个 n 个自然数开始的最大数字集，其位与为正/](https://www.geeksforgeeks.org/maximum-set-of-number-from-the-first-n-natural-numbers-whose-bitwise-and-is-positive/)

给定一个正整数 **N** ，任务是从第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)中找出最大的一组数，自然数的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)为正

**示例:**

> **输入:** N = 7
> **输出:** 4
> **解释:**
> 按位“与”为正的第一个 N(= 7)个自然数的集合为{4，5，6，7}，长度最大。
> 
> **输入:**N = 16
> T3】输出: 8

**方法:**给定的问题可以通过观察 **2 <sup>N</sup> 和(2<sup>N</sup>–1)**得到 **0** 来解决。因此[组](https://www.geeksforgeeks.org/set-in-cpp-stl/)的最大长度不得同时包括同一组中的 **2 <sup>N</sup> 和(2<sup>N</sup>–1)**。具有非零“与”值的最大子阵列可以由下式求出:

*   求 2 小于等于 **N** 的最大[次幂，如果](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/)[T5【N】是 2](https://www.geeksforgeeks.org/program-to-find-whether-a-given-number-is-power-of-2/) 次幂，答案应该是 **N/2** ，比如当 N 为 **16** 时，非零 and 值的最大子阵为 **8** 。
*   否则，答案是 **N** 与 2 的[最大幂之间的长度小于或等于 **N** 。](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum set of
// number whose Bitwise AND is positive
int maximumSizeOfSet(int N)
{
    // Base Case
    if (N == 1)
        return 1;

    // Store the power of 2 less than
    // or equal to N
    int temp = 1;
    while (temp * 2 <= N) {
        temp *= 2;
    }

    // N is power of 2
    if (N & (N - 1) == 0)
        return N / 2;
    else
        return N - temp + 1;
}

// Driver Code
int main()
{
    int N = 7;
    cout << maximumSizeOfSet(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the maximum set of
// number whose Bitwise AND is positive
public static int maximumSizeOfSet(int N)
{

    // Base Case
    if (N == 1)
        return 1;

    // Store the power of 2 less than
    // or equal to N
    int temp = 1;
    while (temp * 2 <= N) {
        temp *= 2;
    }

    // N is power of 2
    if ((N & (N - 1)) == 0)
        return N / 2;
    else
        return N - temp + 1;
}

// Driver Code
public static void main(String args[])
{
    int N = 7;
    System.out.println(maximumSizeOfSet(N));
}

}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the maximum set of
# number whose Bitwise AND is positive
def maximumSizeOfSet(N):

    # Base Case
    if (N == 1):
        return 1

    # Store the power of 2 less than
    # or equal to N
    temp = 1
    while (temp * 2 <= N):
        temp *= 2

    # N is power of 2
    if (N & (N - 1) == 0):
        return N // 2
    else:
        return N - temp + 1

# Driver Code
if __name__ == "__main__":

    N = 7
    print(maximumSizeOfSet(N))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    static int maximumSizeOfSet(int N)
    {

        // Base Case
        if (N == 1)
            return 1;

        // Store the power of 2 less than
        // or equal to N
        int temp = 1;
        while (temp * 2 <= N) {
            temp *= 2;
        }

        // N is power of 2
        if ((N & (N - 1)) == 0)
            return N / 2;
        else
            return N - temp + 1;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 7;

        Console.WriteLine(maximumSizeOfSet(N));
    }
}

// This code is contributed by dwivediyash
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to find the maximum set of
    // number whose Bitwise AND is positive
    const maximumSizeOfSet = (N) => {
        // Base Case
        if (N == 1)
            return 1;

        // Store the power of 2 less than
        // or equal to N
        let temp = 1;
        while (temp * 2 <= N) {
            temp *= 2;
        }

        // N is power of 2
        if (N & (N - 1) == 0)
            return parseInt(N / 2);
        else
            return N - temp + 1;
    }

    // Driver Code
    let N = 7;
    document.write(maximumSizeOfSet(N));

    // This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*