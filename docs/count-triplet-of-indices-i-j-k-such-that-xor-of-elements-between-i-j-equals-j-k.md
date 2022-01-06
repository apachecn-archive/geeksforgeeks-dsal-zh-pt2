# 计数三个索引(I，j，k)，使得[i，j]之间的元素的异或等于[j，k]

> 原文:[https://www . geeksforgeeks . org/count-索引三元组-I-j-k-这样-I-j-之间的元素异或-等于-j-k/](https://www.geeksforgeeks.org/count-triplet-of-indices-i-j-k-such-that-xor-of-elements-between-i-j-equals-j-k/)

给定整数数组 **Arr** 。任务是计算三胞胎 **(i，j，k)** 的数量，使得**a<sub>I</sub>^ a<sub>I+1</sub>^ a<sub>I+2</sub>^。^ a<sub>j-1</sub>= a<sub>j</sub>^ a<sub>j+1</sub>^ a<sub>j+2</sub>^…..^ a<sub>k</sub>t21、 **0 < (i，j，k) < N** ，其中 **N** 为阵的大小。
其中 **^** 是两个数的**按位异或**。
**举例:**** 

> **输入:**arr =【5，2，7】
> **输出:** 2
> **解释:**
> 这三胞胎是(0，2，2)自 5 ^ 2 = 7 和(0，1，2)自 2 ^ 7 = 5。
> **输入:** Arr = [3，6，12，8，6，2，1，5]
> **输出:** 6

**接近**T2】

*   让我们简化给定的表达式:

```
Ai ^ Ai + 1 ^ ...Aj - 1 = Aj ^ Aj + 1 ^ ...Ak

Taking XOR with Aj ^ Aj + 1 ^ ...Ak on both sides

Ai ^ Ai + 1 ^ ...Aj - 1 ^ Aj ^ Aj + 1 ^ ...Ak = 0
```

*   因此，具有异或 0 的子阵列[i，k]将具有**k–I**三元组，因为可以从[i+1，k]中选择任何 j，并且三元组将满足条件。

*   现在问题简化为寻找异或为 0 的所有子阵列的长度，对于每个这样的长度 L，在答案中加上 L–1。

*   在前缀异或阵列中，如果在 2 个索引处，比如说 L 和 R，前缀异或值是相同的——那么这意味着子阵列[L + 1，R]的异或= 0。

*   为了找到计数，我们将存储以下内容:

```
Say we are at index i, and the prefix XOR at i = x.

count[x] = Frequency of x in prefix XOR array before i

ways[x] -> For each all j < i, if prefixXor[j] = x,
then ways[x] += (j+1)
```

*   这些可以用来计算三胞胎，使用公式:

```
Triplets += count[x] * i  - ways[x]
```

以下是上述方法的实现:

## C++

```
// C++ program  to count the Number of
// triplets in array having subarray
// XOR equal
#include <bits/stdc++.h>
using namespace std;

// Function return the count of
// triplets having subarray XOR equal
int CountOfTriplets(int a[], int n)
{
    int answer = 0;

    // XOR value till i
    int x = 0;

    // Count and ways array as defined
    // above
    int count[100005] = { 0 };
    int ways[100005] = { 0 };

    for (int i = 0; i < n; i++)
    {
        x ^= a[i];

        // Using the formula stated
        answer += count[x] * i - ways[x];

        // Increase the frequency of x
        count[x]++;

        // Add i+1 to ways[x] for upcoming
        // indices
        ways[x] += (i + 1);
    }
    return answer;
}

// Driver code
int main()
{

    int Arr[] = { 3, 6, 12, 8, 6, 2, 1, 5 };

    int N = sizeof(Arr) / sizeof(Arr[0]);

    cout << CountOfTriplets(Arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the Number of
// triplets in array having subarray
// XOR equal
import java.io.*;
import java.util.Arrays;
import java.util.ArrayList;
import java.lang.*;
import java.util.Collections;

class GFG
{

// Function return the count of
// triplets having subarray XOR equal
static int CountOfTriplets(int a[], int n)
{
    int answer = 0;

    // XOR value till i
    int x = 0;

    // Count and ways array as defined
    // above
    int count[] = new int[100005];
    int ways[] = new int[100005];

    for (int i = 0; i < n; i++)
    {
        x ^= a[i];

        // Using the formula stated
        answer += count[x] * i - ways[x];

        // Increase the frequency of x
        count[x]++;

        // Add i+1 to ways[x] for upcoming
        // indices
        ways[x] += (i + 1);
    }
    return answer;
}

// Driver code
public static void main(String[] args)
{

    int Arr[] = { 3, 6, 12, 8, 6, 2, 1, 5 };

    int N = Arr.length;

    System.out.print(CountOfTriplets(Arr, N));

}
}
// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program  to count the Number of
# triplets in array having subarray
# XOR equal

# Function return the count of
# triplets having subarray XOR equal
def CountOfTriplets(a,n):
    answer = 0

    # XOR value till i
    x = 0

    # Count and ways array as defined
    # above
    count = [0 for i in range(100005)]
    ways = [0 for i in range(100005)]

    for i in range(n):
        x ^= a[i]

        # Using the formula stated
        answer += count[x] * i - ways[x]

        # Increase the frequency of x
        count[x] += 1

        # Add i+1 to ways[x] for upcoming
        # indices
        ways[x] += (i + 1)
    return answer

# Driver code
if __name__ == '__main__':
    Arr =  [3, 6, 12, 8, 6, 2, 1, 5]

    N = len(Arr)

    print(CountOfTriplets(Arr, N))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program to count the Number of
// triplets in array having subarray
// XOR equal
using System;

class GFG {

// Function return the count of
// triplets having subarray XOR equal
static int CountOfTriplets(int []a, int n)
{
    int answer = 0;

    // XOR value till i
    int x = 0;

    // Count and ways array as defined
    // above
    int []count = new int[100005];
    int []ways = new int[100005];

    for(int i = 0; i < n; i++)
    {
       x ^= a[i];

       // Using the formula stated
       answer += count[x] * i - ways[x];

       // Increase the frequency of x
       count[x]++;

       // Add i+1 to ways[x] for upcoming
       // indices
       ways[x] += (i + 1);
    }

    return answer;
}

// Driver code
public static void Main(String[] args)
{

    int []Arr = { 3, 6, 12, 8, 6, 2, 1, 5 };
    int N = Arr.Length;

    Console.Write(CountOfTriplets(Arr, N));

}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

    // Javascript program  to count the Number of
    // triplets in array having subarray
    // XOR equal

    // Function return the count of
    // triplets having subarray XOR equal
    function CountOfTriplets(a, n)
    {
        let answer = 0;

        // XOR value till i
        let x = 0;

        // Count and ways array as defined
        // above
        let count = new Array(100005);
        let ways = new Array(100005);
        count.fill(0);
        ways.fill(0);

        for (let i = 0; i < n; i++)
        {
            x ^= a[i];

            // Using the formula stated
            answer += count[x] * i - ways[x];

            // Increase the frequency of x
            count[x]++;

            // Add i+1 to ways[x] for upcoming
            // indices
            ways[x] = ways[x] + i + 1;
        }
        return answer;
    }

    let Arr = [ 3, 6, 12, 8, 6, 2, 1, 5 ];

    let N = Arr.length;

    document.write(CountOfTriplets(Arr, N));

</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(N)