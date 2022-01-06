# 给定三元阵列中以 0 为多数元素的子阵列的最小长度

> 原文:[https://www . geesforgeks . org/给定三进制数组中的最小子数组长度以 0 为多数元素/](https://www.geeksforgeeks.org/minimum-length-of-subarray-in-given-ternary-array-having-0-as-the-majority-element/)

给定一个整数[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**的大小 **n** 只有三种类型的整数 **0，1**和**2**。求长度为 **> =2、**的阵列**arr【】**的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最小长度，使其 **0 的**频率大于 **1 的**和 **2 的**。如未找到打印 **-1** 。

> ***输入:*** arr[] = {2，0，2，0，1，2，2}
> ***输出:*** 3
> **解释:** {0，2，0}从索引[2，4]来看是频率为 0 的子阵列，频率大于 1 和 2 的频率。
> 
> ***输入:*** arr[] = {2，2，2，2}
> ***输出:*** -1

**天真方法:**这个问题可以通过遍历每个子阵列，检查 **0、1**和**2**的频率，检查**0**的频率是否大于**2**和**1**的频率，然后存储子阵列的最小长度作为答案来完成。

***时间复杂度:** O(n*n)*
***辅助空间:** O(1)*

**有效方法:**由于只有 3 种类型的整数，满足上述条件的可能长度子阵列 **> =2** 将是

> {0, 0}, {0, 1, 0}, {0, 2, 0}, {0, 1, 2, 0}, {0, 2, 1, 0}, {0, 0, 0, 1, 1, 2, 2}, ….

子阵列的最大可能最小长度为 **7** 。长度为> 7 的满足上述条件的任何其他子阵列将包含上述任何子阵列，因此满足上述条件的子阵列的最大可能长度为 7。

请按照以下步骤解决此问题:

*   将变量**最小长度**初始化为[最大值](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/)
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，n)** 中迭代，并执行以下任务:
    *   [初始化一个数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **用初始频率 **0** 计数[]**
    *   使用**计数[arr[i]]+，增加 **arr[i]** 的频率。**
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，min(n，I+7)】**中迭代，并执行以下任务:
        *   使用**增加 **arr[j]** 的频率，计算每个子阵列大小 **< =7** 的[arr[j]]+【T3]。**
        *   如果**计数【0】**大于**计数【1】**和**计数【2】**并且如果**最小长度> j-i+1** 则分配**最小长度= j-i+1**
*   如果 **min_length** 等于 **INT_MAX** 返回 **-1。**
*   否则打印 **min_length** 作为答案。

下面是上述方法的实现。

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// subarray length with most 0's
int minLength(vector<int> arr)
{
    int min_len = INT_MAX;
    int n = arr.size();

    // Traverse the array to check
    // the required condition
    for (int i = 0; i < n; i++) {

        // Initialize a vector count
        // to store the frequencies
        int count[3] = { 0 };
        count[arr[i]]++;

        // Check all subarrays of length
        // <=7 and count the frequencies
        for (int j = i + 1; j < min(n, i + 7); j++) {
            count[arr[j]]++;

            // If the frequency of 0's is
            // greater than both 1's and 2's
            // then take length of minimum subarray
            if (count[0] > count[1]
                && count[0] > count[2])
                min_len = min(min_len, j - i + 1);
        }
    }

    // If min_len == INT_MAX we have no subarray
    // satisfying the condition return -1;
    if (min_len == INT_MAX)
        min_len = -1;

    return min_len;
}

// Driver Code
int main()
{

    // Initializing list of nums
    vector<int> arr = { 2, 0, 2, 0, 1, 2, 2, 2 };

    // Call the function and print the answer
    cout << (minLength(arr));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the minimum
    // subarray length with most 0's
    static int minLength(ArrayList arr)
    {
        int min_len = Integer.MAX_VALUE;
        int n = arr.size();

        // Traverse the array to check
        // the required condition
        for (int i = 0; i < n; i++) {

            // Initialize a vector count
            // to store the frequencies
            int[] count = new int[3];
            for (int j = 0; j < 3; j++) {
                count[j] = 0;
            }

            int x = (int)arr.get(i);
            count[x]++;

            // Check all subarrays of length
            // <=7 and count the frequencies
            for (int j = i + 1; j < Math.min(n, i + 7);
                 j++) {
                int y = (int)arr.get(j);
                count[y]++;

                // If the frequency of 0's is
                // greater than both 1's and 2's
                // then take length of minimum subarray
                if (count[0] > count[1]
                    && count[0] > count[2])
                    min_len = Math.min(min_len, j - i + 1);
            }
        }

        // If min_len == INT_MAX we have no subarray
        // satisfying the condition return -1;
        if (min_len == Integer.MAX_VALUE)
            min_len = -1;

        return min_len;
    }

    // Driver Code
    public static void main(String[] args)
    {
        ArrayList<Integer> arr = new ArrayList<Integer>();

        arr.add(2);
        arr.add(0);
        arr.add(2);
        arr.add(0);
        arr.add(1);
        arr.add(2);
        arr.add(2);
        arr.add(2);

        // Count of isograms in string array arr[]
        System.out.println(minLength(arr));
    }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# python code for the above approach
INT_MAX = 2147483647

# Function to find the minimum
# subarray length with most 0's
def minLength(arr):

    min_len = INT_MAX
    n = len(arr)

    # Traverse the array to check
    # the required condition
    for i in range(0, n):

        # Initialize a vector count
        # to store the frequencies
        count = [0, 0, 0]
        count[arr[i]] += 1

        # Check all subarrays of length
        # <=7 and count the frequencies
        for j in range(i+1, min(n, i+7)):
            count[arr[j]] += 1

            # If the frequency of 0's is
            # greater than both 1's and 2's
            # then take length of minimum subarray
            if (count[0] > count[1] and count[0] > count[2]):
                min_len = min(min_len, j - i + 1)

    # If min_len == INT_MAX we have no subarray
    # satisfying the condition return -1;
    if (min_len == INT_MAX):
        min_len = -1

    return min_len

# Driver Code
if __name__ == "__main__":

    # Initializing list of nums
    arr = [2, 0, 2, 0, 1, 2, 2, 2]

    # Call the function and print the answer
    print(minLength(arr))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;

class GFG{

// Function to find the minimum
// subarray length with most 0's
static int minLength(ArrayList arr)
{
    int min_len = Int32.MaxValue;
    int n = arr.Count;

    // Traverse the array to check
    // the required condition
    for (int i = 0; i < n; i++) {

        // Initialize a vector count
        // to store the frequencies
        int []count = new int[3];
        for(int j = 0; j < 3; j++) {
            count[j] = 0;
        }

        int x = (int)arr[i];
        count[x]++;

        // Check all subarrays of length
        // <=7 and count the frequencies
        for (int j = i + 1; j < Math.Min(n, i + 7); j++) {
          int y = (int)arr[j];
            count[y]++;

            // If the frequency of 0's is
            // greater than both 1's and 2's
            // then take length of minimum subarray
            if (count[0] > count[1]
                && count[0] > count[2])
                min_len =   Math.Min(min_len, j - i + 1);
        }
    }

    // If min_len == INT_MAX we have no subarray
    // satisfying the condition return -1;
    if (min_len == Int32.MaxValue)
        min_len = -1;

    return min_len;
}

// Driver Code
public static void Main()
{
    ArrayList arr = new ArrayList();

    arr.Add(2);
    arr.Add(0);
    arr.Add(2);
    arr.Add(0);
    arr.Add(1);
    arr.Add(2);
    arr.Add(2);
    arr.Add(2);

    // Count of isograms in string array arr[]
    Console.WriteLine(minLength(arr));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
    // JavaScript code for the above approach
    const INT_MAX = 2147483647

    // Function to find the minimum
    // subarray length with most 0's
    const minLength = (arr) => {
        let min_len = INT_MAX;
        let n = arr.length;

        // Traverse the array to check
        // the required condition
        for (let i = 0; i < n; i++) {

            // Initialize a vector count
            // to store the frequencies
            let count = [0, 0, 0];
            count[arr[i]]++;

            // Check all subarrays of length
            // <=7 and count the frequencies
            for (let j = i + 1; j < Math.min(n, i + 7); j++) {
                count[arr[j]]++;

                // If the frequency of 0's is
                // greater than both 1's and 2's
                // then take length of minimum subarray
                if (count[0] > count[1]
                    && count[0] > count[2])
                    min_len = Math.min(min_len, j - i + 1);
            }
        }

        // If min_len == INT_MAX we have no subarray
        // satisfying the condition return -1;
        if (min_len == INT_MAX)
            min_len = -1;

        return min_len;
    }

    // Driver Code

    // Initializing list of nums
    let arr = [2, 0, 2, 0, 1, 2, 2, 2];

    // Call the function and print the answer
    document.write(minLength(arr));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
3
```

***时间复杂度:**O(n)*
T5**辅助空间:** O(1)