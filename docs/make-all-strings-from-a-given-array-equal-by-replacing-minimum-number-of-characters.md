# 通过替换最小数量的字符使给定数组中的所有字符串相等

> 原文:[https://www . geesforgeks . org/通过替换最小字符数使给定数组中的所有字符串相等/](https://www.geeksforgeeks.org/make-all-strings-from-a-given-array-equal-by-replacing-minimum-number-of-characters/)

给定一个等长字符串的[数组](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/) **arr[]** ，任务是通过用任意其他字符替换字符串的任意字符，使数组中的所有字符串相等，次数最少。

**示例:**

> **输入:** arr[] = {“西”、“东”、“等”}
> **输出:** 3
> **解释:**
> 将 arr[0][1]替换为‘a’将 arr[]修改为{“西”、“东”、“等”}。
> 将 arr[1][0]替换为“w”将 arr[]修改为{“wast”、“wast”、“wait”}。
> 将 arr[2][2]替换为“s”将 arr[]修改为{“wast”、“wast”、“wast”}。
> 因此，要求输出为 3。
> 
> **输入:**arr[]= {“ABCD”、“bcde”、“cdef”}
> T3】输出: 8

**方法:**使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)可以解决问题。按照以下步骤解决问题:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如说**hash【】【】**，其中**hash【I】【j】**存储所有字符串的**j**索引处出现的字符 **i** 的频率。
*   [使用变量 **i** 遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】。对于遇到的每一个 **i <sup>th</sup>** 字符串，计算字符串中每个不同字符的频率，并将其存储到**hash【】【】**数组中。
*   初始化一个变量，比如 **cntMinOp** ，以存储使数组中所有字符串相等所需的最小操作数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **散列[][]** 使用变量 **i** 。对于遇到的每一个 **i <sup>th</sup>** 列，计算该列的和，说 **Sum** ，列中最大的元素，说 **Max** ，更新**cntMinOp+=(Sum–Max)**。
*   最后，打印 **cntMinOp** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count of
// operations required to make all strings
// equal by replacing characters of strings
int minOperation(string arr[], int N)
{

    // Stores minimum count of operations
    // required to make all strings equal
    int cntMinOP = 0;

    // Stores length of the string
    int M = arr[0].length();

    // hash[i][j]: Stores frequency of character
    // i present at j-th index of all strings
    int hash[256][M];

    // Initialize hash[][] to 0
    memset(hash, 0, sizeof(hash));

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Iterate over characters of
        // current string
        for (int j = 0; j < M; j++) {

            // Update frequency of
            // arr[i][j]
            hash[arr[i][j]][j]++;
        }
    }

    // Traverse hash[][] array
    for (int i = 0; i < M; i++) {

        // Stores sum of i-th column
        int Sum = 0;

        // Stores the largest element
        // of i-th column
        int Max = 0;

        // Iterate over all possible
        // characters
        for (int j = 0; j < 256; j++) {

            // Update Sum
            Sum += hash[j][i];

            // Update Max
            Max = max(Max, hash[j][i]);
        }

        // Update cntMinOP
        cntMinOP += (Sum - Max);
    }

    return cntMinOP;
}

// Driver Code
int main()
{

    string arr[] = { "abcd", "bcde", "cdef" };

    int N = sizeof(arr) / sizeof(arr[0]);
    // Function call
    cout << minOperation(arr, N) << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to find the minimum count of
// operations required to make all Strings
// equal by replacing characters of Strings
static int minOperation(String arr[], int N)
{

    // Stores minimum count of operations
    // required to make all Strings equal
    int cntMinOP = 0;

    // Stores length of the String
    int M = arr[0].length();

    // hash[i][j]: Stores frequency of character
    // i present at j-th index of all Strings
    int [][]hash = new int[256][M];

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // Iterate over characters of
        // current String
        for (int j = 0; j < M; j++)
        {

            // Update frequency of
            // arr[i][j]
            hash[arr[i].charAt(j)][j]++;
        }
    }

    // Traverse hash[][] array
    for (int i = 0; i < M; i++)
    {

        // Stores sum of i-th column
        int Sum = 0;

        // Stores the largest element
        // of i-th column
        int Max = 0;

        // Iterate over all possible
        // characters
        for (int j = 0; j < 256; j++)
        {

            // Update Sum
            Sum += hash[j][i];

            // Update Max
            Max = Math.max(Max, hash[j][i]);
        }

        // Update cntMinOP
        cntMinOP += (Sum - Max);
    }

    return cntMinOP;
}

