# 给定数组中表示 S 所需的最小数量

> 原文:[https://www . geesforgeks . org/最小数量-从给定数组到表示-s 的所需数量/](https://www.geeksforgeeks.org/minimum-count-of-numbers-required-from-given-array-to-represent-s/)

给定一个整数 **S** 和一个数组**arr【】**，任务是找到和为 S 的元素的最小个数，这样数组中的任何元素都可以被选择任意次来得到和 S

**示例:**

> **输入:** arr[] = {25，10，5}，S = 30
> **输出:** 2
> **解释:**
> 在给定的数组中有很多可能的解，比如–
> 5+5+5+5+5+5+5 = 30，或者
> 10 + 10 + 10 = 30，或者
> 25 + 5 = 30
> 因此，最小可能的解是 2
> 
> **输入:** arr[] = {2，1，4，3，5，6}，Sum= 6
> **输出:** 1
> **解释:**
> 在给定的数组中有许多可能的解，例如–
> 2+2+2 = 6，或者
> 2 + 4 = 6，或者
> 6 = 6，
> 因此，最小可能的解是 1

**方法:**
思想是递归地寻找每个可能的序列，使得它们的和等于给定的 S，并且还跟踪最小序列，使得它们的和是给定的 S。这样，最小可能解可以容易地计算出来。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum number of sequence
// required from array such that
// their sum is equal to given S

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// minimum elements required to
// get the sum of given value S
int printAllSubsetsRec(int arr[],
                    int n,
                    vector<int> v,
                    int sum)
{
    // Condition if the
    // sequence is found
    if (sum == 0) {
        return (int)v.size();
    }

    if (sum < 0)
        return INT_MAX;

    // Condition when no
    // such sequence found
    if (n == 0)
        return INT_MAX;

    // Calling for without choosing
    // the current index value
    int x = printAllSubsetsRec(
        arr,
        n - 1, v, sum);

    // Calling for after choosing
    // the current index value
    v.push_back(arr[n - 1]);
    int y = printAllSubsetsRec(
        arr, n, v,
        sum - arr[n - 1]);
    return min(x, y);
}

// Function for every array
int printAllSubsets(int arr[],
                    int n, int sum)
{
    vector<int> v;
    return printAllSubsetsRec(arr, n,
                            v, sum);
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 4, 3, 5, 6 };
    int sum = 6;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << printAllSubsets(arr, n, sum)
        << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum number of sequence
// required from array such that
// their sum is equal to given S
import java.util.*;
import java.lang.*;

class GFG{

// Function to find the
// minimum elements required to
// get the sum of given value S
static int printAllSubsetsRec(int arr[],
                              int n,
                              ArrayList<Integer> v,
                              int sum)
{

    // Condition if the
    // sequence is found
    if (sum == 0)
    {
        return (int)v.size();
    }

    if (sum < 0)
        return Integer.MAX_VALUE;

    // Condition when no
    // such sequence found
    if (n == 0)
        return Integer.MAX_VALUE;

    // Calling for without choosing
    // the current index value
    int x = printAllSubsetsRec(
            arr,
            n - 1, v, sum);

    // Calling for after choosing
    // the current index value
    v.add(arr[n - 1]);

    int y = printAllSubsetsRec(
            arr, n, v,
            sum - arr[n - 1]);
    v.remove(v.size() - 1);

    return Math.min(x, y);
}

// Function for every array
static int printAllSubsets(int arr[],
                           int n, int sum)
{
    ArrayList<Integer> v = new ArrayList<>();
    return printAllSubsetsRec(arr, n,
                              v, sum);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 1, 4, 3, 5, 6 };
    int sum = 6;
    int n = arr.length;

    System.out.println(printAllSubsets(arr, n, sum));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum number of sequence
# required from array such that
# their sum is equal to given S
import sys

# Function to find the
# minimum elements required to
# get the sum of given value S
def printAllSubsetsRec(arr, n, v, Sum):

    # Condition if the
    # sequence is found
    if (Sum == 0):
        return len(v)

    if (Sum < 0):
        return sys.maxsize

    # Condition when no
    # such sequence found
    if (n == 0):
        return sys.maxsize

    # Calling for without choosing
    # the current index value
    x = printAllSubsetsRec(arr, n - 1, v, Sum)

    # Calling for after choosing
    # the current index value
    v.append(arr[n - 1])
    y = printAllSubsetsRec(arr, n, v,
                           Sum - arr[n - 1])
    v.pop(len(v) - 1)

    return min(x, y)

# Function for every array
def printAllSubsets(arr, n, Sum):

    v = []
    return printAllSubsetsRec(arr, n, v, Sum)

# Driver code
arr = [ 2, 1, 4, 3, 5, 6 ]
Sum = 6
n = len(arr)

print(printAllSubsets(arr, n, Sum))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation to find the
// minimum number of sequence
// required from array such that
// their sum is equal to given S
using System;
using System.Collections.Generic;

class GFG{

// Function to find the
// minimum elements required to
// get the sum of given value S
static int printAllSubsetsRec(int[] arr, int n,
                            List<int> v, int sum)
{

    // Condition if the
    // sequence is found
    if (sum == 0)
    {
        return v.Count;
    }

    if (sum < 0)
        return Int32.MaxValue;

    // Condition when no
    // such sequence found
    if (n == 0)
        return Int32.MaxValue;

    // Calling for without choosing
    // the current index value
    int x = printAllSubsetsRec(arr, n - 1,
                               v, sum);

    // Calling for after choosing
    // the current index value
    v.Add(arr[n - 1]);

    int y = printAllSubsetsRec(arr, n, v,
                               sum - arr[n - 1]);
    v.RemoveAt(v.Count - 1);

    return Math.Min(x, y);
}

// Function for every array
static int printAllSubsets(int[] arr, int n,
                           int sum)
{
    List<int> v = new List<int>();
    return printAllSubsetsRec(arr, n, v, sum);
}

// Driver code 
static void Main()
{
    int[] arr = { 2, 1, 4, 3, 5, 6 };
    int sum = 6;
    int n = arr.Length;

    Console.WriteLine(printAllSubsets(arr, n, sum));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// minimum number of sequence
// required from array such that
// their sum is equal to given S

// Function to find the
// minimum elements required to
// get the sum of given value S
function prletAllSubsetsRec(arr, n, v,
                              sum)
{

    // Condition if the
    // sequence is found
    if (sum == 0)
    {
        return v.length;
    }

    if (sum < 0)
        return Number.MAX_VALUE;

    // Condition when no
    // such sequence found
    if (n == 0)
        return Number.MAX_VALUE;

    // Calling for without choosing
    // the current index value
    let x = prletAllSubsetsRec(
            arr,
            n - 1, v, sum);

    // Calling for after choosing
    // the current index value
    v.push(arr[n - 1]);

    let y = prletAllSubsetsRec(
            arr, n, v,
            sum - arr[n - 1]);
    v.pop(v.length - 1);

    return Math.min(x, y);
}

// Function for every array
function prletAllSubsets(arr,
                           n, sum)
{
    let v = [];
    return prletAllSubsetsRec(arr, n,
                              v, sum);
}
  // Driver Code

    let arr = [ 2, 1, 4, 3, 5, 6 ];
    let sum = 6;
    let n = arr.length;

    document.write(prletAllSubsets(arr, n, sum));

</script>
```

**Output:** 

```
1
```

**性能分析:**

*   **时间复杂度:**和上面的方法一样，每一步中每一个花费 O(2 <sup>N</sup> 时间的数字都有两个选择，因此时间复杂度为 **O(2 <sup>N</sup> )** 。
*   **空间复杂度:**和上面的方法一样，没有使用额外的空间，因此空间复杂度为 **O(1)** 。

**高效方法:**和上面的方法一样，存在重叠子问题，所以思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)范式来解决这个问题。创建一个 [DP 表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)的 **N * S** 来存储前一个序列的预先计算的答案，这是获得 S–arr[I]和所需的最小长度序列，这样，在计算完数组的每个值后，问题的答案将是 dp[N][S]，其中 m 是数组的长度，S 是给定的和。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum number of sequence
// required from array such that
// their sum is equal to given S

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// minimum length of the sequence
int Count(int S[], int m, int n)
{
    vector<vector<int> > table(
        m + 1,
        vector<int>(
            n + 1, 0));

    // Loop to initialize the array
    // as infinite in the row 0
    for (int i = 1; i <= n; i++) {
        table[0][i] = INT_MAX - 1;
    }

    // Loop to find the solution
    // by pre-computation for the
    // sequence
    for (int i = 1; i <= m; i++) {

        for (int j = 1; j <= n; j++) {
            if (S[i - 1] > j) {
                table[i][j]
                    = table[i - 1][j];
            }
            else {

                // Minimum possible
                // for the previous
                // minimum value
                // of the sequence
                table[i][j]
                    = min(
                        table[i - 1][j],
                        table[i][j - S[i - 1]] + 1);
            }
        }
    }
    return table[m][n];
}

// Driver Code
int main()
{
    int arr[] = { 9, 6, 5, 1 };
    int m = sizeof(arr) / sizeof(arr[0]);
    cout << Count(arr, m, 11);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum number of sequence
// required from array such that
// their sum is equal to given S
import java.util.*;

class GFG{

// Function to find the count of
// minimum length of the sequence
static int Count(int S[], int m, int n)
{
    int [][]table = new int[m + 1][n + 1];

    // Loop to initialize the array
    // as infinite in the row 0
    for(int i = 1; i <= n; i++)
    {
    table[0][i] = Integer.MAX_VALUE - 1;
    }

    // Loop to find the solution
    // by pre-computation for the
    // sequence
    for(int i = 1; i <= m; i++)
    {
    for(int j = 1; j <= n; j++)
    {
        if (S[i - 1] > j)
        {
            table[i][j] = table[i - 1][j];
        }
        else
        {

            // Minimum possible for the
            // previous minimum value
            // of the sequence
            table[i][j] = Math.min(table[i - 1][j],
                            table[i][j - S[i - 1]] + 1);
        }
    }
    }
    return table[m][n];
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 9, 6, 5, 1 };
    int m = arr.length;

    System.out.print(Count(arr, m, 11));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum number of sequence
# required from array such that
# their sum is equal to given S

# Function to find the count of
# minimum length of the sequence
def Count(S, m, n):
    table = [[0 for i in range(n + 1)]
                for i in range(m + 1)]

    # Loop to initialize the array
    # as infinite in the row 0
    for i in range(1, n + 1):
        table[0][i] = 10**9 - 1

    # Loop to find the solution
    # by pre-computation for the
    # sequence
    for i in range(1, m + 1):

        for j in range(1, n + 1):
            if (S[i - 1] > j):
                table[i][j] = table[i - 1][j]
            else:

                # Minimum possible
                # for the previous
                # minimum value
                # of the sequence
                table[i][j] = min(table[i - 1][j],
                                table[i][j - S[i - 1]] + 1)

    return table[m][n]

# Driver Code
if __name__ == '__main__':
    arr= [9, 6, 5, 1]
    m = len(arr)
    print(Count(arr, m, 11))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation to find the
// minimum number of sequence
// required from array such that
// their sum is equal to given S
using System;

class GFG{

// Function to find the count of
// minimum length of the sequence
static int Count(int[] S, int m, int n)
{
    int[,] table = new int[m + 1, n + 1];

    // Loop to initialize the array
    // as infinite in the row 0
    for(int i = 1; i <= n; i++)
    {
    table[0, i] = int.MaxValue - 1;
    }

    // Loop to find the solution
    // by pre-computation for the
    // sequence
    for(int i = 1; i <= m; i++)
    {
    for(int j = 1; j <= n; j++)
    {
        if (S[i - 1] > j)
        {
            table[i, j] = table[i - 1, j];
        }
        else
        {

            // Minimum possible for the
            // previous minimum value
            // of the sequence
            table[i, j] = Math.Min(table[i - 1, j],
                            table[i, j - S[i - 1]] + 1);
        }
    }
    }
    return table[m, n];
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 9, 6, 5, 1 };
    int m = 4;

    Console.WriteLine(Count(arr, m, 11));
}
}

// This code is contributed by jrishabh99
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// minimum number of sequence
// required from array such that
// their sum is equal to given S

// Function to find the count of
// minimum length of the sequence
function Count(S, m, n)
{
    let table = [];
    for(let i = 0;i<m+1;i++){
       table[i] = [];
       for(let j = 0;j<n+1;j++){
              table[i][j] = 0;
       }
    }

    // Loop to initialize the array
    // as infinite in the row 0
    for (let i = 1; i <= n; i++) {
        table[0][i] = Number.MAX_VALUE - 1;
    }

    // Loop to find the solution
    // by pre-computation for the
    // sequence
    for (let i = 1; i <= m; i++) {

        for (let j = 1; j <= n; j++) {
            if (S[i - 1] > j) {
                table[i][j]
                    = table[i - 1][j];
            }
            else {

                // Minimum possible
                // for the previous
                // minimum value
                // of the sequence
                table[i][j]
                    = Math.min(
                        table[i - 1][j],
                        table[i][j - S[i - 1]] + 1);
            }
        }
    }
    return table[m][n];
}

// Driver Code
let arr = [ 9, 6, 5, 1 ];
let m = arr.length;
document.write(Count(arr, m, 11));

</script>
```

**Output:** 

```
2
```

**性能分析:**

*   **时间复杂度:**与上述方法一样，计算所需最小长度序列有两个循环，需要 O(N <sup>2</sup> )个时间，因此时间复杂度为 **O(N <sup>2</sup> )** 。
*   **空间复杂度:**和上面的方法一样，使用了一个额外的 dp 表，因此空间复杂度为 **O(N <sup>2</sup> )** 。