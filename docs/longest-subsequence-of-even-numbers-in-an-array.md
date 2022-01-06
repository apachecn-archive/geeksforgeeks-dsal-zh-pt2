# 数组中偶数的最长子序列

> 原文:[https://www . geesforgeks . org/数组中偶数的最长子序列/](https://www.geeksforgeeks.org/longest-subsequence-of-even-numbers-in-an-array/)

给定一个包含 **N** 整数的数组 **arr[]** ，任务是打印数组中偶数的最长子序列的长度。

**示例:**

> **输入:** arr[] = {3，4，11，2，9，21}
> **输出:** 2
> **解释:**
> 包含偶数的最长子序列是{4，2}。
> 因此，答案是 2。
> 
> **输入:** arr[] = {6，4，10，13，9，25}
> **输出:** 3
> 包含偶数的最长子序列是{6，4，10}。
> 因此，答案是 3。

**方法:**需要从数组中进行的一个观察是，仅包含一个偶数的最长子序列将是所有偶数的总数。因此，按照以下步骤计算答案:

*   [逐个元素遍历给定的数组](https://www.geeksforgeeks.org/iterating-arrays-java/)。
*   [如果元素是偶数](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)，则增加结果子序列的长度。
*   当遍历完成时，只包含偶数的最长子序列所需的长度存储在计数器中。

下面是上述方法的实现:

## C++

```
// C++ program to find the length of the
// longest subsequence which contains
// all even numbers

#include <bits/stdc++.h>
using namespace std;
#define N 100000

// Function to find the length of the
// longest subsequence
// which contain all even numbers
int longestEvenSubsequence(int arr[], int n)
{
    // Counter to store the
    // length of the subsequence
    int answer = 0;

    // Iterating through the array
    for (int i = 0; i < n; i++) {

        // Checking if the element is
        // even or not
        if (arr[i] % 2 == 0) {

            // If it is even, then
            // increment the counter
            answer++;
        }
    }

    return answer;
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 11, 2, 9, 21 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << longestEvenSubsequence(arr, n)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of the
// longest subsequence which contains
// all even numbers
import java.util.*;
class GFG{

// Function to find the length of the
// longest subsequence
// which contain all even numbers
static int longestEvenSubsequence(int arr[], int n)
{
    // Counter to store the
    // length of the subsequence
    int answer = 0;

    // Iterating through the array
    for (int i = 0; i < n; i++)
    {

        // Checking if the element is
        // even or not
        if (arr[i] % 2 == 0)
        {

            // If it is even, then
            // increment the counter
            answer++;
        }
    }
    return answer;
}

// Driver code
public static void main(String args[])
{
    int []arr = { 3, 4, 11, 2, 9, 21 };
    int n = arr.length;

    System.out.print(longestEvenSubsequence(arr, n));
}
}

// This code is contributed by Akanksha_Rai
```

## 蟒蛇 3

```
# Python3 program to find the length
# of the longest subsequence which
# contains all even numbers

N = 100000

# Function to find the length
# of the longest subsequence
# which contain all even numbers
def longestEvenSubsequence(arr, n):

    # Counter to store the
    # length of the subsequence
    answer = 0

    # Iterating through the array
    for i in range(n):

        # Checking if the element
        # is even or not
        if (arr[i] % 2 == 0):

            # If it is even, then
            # increment the counter
            answer += 1

    return answer

# Driver code
if __name__ == "__main__":

    arr = [ 3, 4, 11, 2, 9, 21 ]
    n = len(arr)

    print(longestEvenSubsequence(arr, n))

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the length of the
// longest subsequence which contains
// all even numbers
using System;
class GFG{

// Function to find the length of the
// longest subsequence
// which contain all even numbers
static int longestEvenSubsequence(int []arr, int n)
{
    // Counter to store the
    // length of the subsequence
    int answer = 0;

    // Iterating through the array
    for (int i = 0; i < n; i++)
    {

        // Checking if the element is
        // even or not
        if (arr[i] % 2 == 0)
        {

            // If it is even, then
            // increment the counter
            answer++;
        }
    }
    return answer;
}

// Driver code
public static void Main()
{
    int []arr = { 3, 4, 11, 2, 9, 21 };
    int n = arr.Length;

    Console.WriteLine(longestEvenSubsequence(arr, n));
}
}

// This code is contributed by Nidhi_Biet
```

## java 描述语言

```
<script>
// Javascript program to find the length of the
// longest subsequence which contains
// all even numbers

let N = 100000;

// Function to find the length of the
// longest subsequence
// which contain all even numbers
function longestEvenSubsequence(arr, n) {
    // Counter to store the
    // length of the subsequence
    let answer = 0;

    // Iterating through the array
    for (let i = 0; i < n; i++) {

        // Checking if the element is
        // even or not
        if (arr[i] % 2 == 0) {

            // If it is even, then
            // increment the counter
            answer++;
        }
    }

    return answer;
}

// Driver code
let arr = [3, 4, 11, 2, 9, 21];
let n = arr.length;

document.write(longestEvenSubsequence(arr, n) + "<br>");

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
2
```

**时间复杂度:** *O(N)* ，其中 N 为数组长度。
**辅助空间:** O(1)