# 查找给定数组的索引范围[L，R]中是否存在波峰

> 原文:[https://www . geeksforgeeks . org/find-if-a-crest-is-in-index-range-l-r-of-the-给定数组/](https://www.geeksforgeeks.org/find-if-a-crest-is-present-in-the-index-range-l-r-of-the-given-array/)

给定一个由 **N** 个不同元素组成的数组 **arr[]** ，以及一个索引范围**【L，R】**。任务是找出一个波峰是否出现在数组的索引范围内。子阵列 **arr[L…R]** 中的任何元素 **arr[i]** 如果子阵列 **arr[L…i]** 的所有元素严格递增，子阵列 **arr[i…R]** 的所有元素严格递减，则称为波峰。
**举例:**

> **输入:** arr[] = {2，1，3，5，12，11，7，9}，L = 2，R = 6
> **输出:**是
> 元素 12 是子阵列{3，5，12，11，7}中的一个波峰。
> **输入:** arr[] = {2，1，3，5，12，11，7，9}，L = 0，R = 2
> **输出:**否

**进场:**

*   检查在给定的指标范围**【L，R】**内是否存在满足**性质**的元素，其中**arr[I–1]≥arr[I]≤arr[I+1]**。
*   如果给定范围内的任何元素满足上述属性，则给定范围不能包含波峰，否则波峰总是可能的。
*   要找到满足上述属性的元素，请维护一个数组 **present[]** ，其中如果**arr[I–1]≥arr[I]≤arr[I+1]**，则 **present[i]** 将为 **1** ，否则 **present[i]** 将为 **0** 。
*   现在将 **present[]** 数组转换为其累积和，其中 **present[i]** 现在将表示索引范围**【0，I】**中满足该属性的元素数量。
*   对于包含波峰的指数范围**【L，R】**，出现的**【L】**必须等于出现的**【R–1】**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the
// array contains a crest in
// the index range [L, R]
bool hasCrest(int arr[], int n, int L, int R)
{
    // To keep track of elements
    // which satisfy the Property
    int present[n] = { 0 };

    for (int i = 1; i <= n - 2; i++) {

        // Property is satisfied for
        // the current element
        if ((arr[i] <= arr[i + 1])
            && (arr[i] <= arr[i - 1])) {
            present[i] = 1;
        }
    }

    // Cumulative Sum
    for (int i = 1; i < n; i++) {
        present[i] += present[i - 1];
    }

    // If a crest is present in
    // the given index range
    if (present[L] == present[R - 1])
        return true;

    return false;
}

// Driver code
int main()
{
    int arr[] = { 2, 1, 3, 5, 12, 11, 7, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int L = 2;
    int R = 6;

    if (hasCrest(arr, N, L, R))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if the
// array contains a crest in
// the index range [L, R]
static boolean hasCrest(int arr[], int n,
                        int L, int R)
{
    // To keep track of elements
    // which satisfy the Property
    int []present = new int[n];
    for(int i = 0; i < n; i++)
    {
        present[i] = 0;
    }

    for (int i = 1; i <= n - 2; i++)
    {

        // Property is satisfied for
        // the current element
        if ((arr[i] <= arr[i + 1]) &&
            (arr[i] <= arr[i - 1]))
        {
            present[i] = 1;
        }
    }

    // Cumulative Sum
    for (int i = 1; i < n; i++)
    {
        present[i] += present[i - 1];
    }

    // If a crest is present in
    // the given index range
    if (present[L] == present[R - 1])
        return true;

    return false;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 2, 1, 3, 5, 12, 11, 7, 9 };
    int N = arr.length;
    int L = 2;
    int R = 6;

    if (hasCrest(arr, N, L, R))
        System.out.println("Yes");
    else
        System.out.println("No");

}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the
# array contains a crest in
# the index range [L, R]
def hasCrest(arr, n, L, R) :

    # To keep track of elements
    # which satisfy the Property
    present = [0] * n ;

    for i in range(1, n - 2 + 1) :

        # Property is satisfied for
        # the current element
        if ((arr[i] <= arr[i + 1]) and
            (arr[i] <= arr[i - 1])) :
            present[i] = 1;

    # Cumulative Sum
    for i in range(1, n) :
        present[i] += present[i - 1];

    # If a crest is present in
    # the given index range
    if (present[L] == present[R - 1]) :
        return True;

    return False;

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 1, 3, 5, 12, 11, 7, 9 ];
    N = len(arr);
    L = 2;
    R = 6;

    if (hasCrest(arr, N, L, R)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```

// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if the
// array contains a crest in
// the index range [L, R]
static bool hasCrest(int []arr, int n,
                        int L, int R)
{
    // To keep track of elements
    // which satisfy the Property
    int []present = new int[n];
    for(int i = 0; i < n; i++)
    {
        present[i] = 0;
    }

    for (int i = 1; i <= n - 2; i++)
    {

        // Property is satisfied for
        // the current element
        if ((arr[i] <= arr[i + 1]) &&
            (arr[i] <= arr[i - 1]))
        {
            present[i] = 1;
        }
    }

    // Cumulative Sum
    for (int i = 1; i < n; i++)
    {
        present[i] += present[i - 1];
    }

    // If a crest is present in
    // the given index range
    if (present[L] == present[R - 1])
        return true;

    return false;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 2, 1, 3, 5, 12, 11, 7, 9 };
    int N = arr.Length;
    int L = 2;
    int R = 6;

    if (hasCrest(arr, N, L, R))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that returns true if the
// array contains a crest in
// the index range [L, R]
function hasCrest(arr, n, L, R)
{
    // To keep track of elements
    // which satisfy the Property
    let present = new Uint8Array(n);

    for (let i = 1; i <= n - 2; i++) {

        // Property is satisfied for
        // the current element
        if ((arr[i] <= arr[i + 1])
            && (arr[i] <= arr[i - 1])) {
            present[i] = 1;
        }
    }

    // Cumulative Sum
    for (let i = 1; i < n; i++) {
        present[i] += present[i - 1];
    }

    // If a crest is present in
    // the given index range
    if (present[L] == present[R - 1])
        return true;

    return false;
}

// Driver code

    let arr = [ 2, 1, 3, 5, 12, 11, 7, 9 ];
    let N = arr.length;
    let L = 2;
    let R = 6;

    if (hasCrest(arr, N, L, R))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
Yes
```