# 大小为 k 的子集的乘积中尾随零的最大数量

> 原文:[https://www . geeksforgeeks . org/大小为 k 的子集中尾随零的最大数量/](https://www.geeksforgeeks.org/maximum-number-of-trailing-zeros-in-the-product-of-the-subsets-of-size-k/)

给定大小为 n 和正整数 k 的数组，求大小为 k 的子集乘积中尾随零的最大数量。
示例:

```
Input : arr = {50, 4, 20}
        k = 2
Output : 3
Here, we have 3 subsets of size 2\. [50, 4] 
has product 200, having 2 zeros at the end, 
[4, 20] — product 80, having 1 zero at the 
end, [50, 20] — product 1000, having 3 zeros
at the end. Therefore, the maximum zeros at
the end of the product is 3.

Input : arr = {15, 16, 3, 25, 9}
        k = 3
Output : 3
Here, the subset [15, 16, 25] has product 6000.

Input : arr = {9, 77, 13}
        k = 3
Output : 0
Here, the subset [9, 77, 13] has product 9009
having no zeros at the end.
```

**动态规划法:**
显然，数字末尾的零的个数是由数字中 **2** 和 **5** 的最小幂决定的。设 **pw5** 为数量上 **5** 的最大功率， **pw2** 为 **2** 的最大功率。
假设，**子集【I】【j】**是我们可以收集的最大 2s 数量，考虑到 **i** 个数字中的每一个都有 j 个 5s。
我们遍历给定的所有个数，对于每个数组元素，我们统计其中 2s 和 5s 的个数。设 pw2 为当前数中的 2s 数，pw5 为 5s 数。
现在**子集【I】【j】**:
//对于当前数(pw2 二和 pw5 五)我们检查
//是否可以增加子集【I】【j】的值。
子集[i][j] = max(子集[i][j]，子集[i-1][j-pw5] + pw2)
以上表达式也可以写成如下。
**子集[i + 1][j + pw5] = max(子集[i + 1][j + pw5]，子集[I][j]+pw2)；**
答案将是**最大值(ans，min(i，子集[k][i])**

## C++

```
// CPP program for finding the maximum number
// of trailing zeros in the product of the
// selected subset of size k.
#include <bits/stdc++.h>
using namespace std;
#define MAX5 100

// Function to calculate maximum zeros.
int maximumZeros(int* arr, int n, int k)
{
    // Initializing each value with -1;
    int subset[k+1][MAX5+5];   
    memset(subset, -1, sizeof(subset));

    subset[0][0] = 0;

    for (int p = 0; p < n; p++) {
        int pw2 = 0, pw5 = 0;

        // Calculating maximal power of 2 for
        // arr[p].
        while (arr[p] % 2 == 0) {
            pw2++;
            arr[p] /= 2;
        }

        // Calculating maximal power of 5 for
        // arr[p].
        while (arr[p] % 5 == 0) {
            pw5++;
            arr[p] /= 5;
        }

        // Calculating subset[i][j] for maximum
        // amount of twos we can collect by
        // checking first i numbers and taking
        // j of them with total power of five.
        for (int i = k - 1; i >= 0; i--)
            for (int j = 0; j < MAX5; j++)

                // If subset[i][j] is not calculated.
                if (subset[i][j] != -1)
                    subset[i + 1][j + pw5] =
                    max(subset[i + 1][j + pw5],
                         subset[i][j] + pw2);
    }

    // Calculating maximal number of zeros.
    // by taking minimum of 5 or 2 and then
    // taking maximum.
    int ans = 0;
    for (int i = 0; i < MAX5; i++)
        ans = max(ans, min(i, subset[k][i]));

    return ans;
}

// Driver function
int main()
{
    int arr[] = { 50, 4, 20 };
    int k = 2;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maximumZeros(arr, n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java program for finding the maximum number
// of trailing zeros in the product of the
// selected subset of size k.
class GFG {

    final static int MAX5 = 100;

// Function to calculate maximum zeros.
    static int maximumZeros(int arr[], int n, int k) {
        // Initializing each value with -1;
        int subset[][] = new int[k + 1][MAX5 + 5];
        // Fill each row with 1.0
        for (int[] row : subset) {
            Arrays.fill(row, -1);
        }
        //memset(subset, -1, sizeof(subset));

        subset[0][0] = 0;

        for (int p = 0; p < n; p++) {
            int pw2 = 0, pw5 = 0;

            // Calculating maximal power of 2 for
            // arr[p].
            while (arr[p] % 2 == 0) {
                pw2++;
                arr[p] /= 2;
            }

            // Calculating maximal power of 5 for
            // arr[p].
            while (arr[p] % 5 == 0) {
                pw5++;
                arr[p] /= 5;
            }

            // Calculating subset[i][j] for maximum
            // amount of twos we can collect by
            // checking first i numbers and taking
            // j of them with total power of five.
            for (int i = k - 1; i >= 0; i--) {
                for (int j = 0; j < MAX5; j++) // If subset[i][j] is not calculated.
                {
                    if (subset[i][j] != -1) {
                        subset[i + 1][j + pw5]
                                = Math.max(subset[i + 1][j + pw5],
                                        subset[i][j] + pw2);
                    }
                }
            }
        }

        // Calculating maximal number of zeros.
        // by taking minimum of 5 or 2 and then
        // taking maximum.
        int ans = 0;
        for (int i = 0; i < MAX5; i++) {
            ans = Math.max(ans, Math.min(i, subset[k][i]));
        }

        return ans;
    }

// Driver function
    public static void main(String[] args) {
        int arr[] = {50, 4, 20};
        int k = 2;
        int n = arr.length;
        System.out.println(maximumZeros(arr, n, k));

    }
}
//this code contributed by 29AJayKumar
```

## 蟒蛇 3

```
# Python3 program for finding the maximum number
# of trailing zeros in the product of the
# selected subset of size k.
MAX5 = 100

# Function to calculate maximum zeros.
def maximumZeros(arr, n, k):
    global MAX5

    # Initializing each value with -1
    subset = [[-1] * (MAX5 + 5) for _ in range(k + 1)]

    subset[0][0] = 0

    for p in arr:

        pw2, pw5 = 0, 0

        # Calculating maximal power
        # of 2 for arr[p].
        while not p % 2 :
            pw2 += 1
            p //= 2

        # Calculating maximal power
        # of 5 for arr[p].
        while not p % 5 :
            pw5 += 1
            p //= 5

        # Calculating subset[i][j] for maximum
        # amount of twos we can collect by
        # checking first i numbers and taking
        # j of them with total power of five.
        for i in range(k-1, -1, -1):

            for j in range(MAX5):

                # If subset[i][j] is not calculated.
                if subset[i][j] != -1:
                    subset[i + 1][j + pw5] = (
                        max(subset[i + 1][j + pw5],
                        (subset[i][j] + pw2)))

    # Calculating maximal number of zeros.
    # by taking minimum of 5 or 2 and then
    # taking maximum.
    ans = 0
    for i in range(MAX5):
        ans = max(ans, min(i, subset[k][i]))

    return ans

# Driver function
arr = [ 50, 4, 20 ]
k = 2
n = len(arr)

print(maximumZeros(arr, n, k))

# This code is contributed by Ansu Kumari.
```

## C#

```

// C# program for finding the maximum number
// of trailing zeros in the product of the
// selected subset of size k.
using System;
public class GFG {

static readonly int MAX5 = 100;
// Function to calculate maximum zeros.
    static int maximumZeros(int []arr, int n, int k) {
        // Initializing each value with -1;
        int [,]subset = new int[k + 1,MAX5 + 5];
        // Fill each row with 1.0
        for (int i = 0; i < subset.GetLength(0); i++)
            for (int j = 0; j < subset.GetLength(1); j++)
                subset[i,j] = -1;

        subset[0,0] = 0;

        for (int p = 0; p < n; p++) {
            int pw2 = 0, pw5 = 0;

            // Calculating maximal power of 2 for
            // arr[p].
            while (arr[p] % 2 == 0) {
                pw2++;
                arr[p] /= 2;
            }

            // Calculating maximal power of 5 for
            // arr[p].
            while (arr[p] % 5 == 0) {
                pw5++;
                arr[p] /= 5;
            }

            // Calculating subset[i][j] for maximum
            // amount of twos we can collect by
            // checking first i numbers and taking
            // j of them with total power of five.
            for (int i = k - 1; i >= 0; i--) {
                for (int j = 0; j < MAX5; j++) // If subset[i][j] is not calculated.
                {
                    if (subset[i,j] != -1) {
                        subset[i + 1,j + pw5]
                                = Math.Max(subset[i + 1,j + pw5],
                                        subset[i,j] + pw2);
                    }
                }
            }
        }

        // Calculating maximal number of zeros.
        // by taking minimum of 5 or 2 and then
        // taking maximum.
        int ans = 0;
        for (int i = 0; i < MAX5; i++) {
            ans = Math.Max(ans, Math.Min(i, subset[k,i]));
        }
        return ans;
    }

    // Driver function
    public static void Main() {
        int []arr = {50, 4, 20};
        int k = 2;
        int n = arr.Length;
        Console.Write(maximumZeros(arr, n, k));

    }
}
//this code contributed by 29AJayKumar
```

## java 描述语言

```
<script>
    // Javascript program for finding the maximum number
    // of trailing zeros in the product of the
    // selected subset of size k.

    let MAX5 = 100;

    // Function to calculate maximum zeros.
    function maximumZeros(arr, n, k)
    {
        // Initializing each value with -1;
        let subset = new Array(k+1);
        for(let i = 0; i < k + 1; i++)
        {
            subset[i] = new Array(MAX5+5);
            for(let j = 0; j < MAX5+5; j++)
            {
                subset[i][j] = -1;
            }
        }

        subset[0][0] = 0;

        for (let p = 0; p < n; p++) {
            let pw2 = 0, pw5 = 0;

            // Calculating maximal power of 2 for
            // arr[p].
            while (arr[p] % 2 == 0) {
                pw2++;
                arr[p] = parseInt(arr[p] / 2, 10);
            }

            // Calculating maximal power of 5 for
            // arr[p].
            while (arr[p] % 5 == 0) {
                pw5++;
                arr[p] = parseInt(arr[p] / 5, 10);
            }

            // Calculating subset[i][j] for maximum
            // amount of twos we can collect by
            // checking first i numbers and taking
            // j of them with total power of five.
            for (let i = k - 1; i >= 0; i--)
                for (let j = 0; j < MAX5; j++)

                    // If subset[i][j] is not calculated.
                    if (subset[i][j] != -1)
                        subset[i + 1][j + pw5] =
                        Math.max(subset[i + 1][j + pw5],
                             subset[i][j] + pw2);
        }

        // Calculating maximal number of zeros.
        // by taking minimum of 5 or 2 and then
        // taking maximum.
        let ans = 0;
        for (let i = 0; i < MAX5; i++)
            ans = Math.max(ans, Math.min(i, subset[k][i]));

        return ans;
    }

      let arr = [ 50, 4, 20 ];
    let k = 2;
    let n = arr.length;
    document.write(maximumZeros(arr, n, k));

    // This code is contributed by divyesh072019.
</script>
```

**Output :** 

```
3
```