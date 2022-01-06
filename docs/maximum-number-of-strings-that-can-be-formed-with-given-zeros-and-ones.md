# 给定 0 和 1 可以形成的最大字符串数

> 原文:[https://www . geesforgeks . org/可由给定 0 和 1 组成的最大字符串数/](https://www.geeksforgeeks.org/maximum-number-of-strings-that-can-be-formed-with-given-zeros-and-ones/)

给定一个只有 0 和 1 的字符串**arr【】**和两个整数 **N** 和 **M** 的 **N** 是 **1 的**的数量， **M** 是 **0 的**的数量。任务是从给定的字符串列表中找到最大数量的[字符串](https://www.geeksforgeeks.org/string-data-structure/)，这些字符串可以用给定数量的 0 和 1 来构造。

**示例:**

> **输入:**arr[]= {“10”，“0001”，“11100”，“1”，“0”}，M = 5，N = 3
> **输出:** 4
> **说明:**
> 可以用 5 个 0 和 3 个 1 组成的 4 个字符串是:“10”，“0001”，“1”，“0”
> 
> **输入:**arr[]= {“10”、“00”、“000”、“0001”、“111001”、“1”、“0”}，M = 3，N = 1
> **输出:** 3
> **解释:**
> 可以用三个 0 和一个 1 组成的三个字符串是:“00”、“1”、“0”

**天真方法:**想法是生成给定字符串列表的所有组合，并检查满足给定条件的 0 和 1 的计数。但是这个解决方案的时间复杂度是指数级的。

**时间复杂度:**O(**2<sup>N</sup>T5)，其中 **N** 为列表中的字符串个数。**

**有效方法:**
通过使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)给出了一个有效的解决方案。其思想是使用[递归](https://www.geeksforgeeks.org/recursion/)生成所有可能的组合，并在[递归](https://www.geeksforgeeks.org/recursion/)过程中存储[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)的结果。

以下是步骤:

*   思路是使用 3D dp 数组( **dp[M][N][i]** )，其中 **N** 和 **M** 分别是 **1 的**和 **0 的**的个数， **i** 是列表中字符串的索引。
*   找出当前字符串中 **1 的**和 **0 的**的数量，检查 0 和 1 的计数是否分别小于或等于给定的计数 **N 和 M** 。
*   如果上述条件成立，则检查当前状态值是否存储在 dp 表中。如果是，则返回该值。
*   否则通过包含和排除当前字符串递归移动到下一个迭代，如下所示:

```
// By including the current string
x = 1 + recursive_function(M - zero, N - ones, arr, i + 1)

// By excluding the current string 
y = recursive_function(M, N, arr, i + 1)

// and update the dp table as:
dp[M][N][i] = max(x, y)
```

*   以上两个递归调用的最大值将给出当前状态的最大数字 **N 1 和 M 0**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// 3D dp table to store the state value
int dp[100][100][100];

// Function that count the combination
// of 0's and 1's from the given list
// of string
int countString(int m, int n,
                vector<string>& arr, int i)
{
    // Base Case if count of 0's or 1's
    // becomes negative
    if (m < 0 || n < 0) {
        return INT_MIN;
    }

    // If index reaches out of bound
    if (i >= arr.size()) {
        return 0;
    }

    // Return the prestored result
    if (dp[m][n][i] != -1) {
        return dp[m][n][i];
    }

    // Initialize count of 0's and 1's
    // to 0 for the current state
    int zero = 0, one = 0;

    // Calculate the number of 1's and
    // 0's in current string
    for (char c : arr[i]) {
        if (c == '0') {
            zero++;
        }
        else {
            one++;
        }
    }

    // Include the current string and
    // recurr for the next iteration
    int x = 1 + countString(m - zero,
                            n - one,
                            arr, i + 1);

    // Exclude the current string and
    // recurr for the next iteration
    int y = countString(m, n, arr, i + 1);

    // Update the maximum of the above
    // two states to the current dp state
    return dp[m][n][i] = max(x, y);
}

// Driver Code
int main()
{
    vector<string> arr = { "10", "0001", "1",
                           "111001", "0" };

    // N 0's and M 1's
    int N = 3, M = 5;

    // Initialize dp array to -1
    memset(dp, -1, sizeof(dp));

    // Function call
    cout << countString(M, N, arr, 0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// 3D dp table to store the state value
static int [][][]dp = new int[100][100][100];

// Function that count the combination
// of 0's and 1's from the given list
// of String
static int countString(int m, int n,
                String []arr, int i)
{
    // Base Case if count of 0's or 1's
    // becomes negative
    if (m < 0 || n < 0) {
        return Integer.MIN_VALUE;
    }

    // If index reaches out of bound
    if (i >= arr.length) {
        return 0;
    }

    // Return the prestored result
    if (dp[m][n][i] != -1) {
        return dp[m][n][i];
    }

    // Initialize count of 0's and 1's
    // to 0 for the current state
    int zero = 0, one = 0;

    // Calculate the number of 1's and
    // 0's in current String
    for (char c : arr[i].toCharArray()) {
        if (c == '0') {
            zero++;
        }
        else {
            one++;
        }
    }

    // Include the current String and
    // recurr for the next iteration
    int x = 1 + countString(m - zero,
                            n - one,
                            arr, i + 1);

    // Exclude the current String and
    // recurr for the next iteration
    int y = countString(m, n, arr, i + 1);

    // Update the maximum of the above
    // two states to the current dp state
    return dp[m][n][i] = Math.max(x, y);
}

// Driver Code
public static void main(String[] args)
{
    String []arr = { "10", "0001", "1",
                           "111001", "0" };

    // N 0's and M 1's
    int N = 3, M = 5;

    // Initialize dp array to -1
    for(int i = 0;i<100;i++){
        for(int j = 0;j<100;j++){
            for(int l=0;l<100;l++)
            dp[i][j][l]=-1;
        }
    }

    // Function call
    System.out.print(countString(M, N, arr, 0));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys

# 3D dp table to store the state value
dp = [[[-1 for i in range(100)]for j in range(100)] for k in range(100)]

# Function that count the combination
# of 0's and 1's from the given list
# of string
def countString(m, n, arr, i):

    # Base Case if count of 0's or 1's
    # becomes negative
    if (m < 0 or n < 0):
        return -sys.maxsize - 1

    # If index reaches out of bound
    if (i >= len(arr)):
        return 0

    # Return the prestored result
    if (dp[m][n][i] != -1):
        return dp[m][n][i]

    # Initialize count of 0's and 1's
    # to 0 for the current state
    zero = 0
    one = 0

    # Calculate the number of 1's and
    # 0's in current string
    for c in arr[i]:
        if (c == '0'):
            zero += 1
        else:
            one += 1

    # Include the current string and
    # recurr for the next iteration
    x = 1 + countString(m - zero, n - one, arr, i + 1)

    # Exclude the current string and
    # recurr for the next iteration
    y = countString(m, n, arr, i + 1)

    dp[m][n][i] = max(x, y)

    # Update the maximum of the above
    # two states to the current dp state
    return dp[m][n][i]

# Driver Code
if __name__ == '__main__':
    arr = ["10", "0001", "1","111001", "0"]

    # N 0's and M 1's
    N = 3
    M = 5

    # Function call
    print(countString(M, N, arr, 0))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// 3D dp table to store the state value
static int [,,]dp = new int[100, 100, 100];

// Function that count the combination
// of 0's and 1's from the given list
// of String
static int countString(int m, int n,
                String []arr, int i)
{
    // Base Case if count of 0's or 1's
    // becomes negative
    if (m < 0 || n < 0) {
        return int.MinValue;
    }

    // If index reaches out of bound
    if (i >= arr.Length) {
        return 0;
    }

    // Return the prestored result
    if (dp[m, n, i] != -1) {
        return dp[m, n, i];
    }

    // Initialize count of 0's and 1's
    // to 0 for the current state
    int zero = 0, one = 0;

    // Calculate the number of 1's and
    // 0's in current String
    foreach (char c in arr[i].ToCharArray()) {
        if (c == '0') {
            zero++;
        }
        else {
            one++;
        }
    }

    // Include the current String and
    // recurr for the next iteration
    int x = 1 + countString(m - zero,
                            n - one,
                            arr, i + 1);

    // Exclude the current String and
    // recurr for the next iteration
    int y = countString(m, n, arr, i + 1);

    // Update the maximum of the above
    // two states to the current dp state
    return dp[m, n, i] = Math.Max(x, y);
}

// Driver Code
public static void Main(String[] args)
{
    String []arr = { "10", "0001", "1",
                           "111001", "0" };

    // N 0's and M 1's
    int N = 3, M = 5;

    // Initialize dp array to -1
    for(int i = 0; i < 100; i++){
        for(int j = 0; j < 100; j++){
            for(int l = 0; l < 100; l++)
            dp[i, j, l] = -1;
        }
    }

    // Function call
    Console.Write(countString(M, N, arr, 0));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// 3D dp table to store the state value
let dp = new Array();

// Initialize dp array to -1
for(let i = 0; i < 100; i++)
{
    dp[i] = new Array();
     for(let j = 0; j < 100; j++)
     {
          dp[i][j] = new Array();
        for(let l = 0; l < 100; l++)
        {
            dp[i][j][l] = -1;
        }
     }
} 

// Function that count the combination
// of 0's and 1's from the given list
// of String
function countString(m, n, arr, i)
{

    // Base Case if count of 0's or 1's
    // becomes negative
    if (m < 0 || n < 0)
    {
        return Number.MIN_VALUE;
    }

    // If index reaches out of bound
    if (i >= arr.length)
    {
        return 0;
    }

    // Return the prestored result
    if (dp[m][n][i] != -1)
    {
        return dp[m][n][i];
    }

    // Initialize count of 0's and 1's
    // to 0 for the current state
    let zero = 0, one = 0;

    // Calculate the number of 1's and
    // 0's in current String
    for(let c = 0; c < arr[i].length; c++)
    {
        if (arr[i] == '0')
        {
            zero++;
        }
        else
        {
            one++;
        }
    }

    // Include the current String and
    // recurr for the next iteration
    let x = 1 + countString(m - zero,
                            n - one,
                       arr, i + 1);

    // Exclude the current String and
    // recurr for the next iteration
    let y = countString(m, n, arr, i + 1);

    // Update the maximum of the above
    // two states to the current dp state
    return dp[m][n][i] = Math.max(x, y);
}

// Driver Code
let arr = [ "10", "0001", "1", "111001", "0" ];

// N 0's and M 1's
let N = 3, M = 5;

// Function call
document.write(countString(M, N, arr, 0));

// This code is contributed by Dharanendra L V.

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N*M*len)，其中 **N** 和 **M** 分别是 **1 的**和 **0 的**的数字， **len** 是列表的长度。
**辅助空间:** O(N*M*len)