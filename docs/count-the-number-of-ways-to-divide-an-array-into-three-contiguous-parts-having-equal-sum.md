# 计算将一个数组分成三个相等和的连续部分的方法数

> 原文:[https://www . geeksforgeeks . org/count-将一个数组划分为三个具有相等和的连续部分的方法数/](https://www.geeksforgeeks.org/count-the-number-of-ways-to-divide-an-array-into-three-contiguous-parts-having-equal-sum/)

给定一组 n 个数字。我们的任务是找出将数组分成三个连续部分的方法，使三个部分的总和相等。换句话说，我们需要找到索引对 I 和 j 的数量，使得从 0 到 i-1 的元素之和等于从 I 到 j 的元素之和等于从 j+1 到 n-1 的元素之和。

**示例:**

```
Input  : arr[] = {1, 2, 3, 0, 3}
Output : 2
Following are two possible ways to partition
1) Three parts are (1, 2), (3) and (0, 3)
2) Three parts are (1, 2), (3,0) and (3)

Input : arr[] = {0, 1, -1, 0}
Output : 1
It is only one way to partition.
1) Three parts are (0), (1,-1) and (0)
```

如果数组中所有元素的和不能被 3 整除，则返回 0。否则很明显，每个连续部分的每个部分的总和将等于所有元素的总和除以 3。

**步骤 1 :** 创建一个与给定数组大小相同的数组，该数组的第 I 个索引保存给定数组从索引 0 到 I 的元素之和的值。让我们称它为前缀数组
**步骤 2 :** 创建另一个与给定数组大小相同的数组，其第 I 个索引是给定数组中从索引 I 到 n-1 的元素之和的值。姑且称之为后缀数组。
**第三步:**思路很简单，我们开始遍历前缀数组，假设在前缀数组的第 I 个索引处，前缀数组的值等于(给定数组所有元素的和)/3。
**步骤 4 :** 对于我在上面的步骤中发现的我们从第(i+2)个索引开始查看后缀数组，只要后缀数组的值等于(给定数组所有元素的和)/3，我们就将计数器变量增加 1。

为了实现步骤 4，我们遍历后缀数组，只要后缀数组的值等于给定数组所有元素的和/3，我们就将后缀数组的索引推入向量。我们在向量中做一个二分搜索法运算，计算后缀数组中的值的数量，如步骤 4 所示。

我们在后缀数组中搜索，因为在第一部分和第三部分之间应该至少有一个元素。

有关更多解释，请参见下面的实现

## C++

```
// C++ program to count number of ways we can
// partition an array in three parts with equal
// sum.
#include<bits/stdc++.h>
using namespace std;

// binary search to find the number of required
// indices in suffix array. Returns index of
// first element which is greater than x.
int binarysearch(vector <int> &v, int x)
{
    int low = 0, high = v.size()-1;
    while (low <= high)
    {
        int mid = (low + high)/2;
        if (v[mid] <= x)
            low = mid + 1;
        else if (v[mid] > x && v[mid-1] <= x)
            return mid;
        else if (v[mid] > x && mid == 0)
            return mid;
        else
            high = mid-1;
    }
    return -1;
}

// function to calculate the number of ways to
// divide the array into three contiguous parts
int CountContiguousParts(int arr[] ,int n)
{
    int count = 0;  // initializing answer

    // Creating and filling  prefix array
    int prefix[n];
    prefix[0] = arr[0];
    for (int i=1; i<n; i++)
        prefix[i] = prefix[i-1] + arr[i];

    // Total sum of elements is equal to last
    // value in prefix array.
    int total_sum = prefix[n-1];

    // If sum of all the elements is not divisible
    // by 3, we can't divide array in 3 parts of
    // same sum.
    if (total_sum%3 != 0)
        return 0;

    // Creating and filling suffix array
    int suffix[n];
    suffix[n-1] = arr[n-1];
    for (int i=n-2; i>=0; i--)
        suffix[i] = suffix[i+1] + arr[i];

    // Storing all indexes with suffix
    // sum equal to total sum by 3.
    vector <int> v;
    for (int i=0; i<n; i++)
        if (suffix[i] == total_sum/3)
            v.push_back(i);

    // Traversing the prefix array and
    // doing binary search in above vector
    for (int i=0; i<n; i++)
    {
        // We found a prefix with total_sum/3
        if (prefix[i] == total_sum/3)
        {
            // Find first index in v[] which
            // is greater than i+1.
            int res = binarysearch(v, i+1);

            if (res != -1)
                count += v.size() - res;
        }
    }

    return count;
}

// driver function
int main()
{
    int arr[] = {1 , 2 , 3 , 0 , 3};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << CountContiguousParts(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of ways we can
// partition an array in three parts with equal
// sum.
import java.util.*;

class GFG
{

// binary search to find the number of required
// indices in suffix array. Returns index of
// first element which is greater than x.
static int binarysearch(Vector<Integer> v, int x)
{
    int low = 0, high = v.size() - 1;
    while (low <= high)
    {
        int mid = (low + high) / 2;
        if (v.get(mid) <= x)
            low = mid + 1;
        else if (v.get(mid) > x &&
                 v.get(mid) <= x)
            return mid;
        else if (v.get(mid) > x && mid == 0)
            return mid;
        else
            high = mid - 1;
    }
    return -1;
}

// function to calculate the number of ways to
// divide the array into three contiguous parts
static int CountContiguousParts(int arr[], int n)
{
    int count = 0; // initializing answer

    // Creating and filling prefix array
    int []prefix = new int[n];
    prefix[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];

    // Total sum of elements is equal to last
    // value in prefix array.
    int total_sum = prefix[n - 1];

    // If sum of all the elements is not divisible
    // by 3, we can't divide array in 3 parts of
    // same sum.
    if (total_sum % 3 != 0)
        return 0;

    // Creating and filling suffix array
    int []suffix = new int[n];
    suffix[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
        suffix[i] = suffix[i + 1] + arr[i];

    // Storing all indexes with suffix
    // sum equal to total sum by 3.
    Vector<Integer> v = new Vector<>();
    for (int i = 0; i < n; i++)
        if (suffix[i] == total_sum / 3)
            v.add(i);

    // Traversing the prefix array and
    // doing binary search in above vector
    for (int i = 0; i < n; i++)
    {
        // We found a prefix with total_sum/3
        if (prefix[i] == total_sum / 3)
        {
            // Find first index in v[] which
            // is greater than i+1.
            int res = binarysearch(v, i + 1);

            if (res != -1)
                count += v.size() - res;
        }
    }
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = {1 , 2 , 3 , 0 , 3};
    int n = arr.length;
    System.out.println(CountContiguousParts(arr, n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 program to count the number of ways we can
# partition an array in three parts with equal
# sum.

# binary search to find the number of required
# indices in suffix array. Returns index of
# first element which is greater than x.
def binarysearch(v, x):
    low = 0
    high = len(v) - 1
    while (low <= high):
        mid = int((low + high) / 2)
        if (v[mid] <= x):
            low = mid + 1
        elif (v[mid] > x and v[mid - 1] <= x):
            return mid
        elif (v[mid] > x and mid == 0):
            return mid
        else:
            high = mid - 1

    return -1

# function to calculate the number of ways to
# divide the array into three contiguous parts
def CountContiguousParts(arr,n):
    count = 0 # initializing answer

    # Creating and filling prefix array
    prefix = [0 for i in range(n)]
    prefix[0] = arr[0]
    for i in range(1, n, 1):
        prefix[i] = prefix[i - 1] + arr[i]

    # Total sum of elements is equal to last
    # value in prefix array.
    total_sum = prefix[n - 1]

    # If sum of all the elements is not divisible
    # by 3, we can't divide array in 3 parts of
    # same sum.
    if (total_sum % 3 != 0):
        return 0

    # Creating and filling suffix array
    suffix = [0 for i in range(n)]
    suffix[n - 1] = arr[n - 1]
    i = n - 2
    while(i >= 0):
        suffix[i] = suffix[i + 1] + arr[i]
        i -= 1

    # Storing all indexes with suffix
    # sum equal to total sum by 3.
    v = []
    for i in range(n):
        if (suffix[i] == int(total_sum / 3)):
            v.append(i)

    # Traversing the prefix array and
    # doing binary search in above vector
    for i in range(n):

        # We found a prefix with total_sum/3
        if (prefix[i] == int(total_sum / 3)):

            # Find first index in v[] which
            # is greater than i+1.
            res = binarysearch(v, i + 1)

            if (res != -1):
                count += len(v) - res

    return count

# Driver Code
if __name__ == '__main__':
    arr = [1 , 2 , 3 , 0 , 3]
    n = len(arr)
    print(CountContiguousParts(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count number of ways we can
// partition an array in three parts with equal
using System;
using System.Collections.Generic;

class GFG
{

// binary search to find the number of required
// indices in suffix array. Returns index of
// first element which is greater than x.
static int binarysearch(List<int> v, int x)
{
    int low = 0, high = v.Count - 1;
    while (low <= high)
    {
        int mid = (low + high) / 2;
        if (v[mid] <= x)
            low = mid + 1;
        else if (v[mid] > x &&
                v[mid] <= x)
            return mid;
        else if (v[mid] > x && mid == 0)
            return mid;
        else
            high = mid - 1;
    }
    return -1;
}

// function to calculate the number of ways to
// divide the array into three contiguous parts
static int CountContiguousParts(int []arr, int n)
{
    int count = 0; // initializing answer

    // Creating and filling prefix array
    int []prefix = new int[n];
    prefix[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];

    // Total sum of elements is equal to last
    // value in prefix array.
    int total_sum = prefix[n - 1];

    // If sum of all the elements is not divisible
    // by 3, we can't divide array in 3 parts of
    // same sum.
    if (total_sum % 3 != 0)
        return 0;

    // Creating and filling suffix array
    int []suffix = new int[n];
    suffix[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
        suffix[i] = suffix[i + 1] + arr[i];

    // Storing all indexes with suffix
    // sum equal to total sum by 3.
    List<int> v = new List<int>();
    for (int i = 0; i < n; i++)
        if (suffix[i] == total_sum / 3)
            v.Add(i);

    // Traversing the prefix array and
    // doing binary search in above vector
    for (int i = 0; i < n; i++)
    {
        // We found a prefix with total_sum/3
        if (prefix[i] == total_sum / 3)
        {
            // Find first index in v[] which
            // is greater than i+1.
            int res = binarysearch(v, i + 1);

            if (res != -1)
                count += v.Count - res;
        }
    }
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {1 , 2 , 3 , 0 , 3};
    int n = arr.Length;
    Console.WriteLine(CountContiguousParts(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to count number
// of ways we can partition an array
// in three parts with equal sum.

// Binary search to find the number of required
// indices in suffix array. Returns index of
// first element which is greater than x.
function binarysearch(v, x)
{
    let low = 0, high = v.length - 1;

    while (low <= high)
    {
        let mid = Math.floor((low + high) / 2);

        if (v[mid] <= x)
            low = mid + 1;
        else if (v[mid] > x && v[mid] <= x)
            return mid;
        else if (v[mid] > x && mid == 0)
            return mid;
        else
            high = mid - 1;
    }
    return -1;
}

// Function to calculate the number of ways to
// divide the array into three contiguous parts
function CountContiguousParts(arr, n)
{

    // Initializing answer
    let count = 0;

    // Creating and filling prefix array
    let prefix = new Array(n);
    prefix[0] = arr[0];

    for(let i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];

    // Total sum of elements is equal to last
    // value in prefix array.
    let total_sum = prefix[n - 1];

    // If sum of all the elements is not divisible
    // by 3, we can't divide array in 3 parts of
    // same sum.
    if (total_sum % 3 != 0)
        return 0;

    // Creating and filling suffix array
    let suffix = new Array(n);
    suffix[n - 1] = arr[n - 1];

    for(let i = n - 2; i >= 0; i--)
        suffix[i] = suffix[i + 1] + arr[i];

    // Storing all indexes with suffix
    // sum equal to total sum by 3.
    let v = [];
    for(let i = 0; i < n; i++)
        if (suffix[i] == Math.floor(total_sum / 3))
            v.push(i);

    // Traversing the prefix array and
    // doing binary search in above vector
    for(let i = 0; i < n; i++)
    {

        // We found a prefix with total_sum/3
        if (prefix[i] == Math.floor(total_sum / 3))
        {

            // Find first index in v[] which
            // is greater than i+1.
            let res = binarysearch(v, i + 1);

            if (res != -1)
                count += v.length - res;
        }
    }
    return count;
}

// Driver Code
let arr = [ 1 , 2 , 3 , 0 , 3 ];
let  n = arr.length;

document.write(CountContiguousParts(arr, n));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
2
```

时间复杂度为 0(对数 n)

**高效方法[ O(n)解] :**

1.  如果数组中所有元素的总和不能被 3 整除，则返回 0。
2.  很明显，每个连续部分的每个部分的总和将等于所有元素的总和除以 3。
3.  让我们创建一个数组 cnt[ ]，其中 cnt[ i ]等于 1，如果从第 I 个到第 n 个元素的和等于 Array_Sum/3 否则为 0。现在，从最后一个索引开始计算 *cnt* 数组的累积和。
4.  因此，我们得到了一个非常简单的解:对于初始数组 1…i 的每个前缀，其和等于 Array_Sum/3，我们需要将它们加到答案和[ i+2 ]中。

下面是上述方法的代码。

## C++

```
// C++ program to count the ways
// to break the array in 3 equal parts
// having equal sum.
#include <bits/stdc++.h>
using namespace std;

// Function to count the no of ways
int countways(int a[], int n)
{
    int cnt[n] = {0}, s = 0;

    // Calculating the sum of the array
    // and storing it in variable s
    for (int i = 0 ; i < n ; i++)
    {
        s += a[i];
    }

    // Checking s is divisible by 3 or not
    if (s % 3 != 0)
        return 0;

    // Calculating the sum of each part
    s /= 3;

    int ss = 0;

    // If the sum of elements from i-th to n-th
    // equals to sum of part putting 1 in cnt
    // array otherwise 0.
    for (int i = n-1; i >= 0 ; i--)
    {
        ss += a[i];
        if (ss == s)
            cnt[i] = 1;
    }

    // Calculating the cumulative sum
    // of the array cnt from the last index.
    for (int i = n-2 ; i >= 0 ; i--)
        cnt[i] += cnt[i + 1];

    int ans = 0;
    ss = 0;

    // Calculating answer using original
    // and cnt array.
    for (int i = 0 ; i+2 < n ; i++)
    {
        ss += a[i];
        if (ss == s)
            ans += cnt[i + 2];
    }
    return ans;
}

// Driver function
int main()
{
    int n = 5;
    int a[] = {1, 2, 3, 0, 3};
    cout << countways(a, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the ways to
// break the array in 3 equal parts
// having equal sum.
import java.io.*;

class GFG {

    // Function to count the no of ways
    static int countways(int a[], int n)
    {
        int cnt[] = new int[n];
        int s = 0;

        // Calculating the sum of the array
        // and storing it in variable s
        for (int i = 0 ; i < n ; i++)
        {
            s += a[i];
        }

        // Checking s is divisible by 3 or not
        if (s % 3 != 0)
            return 0;

        // Calculating the sum of each part
        s /= 3;

        int ss = 0;

        // If the sum of elements from i-th to n-th
        // equals to sum of part putting 1 in cnt
        // array otherwise 0.
        for (int i = n-1; i >= 0 ; i--)
        {
            ss += a[i];
            if (ss == s)
                cnt[i] = 1;
        }

        // Calculating the cumulative sum
        // of the array cnt from the last index.
        for (int i = n-2 ; i >= 0 ; i--)
            cnt[i] += cnt[i + 1];

        int ans = 0;
        ss = 0;

        // Calculating answer using original
        // and cnt array.
        for (int i = 0 ; i+2 < n ; i++)
        {
            ss += a[i];
            if (ss == s)
                ans += cnt[i + 2];
        }
        return ans;
    }

    // Driver function
    public static void main (String[] args)
    {
        int n = 5;
        int a[] = {1, 2, 3, 0, 3};
        System.out.println(countways(a, n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to count the ways
# to break the array in 3 equal parts
# having equal sum.

# Function to count the no of ways
def countways(a, n):

    cnt = [0 for i in range(n)]
    s = 0

    # Calculating the sum of the array
    # and storing it in variable s
    s = sum(a)

    # Checking s is divisible by 3 or not
    if (s % 3 != 0):
        return 0

    # Calculating the sum of each part
    s //= 3

    ss = 0

    # If the sum of elements from i-th
    # to n-th equals to sum of part
    # putting 1 in cnt array otherwise 0.
    for i in range(n - 1, -1, -1):

        ss += a[i]
        if (ss == s):
            cnt[i] = 1

    # Calculating the cumulative sum
    # of the array cnt from the last index.
    for i in range(n - 2, -1, -1):
        cnt[i] += cnt[i + 1]

    ans = 0
    ss = 0

    # Calculating answer using original
    # and cnt array.
    for i in range(0, n - 2):
        ss += a[i]
        if (ss == s):
            ans += cnt[i + 2]

    return ans

# Driver Code
n = 5
a = [1, 2, 3, 0, 3]
print(countways(a, n))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# program to count the ways to
// break the array in 3 equal parts
// having an equal sum.
using System;

class GFG
{

    // Function to count the no of ways
    static int countways(int[] a, int n)
    {
        int[] cnt = new int[n];
        int s = 0;

        // Calculating the sum of the array
        // and storing it in variable s
        for (int i = 0 ; i < n ; i++)
        {
            s += a[i];
        }

        // Checking s is divisible by 3 or not
        if (s % 3 != 0)
            return 0;

        // Calculating the sum of each part
        s /= 3;

        int ss = 0;

        // If the sum of elements from i-th to n-th
        // equals to sum of part putting 1 in cnt
        // array otherwise 0.
        for (int i = n - 1; i >= 0 ; i--)
        {
            ss += a[i];
            if (ss == s)
                cnt[i] = 1;
        }

        // Calculating the cumulative sum
        // of the array cnt from the last index.
        for (int i = n - 2 ; i >= 0 ; i--)
            cnt[i] += cnt[i + 1];

        int ans = 0;
        ss = 0;

        // Calculating answer using original
        // and cnt array.
        for (int i = 0 ; i + 2 < n ; i++)
        {
            ss += a[i];
            if (ss == s)
                ans += cnt[i + 2];
        }
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int n = 5;
        int[] a = {1, 2, 3, 0, 3};
        Console.Write(countways(a, n));
    }
}

// This code is contributed by Ita_c.
```

## java 描述语言

```
<script>

// Javascript program to count the ways to
// break the array in 3 equal parts
// having equal sum.

    // Function to count the no of ways
    function countways(a,n)
    {
        let cnt = new Array(n);
        let s = 0;

        // Calculating the sum of the array
        // and storing it in variable s
        for (let i = 0 ; i < n ; i++)
        {
            s += a[i];
        }

        // Checking s is divisible by 3 or not
        if (s % 3 != 0)
            return 0;

        // Calculating the sum of each part
        s = Math.floor(s/3);

        let ss = 0;

        // If the sum of elements from i-th to n-th
        // equals to sum of part putting 1 in cnt
        // array otherwise 0.
        for (let i = n-1; i >= 0 ; i--)
        {
            ss += a[i];
            if (ss == s)
                cnt[i] = 1;
        }

        // Calculating the cumulative sum
        // of the array cnt from the last index.
        for (let i = n-2 ; i >= 0 ; i--)
            cnt[i] += cnt[i + 1];

        let ans = 0;
        ss = 0;

        // Calculating answer using original
        // and cnt array.
        for (let i = 0 ; i+2 < n ; i++)
        {
            ss += a[i];
            if (ss == s)
                ans += cnt[i + 2];
        }
        return ans;
    }

    // Driver function
    let n = 5;
    let a=[1, 2, 3, 0, 3];
    document.write(countways(a, n));

    // This code is contributed by rag2127

</script>
```

**输出:**

```
2
```

**时间复杂度:** O(n)。

这种方法是由 **Abhishek Sharma** 贡献的。
本文由**阿育什·贾**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。