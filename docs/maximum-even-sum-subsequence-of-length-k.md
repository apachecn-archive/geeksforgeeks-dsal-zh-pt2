# 长度为 K 的最大偶和子序列

> 原文:[https://www . geesforgeks . org/最大偶数和长度子序列-k/](https://www.geeksforgeeks.org/maximum-even-sum-subsequence-of-length-k/)

给定一个由 **N** 个正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是找到大小为 **K** 的任意[个子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大可能**偶和**。如果找不到任何大小为 **K** 的偶数和子序列，则打印 **-1** 。

**示例:**

> **输入:** arr[] ={4，2，6，7，8}，K = 3
> **输出:** 18
> **说明:**大小 K( = 3)的最大偶和的子序列为{4，6，8}。
> 因此，要求的输出为 4 + 6 + 8 = 18。
> 
> **输入:** arr[] = {5，5，1，1，3}，K = 3
> T3】输出: -1

**朴素方法:**解决这个问题最简单的方法是[从给定的数组中生成大小为 K](https://www.geeksforgeeks.org/print-all-sequences-of-given-length/) 的所有可能的子序列，并打印给定数组的可能子序列的最大可能偶和的值。

***时间复杂度:**O(K * N<sup>K</sup>)*
***辅助空间:** O(K)*

**高效方法:**为了优化上述方法，我们的想法是将给定数组的所有 e [偶数和奇数存储到两个独立的数组中，然后](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)[对这两个数组](https://www.geeksforgeeks.org/sorting-algorithms/)进行排序。最后，使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)计算尺寸 **K** 的最大和偶子序列。按照以下步骤解决问题:

*   初始化一个变量，比如 **maxSum** 来存储给定数组的子序列的最大偶数和。
*   初始化两个数组，比如**偶数[]** 和**奇数[]** 分别存储给定数组的所有偶数和奇数。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，将给定数组的所有[偶数和奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)分别存储到**偶数[]** 和**奇数[]** 数组中。
*   排序**偶[]****奇[]** 数组。
*   初始化两个变量，说 **i** 和 **j** 分别存储**偶[]** 和**奇[]** 数组的索引。
*   遍历**偶[]** 、**奇[]** 数组，检查以下条件:
    *   如果 **K % 2 == 1** ，则将 **maxSum** 的值增加**偶数【I】**。
    *   否则，将 **maxSum** 的值增加 **max(偶数[i] +偶数[I–1]、奇数[j] +奇数[j–1])**。
*   最后打印 **maxSum** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// maximum even sum of any
// subsequence of length K
int evenSumK(int arr[], int N, int K)
{

    // If count of elements
    // is less than K
    if (K > N) {
        return -1;
    }

    // Stores maximum
    // even subsequence sum
    int maxSum = 0;

    // Stores Even numbers
    vector<int> Even;

    // Stores Odd numbers
    vector<int> Odd;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If current element
        // is an odd number
        if (arr[i] % 2) {

            // Insert odd number
            Odd.push_back(arr[i]);
        }
        else {

            // Insert even numbers
            Even.push_back(arr[i]);
        }
    }

    // Sort Odd[] array
    sort(Odd.begin(), Odd.end());

    // Sort Even[] array
    sort(Even.begin(), Even.end());

    // Stores current index
    // Of Even[] array
    int i = Even.size() - 1;

    // Stores current index
    // Of Odd[] array
    int j = Odd.size() - 1;

    while (K > 0) {

        // If K is odd
        if (K % 2 == 1) {

            // If count of elements
            // in Even[] >= 1
            if (i >= 0) {

                // Update maxSum
                maxSum += Even[i];

                // Update i
                i--;
            }

            // If count of elements
            // in Even[] array is 0.
            else {
                return -1;
            }

            // Update K
            K--;
        }

        // If count of elements
        // in Even[] and odd[] >= 2
        else if (i >= 1 && j >= 1) {

            if (Even[i] + Even[i - 1]
                <= Odd[j] + Odd[j - 1]) {

                // Update maxSum
                maxSum += Odd[j] + Odd[j - 1];

                // Update j.
                j -= 2;
            }
            else {

                // Update maxSum
                maxSum += Even[i] + Even[i - 1];

                // Update i
                i -= 2;
            }

            // Update K
            K -= 2;
        }

        // If count of elements
        // in Even[] array >= 2.
        else if (i >= 1) {

            // Update maxSum
            maxSum += Even[i] + Even[i - 1];

            // Update i.
            i -= 2;

            // Update K.
            K -= 2;
        }

        // If count of elements
        // in Odd[] array >= 1
        else if (j >= 1) {

            // Update maxSum
            maxSum += Odd[j] + Odd[j - 1];

            // Update i.
            j -= 2;

            // Update K.
            K -= 2;
        }
    }

    return maxSum;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 10, 3, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;
    cout << evenSumK(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG {

    // Function to find the
    // maximum even sum of any
    // subsequence of length K
    static int evenSumK(int arr[], int N, int K)
    {

        // If count of elements
        // is less than K
        if (K > N) {
            return -1;
        }

        // Stores maximum even
        // subsequence sum
        int maxSum = 0;

        // Stores Even numbers
        ArrayList<Integer> Even = new ArrayList<Integer>();

        // Stores Odd numbers
        ArrayList<Integer> Odd = new ArrayList<Integer>();

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // If current element
            // is an odd number
            if (arr[i] % 2 == 1) {

                // Insert odd number
                Odd.add(arr[i]);
            }
            else {

                // Insert even numbers
                Even.add(arr[i]);
            }
        }

        // Sort Odd[] array
        Collections.sort(Odd);

        // Sort Even[] array
        Collections.sort(Even);

        // Stores current index
        // Of Even[] array
        int i = Even.size() - 1;

        // Stores current index
        // Of Odd[] array
        int j = Odd.size() - 1;

        while (K > 0) {

            // If K is odd
            if (K % 2 == 1) {

                // If count of elements
                // in Even[] >= 1
                if (i >= 0) {

                    // Update maxSum
                    maxSum += Even.get(i);

                    // Update i
                    i--;
                }

                // If count of elements
                // in Even[] array is 0.
                else {
                    return -1;
                }

                // Update K
                K--;
            }

            // If count of elements
            // in Even[] and odd[] >= 2
            else if (i >= 1 && j >= 1) {
                if (Even.get(i) + Even.get(i - 1)
                    <= Odd.get(j) + Odd.get(j - 1)) {

                    // Update maxSum
                    maxSum += Odd.get(j) + Odd.get(j - 1);

                    // Update j
                    j -= 2;
                }
                else {

                    // Update maxSum
                    maxSum += Even.get(i) + Even.get(i - 1);

                    // Update i
                    i -= 2;
                }

                // Update K
                K -= 2;
            }

            // If count of elements
            // in Even[] array >= 2.
            else if (i >= 1) {

                // Update maxSum
                maxSum += Even.get(i) + Even.get(i - 1);

                // Update i
                i -= 2;

                // Update K
                K -= 2;
            }

            // If count of elements
            // in Odd[] array >= 1
            else if (j >= 1) {

                // Update maxSum
                maxSum += Odd.get(j) + Odd.get(j - 1);

                // Update i.
                j -= 2;

                // Update K.
                K -= 2;
            }
        }
        return maxSum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 4, 10, 3, 5 };
        int N = arr.length;
        int K = 3;

        System.out.println(evenSumK(arr, N, K));
    }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the
# maximum even sum of any
# subsequence of length K

def evenSumK(arr, N, K):

    # If count of elements
    # is less than K
    if (K > N):
        return -1

    # Stores maximum
    # even subsequence sum
    maxSum = 0

    # Stores Even numbers
    Even = []

    # Stores Odd numbers
    Odd = []

    # Traverse the array
    for i in range(N):

        # If current element
        # is an odd number
        if (arr[i] % 2):

            # Insert odd number
            Odd.append(arr[i])

        else:

            # Insert even numbers
            Even.append(arr[i])

    # Sort Odd[] array
    Odd.sort(reverse=False)

    # Sort Even[] array
    Even.sort(reverse=False)

    # Stores current index
    # Of Even[] array
    i = len(Even) - 1

    # Stores current index
    # Of Odd[] array
    j = len(Odd) - 1

    while (K > 0):

        # If K is odd
        if (K % 2 == 1):

            # If count of elements
            # in Even[] >= 1
            if (i >= 0):

                # Update maxSum
                maxSum += Even[i]

                # Update i
                i -= 1

            # If count of elements
            # in Even[] array is 0.
            else:
                return -1

            # Update K
            K -= 1

        # If count of elements
        # in Even[] and odd[] >= 2
        elif (i >= 1 and j >= 1):
            if (Even[i] + Even[i - 1] <=
                    Odd[j] + Odd[j - 1]):

                # Update maxSum
                maxSum += Odd[j] + Odd[j - 1]

                # Update j.
                j -= 2

            else:

                # Update maxSum
                maxSum += Even[i] + Even[i - 1]

                # Update i
                i -= 2

            # Update K
            K -= 2

        # If count of elements
        # in Even[] array >= 2.
        elif (i >= 1):

            # Update maxSum
            maxSum += Even[i] + Even[i - 1]

            # Update i.
            i -= 2

            # Update K.
            K -= 2

        # If count of elements
        # in Odd[] array >= 2
        elif (j >= 1):

            # Update maxSum
            maxSum += Odd[j] + Odd[j - 1]

            # Update i.
            j -= 2

            # Update K.
            K -= 2

    return maxSum

# Driver Code
if __name__ == '__main__':

    arr = [2, 4, 10, 3, 5]
    N = len(arr)
    K = 3

    print(evenSumK(arr, N, K))

# This code is contributed by ipg2016107
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the
    // maximum even sum of any
    // subsequence of length K
    static int evenSumK(int[] arr, int N, int K)
    {
        // If count of elements
        // is less than K
        if (K > N) {
            return -1;
        }

        // Stores maximum even
        // subsequence sum
        int maxSum = 0;

        // Stores Even numbers
        List<int> Even = new List<int>();

        // Stores Odd numbers
        List<int> Odd = new List<int>();

        // Traverse the array
        for (int l = 0; l < N; l++) {
            // If current element
            // is an odd number
            if (arr[l] % 2 == 1) {
                // Insert odd number
                Odd.Add(arr[l]);
            }
            else {
                // Insert even numbers
                Even.Add(arr[l]);
            }
        }

        // Sort Odd[] array
        Odd.Sort();

        // Sort Even[] array
        Even.Sort();

        // Stores current index
        // Of Even[] array
        int i = Even.Count - 1;

        // Stores current index
        // Of Odd[] array
        int j = Odd.Count - 1;

        while (K > 0) {
            // If K is odd
            if (K % 2 == 1) {
                // If count of elements
                // in Even[] >= 1
                if (i >= 0) {
                    // Update maxSum
                    maxSum += Even[i];

                    // Update i
                    i--;
                }

                // If count of elements
                // in Even[] array is 0.
                else {
                    return -1;
                }

                // Update K
                K--;
            }

            // If count of elements
            // in Even[] and odd[] >= 2
            else if (i >= 1 && j >= 1) {
                if (Even[i] + Even[i - 1]
                    <= Odd[j] + Odd[j - 1]) {
                    // Update maxSum
                    maxSum += Odd[j] + Odd[j - 1];

                    // Update j
                    j -= 2;
                }
                else {
                    // Update maxSum
                    maxSum += Even[i] + Even[i - 1];

                    // Update i
                    i -= 2;
                }

                // Update K
                K -= 2;
            }

            // If count of elements
            // in Even[] array >= 2.
            else if (i >= 1) {
                // Update maxSum
                maxSum += Even[i] + Even[i - 1];

                // Update i
                i -= 2;

                // Update K
                K -= 2;
            }

            // If count of elements
            // in Odd[] array >= 2
            else if (j >= 1) {
                // Update maxSum
                maxSum += Odd[j] + Odd[j - 1];

                // Update i.
                j -= 2;

                // Update K.
                K -= 2;
            }
        }
        return maxSum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 2, 4, 10, 3, 5 };
        int N = arr.Length;
        int K = 3;
        Console.WriteLine(evenSumK(arr, N, K));
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the
// maximum even sum of any
// subsequence of length K
function evenSumK(arr, N, K)
{

    // If count of elements
    // is less than K
    if (K > N) {
        return -1;
    }

    // Stores maximum
    // even subsequence sum
    var maxSum = 0;

    // Stores Even numbers
    var Even = [];

    // Stores Odd numbers
    var Odd = [];

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // If current element
        // is an odd number
        if (arr[i] % 2) {

            // Insert odd number
            Odd.push(arr[i]);
        }
        else {

            // Insert even numbers
            Even.push(arr[i]);
        }
    }

    // Sort Odd[] array
    Odd.sort((a,b)=> a-b);
    Even.sort((a,b)=> a-b);

    // Stores current index
    // Of Even[] array
    var i = Even.length - 1;

    // Stores current index
    // Of Odd[] array
    var j = Odd.length - 1;

    while (K > 0) {

        // If K is odd
        if (K % 2 == 1) {

            // If count of elements
            // in Even[] >= 1
            if (i >= 0) {

                // Update maxSum
                maxSum += Even[i];

                // Update i
                i--;
            }

            // If count of elements
            // in Even[] array is 0.
            else {
                return -1;
            }

            // Update K
            K--;
        }

        // If count of elements
        // in Even[] and odd[] >= 2
        else if (i >= 1 && j >= 1) {

            if (Even[i] + Even[i - 1]
                <= Odd[j] + Odd[j - 1]) {

                // Update maxSum
                maxSum += Odd[j] + Odd[j - 1];

                // Update j.
                j -= 2;
            }
            else {

                // Update maxSum
                maxSum += Even[i] + Even[i - 1];

                // Update i
                i -= 2;
            }

            // Update K
            K -= 2;
        }

        // If count of elements
        // in Even[] array >= 2.
        else if (i >= 1) {

            // Update maxSum
            maxSum += Even[i] + Even[i - 1];

            // Update i.
            i -= 2;

            // Update K.
            K -= 2;
        }

        // If count of elements
        // in Odd[] array >= 1
        else if (j >= 1) {

            // Update maxSum
            maxSum += Odd[j] + Odd[j - 1];

            // Update i.
            j -= 2;

            // Update K.
            K -= 2;
        }
    }

    return maxSum;
}

// Driver Code
var arr = [2, 4, 10, 3, 5];
var N = arr.length;
var K = 3;
document.write( evenSumK(arr, N, K));

</script>
```

**Output**

```
18
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*