# 为使阵元频率等于 N / M 所需替换的子阵的最小长度

> 原文:[https://www . geeksforgeeks . org/最小长度子阵列-需要替换-使阵列元素的频率等于 n-m/](https://www.geeksforgeeks.org/minimum-length-of-the-subarray-required-to-be-replaced-to-make-frequency-of-array-elements-equal-to-n-m/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**仅由第一个 **M** [自然数](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)组成，任务是找到需要替换的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最小长度，使得数组元素的[频率为 **N / M** 。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)

***注:** **N** 是 **M** 的倍数。*

**示例:**

> **输入:** M = 3，arr[] = {1，1，1，2，3}
> **输出:** 2
> **解释:**
> 将范围[2，3]内的子阵列替换为元素{2，3}将数组 arr[]修改为{1，1，2，3，2，3}。现在，每个数组元素的频率是 N / M( = 6 / 3 = 2)。
> 因此，需要更换的最小长度子阵为 2。
> 
> **输入:** M = 6，arr[] = {1，3，6，6，2，1，5，4，1，4，1，2，3，2，2，2，4，3}
> **输出:** 4

**逼近:**利用[两点逼近](https://www.geeksforgeeks.org/two-pointers-technique/)求所有在此范围之外的数的计数都小于或等于 **N/M** 的子阵的最小长度，可以解决给定的问题。按照以下步骤解决问题:

*   [初始化一个向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)，用 **0** 表示 **M+1** 大小的 **mapu[]** ，存储每个数组元素的频率。
*   将变量 **c** 初始化为 **0** ，以存储数组中额外出现的元素数量。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
    *   通过 **1** 增加[矢量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **马普【】**中**arr【I】**的值。
    *   如果**mapu【arr[I]】**的值等于 **(N/M) + 1** ，那么将 **c** 的值增加 **1** 。
*   如果 **c** 的值为 **0** ，则返回 **0** 作为结果。
*   将变量**和**初始化为 **N** 存储答案， **L** 和**R**T8】两个指针为 **0** 和**(N–1)**存储范围的左右。
*   [循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **R** 小于 **N** ，执行以下任务:
    *   如果**(mapu[arr[R]]–1)**的值等于 **N/M** ，则用 **1** 减去 **c** 的值。
    *   如果 **c** 等于 **0** ，则[循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **L** 小于等于 **R** ， **c** 的值等于 **0** 并执行以下任务:
        *   将 **ans** 的值更新为 **ans** 或**(R–L+1)**的最小值
        *   将**mapu【arr[L]】**的值增加 **1** ，如果大于 **N/M** ，则将 **c** 的值增加 **1** 。
        *   将 **L** 的值增加 **1** 。
    *   将 **R** 的值增加 **1** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum length
// of the subarray to be changed.
int minimumSubarray(vector<int> arr,
                    int n, int m)
{

    // Stores the frequencies of array
    // elements
    vector<int> mapu(m + 1, 0);

    // Stores the number of array elements
    // that are present more than N/M times
    int c = 0;

    // Iterate over the range
    for (int i = 0; i < n; i++) {

        // Increment the frequency
        mapu[arr[i]]++;
        if (mapu[arr[i]] == (n / m) + 1)
            c++;
    }

    // If the frequency of all array
    // elements are already N/M
    if (c == 0)
        return 0;

    // Stores the resultant length of
    // the subarray
    int ans = n;

    // The left and right pointers
    int l = 0, r = 0;

    // Iterate over the range
    while (r < n) {

        // If the current element is
        if (--mapu[arr[r]] == (n / m))
            c--;

        // If the value of c is 0, then
        // find the possible answer
        if (c == 0) {

            // Iterate over the range
            while (l <= r && c == 0) {
                ans = min(ans, r - l + 1);

                // If the element at left
                // is making it extra
                if (++mapu[arr[l]] > (n / m))
                    c++;

                // Update the left pointer
                l++;
            }
        }

        // Update the right pointer
        r++;
    }

    // Return the resultant length
    return ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 1, 2, 1, 1, 2 };
    int M = 2;
    int N = arr.size();

    cout << minimumSubarray(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

// Function to find the minimum length
// of the subarray to be changed.
public static int minimumSubarray(int[] arr, int n,
                                  int m)
{

    // Stores the frequencies of array
    // elements
    int[] mapu = new int[m + 1];

    Arrays.fill(mapu, 0);

    // Stores the number of array elements
    // that are present more than N/M times
    int c = 0;

    // Iterate over the range
    for(int i = 0; i < n; i++)
    {

        // Increment the frequency
        mapu[arr[i]]++;

        if (mapu[arr[i]] == (n / m) + 1)
            c++;
    }

    // If the frequency of all array
    // elements are already N/M
    if (c == 0)
        return 0;

    // Stores the resultant length of
    // the subarray
    int ans = n;

    // The left and right pointers
    int l = 0, r = 0;

    // Iterate over the range
    while (r < n)
    {

        // If the current element is
        if (--mapu[arr[r]] == (n / m))
            c--;

        // If the value of c is 0, then
        // find the possible answer
        if (c == 0)
        {

            // Iterate over the range
            while (l <= r && c == 0)
            {
                ans = Math.min(ans, r - l + 1);

                // If the element at left
                // is making it extra
                if (++mapu[arr[l]] > (n / m))
                    c++;

                // Update the left pointer
                l++;
            }
        }

        // Update the right pointer
        r++;
    }

    // Return the resultant length
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int[] arr = { 1, 1, 2, 1, 1, 2 };
    int M = 2;
    int N = arr.length;

    System.out.println(minimumSubarray(arr, N, M));
}
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum length
# of the subarray to be changed.
def minimumSubarray(arr, n, m):

    # Stores the frequencies of array
    # elements
    mapu = [0 for i in range(m+1)]

    # Stores the number of array elements
    # that are present more than N/M times
    c = 0

    # Iterate over the range
    for i in range(n):

        # Increment the frequency
        mapu[arr[i]] += 1
        if (mapu[arr[i]] == (n // m) + 1):
            c += 1

    # If the frequency of all array
    # elements are already N/M
    if (c == 0):
        return 0

    # Stores the resultant length of
    # the subarray
    ans = n

    # The left and right pointers
    l = 0
    r = 0

    # Iterate over the range
    while (r < n):

        # If the current element is
        mapu[arr[r]] -= 1
        if (mapu[arr[r]] == (n // m)):
            c -= 1

        # If the value of c is 0, then
        # find the possible answer
        if (c == 0):

            # Iterate over the range
            while (l <= r and c == 0):
                ans = min(ans, r - l + 1)

                # If the element at left
                # is making it extra
                mapu[arr[l]] += 1
                if (mapu[arr[l]] > (n // m)):
                    c += 1

                # Update the left pointer
                l += 1

        # Update the right pointer
        r += 1

    # Return the resultant length
    return ans

# Driver Code
if __name__ == '__main__':
    arr = [1, 1, 2, 1, 1, 2]
    M = 2
    N = len(arr)

    print(minimumSubarray(arr, N, M))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum length
// of the subarray to be changed.
public static int minimumSubarray(int[] arr, int n,
                                  int m)
{

    // Stores the frequencies of array
    // elements
    int[] mapu = new int[m + 1];

    Array.Fill(mapu, 0);

    // Stores the number of array elements
    // that are present more than N/M times
    int c = 0;

    // Iterate over the range
    for(int i = 0; i < n; i++)
    {

        // Increment the frequency
        mapu[arr[i]]++;

        if (mapu[arr[i]] == (n / m) + 1)
            c++;
    }

    // If the frequency of all array
    // elements are already N/M
    if (c == 0)
        return 0;

    // Stores the resultant length of
    // the subarray
    int ans = n;

    // The left and right pointers
    int l = 0, r = 0;

    // Iterate over the range
    while (r < n)
    {

        // If the current element is
        if (--mapu[arr[r]] == (n / m))
            c--;

        // If the value of c is 0, then
        // find the possible answer
        if (c == 0)
        {

            // Iterate over the range
            while (l <= r && c == 0)
            {
                ans = Math.Min(ans, r - l + 1);

                // If the element at left
                // is making it extra
                if (++mapu[arr[l]] > (n / m))
                    c++;

                // Update the left pointer
                l++;
            }
        }

        // Update the right pointer
        r++;
    }

    // Return the resultant length
    return ans;
}

// Driver Code
public static void Main(String []args)
{
    int[] arr = { 1, 1, 2, 1, 1, 2 };
    int M = 2;
    int N = arr.Length;

    Console.Write(minimumSubarray(arr, N, M));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum length
// of the subarray to be changed.
function minimumSubarray(arr, n, m)
{

    // Stores the frequencies of array
    // elements
    let mapu = new Array(m + 1).fill(0);

    // Stores the number of array elements
    // that are present more than N/M times
    let c = 0;

    // Iterate over the range
    for(let i = 0; i < n; i++)
    {

        // Increment the frequency
        mapu[arr[i]]++;

        if (mapu[arr[i]] == (n / m) + 1)
            c++;
    }

    // If the frequency of all array
    // elements are already N/M
    if (c == 0)
        return 0;

    // Stores the resultant length of
    // the subarray
    let ans = n;

    // The left and right pointers
    let l = 0, r = 0;

    // Iterate over the range
    while (r < n)
    {

        // If the current element is
        if (--mapu[arr[r]] == (n / m))
            c--;

        // If the value of c is 0, then
        // find the possible answer
        if (c == 0)
        {

            // Iterate over the range
            while (l <= r && c == 0)
            {
                ans = Math.min(ans, r - l + 1);

                // If the element at left
                // is making it extra
                if (++mapu[arr[l]] > (n / m))
                    c++;

                // Update the left pointer
                l++;
            }
        }

        // Update the right pointer
        r++;
    }

    // Return the resultant length
    return ans;
}

// Driver Code
let arr = [ 1, 1, 2, 1, 1, 2 ];
let M = 2;
let N = arr.length;

document.write(minimumSubarray(arr, N, M));

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)