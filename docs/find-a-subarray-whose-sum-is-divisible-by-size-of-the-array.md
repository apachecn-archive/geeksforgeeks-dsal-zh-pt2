# 找到一个和可以被数组大小整除的子数组

> 原文:[https://www . geesforgeks . org/find-a-subarray-其和可被数组大小整除/](https://www.geeksforgeeks.org/find-a-subarray-whose-sum-is-divisible-by-size-of-the-array/)

给定一个长度为 **N** 的数组 **arr[]** 。任务是检查是否有任何子阵列的和是 **N** 的倍数。如果存在这样的子阵列，则打印该子阵列的开始和结束索引，否则打印 **-1** 。如果有多个这样的子阵列，打印其中任何一个。

**示例:**

> **输入:** arr[] = {7，5，3，7}
> **输出:** 0 1
> 从索引 0 到 1 的子阵列是[7，5]
> 这个子阵列的和是 12，是 4 的倍数
> 
> **输入:** arr[] = {3，7，14}
> **输出:** 0 0

**天真方法:**天真方法是生成所有的子数组并计算它们的和。如果任何子阵列的总和是 N 的倍数，则返回起始和结束索引。

**时间复杂度:** O(N <sup>3</sup> )

**更好的方法:**更好的方法是维护前缀和数组，该数组存储所有先前元素的和。要计算指数 I 和 j 之间的子阵列之和，我们可以使用以下公式:

> 子数组和[i：j] = 假定[j]-假定[i-1]

现在检查每个子阵列的总和是否为 <sup>N</sup> 的倍数。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find a subarray
// whose sum is a multiple of N
void CheckSubarray(int arr[], int N)
{

    // Prefix sum array to store cumulative sum
    int presum[N + 1] = { 0 };

    // Single state dynamic programming
    // relation for prefix sum array
    for (int i = 1; i <= N; i += 1) {

        presum[i] = presum[i - 1] + arr[i - 1];
    }

    // Generating all sub-arrays
    for (int i = 1; i <= N; i += 1) {

        for (int j = i; j <= N; j += 1) {

            // If the sum of the sub-array[i:j]
            // is a multiple of N
            if ((presum[j] - presum[i - 1]) % N == 0) {
                cout << i - 1 << " " << j - 1;
                return;
            }
        }
    }

    // If the function reaches here it means
    // there are no subarrays with sum
    // as a multiple of N
    cout << -1;
}

// Driver code
int main()
{
    int arr[] = { 7, 5, 3, 7 };

    int N = sizeof(arr) / sizeof(arr[0]);

    CheckSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG
{

// Function to find a subarray
// whose sum is a multiple of N
static void CheckSubarray(int arr[], int N)
{

    // Prefix sum array to store cumulative sum
    int presum[] = new int[N + 1];

    // Single state dynamic programming
    // relation for prefix sum array
    for (int i = 1; i <= N; i += 1)
    {

        presum[i] = presum[i - 1] + arr[i - 1];
    }

    // Generating all sub-arrays
    for (int i = 1; i <= N; i += 1)
    {

        for (int j = i; j <= N; j += 1)
        {

            // If the sum of the sub-array[i:j]
            // is a multiple of N
            if ((presum[j] - presum[i - 1]) % N == 0)
            {
                System.out.print((i - 1) + " " + (j - 1));
                return;
            }
        }
    }

    // If the function reaches here it means
    // there are no subarrays with sum
    // as a multiple of N
    System.out.print(-1);
}

// Driver code
public static void main (String[] args)
{
    int []arr = { 7, 5, 3, 7 };

    int N = arr.length;

    CheckSubarray(arr, N);

}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to find a subarray
# whose sum is a multiple of N
def CheckSubarray(arr, N):

    # Prefix sum array to store cumulative sum
    presum=[0 for i in range(N + 1)]

    # Single state dynamic programming
    # relation for prefix sum array
    for i in range(1, N+1):
        presum[i] = presum[i - 1] + arr[i - 1]

    # Generating all sub-arrays
    for i in range(1, N+1):

        for j in range(i, N+1):

            # If the sum of the sub-array[i:j]
            # is a multiple of N
            if ((presum[j] - presum[i - 1]) % N == 0):
                print(i - 1,j - 1)
                return

    # If the function reaches here it means
    # there are no subarrays with sum
    # as a multiple of N
    print("-1")

# Driver code

arr = [ 7, 5, 3, 7]

N = len(arr)

CheckSubarray(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to find a subarray
// whose sum is a multiple of N
static void CheckSubarray(int []arr, int N)
{

    // Prefix sum array to store cumulative sum
    int []presum = new int[N + 1];

    // Single state dynamic programming
    // relation for prefix sum array
    for (int i = 1; i <= N; i += 1)
    {

        presum[i] = presum[i - 1] + arr[i - 1];
    }

    // Generating all sub-arrays
    for (int i = 1; i <= N; i += 1)
    {

        for (int j = i; j <= N; j += 1)
        {

            // If the sum of the sub-array[i:j]
            // is a multiple of N
            if ((presum[j] - presum[i - 1]) % N == 0)
            {
                Console.Write((i - 1) + " " + (j - 1));
                return;
            }
        }
    }

    // If the function reaches here it means
    // there are no subarrays with sum
    // as a multiple of N
    Console.Write(-1);
}

// Driver code
public static void Main ()
{
    int []arr = { 7, 5, 3, 7 };

    int N = arr.Length;

    CheckSubarray(arr, N);

}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to find a subarray
// whose sum is a multiple of N
function CheckSubarray(arr, N)
{

    // Prefix sum array to store cumulative sum
    let presum = new Array(N + 1).fill(0);

    // Single state dynamic programming
    // relation for prefix sum array
    for (let i = 1; i <= N; i += 1) {

        presum[i] = presum[i - 1] + arr[i - 1];
    }

    // Generating all sub-arrays
    for (let i = 1; i <= N; i += 1) {

        for (let j = i; j <= N; j += 1) {

            // If the sum of the sub-array[i:j]
            // is a multiple of N
            if ((presum[j] - presum[i - 1]) % N == 0) {
                document.write((i - 1) + " " + (j - 1));
                return;
            }
        }
    }

    // If the function reaches here it means
    // there are no subarrays with sum
    // as a multiple of N
    document.write(-1);
}

// Driver code
    let arr = [ 7, 5, 3, 7 ];

    let N = arr.length;

    CheckSubarray(arr, N);

</script>
```

**Output:** 

```
0 1
```

**时间复杂度:** O(N <sup>2</sup> )

**有效途径:**思路是利用鸽子洞原理。假设数组元素是一个 <sub>1</sub> ，一个<sub>2</sub>…一个 <sub>N</sub> 。
对于如下的数字序列:

> a <sub>1</sub> 、a <sub>1</sub> + a <sub>2</sub> 、a<sub>1</sub>+a<sub>2</sub>+a<sub>3</sub>、…、a<sub>1</sub>+a<sub>2</sub>+a<sub>3</sub>+…+a<sub>N</sub>

在上面的序列中，有 N 个术语。有两种可能的情况:

1.  如果上述前缀和之一是 **N** 的倍数，则打印**I<sup>th</sup>T5】子阵列指数。**
2.  如果上述序列元素都不在 **N** 的 **0** 模类中，那么就剩下**(N–1)**模类了。通过**鸽子洞原理**，有 **N** 鸽子(前缀和序列的元素)和**(N–1)**洞(模类)，我们可以说至少有两个元素位于同一个模类中。这两个元素之间的差异将产生一个子阵列，其总和将是 **N** 的倍数。

可以看出，总是有可能得到这样的子阵列。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check is there exists a
// subarray whose sum is a multiple of N
void CheckSubarray(int arr[], int N)
{

    // Prefix sum array to store cumulative sum
    int presum[N + 1] = { 0 };

    // Single state dynamic programming
    // relation for prefix sum array
    for (int i = 1; i <= N; i += 1) {

        presum[i] = presum[i - 1] + arr[i - 1];
    }

    // Modulo class vector
    vector<int> moduloclass[N];

    // Storing the index value in the modulo class vector
    for (int i = 1; i <= N; i += 1) {
        moduloclass[presum[i] % N].push_back(i - 1);
    }

    // If there exists a sub-array with
    // starting index equal to zero
    if (moduloclass[0].size() > 0) {
        cout << 0 << " " << moduloclass[0][0];
        return;
    }

    for (int i = 1; i < N; i += 1) {

        // In this class, there are more than two presums%N
        // Hence difference of any two subarrays would be a
        // multiple of N
        if (moduloclass[i].size() >= 2) {

            // 0 based indexing
            cout << moduloclass[i][0] + 1 << " " << moduloclass[i][1];
            return;
        }
    }
}

// Driver code
int main()
{
    int arr[] = { 7, 3, 5, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    CheckSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{

// Function to check is there exists a
// subarray whose sum is a multiple of N
static void CheckSubarray(int arr[], int N)
{

    // Prefix sum array to store cumulative sum
    int[] presum = new int[N + 1];

    // Single state dynamic programming
    // relation for prefix sum array
    for (int i = 1; i <= N; i += 1)
    {
        presum[i] = presum[i - 1] + arr[i - 1];
    }

    // Modulo class vector
    Vector<Integer>[] moduloclass = new Vector[N];
    for (int i = 0; i < N; i += 1)
    {
        moduloclass[i] = new Vector<>();
    }

    // Storing the index value
    // in the modulo class vector
    for (int i = 1; i <= N; i += 1)
    {
        moduloclass[presum[i] % N].add(i - 1);
    }

    // If there exists a sub-array with
    // starting index equal to zero
    if (moduloclass[0].size() > 0)
    {
        System.out.print(0 + " " +
               moduloclass[0].get(0));
        return;
    }

    for (int i = 1; i < N; i += 1)
    {

        // In this class, there are more than
        // two presums%N. Hence difference of
        // any two subarrays would be a multiple of N
        if (moduloclass[i].size() >= 2)
        {

            // 0 based indexing
            System.out.print(moduloclass[i].get(0) + 1 +
                       " " + moduloclass[i].get(1));
            return;
        }
    }
}

// Driver code
public static void main(String args[])
{
    int arr[] = {7, 3, 5, 2};

    int N = arr.length;

    CheckSubarray(arr, N);
}                    
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to check is there exists a
# subarray whose sum is a multiple of N
def CheckSubarray(arr, N):
    # Prefix sum array to store cumulative sum
    presum = [0 for i in range(N+1)]

    # Single state dynamic programming
    # relation for prefix sum array
    for i in range(1,N+1):
        presum[i] = presum[i - 1] + arr[i - 1]

    # Modulo class vector
    moduloclass = [[]]*N

    # Storing the index value in the modulo class vector
    for i in range(1,N+1,1):
        moduloclass[presum[i] % N].append(i - 1)

    # If there exists a sub-array with
    # starting index equal to zero
    if (len(moduloclass[0]) > 0):
        print(0+1,moduloclass[0][0]+2)
        return

    for i in range(1,N):
        # In this class, there are more than two presums%N
        # Hence difference of any two subarrays would be a
        # multiple of N
        if (len(moduloclass[i]) >= 2):
            # 0 based indexing
            print(moduloclass[i][0] + 1,moduloclass[i][1])
            return
# Driver code
if __name__ == '__main__':
    arr = [7, 3, 5, 2]

    N = len(arr)

    CheckSubarray(arr, N)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to check is there exists a
// subarray whose sum is a multiple of N
static void CheckSubarray(int []arr, int N)
{

    // Prefix sum array to store cumulative sum
    int[] presum = new int[N + 1];

    // Single state dynamic programming
    // relation for prefix sum array
    for (int i = 1; i <= N; i += 1)
    {
        presum[i] = presum[i - 1] + arr[i - 1];
    }

    // Modulo class vector
    List<int>[] moduloclass = new List<int>[N];
    for (int i = 0; i < N; i += 1)
    {
        moduloclass[i] = new List<int>();
    }

    // Storing the index value
    // in the modulo class vector
    for (int i = 1; i <= N; i += 1)
    {
        moduloclass[presum[i] % N].Add(i - 1);
    }

    // If there exists a sub-array with
    // starting index equal to zero
    if (moduloclass[0].Count > 0)
    {
        Console.Write(0 + " " +
            moduloclass[0][0]);
        return;
    }

    for (int i = 1; i < N; i += 1)
    {

        // In this class, there are more than
        // two presums%N. Hence difference of
        // any two subarrays would be a multiple of N
        if (moduloclass[i].Count >= 2)
        {

            // 0 based indexing
            Console.Write(moduloclass[i][0] + 1 +
                    " " + moduloclass[i][1]);
            return;
        }
    }
}

// Driver code
public static void Main(String []args)
{
    int []arr = {7, 3, 5, 2};

    int N = arr.Length;

    CheckSubarray(arr, N);
}                    
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to check is there exists a
// subarray whose sum is a multiple of N
function CheckSubarray(arr, N)
{

    // Prefix sum array to store cumulative sum
    let presum = new Array(N + 1);
     for(let i = 0; i < (N + 1); i++)
        presum[i] = 0;

    // Single state dynamic programming
    // relation for prefix sum array
    for(let i = 1; i <= N; i += 1)
    {
        presum[i] = presum[i - 1] + arr[i - 1];
    }

    // Modulo class vector
    let moduloclass = new Array(N);
    for(let i = 0; i < N; i += 1)
    {
        moduloclass[i] = [];
    }

    // Storing the index value
    // in the modulo class vector
    for(let i = 1; i <= N; i += 1)
    {
        moduloclass[presum[i] % N].push(i - 1);
    }

    // If there exists a sub-array with
    // starting index equal to zero
    if (moduloclass[0].length > 0)
    {
        document.write(0 + " " +
                       moduloclass[0][0]);
        return;
    }

    for(let i = 1; i < N; i += 1)
    {

        // In this class, there are more than
        // two presums%N. Hence difference of
        // any two subarrays would be a multiple of N
        if (moduloclass[i].length >= 2)
        {

            // 0 based indexing
            document.write(moduloclass[i][0] + 1 +
                     " " + moduloclass[i][1]);
            return;
        }
    }
}

// Driver code
let arr = [ 7, 3, 5, 2 ];
let N = arr.length;

CheckSubarray(arr, N);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
1 2
```

**时间复杂度:** O(N)