// Driver Code
public static void main(String[] args)
{
    String arr[] = { "abcd", "bcde", "cdef" };
    int N = arr.length;

    // Function call
    System.out.print(minOperation(arr, N)+ "\n");
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find the minimum count of
# operations required to make all Strings
# equal by replacing characters of Strings
def minOperation(arr, N):

    # Stores minimum count of operations
    # required to make all Strings equal
    cntMinOP = 0;

    # Stores length of the String
    M = len(arr[0]);

    # hash[i][j]: Stores frequency of character
    # i present at j-th index of all Strings
    hash = [[0 for i in range(M)] for j in range(256)];

    # Traverse the array arr
    for i in range(N):

        # Iterate over characters of
        # current String
        for j in range(M):

            # Update frequency of
            # arr[i][j]
            hash[ord(arr[i][j])][j] += 1;

    # Traverse hash array
    for i in range(M):

        # Stores sum of i-th column
        Sum = 0;

        # Stores the largest element
        # of i-th column
        Max = 0;

        # Iterate over all possible
        # characters
        for j in range(256):

            # Update Sum
            Sum += hash[j][i];

            # Update Max
            Max = max(Max, hash[j][i]);

        # Update cntMinOP
        cntMinOP += (Sum - Max);
    return cntMinOP;

# Driver Code
if __name__ == '__main__':
    arr = ["abcd", "bcde", "cdef"];
    N = len(arr);

    # Function call
    print(minOperation(arr, N));

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

// Function to find the minimum count of
// operations required to make all Strings
// equal by replacing characters of Strings
static int minOperation(String []arr, int N)
{

    // Stores minimum count of operations
    // required to make all Strings equal
    int cntMinOP = 0;

    // Stores length of the String
    int M = arr[0].Length;

    // hash[i,j]: Stores frequency of character
    // i present at j-th index of all Strings
    int [,]hash = new int[256, M];

    // Traverse the array []arr
    for (int i = 0; i < N; i++)
    {

        // Iterate over characters of
        // current String
        for (int j = 0; j < M; j++)
        {

            // Update frequency of
            // arr[i,j]
            hash[arr[i][j], j]++;
        }
    }

    // Traverse hash[,] array
    for (int i = 0; i < M; i++)
    {

        // Stores sum of i-th column
        int Sum = 0;

        // Stores the largest element
        // of i-th column
        int Max = 0;

        // Iterate over all possible
        // characters
        for (int j = 0; j < 256; j++)
        {

            // Update Sum
            Sum += hash[j, i];

            // Update Max
            Max = Math.Max(Max, hash[j, i]);
        }

        // Update cntMinOP
        cntMinOP += (Sum - Max);
    }
    return cntMinOP;
}

// Driver Code
public static void Main(String[] args)
{
    String []arr = { "abcd", "bcde", "cdef" };
    int N = arr.Length;

    // Function call
    Console.Write(minOperation(arr, N)+ "\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the minimum count of
// operations required to make all strings
// equal by replacing characters of strings
function minOperation(arr, N)
{

    // Stores minimum count of operations
    // required to make all strings equal
    var cntMinOP = 0;

    // Stores length of the string
    var M = arr[0].length;

    // hash[i][j]: Stores frequency of character
    // i present at j-th index of all strings
    var hash = Array.from(Array(256), ()=>Array(M).fill(0));

    // Traverse the array arr[]
    for (var i = 0; i < N; i++) {

        // Iterate over characters of
        // current string
        for (var j = 0; j < M; j++) {

            // Update frequency of
            // arr[i][j]
            hash[arr[i][j].charCodeAt(0)][j]++;
        }
    }

    // Traverse hash[][] array
    for (var i = 0; i < M; i++) {

        // Stores sum of i-th column
        var Sum = 0;

        // Stores the largest element
        // of i-th column
        var Max = 0;

        // Iterate over all possible
        // characters
        for (var j = 0; j < 256; j++) {

            // Update Sum
            Sum += hash[j][i];

            // Update Max
            Max = Math.max(Max, hash[j][i]);
        }

        // Update cntMinOP
        cntMinOP += (Sum - Max);
    }

    return cntMinOP;
}

// Driver Code

var arr = ["abcd", "bcde", "cdef"];
var N = arr.length;

// Function call
document.write( minOperation(arr, N) + "<br>");

</script>
```

**Output:** 

```
8
```

***时间复杂度:** O(N * (M + 256))，其中 M 是字符串的长度*
***辅助空间:** O(M + 256)*