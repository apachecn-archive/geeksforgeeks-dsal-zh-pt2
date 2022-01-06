# 通过最多加或减 K 使数组的所有元素相等

> 原文:[https://www . geeksforgeeks . org/通过最多加或减 k 使数组的所有元素相等/](https://www.geeksforgeeks.org/make-all-elements-of-an-array-equal-by-adding-or-subtracting-at-most-k/)

给定一个包含大小为 **N** 的正整数和一个整数 **K** 的数组 **arr[]** ，任务是使数组中的所有元素等于某个值 **D (D > 0)** ，使得**| arr[I]–D |≤K**。如果无法使数组相等，打印 **D** 或 **-1** 的值。
**举例:**

> **输入:** arr[] = {1，2，3，4，5}， K = 2
> **输出:** 3
> **说明:**
> 数组中的所有元素都可以等于 3 作为:
> | arr[0]–3 | = 2≤2
> | arr[1]–3 | = 1≤2
> | arr[2]–3 | = 0≤2
> | arr[3]–3 | = 1≤2
> | arr[4]–3 | = 2≤2
> T11

**方法:**思路是先找到数组的最小元素。

*   如果 **M** 是数组的最小元素，那么 **M + K** 是这个最小元素可以取的最大可能值，以满足条件**arr[I]–D≤K**。
*   然后， **D = M + K** ，如果对于数组中的所有元素，(M + K)位于范围**【arr[I]–K，arr[I]+K】**内。
*   因此，我们只需迭代数组中的每个元素，并检查这种情况。

以下是上述方法的实现:

## C++

```
// C++ program to make all elements
// of an Array equal by adding or
// subtracting at most K

#include <bits/stdc++.h>
using namespace std;

// Function to equalize the array by
// adding or subtracting at most K
// value from each element
int equalize(int arr[], int n, int k)
{

    // Finding the minimum element
    // from the array
    int min_ele
        = *min_element(arr, arr + n);

    // Boolean variable to check if the
    // array can be equalized or not
    bool flag = true;

    // Traversing the array
    for (int i = 0; i < n; i++) {

        // Checking if the values lie
        // within the possible range
        // for each element
        if (!((arr[i] + k) >= min_ele + k
              && min_ele + k >= (arr[i] - k))) {

            // If any value doesn't lie in
            // the range then exit the loop
            flag = false;
            break;
        }
    }

    if (flag) {

        // Value after equalizing the array
        return min_ele + k;
    }

    // Array cannot be equalized
    else
        return -1;
}

// Driver code
int main()
{
    int K = 2;
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << equalize(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make all elements
// of an Array equal by adding or
// subtracting at most K
import java.util.*;

class GFG{

// Function to equalize the array by
// adding or subtracting at most K
// value from each element
static int equalize(int arr[], int n, int k)
{

    // Finding the minimum element
    // from the array
    int min_ele
        = Arrays.stream(arr).min().getAsInt();

    // Boolean variable to check if the
    // array can be equalized or not
    boolean flag = true;

    // Traversing the array
    for (int i = 0; i < n; i++) {

        // Checking if the values lie
        // within the possible range
        // for each element
        if (!((arr[i] + k) >= min_ele + k
              && min_ele + k >= (arr[i] - k))) {

            // If any value doesn't lie in
            // the range then exit the loop
            flag = false;
            break;
        }
    }

    if (flag) {

        // Value after equalizing the array
        return min_ele + k;
    }

    // Array cannot be equalized
    else
        return -1;
}

// Driver code
public static void main(String[] args)
{
    int K = 2;
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = arr.length;

    System.out.print(equalize(arr, N, K));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python program to make all elements
# of an Array equal by adding or
# subtracting at most K

# Function to equalize the array by
# adding or subtracting at most K
# value from each element
def equalize(arr, n, k):

    # Finding the minimum element
    # from the array
    min_ele = min(arr);

    # Boolean variable to check if the
    # array can be equalized or not
    flag = True;

    # Traversing the array
    for i in range(n):

        # Checking if the values lie
        # within the possible range
        # for each element
        if (not((arr[i] + k) >= (min_ele + k) and
            (min_ele + k) >= (arr[i] - k))) :

            # If any value doesn't lie in
            # the range then exit the loop
            flag = False;
            break;

    if (flag):

        # Value after equalizing the array
        return min_ele + k;

    # Array cannot be equalized
    else:
        return -1;

# Driver code
if __name__=='__main__':

    K = 2;
    arr = [ 1, 2, 3, 4, 5] ;
    N = len(arr)

    print(equalize(arr, N, K))

# This code is contributed by Princi Singh
```

## C#

```
// C# program to make all elements
// of an Array equal by adding or
// subtracting at most K
using System;
using System.Linq;

class GFG{

// Function to equalize the array by
// adding or subtracting at most K
// value from each element
static int equalize(int []arr, int n, int k)
{

    // Finding the minimum element
    // from the array
    int min_ele = arr.Min();

    // Boolean variable to check if the
    // array can be equalized or not
    bool flag = true;

    // Traversing the array
    for (int i = 0; i < n; i++) {

        // Checking if the values lie
        // within the possible range
        // for each element
        if (!((arr[i] + k) >= min_ele + k
              && min_ele + k >= (arr[i] - k))) {

            // If any value doesn't lie in
            // the range then exit the loop
            flag = false;
            break;
        }
    }

    if (flag) {

        // Value after equalizing the array
        return min_ele + k;
    }

    // Array cannot be equalized
    else
        return -1;
}

// Driver code
public static void Main(String[] args)
{
    int K = 2;
    int []arr = { 1, 2, 3, 4, 5 };
    int N = arr.Length;

    Console.Write(equalize(arr, N, K));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to make all elements
// of an Array equal by adding or
// subtracting at most K

// Function to equalize the array by
// adding or subtracting at most K
// value from each element
function equalize(arr, n, k)
{

    // Finding the minimum element
    // from the array
    let min_ele
        = arr.sort((a, b) => a - b)[0];

    // Boolean variable to check if the
    // array can be equalized or not
    let flag = true;

    // Traversing the array
    for (let i = 0; i < n; i++) {

        // Checking if the values lie
        // within the possible range
        // for each element
        if (!((arr[i] + k) >= min_ele + k
            && min_ele + k >= (arr[i] - k))) {

            // If any value doesn't lie in
            // the range then exit the loop
            flag = false;
            break;
        }
    }

    if (flag) {

        // Value after equalizing the array
        return min_ele + k;
    }

    // Array cannot be equalized
    else
        return -1;
}

// Driver code

let K = 2;
let arr = [ 1, 2, 3, 4, 5 ];
let N = arr.length;

document.write(equalize(arr, N, K));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
3
```