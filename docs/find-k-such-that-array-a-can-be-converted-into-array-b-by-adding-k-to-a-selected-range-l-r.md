# 找到 K，通过将 K 加到选定的范围[L，R]

可以将数组 A 转换成数组 B

> 原文:[https://www . geesforgeks . org/find-k-so-array-a 可以通过将-k-to-a-selected-range-l-r/](https://www.geeksforgeeks.org/find-k-such-that-array-a-can-be-converted-into-array-b-by-adding-k-to-a-selected-range-l-r/) 相加转换为-array-b

给定由唯一元素组成的两个长度为 **N** 的数组**a【】**和**b【】**，任务是找到一个数字 **K** (K > 0)，这样通过将 K 加到数组中选定的范围【L，R】就可以将第一个数组转换为第二个数组。如果没有这样的数字 K，打印 **NA**

**示例:**

> **输入:** a[] = {3，7，1，4，0，2，2}，b[] = {3，7，3，6，2，2，2}
> **输出:** 2
> **说明:**
> 数组 a[]可以通过在范围[2，4]中添加 K = 2 转换为数组 b[]
> 
> **输入:** a[] = {3，7，1，4，0，1，2}，b[] = {3，7，3，6，2，2}
> **输出:** NA

**接近**:

*   创建一个临时的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**c【】**其中包含数组元素的区别，即

```
ci = bi - ai
```

*   然后为数组 c[n]的所有非零元素及其索引创建一个[向量对](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)。因此，向量对将为:

```
vector<c[i], o>

where c[i] is a non zero value in c[]
and i is the index of c[i]
```

*   如果指标值相差 1，差值相同，那么 **K =差值**和【L，R】=指标范围。
*   因此，数组 a[n]可以通过将 K 加到[a[L]，a[R]]上转换成 b[n]。

**例如**:

*   考虑到

```
a[n] = [3, 7, 1, 4, 0, 2, 2]
b[n] = [3, 7, 3, 6, 2, 2, 2]
```

*   因此，在创建临时数组 c[]和向量对时:

```
c[n] = [0, 0, 2, 2, 2, 0, 0]
vector pair = {{2, 2}, {2, 3}, {2, 4}}
```

*   由于向量对中的所有索引值(2，3，4)相差 1，因此它们是连续的。
*   和差值相同(2)。
*   因此，我们可以简单地将给定索引[2，4]中第一个数组 a[n]中的不同值相加，将其转换为第二个数组 b[n]。

*   因此，所需的 K 值将是 2

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function to Check if it is possible to
// convert a given array to another array
// by adding elements to first array
bool checkconv(int a[], int b[], int n)
{
    int c[n], flag = 0;

    // Create a temporary array c[]
    // which contains the difference
    // of the array elements
    for (int i = 0; i < n; i++) {

        c[i] = b[i] - a[i];
    }

    // Create a vector pair for all non zero
    // elements of array c[n] with there index
    vector<pair<int, int> > idxs;
    for (int i = 0; i < n; i++) {
        if (c[i] != 0)
            idxs.push_back(make_pair(i, c[i]));
    }

    // Check If the index value differs by 1
    // and the difference value is same
    for (int i = 0; i < idxs.size() - 1; i++) {
        if (idxs[i + 1].first - idxs[i].first != 1
            || idxs[i + 1].second != idxs[i].second) {
            flag = 1;
            break;
        }
    }

    return !flag;
}

// Function to calculate the value of K
int diffofarrays(int a[], int b[], int n)
{
    int c[n], ans = 0;
    for (int i = 0; i < n; i++) {
        c[i] = b[i] - a[i];
    }
    for (int i = 0; i < n; i++) {
        if (c[i] != 0) {
            ans = c[i];
            break;
        }
    }

    return ans;
}

// Driver code
int main()
{
    int A[] = { 3, 7, 1, 4, 0, 2, 2 };
    int B[] = { 3, 7, 3, 6, 2, 2, 2 };
    int arr_size = sizeof(A) / sizeof(A[0]);

    if (checkconv(A, B, arr_size)) {
        cout << diffofarrays(A, B, arr_size) << endl;
    }
    else
        cout << "NA" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{
    static class pair
    {
        int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

// Function to Check if it is possible to
// convert a given array to another array
// by adding elements to first array
static boolean checkconv(int a[], int b[], int n)
{
    int []c = new int[n];
    int flag = 0;

    // Create a temporary array c[]
    // which contains the difference
    // of the array elements
    for (int i = 0; i < n; i++)
    {

        c[i] = b[i] - a[i];
    }

    // Create a vector pair for all non zero
    // elements of array c[n] with there index
    Vector<pair > idxs = new Vector<pair>();
    for (int i = 0; i < n; i++)
    {
        if (c[i] != 0)
            idxs.add(new pair(i, c[i]));
    }

    // Check If the index value differs by 1
    // and the difference value is same
    for (int i = 0; i < idxs.size() - 1; i++)
    {
        if (idxs.get(i + 1).first - idxs.get(i).first != 1
            || idxs.get(i + 1).second != idxs.get(i).second)
        {
            flag = 1;
            break;
        }
    }

    return flag == 1 ? false:true;
}

// Function to calculate the value of K
static int diffofarrays(int a[], int b[], int n)
{
    int []c = new int[n];
    int ans = 0;
    for (int i = 0; i < n; i++)
    {
        c[i] = b[i] - a[i];
    }
    for (int i = 0; i < n; i++)
    {
        if (c[i] != 0)
        {
            ans = c[i];
            break;
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int A[] = { 3, 7, 1, 4, 0, 2, 2 };
    int B[] = { 3, 7, 3, 6, 2, 2, 2 };
    int arr_size = A.length;

    if (checkconv(A, B, arr_size))
    {
        System.out.print(diffofarrays(A, B, arr_size) +"\n");
    }
    else
        System.out.print("NA" +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to Check if it is possible to
# convert a given array to another array
# by adding elements to first array
def checkconv(a, b, n) :

    c = [0]*n; flag = 0;

    # Create a temporary array c[]
    # which contains the difference
    # of the array elements
    for i in range(n) :
        c[i] = b[i] - a[i];

    # Create a vector pair for all non zero
    # elements of array c[n] with there index
    idxs = [];
    for i in range(n) :
        if (c[i] != 0) :
            idxs.append((i, c[i]));

    # Check If the index value differs by 1
    # and the difference value is same
    for i in range(len(idxs) - 1) :
        if (idxs[i + 1][0] - idxs[i][0] != 1
            or idxs[i + 1][1] != idxs[i][1]) :
            flag = 1;
            break;

    return not flag;

# Function to calculate the value of K
def diffofarrays(a, b, n) :
    c = [0] * n;
    ans = 0;

    for i in range(n) :
        c[i] = b[i] - a[i];

    for i in range(n) :
        if (c[i] != 0) :
            ans = c[i];
            break;

    return ans;

# Driver code
if __name__ == "__main__" :

    A = [ 3, 7, 1, 4, 0, 2, 2 ];
    B = [ 3, 7, 3, 6, 2, 2, 2 ];
    arr_size = len(A);

    if (checkconv(A, B, arr_size)) :
        print(diffofarrays(A, B, arr_size));

    else :
        print("NA");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{
    class pair
    {
        public int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

// Function to Check if it is possible to
// convert a given array to another array
// by adding elements to first array
static bool checkconv(int []a, int []b, int n)
{
    int []c = new int[n];
    int flag = 0;

    // Create a temporary array c[]
    // which contains the difference
    // of the array elements
    for (int i = 0; i < n; i++)
    {

        c[i] = b[i] - a[i];
    }

    // Create a vector pair for all non zero
    // elements of array c[n] with there index
    List<pair > idxs = new List<pair>();
    for (int i = 0; i < n; i++)
    {
        if (c[i] != 0)
            idxs.Add(new pair(i, c[i]));
    }

    // Check If the index value differs by 1
    // and the difference value is same
    for (int i = 0; i < idxs.Count - 1; i++)
    {
        if (idxs[i + 1].first - idxs[i].first != 1
            || idxs[i + 1].second != idxs[i].second)
        {
            flag = 1;
            break;
        }
    }

    return flag == 1 ? false:true;
}

// Function to calculate the value of K
static int diffofarrays(int []a, int []b, int n)
{
    int []c = new int[n];
    int ans = 0;
    for (int i = 0; i < n; i++)
    {
        c[i] = b[i] - a[i];
    }
    for (int i = 0; i < n; i++)
    {
        if (c[i] != 0)
        {
            ans = c[i];
            break;
        }
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []A = { 3, 7, 1, 4, 0, 2, 2 };
    int []B = { 3, 7, 3, 6, 2, 2, 2 };
    int arr_size = A.Length;

    if (checkconv(A, B, arr_size))
    {
        Console.Write(diffofarrays(A, B, arr_size) +"\n");
    }
    else
        Console.Write("NA" +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to Check if it is possible to
// convert a given array to another array
// by adding elements to first array
function checkconv(a, b, n) {
    let c = new Array(n);
    let flag = 0;

    // Create a temporary array c[]
    // which contains the difference
    // of the array elements
    for (let i = 0; i < n; i++) {

        c[i] = b[i] - a[i];
    }

    // Create a vector pair for all non zero
    // elements of array c[n] with there index
    let idxs = new Array();

    for (let i = 0; i < n; i++) {
        if (c[i] != 0)
            idxs.push([i, c[i]]);
    }

    // Check If the index value differs by 1
    // and the difference value is same
    for (let i = 0; i < idxs.length - 1; i++) {
        if (idxs[i + 1][0] - idxs[i][0] != 1
            || idxs[i + 1][1] != idxs[i][1]) {
            flag = 1;
            break;
        }
    }

    return !flag;
}

// Function to calculate the value of K
function diffofarrays(a, b, n) {
    let c = new Array(n);
    let ans = 0;
    for (let i = 0; i < n; i++) {
        c[i] = b[i] - a[i];
    }
    for (let i = 0; i < n; i++) {
        if (c[i] != 0) {
            ans = c[i];
            break;
        }
    }

    return ans;
}

// Driver code

let A = [3, 7, 1, 4, 0, 2, 2];
let B = [3, 7, 3, 6, 2, 2, 2];
let arr_size = A.length;

if (checkconv(A, B, arr_size)) {
    document.write(diffofarrays(A, B, arr_size) + "<br>");
}
else
    document.write("NA" + "<br>");
</script>
```

**Output:** 

```
2
```