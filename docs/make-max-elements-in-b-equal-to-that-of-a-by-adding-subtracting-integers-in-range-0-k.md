# 通过加减[0，K]

范围内的整数，使 B[]中的最大元素等于 A[]中的最大元素

> 原文:[https://www . geesforgeks . org/make-max-elements-in-b-等于 a-的加减整数范围-0-k/](https://www.geeksforgeeks.org/make-max-elements-in-b-equal-to-that-of-a-by-adding-subtracting-integers-in-range-0-k/)

给定两个数组 **A[]** 和 **B[]** 以及一个整数 **K** ，任务是通过加减**【0，K】**范围内的任意整数，最大化数组 **B[]** 中可以与数组 **A[]** 相等的整数个数。

**示例:**

> **输入:** K=5，A[]=【100，65，35，85，55】，B[]=【30，60，75，95】
> **输出:** 3
> **解释:**
> 30 + 5，60 + 5，95 + 5 给出的值与数组 A[]的少数元素相等。
> 
> **输入:** K = 5，A[] = [10，20，30，40，50]，B[] = [1，20，3]
> **输出:** 1
> **说明:**
> 只有第 2 个值可以相等，因为它的值[20]可以通过加/减 0 来更改为[20]。

**方法:**思路是检查数组 **B[]** 元素与数组 **A[]** 任意元素的绝对差值是否小于等于 **K** 。如果是的话，就把这个算进去。在检查数组中所有元素的上述条件后，打印所有此类元素的计数 **B[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that count the number of
// integers from array B[] such that
// subtracting element in the range
// [0, K] given any element in A[]
void countElement(int A[], int N,
                  int B[], int M, int K)
{

    // To store the count of element
    int cnt = 0;

    // Traverse the array B[]
    for (int i = 0; i < M; i++) {

        int currentElement = B[i];

        // Traverse the array A[]
        for (int j = 0; j < N; j++) {

            // Find the difference
            int diff
                = abs(currentElement - A[j]);

            // If difference is atmost
            // K then increment the cnt
            if (diff <= K) {
                cnt++;
                break;
            }
        }
    }

    // Print the count
    cout << cnt;
}

// Driver Code
int main()
{
    // Given array A[] and B[]
    int A[] = { 100, 65, 35, 85, 55 };
    int B[] = { 30, 60, 75, 95 };

    // Given K
    int K = 5;

    int N = sizeof(A) / sizeof(A[0]);
    int M = sizeof(B) / sizeof(B[0]);

    // Function Call
    countElement(A, N, B, M, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function that count the number of
// integers from array B[] such that
// subtracting element in the range
// [0, K] given any element in A[]
static void countElement(int A[], int N,
                         int B[], int M, int K)
{

    // To store the count of element
    int cnt = 0;

    // Traverse the array B[]
    for(int i = 0; i < M; i++)
    {
        int currentElement = B[i];

        // Traverse the array A[]
        for(int j = 0; j < N; j++)
        {

            // Find the difference
            int diff = Math.abs(
                       currentElement - A[j]);

            // If difference is atmost
            // K then increment the cnt
            if (diff <= K)
            {
                cnt++;
                break;
            }
        }
    }

    // Print the count
    System.out.print(cnt);
}

// Driver Code
public static void main(String[] args)
{

    // Given array A[] and B[]
    int A[] = { 100, 65, 35, 85, 55 };
    int B[] = { 30, 60, 75, 95 };

    // Given K
    int K = 5;

    int N = A.length;
    int M = B.length;

    // Function call
    countElement(A, N, B, M, K);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function that count the number of
# integers from array B such that
# subtracting element in the range
# [0, K] given any element in A
def countElement(A, N, B, M, K):

    # To store the count of element
    cnt = 0

    # Traverse the array B
    for i in range(M):
        currentElement = B[i]

        # Traverse the array A
        for j in range(N):

            # Find the difference
            diff = abs(currentElement - A[j])

            # If difference is atmost
            # K then increment the cnt
            if(diff <= K):
                cnt += 1
                break

    # Print the count
    print(cnt)

# Driver Code
if __name__ == '__main__':

    # Given array A and B
    A = [ 100, 65, 35, 85, 55 ]
    B = [ 30, 60, 75, 95 ]

    N = len(A)
    M = len(B)

    # Given K
    K = 5

    # Function call
    countElement(A, N, B, M, K)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function that count the number of
// integers from array []B such that
// subtracting element in the range
// [0, K] given any element in []A
static void countElement(int []A, int N,
                         int []B, int M, int K)
{

    // To store the count of element
    int cnt = 0;

    // Traverse the array []B
    for(int i = 0; i < M; i++)
    {
        int currentElement = B[i];

        // Traverse the array []A
        for(int j = 0; j < N; j++)
        {

            // Find the difference
            int diff = Math.Abs(
                       currentElement - A[j]);

            // If difference is atmost
            // K then increment the cnt
            if (diff <= K)
            {
                cnt++;
                break;
            }
        }
    }

    // Print the count
    Console.Write(cnt);
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []A and []B
    int []A = { 100, 65, 35, 85, 55 };
    int []B = { 30, 60, 75, 95 };

    // Given K
    int K = 5;

    int N = A.Length;
    int M = B.Length;

    // Function call
    countElement(A, N, B, M, K);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
// Javascript Script program to implement
// the above approach

// Function that count the number of
// integers from array B[] such that
// subtracting element in the range
// [0, K] given any element in A[]
function countElement(A, N, B, M, K)
{

    // To store the count of element
    let cnt = 0;

    // Traverse the array B[]
    for(let i = 0; i < M; i++)
    {
        let currentElement = B[i];

        // Traverse the array A[]
        for(let j = 0; j < N; j++)
        {

            // Find the difference
            let diff = Math.abs(
                       currentElement - A[j]);

            // If difference is atmost
            // K then increment the cnt
            if (diff <= K)
            {
                cnt++;
                break;
            }
        }
    }

    // Print the count
    document.write(cnt);
}

// Driver Code

    // Given array A[] and B[]
    let A = [ 100, 65, 35, 85, 55 ];
    let B = [ 30, 60, 75, 95 ];

    // Given K
    let K = 5;

    let N = A.length;
    let M = B.length;

    // Function call
    countElement(A, N, B, M, K);

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*M)，其中 N 和 M 是数组 A[]和 B[]的长度。*
***辅助空间:** O(1)*