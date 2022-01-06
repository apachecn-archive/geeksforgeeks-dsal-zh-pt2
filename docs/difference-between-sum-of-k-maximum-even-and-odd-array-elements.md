# K 个最大奇偶数组元素之和的差值

> 原文:[https://www . geesforgeks . org/k 个最大奇偶数组元素之和之差/](https://www.geeksforgeeks.org/difference-between-sum-of-k-maximum-even-and-odd-array-elements/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个数字 **K** ，任务是求 **K 个最大偶数**和**个奇数**数组元素之和的绝对差。
**注:**数组中至少有 **K** 个偶、奇元素分别存在。

**示例:**

> **输入** arr[] = {1，2，3，4，5，6}，K = 2
> **输出:** 2
> **解释**:
> 2 个最大偶数为 6，4。总和是 6 + 4 = 10。
> 2 个最大奇数为 5、3。总和是 5 + 3 = 8。
> 差值= 10–8 = 2。
> 
> **输入** arr[] = {1，8，4，5，6，3}，K = 3
> **输出:** 4
> **解释**:
> 3 个最大偶数为 8，6，4。总和是 8 + 6 + 4 = 18。
> 3 个最大奇数为 5、3、1。总和是 5 + 3 + 1 = 9。
> 差值= 18–9 = 9。

**天真法:**最简单的方法是通过[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)找到 **K 个最大偶数**号和 **K 个最大奇数**号，打印得到的 K 个最大偶数和奇数元素之和的绝对差。

***时间复杂度:** O(N*K)*
***辅助空间:** O(1)*

**高效方法:**对上述方法进行优化，思路是利用[的概念，将数组分离为奇数和偶数](https://www.geeksforgeeks.org/segregate-even-and-odd-numbers/)，然后将数组按照降序分为两部分，分别包含偶数和奇数。按照以下步骤解决问题:

*   [分别分隔给定数组中的偶数和奇数](https://www.geeksforgeeks.org/segregate-even-odd-numbers-set-3/)并从奇数开始存储索引。
*   让奇数开始的索引为 **K** 。按降序排列范围**【0，K-1】**和**【K，N-1】**中的数字。
*   从数组开始和从奇数开始的第一个 **K 个**数的和分别是数组中第一个 **K 个最大值**偶数和奇数的和。
*   打印以上步骤中计算的总和之间的绝对差值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the absolute
// difference between sum of first K
// maximum even and odd numbers
void evenOddDiff(int a[], int n, int k)
{
    // Stores index from where odd
    // number starts
    int j = -1;

    // Segregate even and odd number
    for (int i = 0; i < n; i++) {

        // If current element is even
        if (a[i] % 2 == 0) {
            j++;
            swap(a[i], a[j]);
        }
    }

    j++;

    // Sort in decreasing order even part
    sort(a, a + j, greater<int>());

    // Sort in decreasing order odd part
    sort(a + j, a + n, greater<int>());

    int evenSum = 0, oddSum = 0;

    // Calculate sum of k
    // maximum even number
    for (int i = 0; i < k; i++) {
        evenSum += a[i];
    }

    // Calculate sum of k
    // maximum odd number
    for (int i = j; i < (j + k); i++) {
        oddSum += a[i];
    }

    // Print the absolute difference
    cout << abs(evenSum - oddSum);
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 8, 3, 4, 5 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    int K = 2;

    // Function Call
    evenOddDiff(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the absolute
// difference between sum of first K
// maximum even and odd numbers
static void evenOddDiff(int a[], int n, int k)
{

    // Stores index from where odd
    // number starts
    int j = -1;

    Vector<Integer> even = new Vector<>();
    Vector<Integer> odd = new Vector<>();

    // Segregate even and odd number
    for(int i = 0; i < n; i++)
    {

        // If current element is even
        if (a[i] % 2 == 0)
        {
            even.add(a[i]);
        }
        else
            odd.add(a[i]);
    }

    j++;

    // Sort in decreasing order even part
    Collections.sort(even);
    Collections.reverse(even);

    // Sort in decreasing order odd part
    Collections.sort(odd);
    Collections.reverse(odd);

    int evenSum = 0, oddSum = 0;

    // Calculate sum of k
    // maximum even number
    for(int i = 0; i < k; i++)
    {
        evenSum += even.get(i);
    }

    // Calculate sum of k
    // maximum odd number
    for(int i = 0; i < k; i++)
    {
        oddSum += odd.get(i);
    }

    // Print the absolute difference
    System.out.print(Math.abs(evenSum - oddSum));
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 8, 3, 4, 5 };

    // Size of array
    int N = arr.length;

    int K = 2;

    // Function Call
    evenOddDiff(arr, N, K);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the absolute
# difference between sum of first K
# maximum even and odd numbers
def evenOddDiff(a, n, k) :

    # Stores index from where odd
    # number starts
    j = -1

    even = []
    odd = []

    # Segregate even and odd number
    for i in range(n) :

        # If current element is even
        if (a[i] % 2 == 0) :

            even.append(a[i])
        else :
            odd.append(a[i])

    j += 1

    # Sort in decreasing order even part
    even.sort()
    even.reverse()

    # Sort in decreasing order odd part
    odd.sort()
    odd.reverse()

    evenSum, oddSum = 0, 0

    # Calculate sum of k
    # maximum even number
    for i in range(k) :

        evenSum += even[i]

    # Calculate sum of k
    # maximum odd number
    for i in range(k) :

        oddSum += odd[i]

    # Print the absolute difference
    print(abs(evenSum - oddSum))

# Given array []arr
arr = [ 1, 8, 3, 4, 5 ]

# Size of array
N = len(arr)

K = 2

# Function Call
evenOddDiff(arr, N, K)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the absolute
// difference between sum of first K
// maximum even and odd numbers
static void evenOddDiff(int []a, int n,
                        int k)
{

    // Stores index from where odd
    // number starts
    int j = -1;

    List<int> even = new List<int>();
    List<int> odd = new List<int>();

    // Segregate even and odd number
    for(int i = 0; i < n; i++)
    {

        // If current element is even
        if (a[i] % 2 == 0)
        {
            even.Add(a[i]);
        }
        else
            odd.Add(a[i]);
    }

    j++;

    // Sort in decreasing order even part
    even.Sort();
    even.Reverse();

    // Sort in decreasing order odd part
    odd.Sort();
    odd.Reverse();

    int evenSum = 0, oddSum = 0;

    // Calculate sum of k
    // maximum even number
    for(int i = 0; i < k; i++)
    {
        evenSum += even[i];
    }

    // Calculate sum of k
    // maximum odd number
    for(int i = 0; i < k; i++)
    {
        oddSum += odd[i];
    }

    // Print the absolute difference
    Console.Write(Math.Abs(evenSum - oddSum));
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 1, 8, 3, 4, 5 };

    // Size of array
    int N = arr.Length;

    int K = 2;

    // Function Call
    evenOddDiff(arr, N, K);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find the absolute
    // difference between sum of first K
    // maximum even and odd numbers
    function evenOddDiff(a , n , k) {

        // Stores index from where odd
        // number starts
        var j = -1;

        var even = [];
        var odd = [];

        // Segregate even and odd number
        for (i = 0; i < n; i++) {

            // If current element is even
            if (a[i] % 2 == 0) {
                even.push(a[i]);
            } else
                odd.push(a[i]);
        }

        j++;

        // Sort in decreasing order even part
        even.sort((a,b)=>a-b);
        even.reverse(even);

        // Sort in decreasing order odd part
        odd.sort((a,b)=>a-b);;
        odd.reverse();

        var evenSum = 0, oddSum = 0;

        // Calculate sum of k
        // maximum even number
        for (i = 0; i < k; i++) {
            evenSum += even[i];
        }

        // Calculate sum of k
        // maximum odd number
        for (i = 0; i < k; i++) {
            oddSum += odd[i];
        }

        // Prvar the absolute difference
        document.write(Math.abs(evenSum - oddSum));
    }

    // Driver Code

        // Given array arr
        var arr = [ 1, 8, 3, 4, 5 ];

        // Size of array
        var N = arr.length;

        var K = 2;

        // Function Call
        evenOddDiff(arr, N, K);

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N * log N+K)*
T5**辅助空间:** O(1)