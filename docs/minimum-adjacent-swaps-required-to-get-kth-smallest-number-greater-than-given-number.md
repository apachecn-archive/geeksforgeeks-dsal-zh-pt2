# 获得大于给定数量的第 k 个最小数量所需的最小相邻互换数量

> 原文:[https://www . geeksforgeeks . org/最小-相邻-交换-需要获取-kth-最小-数字-大于给定数字/](https://www.geeksforgeeks.org/minimum-adjacent-swaps-required-to-get-kth-smallest-number-greater-than-given-number/)

给定大小为 **N** 的[数字串](https://www.geeksforgeeks.org/splitting-numeric-string/) **S** 和正整数 **K** ，任务是找到 **S** 中所需的最小相邻交换次数，以获得大于给定串的 [**K <sup>th</sup> 最小数字串**](https://www.geeksforgeeks.org/get-the-kth-smallest-number-using-the-digits-of-the-given-number/) 。

**示例:**

> **输入:** S = "11112 "，K = 4
> **输出:** 4
> **说明:**
> K<sup>第</sup> (= 4 <sup>第</sup>)个大于给定字符串的最小数字字符串为“21111”。相邻互换到串“21111”的顺序为“11112”—>“111**21**—>11**21**1”—>1**21**11”—>“**21**111”。
> 因此，所需的 adacent 互换的最小数量是 4。
> 
> **输入:** S = "12345 "，K = 1
> **输出:** 1

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤解决问题:

*   将当前数值字符串的副本存储在一个变量中，比如 **res** 。
*   创建一个变量，比如 **totalSwaps** ，它存储所需的最小交换。
*   因为需要第 K 个最大数，所以这个语句等于[从当前字符串开始寻找第 K 个置换](https://www.geeksforgeeks.org/find-the-k-th-permutation-sequence-of-first-n-natural-numbers/)。
*   使用[函数](https://www.geeksforgeeks.org/functions-in-c/) [下一个 _ 排列()](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)找到第 K 个排列。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下任务:
    *   如果 **res[i]** 不等于 **str[i]** ，则将变量 **start** 初始化为 **i+1** 和[遍历一段时间循环](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)，直到 **res[i]** 不等于**str【start】**并将 **i** 的值增加 **1。**
    *   [循环](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **i** 不等于 **start** 和[交换值](https://www.geeksforgeeks.org/swap-in-cpp/)**str【start】**和**str【start–1】**，将 **start** 的值减少 **1** ，将 **totalSwaps** 的值增加 **1** 。
*   执行上述步骤后，打印 **totalSwaps** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of swaps required to make the Kth
// smallest string greater than str
void minSwapsKthLargest(string str, int k)
{
    // Store the copy of the string
    string res = str;

    // Find the K-th permutation of
    // the given numeric string
    for (int i = 0; i < k; i++) {
        next_permutation(
            str.begin(), str.end());
      cout<<"str = "<<str<<endl;
    }

    // Stores the count of swaps required
    int swap_count = 0;

    // Traverse the string and find the
    // swaps required greedily
    for (int i = 0; i < res.length(); i++) {

        // If both characters do not match
        if (res[i] != str[i]) {
            int start = i + 1;

            // Search from i+1 index
            while (res[i] != str[start]) {

                // Find the index to swap
                start++;
            }
            while (i != start) {
                swap(str[start], str[start - 1]);

                // Swap untill the characters
                // are at same index
                start--;
                swap_count++;
            }
        }
    }

    // Print the minimum number of counts
    cout << swap_count;
}

// Driver Code
int main()
{
    string S = "11112";
    int K = 4;
    minSwapsKthLargest(S, K);

    return 0;
}
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    static char[] next_permutation(char[] array)
    {
        int i = array.Length - 1;
        while (i > 0 && array[i - 1] >= array[i]) {
            i--;
        }

        int j = array.Length - 1;

        while (array[j] <= array[i - 1]) {
            j--;
        }

        char temp = array[i - 1];
        array[i - 1] = array[j];
        array[j] = temp;

        j = array.Length - 1;

        while (i < j) {
            temp = array[i];
            array[i] = array[j];
            array[j] = temp;
            i++;
            j--;
        }

        return array;
    }

    // Function to find the minimum number
    // of swaps required to make the Kth
    // smallest string greater than str
    static void minSwapsKthLargest(string str, int k)
    {
        // Store the copy of the string
        string res = str;
        char[] str1 = str.ToCharArray();

        // Find the K-th permutation of
        // the given numeric string
        for (int i = 0; i < k; i++) {
            next_permutation(str1);
        }

        // Stores the count of swaps required
        int swap_count = 0;

        // Traverse the string and find the
        // swaps required greedily
        for (int i = 0; i < res.Length; i++) {

            // If both characters do not match
            if (res[i] != str1[i]) {
                int start = i + 1;

                // Search from i+1 index
                while (res[i] != str1[start]) {

                    // Find the index to swap
                    start++;
                }
                while (i != start) {
                    char temp = str1[start];
                    str1[start] = str1[start - 1];
                    str1[start - 1] = temp;

                    // Swap untill the characters
                    // are at same index
                    start--;
                    swap_count++;
                }
            }
        }

        // Print the minimum number of counts
        Console.WriteLine(swap_count);
    }

    // Driver Code
    public static void Main()
    {
        string S = "11112";
        int K = 4;
        minSwapsKthLargest(S, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach
        function next_permutation(array)
        {
            var i = array.length - 1;
            while (i > 0 && array[i - 1].charCodeAt(0) >= array[i].charCodeAt(0)) {
                i--;

            }

            if (i <= 0) {
                return false;
            }

            var j = array.length - 1;

            while (array[j].charCodeAt(0) <= array[i - 1].charCodeAt(0)) {
                j--;
            }

            var temp = array[i - 1];
            array[i - 1] = array[j];
            array[j] = temp;

            j = array.length - 1;

            while (i < j) {
                temp = array[i];
                array[i] = array[j];
                array[j] = temp;
                i++;
                j--;
            }

            return array;
        }

        // Function to find the minimum number
        // of swaps required to make the Kth
        // smallest string greater than str
        function minSwapsKthLargest(str, k)
        {

            // Store the copy of the string
            let res = str.split('');
            str = str.split('')

            // Find the K-th permutation of
            // the given numeric string
            for (let i = 0; i < k; i++) {
                next_permutation(
                    str);
            }

            // Stores the count of swaps required
            let swap_count = 0;

            // Traverse the string and find the
            // swaps required greedily
            for (let i = 0; i < res.length; i++) {

                // If both characters do not match
                if (res[i] != str[i]) {
                    let start = i + 1;

                    // Search from i+1 index
                    while (res[i] != str[start]) {

                        // Find the index to swap
                        start++;
                    }
                    while (i != start) {
                        let temp = str[start];
                        str[start] = str[start - 1]
                        str[start - 1] = temp;

                        // Swap untill the characters
                        // are at same index
                        start--;
                        swap_count++;
                    }
                }
            }

            // Print the minimum number of counts
            document.write(swap_count);
        }

        // Driver Code
        let S = "11112";
        let K = 4;
        minSwapsKthLargest(S, K);

    // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*(N + K))*
***辅助空间:** O(N)*