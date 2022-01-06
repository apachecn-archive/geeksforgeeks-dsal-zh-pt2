# 使字符串不含子序列的最小成本

> 原文:[https://www . geeksforgeeks . org/无字符串生成子序列的最低成本/](https://www.geeksforgeeks.org/minimum-cost-to-make-a-string-free-of-a-subsequence/)

给定字符串**字符串**由小写英文字母和一组相同长度的正整数**arr【】**组成。任务是从给定的字符串中删除一些字符，使得字符串中没有子序列形成字符串**“代码”**。移除字符**字符串【I】**的成本为**arr【I】**。找到实现目标的最小成本。

**示例:**

> **输入:** str = "code "，arr[] = {3，2，1，3}
> **输出:** 1
> 去掉成本最低的‘d’。
> **输入:**str = " ccoodde "，arr[] = {3，2，1，3，3，5，1，6}
> **输出:** 4
> 去掉花费 1 + 3 = 4 的两个' o '

**方法:**如果有任何带有**“代码”**的子序列是可能的，那么需要删除单个字符。移除每个角色的费用在 **arr[]** 中给出。因此，遍历字符串，对于每个字符，即 **c** 、 **o** 、 **d** 或 **e** ，计算移除它们的成本。最后移除所有角色的成本中最小的是所需的最小成本。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum cost
int findCost(string str, int arr[], int n)
{
    long long costofC = 0, costofO = 0,
              costofD = 0, costofE = 0;

    // Traverse the string
    for (int i = 0; i < n; i++) {

        // Min Cost to remove 'c'
        if (str[i] == 'c')
            costofC += arr[i];

        // Min Cost to remove subsequence "co"
        else if (str[i] == 'o')
            costofO = min(costofC, costofO + arr[i]);

        // Min Cost to remove subsequence "cod"
        else if (str[i] == 'd')
            costofD = min(costofO, costofD + arr[i]);

        // Min Cost to remove subsequence "code"
        else if (str[i] == 'e')
            costofE = min(costofD, costofE + arr[i]);
    }

    // Return the minimum cost
    return costofE;
}

// Driver program
int main()
{
    string str = "geekcodergeeks";
    int arr[] = { 1, 2, 1, 3, 4, 2, 6, 4, 6, 2, 3, 3, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findCost(str, arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG {

    // Function to return the minimum cost
    static int findCost(String str, int arr[], int n)
    {
        long costofC = 0, costofO = 0,
             costofD = 0, costofE = 0;

        // Traverse the string
        for (int i = 0; i < n; i++) {

            // Min Cost to remove 'c'
            if (str.charAt(i) == 'c')
                costofC += arr[i];

            // Min Cost to remove subsequence "co"
            else if (str.charAt(i) == 'o')
                costofO = Math.min(costofC, costofO + arr[i]);

            // Min Cost to remove subsequence "cod"
            else if (str.charAt(i) == 'd')
                costofD = Math.min(costofO, costofD + arr[i]);

            // Min Cost to remove subsequence "code"
            else if (str.charAt(i) == 'e')
                costofE = Math.min(costofD, costofE + arr[i]);
        }

        // Return the minimum cost
        return (int)costofE;
    }

    // Driver program
    public static void main(String[] args)
    {
        String str = "geekcodergeeks";
        int arr[] = { 1, 2, 1, 3, 4, 2, 6, 4, 6, 2, 3, 3, 3, 2 };
        int n = arr.length;
        System.out.print(findCost(str, arr, n));
    }
}
// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum cost
def findCost(str, arr, n):
    costofC, costofO = 0, 0
    costofD, costofE = 0, 0

    # Traverse the string
    for i in range(n):

        # Min Cost to remove 'c'
        if (str[i] == 'c'):
            costofC += arr[i]

        # Min Cost to remove subsequence "co"
        elif (str[i] == 'o'):
            costofO = min(costofC, costofO + arr[i])

        # Min Cost to remove subsequence "cod"
        elif (str[i] == 'd'):
            costofD = min(costofO, costofD + arr[i])

        # Min Cost to remove subsequence "code"
        elif (str[i] == 'e'):
            costofE = min(costofD, costofE + arr[i])

    # Return the minimum cost
    return costofE

# Driver Code
if __name__ == '__main__':
    str = "geekcodergeeks"
    arr = [1, 2, 1, 3, 4, 2, 6, 4, 6, 2, 3, 3, 3, 2]
    n = len(arr)
    print(findCost(str, arr, n))

# This code contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum cost
    public static int findCost(string str,
                            int[] arr, int n)
    {
        long costofC = 0, costofO = 0,
              costofD = 0, costofE = 0;

        // Traverse the string
        for (int i = 0; i < n; i++)
        {

            // Min Cost to remove 'c'
            if (str[i] == 'c')
            {
                costofC += arr[i];
            }

            // Min Cost to remove subsequence "co"
            else if (str[i] == 'o')
            {
                costofO = Math.Min(costofC, costofO + arr[i]);
            }

            // Min Cost to remove subsequence "cod"
            else if (str[i] == 'd')
            {
                costofD = Math.Min(costofO, costofD + arr[i]);
            }

            // Min Cost to remove subsequence "code"
            else if (str[i] == 'e')
            {
                costofE = Math.Min(costofD, costofE + arr[i]);
            }
        }

        // Return the minimum cost
        return (int)costofE;
    }

    // Driver program
    public static void Main(string[] args)
    {
        string str = "geekcodergeeks";
        int[] arr = new int[] {1, 2, 1, 3, 4, 2, 6,
                                4, 6, 2, 3, 3, 3, 2};
        int n = arr.Length;
        Console.Write(findCost(str, arr, n));
    }
}

// This code is contributed by shrikanth13
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the Math.minimum cost
function findCost(str, arr, n)
{
    var costofC = 0, costofO = 0,
              costofD = 0, costofE = 0;

    // Traverse the string
    for (var i = 0; i < n; i++) {

        // Math.min Cost to remove 'c'
        if (str[i] == 'c')
            costofC += arr[i];

        // Math.min Cost to remove subsequence "co"
        else if (str[i] == 'o')
            costofO = Math.min(costofC, costofO + arr[i]);

        // Math.min Cost to remove subsequence "cod"
        else if (str[i] == 'd')
            costofD = Math.min(costofO, costofD + arr[i]);

        // Math.min Cost to remove subsequence "code"
        else if (str[i] == 'e')
            costofE = Math.min(costofD, costofE + arr[i]);
    }

    // Return the Math.minimum cost
    return costofE;
}

// Driver program
var str = "geekcodergeeks";
var arr = [ 1, 2, 1, 3, 4, 2, 6, 4, 6, 2, 3, 3, 3, 2 ];
var n = arr.length;
document.write( findCost(str, arr, n));

</script>
```

**Output:** 

```
2
```