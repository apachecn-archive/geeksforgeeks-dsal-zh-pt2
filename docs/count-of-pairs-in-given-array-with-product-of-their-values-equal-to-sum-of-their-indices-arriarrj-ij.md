# 给定数组中其值的乘积等于其索引之和的对的计数(arr[i]*arr[j] = i+j)

> 原文:[https://www . geesforgeks . org/给定数组中的对计数与它们的值的乘积等于它们的指数之和-arriarj-ij/](https://www.geeksforgeeks.org/count-of-pairs-in-given-array-with-product-of-their-values-equal-to-sum-of-their-indices-arriarrj-ij/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ,其具有从 1 到 2*N 的不同整数，任务是计算指数对的数量 **(i，j)** ，使得 **(i < j)** 和 **arr[i] * arr[j] = i + j** ，即计算指数对的数量，使得它们的乘积等于它们的指数之和。

**示例:**

> **输入:** N = 5，arr[] = {3，1，5，9，2}
> **输出:** 3
> **解释:**有三对(I，j)这样(i < j)和 arr[i] * arr[j] = i + j (1，2)，(1，5)，(2，3)
> 
> **输入:** N = 3，arr[] = {6，1，5 }
> T3】输出: 1

**天真方法:** [用 **(i < j)** 对所有指数对 **(i，j)** 进行迭代](https://www.geeksforgeeks.org/iterators-c-stl/)，如果满足上述条件，则检查每对，然后将答案增加 1，否则进入下一对。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// unique pairs
int NumberOfRequiredPairs(int arr[], int N)
{

    // Variable that with stores number
    // of valid pairs
    int ans = 0;

    // Traverse the array for every
    // possible index i
    for (int i = 0; i < N; i++)

        // Traverse the array for every
        // possible j (i < j)
        // Please note that the indices
        // are used as 1 based indexing
        for (int j = i + 1; j < N; j++)
            if ((arr[i] * arr[j])
                == ((i + 1) + (j + 1)))
                ans++;

    // Return the ans
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int N = 5;
    int arr[] = { 3, 1, 5, 9, 2 };

    // Function Call
    cout << NumberOfRequiredPairs(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

// Function to find the number of
// unique pairs
static int NumberOfRequiredPairs(int arr[], int N)
{

    // Variable that with stores number
    // of valid pairs
    int ans = 0;

    // Traverse the array for every
    // possible index i
    for (int i = 0; i < N; i++)

        // Traverse the array for every
        // possible j (i < j)
        // Please note that the indices
        // are used as 1 based indexing
        for (int j = i + 1; j < N; j++)
            if ((arr[i] * arr[j])
                == ((i + 1) + (j + 1)))
                ans++;

    // Return the ans
    return ans;
}

// Driver code
public static void main (String[] args)
{

    // Given Input
    int N = 5;
    int arr[] = { 3, 1, 5, 9, 2 };

    // Function Call
    System.out.println(NumberOfRequiredPairs(arr, N));
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the number of
# unique pairs
def NumberOfRequiredPairs(arr, N):

    # Variable that with stores number
    # of valid pairs
    ans = 0

    # Traverse the array for every
    # possible index i
    for i in range(N):

        # Traverse the array for every
        # possible j (i < j)
        # Please note that the indices
        # are used as 1 based indexing
        for j in range(i + 1, N):
            if ((arr[i] * arr[j]) == ((i + 1) + (j + 1))):
                ans += 1

    # Return the ans
    return ans

# Driver Code
# Given Input
N = 5
arr = [3, 1, 5, 9, 2]

# Function Call
print(NumberOfRequiredPairs(arr, N))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find the number of
// unique pairs
static int NumberOfRequiredPairs(int []arr, int N)
{

    // Variable that with stores number
    // of valid pairs
    int ans = 0;

    // Traverse the array for every
    // possible index i
    for (int i = 0; i < N; i++)

        // Traverse the array for every
        // possible j (i < j)
        // Please note that the indices
        // are used as 1 based indexing
        for (int j = i + 1; j < N; j++)
            if ((arr[i] * arr[j])
                == ((i + 1) + (j + 1)))
                ans++;

    // Return the ans
    return ans;
}

// Driver code
public static void  Main ()
{

    // Given Input
    int N = 5;
    int []arr = { 3, 1, 5, 9, 2 };

    // Function Call
    Console.Write(NumberOfRequiredPairs(arr, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the number of
// unique pairs
function NumberOfRequiredPairs(arr, N)
{

    // Variable that with stores number
    // of valid pairs
    let ans = 0;

    // Traverse the array for every
    // possible index i
    for (let i = 0; i < N; i++)

        // Traverse the array for every
        // possible j (i < j)
        // Please note that the indices
        // are used as 1 based indexing
        for (let j = i + 1; j < N; j++)
            if ((arr[i] * arr[j])
                == ((i + 1) + (j + 1)))
                ans++;

    // Return the ans
    return ans;
}

// Driver Code
// Given Input
let N = 5;
let arr = [ 3, 1, 5, 9, 2 ];

// Function Call
document.write(NumberOfRequiredPairs(arr, N));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
3
```

***时间复杂度:** O(N^2)*
***辅助空间:** O(1)*

**有效方法:**将上述条件改写为

> arr[j] = (i + j)/arr[i]

因此，对于 **arr[i]，**的每个倍数，找到各自的 **j** ，检查 **arr[j]** 是否等于 **(i + j)/ arr[i]。**这种方法是有效的，因为对于每个 **i** ，需要经过多个 **i** 直到 **2*N** 。由于数组中的所有数字都是**不同的**，因此可以得出计算 **j** 的总迭代次数如下:

> N + N/2 + N/3 + N/4 + N/5……

这是众所周知的 **logN** 系列展开的结果。欲了解更多信息，请阅读此处。按照以下步骤解决问题:

*   将变量**和**初始化为 **0** 来存储答案。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   将变量 **k** 初始化为**arr【I】的值。**
    *   [循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **k** 小于等于 **2*N** 并执行以下任务:
        *   将变量 **j** 初始化为 **k-i-1。**
        *   如果 **j** 大于等于 **1** 且小于等于 **N** 和**arr【j–1】**等于**k/arr【I】****j**大于 **i+1，**则将 **ans** 的值增加 **1。**
*   执行上述步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// unique pairs
int NumberOfRequiredPairs(int arr[], int N)
{

    // Variable that with stores
    // number of valid pairs
    int ans = 0;

    // Traverse the array for every
    // possible index i
    for (int i = 0; i < N; i++) {

        // Initialize a dummy variable
        // for arr[i]
        int k = arr[i];

        // We will loop through every
        // multiple of arr[i];
        // Looping through 2*N because
        // the maximum element
        // in array can be 2*N
        // Please not that i and j are
        // in 1 based indexing
        while (k <= 2 * N) {

            // Calculating j
            int j = k - i - 1;

            // Now check if this j lies
            // between the bounds
            // of the array
            if (j >= 1 && j <= N) {

                // Checking the required
                // condition
                if ((arr[j - 1] == k / arr[i])
                    && j > i + 1) {
                    ans++;
                }
            }

            // Increasing k to its next multiple
            k += arr[i];
        }
    }

    // Return the ans
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int N = 5;
    int arr[] = { 3, 1, 5, 9, 2 };

    // Function Call
    cout << NumberOfRequiredPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

// Function to find the number of
// unique pairs
static int NumberOfRequiredPairs(int arr[], int N)
{

    // Variable that with stores
    // number of valid pairs
    int ans = 0;

    // Traverse the array for every
    // possible index i
    for (int i = 0; i < N; i++) {

        // Initialize a dummy variable
        // for arr[i]
        int k = arr[i];

        // We will loop through every
        // multiple of arr[i];
        // Looping through 2*N because
        // the maximum element
        // in array can be 2*N
        // Please not that i and j are
        // in 1 based indexing
        while (k <= 2 * N) {

            // Calculating j
            int j = k - i - 1;

            // Now check if this j lies
            // between the bounds
            // of the array
            if (j >= 1 && j <= N) {

                // Checking the required
                // condition
                if ((arr[j - 1] == k / arr[i])
                    && j > i + 1) {
                    ans++;
                }
            }

            // Increasing k to its next multiple
            k += arr[i];
        }
    }

    // Return the ans
    return ans;
}

// Driver code
public static void main (String args[])
{

    // Given Input
    int N = 5;
    int arr[] = { 3, 1, 5, 9, 2 };

    // Function Call
    System.out.println(NumberOfRequiredPairs(arr, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of
# unique pairs
def NumberOfRequiredPairs(arr, N) :

    # Variable that with stores
    # number of valid pairs
    ans = 0;

    # Traverse the array for every
    # possible index i
    for i in range(N) :

        # Initialize a dummy variable
        # for arr[i]
        k = arr[i];

        # We will loop through every
        # multiple of arr[i];
        # Looping through 2*N because
        # the maximum element
        # in array can be 2*N
        # Please not that i and j are
        # in 1 based indexing
        while (k <= 2 * N) :

            # Calculating j
            j = k - i - 1;

            # Now check if this j lies
            # between the bounds
            # of the array
            if (j >= 1 and j <= N) :

                # Checking the required
                # condition
                if ((arr[j - 1] == k // arr[i]) and j > i + 1) :
                    ans += 1;

            # Increasing k to its next multiple
            k += arr[i];

    # Return the ans
    return ans;

# Driver Code
if __name__ == "__main__" :

    # Given Input
    N = 5;
    arr = [ 3, 1, 5, 9, 2 ];

    # Function Call
    print(NumberOfRequiredPairs(arr, N));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find the number of
// unique pairs
static int NumberOfRequiredPairs(int []arr, int N)
{

    // Variable that with stores
    // number of valid pairs
    int ans = 0;

    // Traverse the array for every
    // possible index i
    for (int i = 0; i < N; i++) {

        // Initialize a dummy variable
        // for arr[i]
        int k = arr[i];

        // We will loop through every
        // multiple of arr[i];
        // Looping through 2*N because
        // the maximum element
        // in array can be 2*N
        // Please not that i and j are
        // in 1 based indexing
        while (k <= 2 * N) {

            // Calculating j
            int j = k - i - 1;

            // Now check if this j lies
            // between the bounds
            // of the array
            if (j >= 1 && j <= N) {

                // Checking the required
                // condition
                if ((arr[j - 1] == k / arr[i])
                    && j > i + 1) {
                    ans++;
                }
            }

            // Increasing k to its next multiple
            k += arr[i];
        }
    }

    // Return the ans
    return ans;
}

// Driver code
public static void  Main ()
{

    // Given Input
    int N = 5;
    int []arr = { 3, 1, 5, 9, 2 };

    // Function Call
    Console.Write(NumberOfRequiredPairs(arr, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the number of
// unique pairs
function NumberOfRequiredPairs(arr, N)
{

    // Variable that with stores
    // number of valid pairs
    let ans = 0;

    // Traverse the array for every
    // possible index i
    for (let i = 0; i < N; i++) {

        // Initialize a dummy variable
        // for arr[i]
        let k = arr[i];

        // We will loop through every
        // multiple of arr[i];
        // Looping through 2*N because
        // the maximum element
        // in array can be 2*N
        // Please not that i and j are
        // in 1 based indexing
        while (k <= 2 * N) {

            // Calculating j
            let j = k - i - 1;

            // Now check if this j lies
            // between the bounds
            // of the array
            if (j >= 1 && j <= N) {

                // Checking the required
                // condition
                if ((arr[j - 1] == k / arr[i])
                    && j > i + 1) {
                    ans++;
                }
            }

            // Increasing k to its next multiple
            k += arr[i];
        }
    }

    // Return the ans
    return ans;
}

// Driver Code
// Given Input
let N = 5;
let arr = [ 3, 1, 5, 9, 2 ];

// Function Call
document.write(NumberOfRequiredPairs(arr, N));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
3
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*