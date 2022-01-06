# 最大化 arr[j]–arr[I]+arr[l]–arr[k]，这样我< j < k < l

> 原文:[https://www . geesforgeks . org/maximize-arrj-arri-arrl-arrk-so-I-j-k-l/](https://www.geeksforgeeks.org/maximize-arrj-arri-arrl-arrk-such-that-i-j-k-l/)

最大化 arr[j]–arr[I]+arr[l]–arr[k]，这样 i < j < k < l .求 arr[j]–arr[I]+arr[l]–arr[k]的最大值，这样 i < j < k < l

**示例:**

```
Let us say our array is {4, 8, 9, 2, 20}
Then the maximum such value is 23 (9 - 4 + 20 - 2)
```

**蛮力法:**
我们可以在给定约束的情况下，简单的找到所有大小为 4 的组合。最大值将是所需答案。这种方法效率很低。

**高效方法(动态规划):**
我们将使用动态规划来解决这个问题。为此，我们创建了四个一维 DP 表。
假设有四个 DP 表，分别为–表 1[]，表 2[]，表 3[]，表 4[]
然后求 arr[l]–arr[k]+arr[j]–arr[I]的最大值， 使得 i < j < k < l
表 1【】应存储 arr[l]
的最大值表 2【】应存储 arr[l]–arr[k]
的最大值表 3【】应存储 arr[l]–arr[k]+arr[j]的最大值表 4【】应存储 arr[l]–arr[k]+arr[j]–arr[I]
的最大值，则最大值将出现在索引中

以下是上述想法的实施–

## C++

```
/* A C++ Program to find maximum value of
arr[l] - arr[k] + arr[j] - arr[i] and i < j < k < l,
given that the array has atleast 4 elements */
#include <bits/stdc++.h>
using namespace std;

// To represent minus infinite
#define MIN -100000000

// A Dynamic Programming based function to find maximum
// value of arr[l] - arr[k] + arr[j] - arr[i] is maximum
// and i < j < k < l
int findMaxValue(int arr[], int n)
{
    // If the array has less than 4 elements
    if (n < 4)
    {
        printf("The array should have atlest 4 elements\n");
        return MIN;
    }

    // We create 4 DP tables
    int table1[n + 1], table2[n], table3[n - 1], table4[n - 2];

    // Initialize all the tables to MIN
    for (int i=0; i<=n; i++)
        table1[i] = table2[i] = table3[i] = table4[i] =  MIN;

    // table1[] stores the maximum value of arr[l]
    for (int i = n - 1; i >= 0; i--)
        table1[i] = max(table1[i + 1], arr[i]);

    // table2[] stores the maximum value of arr[l] - arr[k]
    for (int i = n - 2; i >= 0; i--)
        table2[i] = max(table2[i + 1], table1[i + 1] - arr[i]);

    // table3[] stores the maximum value of arr[l] - arr[k]
    // + arr[j]
    for (int i = n - 3; i >= 0; i--)
        table3[i] = max(table3[i + 1], table2[i + 1] + arr[i]);

    // table4[] stores the maximum value of arr[l] - arr[k]
    // + arr[j] - arr[i]
    for (int i = n - 4; i >= 0; i--)
        table4[i] = max(table4[i + 1], table3[i + 1] - arr[i]);

    /*for (int i = 0; i < n + 1; i++)
        cout << table1[i] << " " ;
    cout << endl;

    for (int i = 0; i < n; i++)
        cout << table2[i] << " " ;
    cout << endl;

    for (int i = 0; i < n - 1; i++)
        cout << table3[i] << " " ;
    cout << endl;

    for (int i = 0; i < n - 2; i++)
        cout << table4[i] << " " ;
    cout << endl;
    */

    // maximum value would be present in table4[0]
    return table4[0];
}

// Driver Program to test above functions
int main()
{
    int arr[] = { 4, 8, 9, 2, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("%d\n", findMaxValue(arr, n));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* A Java Program to find maximum value of
arr[l] - arr[k] + arr[j] - arr[i] and i < j < k < l,
given that the array has atleast 4 elements */
import java.util.Arrays;

class GFG
{
    // A Dynamic Programming based function
    // to find maximum value of
    // arr[l] - arr[k] + arr[j] - arr[i]
    // is maximum and i < j < k < l
    static int findMaxValue(int[] arr, int n)
    {

        // If the array has less than 4 elements
        if (n < 4)
        {
            System.out.println("The array should have" +
                               " atleast 4 elements");
        }

        // We create 4 DP tables
        int table1[] = new int[n + 1];
        int table2[] = new int[n];
        int table3[] = new int[n - 1];
        int table4[] = new int[n - 2];

        // Initialize all the tables to minus Infinity
        Arrays.fill(table1, Integer.MIN_VALUE);
        Arrays.fill(table2, Integer.MIN_VALUE);
        Arrays.fill(table3, Integer.MIN_VALUE);
        Arrays.fill(table4, Integer.MIN_VALUE);

        // table1[] stores the maximum value of arr[l]
        for (int i = n - 1; i >= 0; i--)
        {
            table1[i] = Math.max(table1[i + 1], arr[i]);
        }

        // table2[] stores the maximum value of
        // arr[l] - arr[k]
        for (int i = n - 2; i >= 0; i--)
        {
            table2[i] = Math.max(table2[i + 1],
                                 table1[i + 1] - arr[i]);
        }

        // table3[] stores the maximum value of
        // arr[l] - arr[k] + arr[j]
        for (int i = n - 3; i >= 0; i--)
            table3[i] = Math.max(table3[i + 1],
                                 table2[i + 1] + arr[i]);

        // table4[] stores the maximum value of
        // arr[l] - arr[k] + arr[j] - arr[i]
        for (int i = n - 4; i >= 0; i--)
            table4[i] = Math.max(table4[i + 1],
                                 table3[i + 1] - arr[i]);

        return table4[0];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 4, 8, 9, 2, 20 };
        int n = arr.length;
        System.out.println(findMaxValue(arr, n));
    }
}

// This code is contributed by Vivekkumar Singh
```

## 蟒蛇 3

```
# A Python3 Program to find maximum value of
# arr[l] - arr[k] + arr[j] - arr[i] and i < j < k < l,
# given that the array has atleast 4 elements

# A Dynamic Programming based function to find
# maximum value of arr[l] - arr[k] + arr[j] - arr[i]
# is maximum and i < j < k < l
def findMaxValue(arr, n):

    # If the array has less than 4 elements
    if n < 4:

        print("The array should have atlest 4 elements")
        return MIN

    # We create 4 DP tables
    table1, table2 = [MIN] * (n + 1), [MIN] * n
    table3, table4 = [MIN] * (n - 1), [MIN] * (n - 2)

    # table1[] stores the maximum value of arr[l]
    for i in range(n - 1, -1, -1):
        table1[i] = max(table1[i + 1], arr[i])

    # table2[] stores the maximum
    # value of arr[l] - arr[k]
    for i in range(n - 2, -1, -1):
        table2[i] = max(table2[i + 1],
                        table1[i + 1] - arr[i])

    # table3[] stores the maximum value of
    # arr[l] - arr[k] + arr[j]
    for i in range(n - 3, -1, -1):
        table3[i] = max(table3[i + 1],
                        table2[i + 1] + arr[i])

    # table4[] stores the maximum value of
    # arr[l] - arr[k] + arr[j] - arr[i]
    for i in range(n - 4, -1, -1):
        table4[i] = max(table4[i + 1],
                        table3[i + 1] - arr[i])

    # maximum value would be present in table4[0]
    return table4[0]

# Driver Code
if __name__ == "__main__":

    arr = [4, 8, 9, 2, 20]
    n = len(arr)

    # To represent minus infinite
    MIN = -100000000

    print(findMaxValue(arr, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# Program to find maximum value of
// arr[l] - arr[k] + arr[j] - arr[i]
// and i < j < k < l, given that
// the array has atleast 4 elements
using System;

class GFG
{
    // A Dynamic Programming based function
    // to find maximum value of
    // arr[l] - arr[k] + arr[j] - arr[i]
    // is maximum and i < j < k < l
    static int findMaxValue(int[] arr, int n)
    {

        // If the array has less than 4 elements
        if (n < 4)
        {
            Console.WriteLine("The array should have" +
                              " atleast 4 elements");
        }

        // We create 4 DP tables
        int []table1 = new int[n + 1];
        int []table2 = new int[n];
        int []table3 = new int[n - 1];
        int []table4 = new int[n - 2];

        // Initialize all the tables to minus Infinity
        fill(table1, int.MinValue);
        fill(table2, int.MinValue);
        fill(table3, int.MinValue);
        fill(table4, int.MinValue);

        // table1[] stores the maximum value of arr[l]
        for (int i = n - 1; i >= 0; i--)
        {
            table1[i] = Math.Max(table1[i + 1], arr[i]);
        }

        // table2[] stores the maximum value of
        // arr[l] - arr[k]
        for (int i = n - 2; i >= 0; i--)
        {
            table2[i] = Math.Max(table2[i + 1],
                                 table1[i + 1] - arr[i]);
        }

        // table3[] stores the maximum value of
        // arr[l] - arr[k] + arr[j]
        for (int i = n - 3; i >= 0; i--)
            table3[i] = Math.Max(table3[i + 1],
                                 table2[i + 1] + arr[i]);

        // table4[] stores the maximum value of
        // arr[l] - arr[k] + arr[j] - arr[i]
        for (int i = n - 4; i >= 0; i--)
            table4[i] = Math.Max(table4[i + 1],
                                 table3[i + 1] - arr[i]);

        return table4[0];
    }
    static void fill(int [] arr, int val)
    {
        for(int i = 0; i < arr.Length; i++)
            arr[i] = val;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 4, 8, 9, 2, 20 };
        int n = arr.Length;
        Console.WriteLine(findMaxValue(arr, n));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

/* A Javascript program to find maximum value of
arr[l] - arr[k] + arr[j] - arr[i] and i < j < k < l,
given that the array has atleast 4 elements */

// To represent minus infinite
let MIN = -100000000

// A Dynamic Programming based function to
// find maximum value of arr[l] - arr[k]
// + arr[j] - arr[i] is maximum and
// i < j < k < l
function findMaxValue(arr, n)
{

    // If the array has less than 4 elements
    if (n < 4)
    {
        document.write("The array should have " +
                       "atlest 4 elements\n");
        return MIN;
    }

    // We create 4 DP tables
    let table1 = new Array(n + 1);
    let table2 = new Array(n);
    let table3 = new Array(n - 1);
    let table4 = new Array(n - 2);

    // Initialize all the tables to MIN
    for(let i = 0; i <= n; i++)
        table1[i] = table2[i] =
        table3[i] = table4[i] = MIN;

    // table1[] stores the maximum value of arr[l]
    for(let i = n - 1; i >= 0; i--)
        table1[i] = Math.max(table1[i + 1], arr[i]);

    // table2[] stores the maximum value
    // of arr[l] - arr[k]
    for(let i = n - 2; i >= 0; i--)
        table2[i] = Math.max(table2[i + 1],
                             table1[i + 1] - arr[i]);

    // table3[] stores the maximum value of
    // arr[l] - arr[k] + arr[j]
    for(let i = n - 3; i >= 0; i--)
        table3[i] = Math.max(table3[i + 1],
                             table2[i + 1] + arr[i]);

    // table4[] stores the maximum value of
    // arr[l] - arr[k] + arr[j] - arr[i]
    for(let i = n - 4; i >= 0; i--)
        table4[i] = Math.max(table4[i + 1],
                             table3[i + 1] - arr[i]);

    /*for (int i = 0; i < n + 1; i++)
        cout << table1[i] << " " ;
    cout << endl;

    for (int i = 0; i < n; i++)
        cout << table2[i] << " " ;
    cout << endl;

    for (int i = 0; i < n - 1; i++)
        cout << table3[i] << " " ;
    cout << endl;

    for (int i = 0; i < n - 2; i++)
        cout << table4[i] << " " ;
    cout << endl;
    */

    // Maximum value would be present in table4[0]
    return table4[0];
}

// Driver code
let arr = [ 4, 8, 9, 2, 20 ];
let n = arr.length;

document.write(findMaxValue(arr, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
23
```

**时间复杂度:** O(n)，其中 n 是输入数组的大小
**辅助空间:**由于我们正在创建四个表来存储我们的值，空间为 4*O(n) = O(4*n) = O(n)

**给读者的练习:**
这个问题简单却有力。在给定的条件下，这个问题可以推广到任何表达式。求 arr[j]–2 * arr[I]+3 * arr[l]–7 * arr[k]的最大值，这样我< j < k < l
本文由**拉希特·贝尔瓦亚尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。