# Q 查询给定范围内两个 1 之间 0 的最大计数

> 原文:[https://www . geeksforgeeks . org/q 查询给定范围内 0 到 2-1 的最大计数/](https://www.geeksforgeeks.org/maximum-count-of-0s-between-two-1s-in-given-range-for-q-queries/)

给定大小为 **N** 的二进制[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，以及由形式为 **{L，R}** 的 **M** 对组成的查询的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)**Q[[]**，每个查询的任务是找出位于范围**【L，R】**中的两个 **1s 之间的最大数量 **0s****

**示例:**

> **输入:**S =“1001010”，Q[][] = {{0，4}，{0，5}}
> **输出:**2 3
> T6】说明:
> 查询按以下方式进行:
> 
> 1.  *查询(0，4): 打印 2，因为在[0，4]范围内，即“10010”，子串中的索引 0 和 3 之间最多有 2 个 0。*
> 2.  *查询(0，5): 打印 3，因为在[0，5]即“100101”的范围内，子串中的索引 0 和 5 之间最多有 3 个 0。*
> 
> **输入:**S =“111”，Q[][] = {{0，2 } }
> T3】输出: 0

**天真方法:**解决给定问题的最简单方法是遍历给定的查询数组 **Q[][]** ，并通过在范围**【L，R】**上迭代，为每个查询打印任意两对 **1s 之间的最大数量 **0s** 。**

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的概念进行优化，这将导致查询的恒定时间计算。按照以下步骤解决问题:

*   初始化两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)表示**左界[]** 和**右界[]** 到分别存储最近的 **1s** 右侧的 **0s** 的计数和最近的 **1s** 左侧的 **0s** 的计数。
*   初始化两个变量，比如**计数**和**总计**来更新数组**左绑定[]** 和**右绑定[]** 。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-the-characters-of-a-string-in-java/) **S** ，如果当前字符为“ **1** ，则将 **curr** 的值分配给变量 **total** 。否则，将**总计**增加 **1** ，然后将**电流**的值分配给**右界【I】**。
*   将 **curr** 和**总计**的值更新为 **0** 。
*   [以](https://www.geeksforgeeks.org/iterate-over-the-characters-of-a-string-in-java/)[相反的顺序](https://www.geeksforgeeks.org/collections-reverseorder-java-examples/)遍历字符串，在每次迭代中，如果当前字符是“ **1** ，则将 **curr** 的值更新为**总计**。否则，将**总计**的值增加 **1** ，然后将**电流**的值更新为**左侧的**。
*   完成上述步骤后，[遍历给定的查询数组](https://www.geeksforgeeks.org/iterating-arrays-java/)**Q[][]**，并为每个查询打印**的值(左界[Q[i][0]] +右界[Q[I][1]]–总计)**作为 **0s** 的最大结果数。

下面是上述方法的实现:

## C++

```
#include <iostream>
using namespace std;

// Function to count the number of
// 0s lying between the two 1s for
// each query
void countOsBetween1s(string S, int N, int Q[][2])
{

    // Stores count of 0's that are
    // right to the most recent 1's
    int leftBound[N];

    // Stores count of 0's that are
    // left to the most recent 1's
    int rightBound[N];

    // Stores the count of zeros
    // in a prefix/suffix of array
    int count = 0;

    // Stores the count of total 0s
    int total = 0;

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // If current character is
        // '1'
        if (S[i] == '1') {
            count = total;
        }

        // Otherwise
        else if (S[i] == '0') {
            total++;
        }

        // Update the rightBound[i]
        rightBound[i] = count;
    }

    // Update count and total to 0
    count = 0;
    total = 0;

    // Traverse the string S in
    // reverse manner
    for (int i = N - 1; i >= 0; i--) {

        // If current character is
        // '1'
        if (S[i] == '1') {
            count = total;
        }

        // Otherwise
        else if (S[i] == '0') {
            total++;
        }

        // Update the leftBound[i]
        leftBound[i] = count;
    }

    // Traverse given query array
    for (int q = 0; q < 2; q++) {

        int L = Q[q][0];
        int R = Q[q][1];

        // Update the value of count
        count = leftBound[L] + rightBound[R] - total;

        // Print the count as the
        // result to the current
        // query [L, R]
        cout << count << " ";
    }
}

// Driver Code
int main()
{

    string S = "1001010";
    int Q[][2] = { { 0, 4 }, { 0, 5 } };
    int N = S.length();
    countOsBetween1s(S, N, Q);
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.lang.*;
import java.util.*;

class GFG {

    // Function to count the number of
    // 0s lying between the two 1s for
    // each query
    static void countOsBetween1s(
        String S, int N, int[][] Q)
    {

        // Stores count of 0's that are
        // right to the most recent 1's
        int[] leftBound = new int[N];

        // Stores count of 0's that are
        // left to the most recent 1's
        int[] rightBound = new int[N];

        // Stores the count of zeros
        // in a prefix/suffix of array
        int count = 0;

        // Stores the count of total 0s
        int total = 0;

        // Traverse the string S
        for (int i = 0; i < N; i++) {

            // If current character is
            // '1'
            if (S.charAt(i) == '1') {
                count = total;
            }

            // Otherwise
            else if (S.charAt(i) == '0') {
                total++;
            }

            // Update the rightBound[i]
            rightBound[i] = count;
        }

        // Update count and total to 0
        count = 0;
        total = 0;

        // Traverse the string S in
        // reverse manner
        for (int i = N - 1; i >= 0; i--) {

            // If current character is
            // '1'
            if (S.charAt(i) == '1') {
                count = total;
            }

            // Otherwise
            else if (S.charAt(i) == '0') {
                total++;
            }

            // Update the leftBound[i]
            leftBound[i] = count;
        }

        // Traverse given query array
        for (int q = 0; q < Q.length; q++) {

            int L = Q[q][0];
            int R = Q[q][1];

            // Update the value of count
            count = leftBound[L] + rightBound[R] - total;

            // Print the count as the
            // result to the current
            // query [L, R]
            System.out.print(count + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "1001010";
        int Q[][] = { { 0, 4 }, { 0, 5 } };
        int N = S.length();
        countOsBetween1s(S, N, Q);
    }
}
```

## 蟒蛇 3

```
# Function to count the number of
# 0s lying between the two 1s for
# each query
def countOsBetween1s(S, N, Q):

    # Stores count of 0's that are
    # right to the most recent 1's
    leftBound = [0]*N

    # Stores count of 0's that are
    # left to the most recent 1's
    rightBound = [0]*N

    # Stores the count of zeros
    # in a prefix/suffix of array
    count = 0

    # Stores the count of total 0s
    total = 0

    # Traverse the string S
    for i in range(N):

        # If current character is
        # '1'
        if (S[i] == '1'):
            count = total

        # Otherwise
        elif (S[i] == '0'):
            total += 1

        # Update the rightBound[i]
        rightBound[i] = count

    # Update count and total to 0
    count = 0
    total = 0

    # Traverse the string S in
    # reverse manner
    for i in range(N - 1, -1, -1):

        # If current character is
        # '1'
        if (S[i] == '1'):
            count = total

        # Otherwise
        elif (S[i] == '0'):
            total += 1

        # Update the leftBound[i]
        leftBound[i] = count

    # Traverse given query array
    for q in range(2):

        L = Q[q][0]
        R = Q[q][1]

        # Update the value of count
        count = leftBound[L] + rightBound[R] - total

        # Print the count as the
        # result to the current
        # query [L, R]
        print(count, end=" ")

# Driver Code
if __name__ == "__main__":

    S = "1001010"
    Q = [[0, 4], [0, 5]]
    N = len(S)
    countOsBetween1s(S, N, Q)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to count the number of
    // 0s lying between the two 1s for
    // each query
    static void countOsBetween1s(
        String S, int N, int[,] Q)
    {

        // Stores count of 0's that are
        // right to the most recent 1's
        int[] leftBound = new int[N];

        // Stores count of 0's that are
        // left to the most recent 1's
        int[] rightBound = new int[N];

        // Stores the count of zeros
        // in a prefix/suffix of array
        int count = 0;

        // Stores the count of total 0s
        int total = 0;

        // Traverse the string S
        for (int i = 0; i < N; i++) {

            // If current character is
            // '1'
            if (S[i] == '1') {
                count = total;
            }

            // Otherwise
            else if (S[i] == '0') {
                total++;
            }

            // Update the rightBound[i]
            rightBound[i] = count;
        }

        // Update count and total to 0
        count = 0;
        total = 0;

        // Traverse the string S in
        // reverse manner
        for (int i = N - 1; i >= 0; i--) {

            // If current character is
            // '1'
            if (S[i] == '1') {
                count = total;
            }

            // Otherwise
            else if (S[i] == '0') {
                total++;
            }

            // Update the leftBound[i]
            leftBound[i] = count;
        }

        // Traverse given query array
        for (int q = 0; q < Q.GetLength(0); q++) {

            int L = Q[q,0];
            int R = Q[q,1];

            // Update the value of count
            count = leftBound[L] + rightBound[R] - total;

            // Print the count as the
            // result to the current
            // query [L, R]
            Console.Write(count + " ");
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String S = "1001010";
        int [,]Q = { { 0, 4 }, { 0, 5 } };
        int N = S.Length;
        countOsBetween1s(S, N, Q);
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Function to count the number of
// 0s lying between the two 1s for
// each query
function countOsBetween1s(S, N, Q) {

    // Stores count of 0's that are
    // right to the most recent 1's
    let leftBound = new Array(N);

    // Stores count of 0's that are
    // left to the most recent 1's
    let rightBound = new Array(N);

    // Stores the count of zeros
    // in a prefix/suffix of array
    let count = 0;

    // Stores the count of total 0s
    let total = 0;

    // Traverse the string S
    for (let i = 0; i < N; i++) {

        // If current character is
        // '1'
        if (S[i] == '1') {
            count = total;
        }

        // Otherwise
        else if (S[i] == '0') {
            total++;
        }

        // Update the rightBound[i]
        rightBound[i] = count;
    }

    // Update count and total to 0
    count = 0;
    total = 0;

    // Traverse the string S in
    // reverse manner
    for (let i = N - 1; i >= 0; i--) {

        // If current character is
        // '1'
        if (S[i] == '1') {
            count = total;
        }

        // Otherwise
        else if (S[i] == '0') {
            total++;
        }

        // Update the leftBound[i]
        leftBound[i] = count;
    }

    // Traverse given query array
    for (let q = 0; q < 2; q++) {

        let L = Q[q][0];
        let R = Q[q][1];

        // Update the value of count
        count = leftBound[L] + rightBound[R] - total;

        // Print the count as the
        // result to the current
        // query [L, R]
        document.write(count + " ");
    }
}

// Driver Code

let S = "1001010";
let Q = [[0, 4], [0, 5]];
let N = S.length;
countOsBetween1s(S, N, Q);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
2 3
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N)*