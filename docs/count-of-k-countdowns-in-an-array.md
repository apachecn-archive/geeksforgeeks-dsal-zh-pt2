# 一个数组中 K 个倒数的计数

> 原文:[https://www . geesforgeks . org/count-of-k-count downs-in-a-array/](https://www.geeksforgeeks.org/count-of-k-countdowns-in-an-array/)

给定一个长度为 **N** 的数组**arr【】**和一个数字 **K** ，任务是计算数组中 K-count down 的数量。

> 如果一个连续的子阵列的长度为 K，并且按此顺序包含整数 K，K-1，K-2，…，2，1，则称其为 K 倒数。例如，[4，3，2，1]是 4 倒数，[6，5，4，3，2，1]是 6 倒数。

**例:**

> **输入:** K = 2，arr[] = {3 2 1 2 2 1}
> **输出:** 2
> **解释:**这里，K = 2 所以数组有 2 个 2-Countdowns(2，1)。一个倒计时是从索引 1 到 2，另一个是从索引 4 到 5。
> **输入:** K = 3，arr[]= { 4 3 1 5 3 2 1 }
> **输出:** 2
> **说明:**这里 K = 3 所以数组有 2 个 3-Countdowns(3，2，1)

**方法:**遍历给定的数组，每次遇到数字 K 时，检查数组中是否顺序出现所有数字 K、K-1、K-2、…直到 1。如果是，计数增加 1。如果下一个数字使它失去顺序，那么寻找下一个出现的 K。
以下是上述办法的实施情况:

## C++

```
// C++ code for the above program.

#include <bits/stdc++.h>
using namespace std;

// Function to to count the
// number of K-countdowns for
// multiple queries
int countKCountdown(int arr[],
                    int N,
                    int K)
{

    // flag which stores the
    // current value of value
    // in the countdown
    int flag = -1;

    // count of K-countdowns
    int count = 0;

    // Loop to iterate over the
    // elements of the array
    for (int i = 0; i < N; i++) {

        // condition check if
        // the elements
        // of the array is
        // equal to K
        if (arr[i] == K)
            flag = K;

        // condition check if
        // the elements
        // of the array is in
        // continuous order
        if (arr[i] == flag)
            flag--;

        // condition check if
        // the elements
        // of the array are not
        // in continuous order
        else
            flag = -1;

        // condition check to
        // increment the counter
        // if the there is a
        // K-countdown present
        // in the array
        if (flag == 0)
            count++;
    }

    // returning the count of
    // K-countdowns
    return count;
}

// Driver Code
int main()
{
    int N = 8;
    int K = 3;
    int arr[N] = { 4, 3, 2, 1,
                   5, 3, 2, 1 };

    // Function Call
    cout << countKCountdown(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above program.
class GFG{

// Function to to count the
// number of K-countdowns for
// multiple queries
public static int countKCountdown(int arr[],
                                  int N, int K)
{

    // Flag which stores the
    // current value of value
    // in the countdown
    int flag = -1;

    // Count of K-countdowns
    int count = 0;

    // Loop to iterate over the
    // elements of the array
    for(int i = 0; i < N; i++)
    {

       // Condition check if the
       // elements of the array is
       // equal to K
       if (arr[i] == K)
           flag = K;

       // Condition check if the
       // elements of the array is
       // in continuous order
       if (arr[i] == flag)
           flag--;

       // Condition check if the
       // elements of the array are
       // not in continuous order
       else
           flag = -1;

       // Condition check to increment
       // the counter if the there is a
       // K-countdown present in the array
       if (flag == 0)
           count++;
    }

    // Returning the count of
    // K-countdowns
    return count;
}

// Driver code
public static void main(String[] args)
{
    int N = 8;
    int K = 3;
    int arr[] = { 4, 3, 2, 1, 5, 3, 2, 1 };

    System.out.print(countKCountdown(arr, N, K));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 code for the above program.

# Function to to count the
# number of K-countdowns for
# multiple queries
def countKCountdown(arr, N, K):

    # flag which stores the
    # current value of value
    # in the countdown
    flag = -1;

    # count of K-countdowns
    count = 0;

    # Loop to iterate over the
    # elements of the array
    for i in range(0, N):

        # condition check if
        # the elements
        # of the array is
        # equal to K
        if (arr[i] == K):
            flag = K;

        # condition check if
        # the elements
        # of the array is in
        # continuous order
        if (arr[i] == flag):
            flag -= 1;

        # condition check if
        # the elements
        # of the array are not
        # in continuous order
        else:
            flag = -1;

        # condition check to
        # increment the counter
        # if the there is a
        # K-countdown present
        # in the array
        if (flag == 0):
            count += 1;

    # returning the count of
    # K-countdowns
    return count;

# Driver Code
N = 8;
K = 3;
arr = [ 4, 3, 2, 1,
        5, 3, 2, 1 ];

# Function Call
print(countKCountdown(arr, N, K))

# This code is contributed by Akanksha_Rai
```

## C#

```
// C# code for the above program.
using System;
class GFG{

// Function to to count the
// number of K-countdowns for
// multiple queries
public static int countKCountdown(int []arr,
                                  int N, int K)
{

    // Flag which stores the
    // current value of value
    // in the countdown
    int flag = -1;

    // Count of K-countdowns
    int count = 0;

    // Loop to iterate over the
    // elements of the array
    for(int i = 0; i < N; i++)
    {

    // Condition check if the
    // elements of the array is
    // equal to K
    if (arr[i] == K)
        flag = K;

    // Condition check if the
    // elements of the array is
    // in continuous order
    if (arr[i] == flag)
        flag--;

    // Condition check if the
    // elements of the array are
    // not in continuous order
    else
        flag = -1;

    // Condition check to increment
    // the counter if the there is a
    // K-countdown present in the array
    if (flag == 0)
        count++;
    }

    // Returning the count of
    // K-countdowns
    return count;
}

// Driver code
public static void Main()
{
    int N = 8;
    int K = 3;
    int []arr = { 4, 3, 2, 1, 5, 3, 2, 1 };

    Console.Write(countKCountdown(arr, N, K));
}
}

// This code is contributed by Akanksha_Rai
```

## java 描述语言

```
<script>
//Javascript code for the above program.

// Function to to count the
// number of K-countdowns for
// multiple queries
function countKCountdown( arr, N, K)
{

    // flag which stores the
    // current value of value
    // in the countdown
    var flag = -1;

    // count of K-countdowns
    var count = 0;

    // Loop to iterate over the
    // elements of the array
    for (var i = 0; i < N; i++) {

        // condition check if
        // the elements
        // of the array is
        // equal to K
        if (arr[i] == K)
            flag = K;

        // condition check if
        // the elements
        // of the array is in
        // continuous order
        if (arr[i] == flag)
            flag--;

        // condition check if
        // the elements
        // of the array are not
        // in continuous order
        else
            flag = -1;

        // condition check to
        // increment the counter
        // if the there is a
        // K-countdown present
        // in the array
        if (flag == 0)
            count++;
    }

    // returning the count of
    // K-countdowns
    return count;
}

var N = 8;
var K = 3;
var arr = [ 4, 3, 2, 1, 5, 3, 2, 1 ];
// Function Call
document.write( countKCountdown(arr, N, K));

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***辅助空间复杂度:** O(1)*