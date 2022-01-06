# 三胞胎计数至 N，其乘积最多为 N

> 原文:[https://www . geeksforgeeks . org/三胞胎计数-直到-n-谁的产品最多-n/](https://www.geeksforgeeks.org/count-of-triplets-till-n-whose-product-is-at-most-n/)

给定一个正整数 **N** ，任务是从第一个 N [自然数](https://www.geeksforgeeks.org/natural-numbers/)中找出三元组 **(A，B，C)** 的个数，使得 **A * B * C ≤ N** 。

**示例:**

> **输入:** N = 3
> **输出:** 4
> **解释:**
> 以下是满足给定标准的三元组:
> 
> 1.  ( 1, 1, 1 ) => 1 * 1 * 1 = 1 ≤ 2.
> 2.  ( 1, 1, 2 ) => 1 * 1 * 2 = 2 ≤ 2.
> 3.  ( 1, 2, 1 ) => 1 * 2 * 1 = 2 ≤ 2.
> 4.  ( 2, 1, 1 ) => 2 * 1 * 1 = 2 ≤ 2.
> 
> 因此，三胞胎的总数是 4。
> 
> **输入:**N = 10
> T3】输出: 53

**天真方法:**解决给定问题的最简单方法是从第一个 **N** 自然数生成所有可能的三元组，并对那些满足给定标准的三元组进行计数。检查所有三胞胎后，打印获得的总数。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过观察进行优化，如果 **A** 和 **B** 固定，那么可以通过做 **N/(A*B)** 来计算 **C** 的所有可能选择，因为 **N/(A*B)** 将给出最大值，比如说 **X** ，与 **(A*B)** 相乘得到的值更小所以 **C** 所有可能的选择都是从 **1** 到 **X** 。现在 **A** 和 **B** 可以通过尝试 **A** 到 **N** 的每一个可能的数字，以及 **B** 到 **(N/A)** 的每一个可能的数字来固定。按照以下步骤解决给定的问题:

*   初始化变量，将 **cnt** 设为 **0** ，存储可能的三胞胎数量。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**上迭代一个循环，使用变量 **j** 在范围**【1，N】**上嵌套迭代，并将 **cnt** 的值增加 **cnt/(i*j)** 的值。
*   完成上述步骤后，打印 **cnt** 的值作为结果。

以下是该方法的实施情况:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find number of triplets
// (A, B, C) having A * B * C <= N
int countTriplets(int N)
{
    // Stores the count of triplets
    int cnt = 0;

    // Iterate a loop fixing the value
    // of A
    for (int A = 1; A <= N; ++A) {

        // Iterate a loop fixing the
        // value of A
        for (int B = 1; B <= N / A; ++B) {

            // Find the total count of
            // triplets and add it to cnt
            cnt += N / (A * B);
        }
    }

    // Return the total triplets formed
    return cnt;
}

// Driver Code
int main()
{
    int N = 2;
    cout << countTriplets(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

    // Function to find number of triplets
    // (A, B, C) having A * B * C <= N
    static int countTriplets(int N)
    {

        // Stores the count of triplets
        int cnt = 0;

        // Iterate a loop fixing the value
        // of A
        for (int A = 1; A <= N; ++A) {

            // Iterate a loop fixing the
            // value of A
            for (int B = 1; B <= N / A; ++B) {

                // Find the total count of
                // triplets and add it to cnt
                cnt += N / (A * B);
            }
        }

        // Return the total triplets formed
        return cnt;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 2;

        System.out.println(countTriplets(N));
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find number of triplets
# (A, B, C) having A * B * C <= N
def countTriplets(N) :

    # Stores the count of triplets
    cnt = 0;

    # Iterate a loop fixing the value
    # of A
    for A in range( 1, N + 1) :

        # Iterate a loop fixing the
        # value of A
        for B in range(1, N // A + 1) :

            # Find the total count of
            # triplets and add it to cnt
            cnt += N // (A * B);

    # Return the total triplets formed
    return cnt;

# Driver Code
if __name__ == "__main__" :

    N = 2;
    print(countTriplets(N));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to find number of triplets
    // (A, B, C) having A * B * C <= N
    static int countTriplets(int N)
    {

        // Stores the count of triplets
        int cnt = 0;

        // Iterate a loop fixing the value
        // of A
        for (int A = 1; A <= N; ++A) {

            // Iterate a loop fixing the
            // value of A
            for (int B = 1; B <= N / A; ++B) {

                // Find the total count of
                // triplets and add it to cnt
                cnt += N / (A * B);
            }
        }

        // Return the total triplets formed
        return cnt;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int N = 2;

        Console.WriteLine(countTriplets(N));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find number of triplets
        // (A, B, C) having A * B * C <= N
        function countTriplets(N) {
            // Stores the count of triplets
            let cnt = 0;

            // Iterate a loop fixing the value
            // of A
            for (let A = 1; A <= N; ++A) {

                // Iterate a loop fixing the
                // value of A
                for (let B = 1; B <= N / A; ++B) {

                    // Find the total count of
                    // triplets and add it to cnt
                    cnt += N / (A * B);
                }
            }

            // Return the total triplets formed
            return cnt;
        }

        // Driver Code

        let N = 2;
        document.write(countTriplets(N));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*