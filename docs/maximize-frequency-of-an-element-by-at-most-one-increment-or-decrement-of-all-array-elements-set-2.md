# 最多增加或减少一个数组元素的频率|设置 2

> 原文:[https://www . geeksforgeeks . org/最多增加或减少一个数组元素的频率-集合-2/](https://www.geeksforgeeks.org/maximize-frequency-of-an-element-by-at-most-one-increment-or-decrement-of-all-array-elements-set-2/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过将每个数组元素递增或递减 **1** 至多一次来找到任意数组元素[的最大频率。](https://www.geeksforgeeks.org/frequent-element-array/)

**示例:**

> ***输入:** arr[] = { 3，1，4，1，5，9，2 }*
> ***输出:** 4*
> ***解释:***
> *将 arr[0]的值减 1 将 arr[]修改为{ 2，1，4，1，5，9，2 }*
> *将 arr[1]的值增加 1 将 arr[]修改为{ 0 2 }*
> *将 arr[3]的值增加 1 会将 arr[]修改为{ 2，2，4，1，5，9，2 }*
> *因此，数组元素(arr[0])的频率为 4，这是最大可能值。*
> 
> ***输入:** arr[] = { 0，1，2，3，4，5，6 }*
> ***输出:** 3*
> ***解释:***
> *将 arr[0]的值递增 1 将 arr[]修改为{ 1，1，2，3，4，5，6 }*
> *将 arr[2]的值递减 1 将 arr[]修改为{ 0*

**贪婪方法:**解决这个问题的贪婪方法已经在本文的[集 1 中讨论过了。](https://www.geeksforgeeks.org/maximize-frequency-of-an-element-by-at-most-one-increment-or-decrement-of-all-array-elements/) 

**频率计数方法:**想法是创建一个频率数组，并存储数组所有元素的[频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)**arr【I】。**现在，对于元素的每个可能值，尝试将左右值合并到这一点，即 **freq[i] + freq[i-1] + freq[i+1]。**按照以下步骤解决问题:

*   用值 **1e5 定义一个变量 **MAXN** 。**
*   [用值 **0 初始化一个数组**](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**freq【MAXN】**。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下任务:
    *   将**频率[arr[I]]【T1]的值增加 **1。****
*   用值 **-MAXN 初始化变量 **max_freq** 。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，MAXN-1)** ，并执行以下任务:
    *   将 **max_freq** 的值设置为 **max_freq** 或 **freq[i-1] + freq[i] + freq[i+1]的最大值。**
*   执行上述步骤后，打印 **max_freq** 的值作为答案。

下面是上述方法的实现。

## C++

```
// C++ program to implement the above approach
#include <bits/stdc++.h>
using namespace std;
#define MAXN 100005

// Function to maximize the frequency
// of an array element by incrementing or
// decrementing array elements at most once
void max_freq(int arr[], int N)
{

    // Store the frequency of each element
    int freq[MAXN];
    memset(freq, 0, sizeof(freq));

    for (int i = 0; i < N; i++) {
        freq[arr[i]]++;
    }

    // Iterate through each value
    // try to merge left and
    // right values to it
    int max_freq = -MAXN;
    for (int i = 1; i < MAXN - 1; i++) {
        max_freq = max(max_freq,
                       freq[i] + freq[i - 1]
                           + freq[i + 1]);
    }

    cout << max_freq;
}

// Driver Code
int main()
{

    int arr[] = { 3, 1, 4, 1, 5, 9, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    max_freq(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
import java.util.Arrays;

class GFG
{
    public static int MAXN = 100005;

    // Function to maximize the frequency
    // of an array element by incrementing or
    // decrementing array elements at most once
    public static void max_freq(int arr[], int N)
    {

        // Store the frequency of each element
        int[] freq = new int[MAXN];
        Arrays.fill(freq, 0);

        for (int i = 0; i < N; i++) {
            freq[arr[i]]++;
        }

        // Iterate through each value
        // try to merge left and
        // right values to it
        int max_freq = -MAXN;
        for (int i = 1; i < MAXN - 1; i++) {
            max_freq = Math.max(max_freq, freq[i] + freq[i - 1] + freq[i + 1]);
        }

        System.out.println(max_freq);
    }

    // Driver Code
    public static void main(String args[]) {

        int arr[] = { 3, 1, 4, 1, 5, 9, 2 };
        int N = arr.length;

        // Function call
        max_freq(arr, N);
    }
}

// This code is contributed by Saurabh Jaiswal
```

## 蟒蛇 3

```
# Python3 program to implement the above approach
MAXN = 100005;

# Function to maximize the frequency
# of an array element by incrementing or
# decrementing array elements at most once
def max_freq(arr, N) :

    # Store the frequency of each element
    freq = [0] * MAXN;

    for i in range(N) :
        freq[arr[i]] += 1;

    # Iterate through each value
    # try to merge left and
    # right values to it
    max_freq = -MAXN;

    for i in range(1, MAXN - 1) :
        max_freq = max(max_freq, freq[i] + freq[i - 1] + freq[i + 1]);

    print(max_freq);

# Driver Code
if __name__ == "__main__" :

    arr = [ 3, 1, 4, 1, 5, 9, 2 ];
    N = len(arr);

    # Function call
    max_freq(arr, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program to implement the above approach
using System;
class GFG
{
    static int MAXN = 100005;

    // Function to maximize the frequency
    // of an array element by incrementing or
    // decrementing array elements at most once
    static void max_freq(int []arr, int N)
    {
        // Store the frequency of each element
        int []freq = new int[MAXN];
          Array.Clear(freq, 0, freq.Length);

        for (int i = 0; i < N; i++) {
            freq[arr[i]]++;
        }

        // Iterate through each value
        // try to merge left and
        // right values to it
        int max_freq = -MAXN;
        for (int i = 1; i < MAXN - 1; i++) {
            max_freq = Math.Max(max_freq, freq[i] + freq[i - 1] + freq[i + 1]);
        }

        Console.Write(max_freq);
    }

    // Driver Code
    public static void Main() {

        int []arr = { 3, 1, 4, 1, 5, 9, 2 };
        int N = arr.Length;

        // Function call
        max_freq(arr, N);
    }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach
        var MAXN = 100005

        // Function to maximize the frequency
        // of an array element by incrementing or
        // decrementing array elements at most once
        function max_freq(arr, N) {

            // Store the frequency of each element
            let freq = new Array(MAXN).fill(0);

            for (let i = 0; i < N; i++) {
                freq[arr[i]]++;
            }

            // Iterate through each value
            // try to merge left and
            // right values to it
            let max_freq = -MAXN;
            for (let i = 1; i < MAXN - 1; i++) {
                max_freq = Math.max(max_freq,
                    freq[i] + freq[i - 1]
                    + freq[i + 1]);
            }

            document.write(max_freq);
        }

        // Driver Code
        let arr = [3, 1, 4, 1, 5, 9, 2];
        let N = arr.length;

        // Function call
        max_freq(arr, N);

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
4
```

***时间复杂度:** O(N)*
***辅助空间:** O(|Max|)，其中 Max 是数组中最大的元素*