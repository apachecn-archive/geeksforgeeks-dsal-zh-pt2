# 使用给定的一组数字

可以生成的不同的 N 位奇数的计数

> 原文:[https://www . geesforgeks . org/count-of-distinct-n-digital-奇数-可以使用给定的数字集生成的整数/](https://www.geeksforgeeks.org/count-of-distinct-n-digit-odd-integers-that-can-be-generated-using-given-set-of-digits/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，代表从 **0** 到 **9** 的数字，任务是计算使用数组中的给定数字可以形成的不同奇数 **N** 数字整数的数量。

**示例:**

> **输入:** arr[] = {1，0，2，4}
> **输出:** 4
> **解释:**可以使用给定数字形成的可能的 4 位奇数是 2041、2401、4021 和 4201。
> 
> **输入:** arr[] = {2，3，4，1，2，3 }
> T3】输出: 90

**方法:**给定的问题可以使用以下观察结果来解决:

*   对于奇数，其单位位置(即 1 <sup>st</sup> 位)应具有奇数位，即{1，3，5，7，9}
*   因为整数应该有 **N** 位，所以最高有效位(第 N <sup>位的数字</sup>不能等于 **0** 。
*   除了第 1 <sup>位</sup>和第 N <sup>位</sup>的数字外，其他所有数字都可以有任何其他数字。
*   排列 **X** 位的方式总数为 **X！/ ( freq[0]！* freq[1]！*……* freq[9]！)**，其中**频率[i]** 表示给定 **X** 位数中数字 **i** 的频率。

为了解决这个问题，记录变量**奇数**中的奇数位数和变量**零**中等于 0 的位数。所以根据以上观察，如果 **i** 代表 **N <sup>th</sup>** 数字， **j** 代表 **1 <sup>st</sup>** 数字，则迭代 **i** 和 **j** 的所有可能值，对于每个有效的 **(i，j)** ，计算剩余 **(N-2)【的排列方式数**

下面是上述方法的实现:

## C++14

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of distinct
// odd integers with N digits using the
// given digits in the array arr[]
int countOddIntegers(int arr[], int N)
{
    // Stores the factorial of a number
    int Fact[N] = {};

    // Calculate the factorial of all
    // numbers from 1 to N
    Fact[0] = 1;
    for (int i = 1; i < N; i++) {
        Fact[i] = i * Fact[i - 1];
    }

    // Stores the frequency of each digit
    int freq[10] = {};
    for (int i = 0; i < N; i++) {
        freq[arr[i]]++;
    }

    // Stores the final answer
    int ans = 0;

    // Loop to iterate over all values of
    // Nth digit i and 1st digit j
    for (int i = 1; i <= 9; i += 2) {

        // If digit i does not exist in
        // the given array move to next i
        if (!freq[i])
            continue;

        // Fixing i as Nth digit
        freq[i]--;

        for (int j = 1; j <= 9; j++) {

            // Stores the answer of a specific
            // value of i and j
            int cur_ans = 0;

            // If digit j does not exist
            // move to the next j
            if (freq[j] == 0) {
                continue;
            }

            // Fixing j as 1st digit
            freq[j]--;

            // Calculate number of ways to
            // arrange remaining N-2 digits
            cur_ans = Fact[N - 2];
            for (int k = 0; k <= 9; k++) {
                cur_ans = cur_ans / Fact[freq[k]];
            }
            ans += cur_ans;

            // Including j back into
            // the set of digits
            freq[j]++;
        }
        // Including i back into the
        // set of the digits
        freq[i]++;
    }

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    int A[] = { 2, 3, 4, 1, 2, 3 };
    int N = sizeof(A) / sizeof(int);

    // Function Call
    cout << countOddIntegers(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG{

// Function to find the count of distinct
// odd integers with N digits using the
// given digits in the array arr[]
static int countOddIntegers(int arr[], int N)
{

    // Stores the factorial of a number
    int Fact[] = new int[N];

    // Calculate the factorial of all
    // numbers from 1 to N
    Fact[0] = 1;
    for(int i = 1; i < N; i++)
    {
        Fact[i] = i * Fact[i - 1];
    }

    // Stores the frequency of each digit
    int freq[] = new int[10];
    for(int i = 0; i < N; i++)
    {
        freq[arr[i]]++;
    }

    // Stores the final answer
    int ans = 0;

    // Loop to iterate over all values of
    // Nth digit i and 1st digit j
    for(int i = 1; i <= 9; i += 2)
    {

        // If digit i does not exist in
        // the given array move to next i
        if (freq[i] == 0)
            continue;

        // Fixing i as Nth digit
        freq[i]--;

        for(int j = 1; j <= 9; j++)
        {

            // Stores the answer of a specific
            // value of i and j
            int cur_ans = 0;

            // If digit j does not exist
            // move to the next j
            if (freq[j] == 0)
            {
                continue;
            }

            // Fixing j as 1st digit
            freq[j]--;

            // Calculate number of ways to
            // arrange remaining N-2 digits
            cur_ans = Fact[N - 2];
            for(int k = 0; k <= 9; k++)
            {
                cur_ans = cur_ans / Fact[freq[k]];
            }
            ans += cur_ans;

            // Including j back into
            // the set of digits
            freq[j]++;
        }

        // Including i back into the
        // set of the digits
        freq[i]++;
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 2, 3, 4, 1, 2, 3 };
    int N = A.length;

    // Function Call
    System.out.print(countOddIntegers(A, N));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python Program for the above approach
from array import *
from math import *

# Function to find the count of distinct
# odd integers with N digits using the
# given digits in the array arr[]
def countOddIntegers(arr, N):

    # Stores the factorial of a number
    # Calculate the factorial of all
    # numbers from 1 to N
    Fact = [0] * N
    Fact[0] = 1
    for i in range(1,N):
        Fact[i] = i * Fact[i - 1]

    # Stores the frequency of each digit
    freq= [0] * 10
    for i in range(len(freq)):
        freq[i] = 0;
    for i in range(N):
        freq[arr[i]] = freq[arr[i]] + 1;

    # Stores the final answer
    ans = 0

    # Loop to iterate over all values of
    # Nth digit i and 1st digit j
    for i in range(1, 10, 2) :

        # If digit i does not exist in
        # the given array move to next i
        if (freq[i] == 0):
            continue

        # Fixing i as Nth digit
        freq[i] = freq[i] - 1;

        for j in range(1, 10, 1) :

            # Stores the answer of a specific
            # value of i and j
            cur_ans = 0

            # If digit j does not exist
            # move to the next j
            if (freq[j] == 0) :
                continue

            # Fixing j as 1st digit
            freq[j]=freq[j]-1;

            # Calculate number of ways to
            # arrange remaining N-2 digits
            cur_ans = Fact[N - 2]
            for k in range(10):
                cur_ans = cur_ans / Fact[freq[k]]

            ans += cur_ans

            # Including j back into
            # the set of digits
            freq[j] = freq[j] + 1;

        # Including i back into the
        # set of the digits
        freq[i] = freq[i] + 1;

    # Return Answer
    return ceil(ans)

# Driver Code
if __name__ ==  "__main__":
    A = [ 2, 3, 4, 1, 2, 3 ]
    N = len(A)

    # Function Call
    print(countOddIntegers(A, N))

    # This code is contributed by anudeep23042002.
```

## C#

```
// C# program of the above approach
using System;

class GFG{

// Function to find the count of distinct
// odd integers with N digits using the
// given digits in the array arr[]
static int countOddIntegers(int []arr, int N)
{

    // Stores the factorial of a number
    int []Fact = new int[N];

    // Calculate the factorial of all
    // numbers from 1 to N
    Fact[0] = 1;
    for(int i = 1; i < N; i++)
    {
        Fact[i] = i * Fact[i - 1];
    }

    // Stores the frequency of each digit
    int []freq = new int[10];
    for(int i = 0; i < N; i++)
    {
        freq[arr[i]]++;
    }

    // Stores the final answer
    int ans = 0;

    // Loop to iterate over all values of
    // Nth digit i and 1st digit j
    for(int i = 1; i <= 9; i += 2)
    {

        // If digit i does not exist in
        // the given array move to next i
        if (freq[i] == 0)
            continue;

        // Fixing i as Nth digit
        freq[i]--;

        for(int j = 1; j <= 9; j++)
        {

            // Stores the answer of a specific
            // value of i and j
            int cur_ans = 0;

            // If digit j does not exist
            // move to the next j
            if (freq[j] == 0)
            {
                continue;
            }

            // Fixing j as 1st digit
            freq[j]--;

            // Calculate number of ways to
            // arrange remaining N-2 digits
            cur_ans = Fact[N - 2];
            for(int k = 0; k <= 9; k++)
            {
                cur_ans = cur_ans / Fact[freq[k]];
            }
            ans += cur_ans;

            // Including j back into
            // the set of digits
            freq[j]++;
        }

        // Including i back into the
        // set of the digits
        freq[i]++;
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 2, 3, 4, 1, 2, 3 };
    int N = A.Length;

    // Function Call
    Console.Write(countOddIntegers(A, N));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the count of distinct
        // odd integers with N digits using the
        // given digits in the array arr[]
        function countOddIntegers(arr, N)
        {
            // Stores the factorial of a number
            let Fact = new Array(N);

            // Calculate the factorial of all
            // numbers from 1 to N
            Fact[0] = 1;
            for (let i = 1; i < N; i++) {
                Fact[i] = i * Fact[i - 1];
            }

            // Stores the frequency of each digit
            let freq = new Array(10).fill(0);
            for (let i = 0; i < N; i++) {
                freq[arr[i]]++;
            }

            // Stores the final answer
            let ans = 0;

            // Loop to iterate over all values of
            // Nth digit i and 1st digit j
            for (let i = 1; i <= 9; i += 2) {

                // If digit i does not exist in
                // the given array move to next i
                if (!freq[i]) {
                    continue;
                }

                // Fixing i as Nth digit
                freq[i]--;

                for (let j = 1; j <= 9; j++) {

                    // Stores the answer of a specific
                    // value of i and j
                    let cur_ans = 0;

                    // If digit j does not exist
                    // move to the next j
                    if (freq[j] == 0) {
                        continue;
                    }

                    // Fixing j as 1st digit
                    freq[j]--;

                    // Calculate number of ways to
                    // arrange remaining N-2 digits
                    cur_ans = Fact[N - 2];
                    for (let k = 0; k <= 9; k++) {
                        cur_ans = Math.floor(cur_ans / Fact[freq[k]]);
                    }
                    ans = ans + cur_ans;

                    // Including j back into
                    // the set of digits
                    freq[j]++;
                }
                // Including i back into the
                // set of the digits
                freq[i]++;
            }

            // Return Answer
            return ans;
        }

        // Driver Code

        let A = [2, 3, 4, 1, 2, 3];
        let N = A.length;

        // Function Call
        document.write(countOddIntegers(A, N));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
90
```

***时间复杂度:** O(N * 50)*
***辅助空间:** O(1)*