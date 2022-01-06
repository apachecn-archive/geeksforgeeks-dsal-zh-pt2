# 给定数组中具有奇数位“与”值的子序列的计数

> 原文:[https://www . geeksforgeeks . org/给定数组中具有奇数位和值的子序列计数/](https://www.geeksforgeeks.org/count-of-subsequences-having-odd-bitwise-and-values-in-the-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找出给定数组的[个子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量，使得它们的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值为奇数。

**示例:**

> **输入:** arr[] = {2，3，1}
> **输出:** 3
> **解释:**给定数组中具有奇数位“与”值的子序列为 **{3}** = 3、 **{1}** = 1、 **{3，1}** = 3 & 1 = 1。
> 
> **输入:** arr[] = {1，3，3 }
> T3】输出: 7

[推荐:请先在 ***{IDE}*** 上尝试你的方法，然后再进入解决方案。](https://ide.geeksforgeeks.org/)

**天真方法:**给定的问题可以通过[生成给定数组的所有子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)**arr【】**并跟踪子序列的计数，使得它们的按位与值为奇数来解决。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过观察进行优化，即对于一组整数的位与值为奇数，该组中每个元素的最低有效位必须是一个[设置位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)。因此，对于具有奇数位“与”值的子序列，子序列的所有元素都必须是奇数。利用这一观察，可以使用以下步骤解决给定的问题:

*   创建一个变量**奇数**，它存储给定数组 **arr[]** 中奇数的总数[。用 **0** 初始化。](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)
*   [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，如果当前整数为奇数，则将**奇数**的值增加 **1** 。
*   具有 **X** 元素的数组的非空子序列的计数是**2<sup>X</sup>–1**。因此，包含所有奇数元素的非空子序列的个数为 **2 <sup>奇数</sup>–1**，这是需要的答案。

以下是该方法的实施情况:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find count of subsequences
// having odd bitwise AND value
int countSubsequences(vector<int> arr)
{
    // Stores count of odd elements
    int odd = 0;

    // Traverse the array arr[]
    for (int x : arr) {

        // If x is odd increment count
        if (x & 1)
            odd++;
    }

    // Return Answer
    return (1 << odd) - 1;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 3, 3 };

    // Function Call
    cout << countSubsequences(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

    // Function to find count of subsequences
    // having odd bitwise AND value
    static int countSubsequences(int arr[], int N)
    {
        // Stores count of odd elements
        int odd = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // If x is odd increment count
            if ((arr[i] & 1) % 2 == 1)
                odd++;
        }

        // Return Answer
        return (1 << odd) - 1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 3;

        int arr[] = { 1, 3, 3 };
        // Function Call
        System.out.println(countSubsequences(arr, N));
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find count of subsequences
# having odd bitwise AND value
def countSubsequences(arr):

    # Stores count of odd elements
    odd = 0

    # Traverse the array arr[]
    for x in arr:

        # If x is odd increment count
        if (x & 1):
            odd = odd + 1

    # Return Answer
    return (1 << odd) - 1

# Driver Code
if __name__ == "__main__":

    arr = [1, 3, 3]

    # Function Call
    print(countSubsequences(arr))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

    // Function to find count of subsequences
    // having odd bitwise AND value
    static int countSubsequences(int []arr, int N)
    {

        // Stores count of odd elements
        int odd = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // If x is odd increment count
            if ((arr[i] & 1) % 2 == 1)
                odd++;
        }

        // Return Answer
        return (1 << odd) - 1;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int N = 3;

        int []arr = { 1, 3, 3 };

        // Function Call
        Console.WriteLine(countSubsequences(arr, N));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find count of subsequences
// having odd bitwise AND value
function countSubsequences(arr)
{
    // Stores count of odd elements
    let odd = 0;

    // Traverse the array arr[]
    for (let x = 0; x < arr.length; x++) {

        // If x is odd increment count
        if (arr[x] & 1)
            odd++;
    }

    // Return Answer
    return (1 << odd) - 1;
}

// Driver Code
    let arr = [ 1, 3, 3 ];

    // Function Call
    document.write(countSubsequences(arr));

// This code is contributed by subham348.
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)