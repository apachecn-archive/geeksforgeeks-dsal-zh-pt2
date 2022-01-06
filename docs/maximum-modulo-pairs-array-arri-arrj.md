# 所有数组对的最大模，其中 arr[i] > = arr[j]

> 原文:[https://www . geesforgeks . org/maximum-mod-pairs-array-arrj/](https://www.geeksforgeeks.org/maximum-modulo-pairs-array-arri-arrj/)

给定 n 个整数的数组。求 arr[i] mod arr[j]的最大值，其中 arr[i] >= arr[j]和 1 <= i, j <= n 
**例:**

```
Input: arr[] = {3, 4, 7}
Output: 3
Explanation:
There are 3 pairs which satisfies arr[i] >= arr[j] are:-
4, 3 => 4 % 3 = 1
7, 3 => 7 % 3 = 1
7, 4 => 7 % 4 = 3
Hence Maximum value among all is 3.

Input: arr[] = {3, 7, 4, 11}
Output: 4

Input: arr[] = {4, 4, 4}
Output: 0
```

一种**天真的方法**是运行两个嵌套的循环，并在取它们的模后选择每个可能对的最大值。这种方法的时间复杂度为 0(n<sup>2</sup>，这对于 n 的大值来说是不够的。
一种有效的方法(当元素来自小范围时)是使用排序和二分搜索法方法。首先，我们将对数组进行排序，以便能够对其应用二分搜索法。因为我们需要最大化 arr[i] mod arr[j]的值，所以我们迭代从 2*arr[j]到 M+arr[j]范围内的每个 x(这样的 x 可被 arr[j]整除)，其中 M 是序列的最大值。对于 x 的每个值，我们需要找到 arr[i]的最大值，这样 arr[i] < x.
通过这样做，我们将确保我们只选择了 arr[i]的那些值，它们将给出 arr[i] mod arr[j]的最大值。之后，我们只需要对 arr[j]的其他值重复上述过程，并用值 a[i] mod arr[j]更新答案。例如:-

```
If arr[] = {4, 6, 7, 8, 10, 12, 15} then for
first element, i.e., arr[j] = 4 we iterate
through x = {8, 12, 16}. 
Therefore for each value of x, a[i] will be:-
x = 8, arr[i] = 7 (7 < 8)
       ans = 7 mod 4 = 3 
x = 12, arr[i] = 10 (10 < 12)
       ans = 10 mod 4 = 2 (Since 2 < 3, 
                                No update)
x = 16, arr[i] = 15 (15 < 16)
       ans  = 15 mod 4 = 3 (Since 3 == 3,  
                        No need to update)
```

## C++

```
// C++ program to find Maximum modulo value
#include <bits/stdc++.h>
using namespace std;

int maxModValue(int arr[], int n)
{
    int ans = 0;
    // Sort the array[] by using inbuilt sort function
    sort(arr, arr + n);

    for (int j = n - 2; j >= 0; --j) {
        // Break loop if answer is greater or equals to
        // the arr[j] as any number modulo with arr[j]
        // can only give maximum value up-to arr[j]-1
        if (ans >= arr[j])
            break;

        // If both elements are same then skip the next
        // loop as it would be worthless to repeat the
        // rest process for same value
        if (arr[j] == arr[j + 1])
            continue;

        for (int i = 2 * arr[j]; i <= arr[n - 1] + arr[j]; i += arr[j]) {
            // Fetch the index which is greater than or
            // equals to arr[i] by using binary search
            // inbuilt lower_bound() function of C++
            int ind = lower_bound(arr, arr + n, i) - arr;

            // Update the answer
            ans = max(ans, arr[ind - 1] % arr[j]);
        }
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 5, 9, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxModValue(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Maximum modulo value

import java.util.Arrays;

class Test {
    static int maxModValue(int arr[], int n)
    {
        int ans = 0;

        // Sort the array[] by using inbuilt sort function
        Arrays.sort(arr);

        for (int j = n - 2; j >= 0; --j) {
            // Break loop if answer is greater or equals to
            // the arr[j] as any number modulo with arr[j]
            // can only give maximum value up-to arr[j]-1
            if (ans >= arr[j])
                break;

            // If both elements are same then skip the next
            // loop as it would be worthless to repeat the
            // rest process for same value
            if (arr[j] == arr[j + 1])
                continue;

            for (int i = 2 * arr[j]; i <= arr[n - 1] + arr[j]; i += arr[j]) {
                // Fetch the index which is greater than or
                // equals to arr[i] by using binary search

                int ind = Arrays.binarySearch(arr, i);

                if (ind < 0)
                    ind = Math.abs(ind + 1);

                else {
                    while (arr[ind] == i) {
                        ind--;

                        if (ind == 0) {
                            ind = -1;
                            break;
                        }
                    }
                    ind++;
                }

                // Update the answer
                ans = Math.max(ans, arr[ind - 1] % arr[j]);
            }
        }
        return ans;
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = { 3, 4, 5, 9, 11 };
        System.out.println(maxModValue(arr, arr.length));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find Maximum modulo value

def maxModValue(arr, n):

    ans = 0

    # Sort the array[] by using inbuilt
    # sort function
    arr = sorted(arr)

    for j in range(n - 2, -1, -1):

        # Break loop if answer is greater or equals to
        # the arr[j] as any number modulo with arr[j]
        # can only give maximum value up-to arr[j]-1
        if (ans >= arr[j]):
            break

        # If both elements are same then skip the next
        # loop as it would be worthless to repeat the
        # rest process for same value
        if (arr[j] == arr[j + 1]) :
            continue
        i = 2 * arr[j]
        while(i <= arr[n - 1] + arr[j]):

            # Fetch the index which is greater than or
            # equals to arr[i] by using binary search
            # inbuilt lower_bound() function of C++
            ind = 0
            for k in arr:
                if k >= i:
                    ind = arr.index(k)

            # Update the answer
            ans = max(ans, arr[ind - 1] % arr[j])
            i += arr[j]

    return ans

# Driver Code
arr = [3, 4, 5, 9, 11 ]
n = 5
print(maxModValue(arr, n))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to find Maximum modulo value
using System;

public class GFG {

    static int maxModValue(int[] arr, int n)
    {

        int ans = 0;

        // Sort the array[] by using inbuilt
        // sort function
        Array.Sort(arr);

        for (int j = n - 2; j >= 0; --j)
        {

            // Break loop if answer is greater
            // or equals to the arr[j] as any
            // number modulo with arr[j] can
            // only give maximum value up-to
            // arr[j]-1
            if (ans >= arr[j])
                break;

            // If both elements are same then
            // skip the next loop as it would
            // be worthless to repeat the
            // rest process for same value
            if (arr[j] == arr[j + 1])
                continue;

            for (int i = 2 * arr[j];
                      i <= arr[n - 1] + arr[j];
                                   i += arr[j])
            {

                // Fetch the index which is
                // greater than or equals to
                // arr[i] by using binary search

                int ind = Array.BinarySearch(arr, i);

                if (ind < 0)
                    ind = Math.Abs(ind + 1);

                else {
                    while (arr[ind] == i) {
                        ind--;

                        if (ind == 0) {
                            ind = -1;
                            break;
                        }
                    }
                    ind++;
                }

                // Update the answer
                ans = Math.Max(ans, arr[ind - 1]
                                       % arr[j]);
            }
        }

        return ans;
    }

    // Driver method
    public static void Main()
    {

        int[] arr = { 3, 4, 5, 9, 11 };

        Console.WriteLine(
                 maxModValue(arr, arr.Length));
    }
}

// This code is contributed by Sam007.
```

## java 描述语言

```
<script>

// JavaScript program to find Maximum modulo value

function maxModValue(arr, n) {
    let ans = 0;

    // Sort the array[] by using inbuilt sort function
    arr.sort((a, b) => a - b);

    for (let j = n - 2; j >= 0; --j) {
        // Break loop if answer is greater or equals to
        // the arr[j] as any number modulo with arr[j]
        // can only give maximum value up-to arr[j]-1
        if (ans >= arr[j])
            break;

        // If both elements are same then skip the next
        // loop as it would be worthless to repeat the
        // rest process for same value
        if (arr[j] == arr[j + 1])
            continue;

        for (let i = 2 * arr[j]; i <= arr[n - 1] + arr[j];
        i += arr[j])
        {
            // Fetch the index which is greater than or
            // equals to arr[i] by using binary search

            let ind = arr.indexOf(i);

            if (ind < 0)
                ind = Math.abs(ind) + 1;

            else {
                while (arr[ind] == i) {
                    ind--;

                    if (ind == 0) {
                        ind = -1;
                        break;
                    }
                }
                ind++;
            }

            // Update the answer
            ans = Math.max(ans, arr[ind - 1] % arr[j]);
        }
    }
    return ans;
}

// Driver method

let arr = [3, 4, 5, 9, 11];
document.write(maxModValue(arr, arr.length));

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(nlog(n) + Mlog(M))，其中 n 为元素总数，M 为所有元素的最大值。
**辅助空间:** O(1)
本博客由 [Shubham Bansal](https://www.quora.com/profile/Shubham-Bansal-209) 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。