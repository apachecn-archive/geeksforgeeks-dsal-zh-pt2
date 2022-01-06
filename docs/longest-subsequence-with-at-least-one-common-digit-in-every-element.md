# 每个元素中至少有一个公共数字的最长子序列

> 原文:[https://www . geesforgeks . org/每元素中至少有一个公共数字的最长子序列/](https://www.geeksforgeeks.org/longest-subsequence-with-at-least-one-common-digit-in-every-element/)

给定一个数组。任务是找到最长子序列的长度，其中所有元素必须至少有一个共同的数字。

**示例:**

> **输入** : arr[] = { 11，12，23，74，13 }
> **输出** : 3
> **解释**:元素 11，12，13 有数字‘1’为公共。所以它是所需的最长的子序列。
> **输入** : arr[] = { 12，90，67，78，45 }
> **输出** : 2

**正常方法:**找到数组的所有子序列，找到每个元素必须有一个公共数字的子序列。然后，我们必须找到最长的子序列，并打印该子序列的长度。这种方法需要指数时间复杂度。

**高效方法:**想法是取一个大小为 10 的散列数组来存储数组元素中出现的 0-9 位数。遍历数组，对于数组的每个元素，找到该元素中的唯一数字，并增加它们在哈希数组中的计数。现在，散列数组中计数最大的数字表示它是数组元素中出现最多的公共数字。因此，所需的最长子序列的长度将是哈希数组中最大值的计数。

让我们举个例子，

> 让数组为 arr[] = {11，12，13，24}
> 最初计数数组为{ 0，0，0，0，0，0，0，0，0，0 }
> 第一个元素为 11，因此数字为 1 和 1(但 1 将被计数一次)}
> 计数数组为{ 0，1，0，0，0，0，0，0 }
> 第二个元素为 12，因此数字为 1，2
> 计数数组为{ 0，2，1，0 0，0，0，0 }
> 第三个元素是 13 所以数字是 1，3
> 计数数组是{ 0，3，1，1，0，0，0，0，0 }
> 第四个元素是 24 所以数字是 2，4
> 计数数组是{ 0，3，2，1，1，0，0，0，0 }
> 所以计数数组中的最大值是 3
> 所以，3 就是答案

以下是上述方法的实现:

## C++

```
// C++ program to find the length of subsequence which has
// atleast one digit common among all its elements
#include <bits/stdc++.h>
using namespace std;

// If the number contains a digit increase
// the count by 1 (even if it has multiple
// same digit the count should be increased
// by only once)
void count_(int count[], int e)
{
    // Hash to make it sure that a digit
    // is counted only once
    bool hash[10];

    // Set the hash to its initial value
    memset(hash, false, sizeof(hash));

    // Extract the digits
    while (e > 0) {

        // If the digit did not appear before
        if (hash[e % 10] == false)

            // Increase the count
            count[e % 10]++;

        // Mark the digit as visited
        hash[e % 10] = true;

        // Delete the digit
        e /= 10;
    }
}

// Function to find the length of subsequence which has
// atleast one digit common among all its elements
void find_subsequence(int arr[], int n)
{
    // Count of digits
    int count[10];

    // Set the initial value to zero
    memset(count, 0, sizeof(count));
    for (int i = 0; i < n; i++) {

        // Extract the digits of the element
        // and increase the count
        count_(count, arr[i]);
    }

    // Longest subsequence
    int longest = 0;

    // Get the longest subsequence
    for (int i = 0; i < 10; i++)
        longest = max(count[i], longest);

    // Print the length of longest subsequence
    cout << longest << endl;
}

// Driver code
int main()
{
    int arr[] = { 11, 12, 23, 74, 13 };

    int n = sizeof(arr) / sizeof(arr[0]);

    find_subsequence(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of subsequence which has
// atleast one digit common among all its elements

import java.io.*;

class GFG {

// If the number contains a digit increase
// the count by 1 (even if it has multiple
// same digit the count should be increased
// by only once)
static void count_(int count[], int e)
{
    // Hash to make it sure that a digit
    // is counted only once
    boolean hash[] = new boolean[10];

    // Set the hash to its initial value
    //memset(hash, false, sizeof(hash));

    // Extract the digits
    while (e > 0) {

        // If the digit did not appear before
        if (hash[e % 10] == false)

            // Increase the count
            count[e % 10]++;

        // Mark the digit as visited
        hash[e % 10] = true;

        // Delete the digit
        e /= 10;
    }
}

// Function to find the length of subsequence which has
// atleast one digit common among all its elements
static void find_subsequence(int arr[], int n)
{
    // Count of digits
    int count[] = new int[10];

    // Set the initial value to zero
    //memset(count, 0, sizeof(count));
    for (int i = 0; i < n; i++) {

        // Extract the digits of the element
        // and increase the count
        count_(count, arr[i]);
    }

    // Longest subsequence
    int longest = 0;

    // Get the longest subsequence
    for (int i = 0; i < 10; i++)
        longest = Math.max(count[i], longest);

    // Print the length of longest subsequence
    System.out.print( longest);
}

        // Driver code
    public static void main (String[] args) {
            int arr[] = { 11, 12, 23, 74, 13 };

    int n =arr.length;

    find_subsequence(arr, n);

    }
}
// This code is contributed
// by shs
```

## 蟒蛇 3

```
# Python3 program to find the length
# of subsequence which has atleast
# one digit common among all its elements

# If the number contains a digit increase
# the count by 1 (even if it has multiple
# same digit the count should be increased
# by only once)
def count_(count, e):

    # Hash to make it sure that a digit
    # is counted only once
    hash = [False] * 10

    # Extract the digits
    while (e > 0):

        # If the digit did not
        # appear before
        if (hash[e % 10] == False) :

            # Increase the count
            count[e % 10] += 1

        # Mark the digit as visited
        hash[e % 10] = True

        # Delete the digit
        e //= 10

# Function to find the length of
# subsequence which has atleast
# one digit common among all its elements
def find_subsequence(arr, n) :

    # Count of digits
    count = [0] * 10

    for i in range ( n) :

        # Extract the digits of the element
        # and increase the count
        count_(count, arr[i])

    # Longest subsequence
    longest = 0

    # Get the longest subsequence
    for i in range(10) :
        longest = max(count[i], longest)

    # Print the length of
    # longest subsequence
    print (longest)

# Driver code
if __name__ == "__main__":

    arr = [ 11, 12, 23, 74, 13 ]

    n = len(arr)

    find_subsequence(arr, n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the length
// of subsequence which has atleast
// one digit common among all its elements
using System;

class GFG
{

// If the number contains a digit increase
// the count by 1 (even if it has multiple
// same digit the count should be increased
// by only once)
static void count_(int []count, int e)
{
    // Hash to make it sure that a
    // digit is counted only once
    bool []hash = new bool[10];

    // Set the hash to its initial value
    //memset(hash, false, sizeof(hash));

    // Extract the digits
    while (e > 0)
    {

        // If the digit did not
        // appear before
        if (hash[e % 10] == false)

            // Increase the count
            count[e % 10]++;

        // Mark the digit as visited
        hash[e % 10] = true;

        // Delete the digit
        e /= 10;
    }
}

// Function to find the length of
// subsequence which has atleast
// one digit common among all its elements
static void find_subsequence(int []arr,
                             int n)
{
    // Count of digits
    int []count = new int[10];

    // Set the initial value to zero
    //memset(count, 0, sizeof(count));
    for (int i = 0; i < n; i++)
    {

        // Extract the digits of the element
        // and increase the count
        count_(count, arr[i]);
    }

    // Longest subsequence
    int longest = 0;

    // Get the longest subsequence
    for (int i = 0; i < 10; i++)
        longest = Math.Max(count[i], longest);

    // Print the length of
    // longest subsequence
    Console.WriteLine(longest);
}

// Driver code
public static void Main ()
{
    int []arr = { 11, 12, 23, 74, 13 };

    int n = arr.Length;

    find_subsequence(arr, n);
}
}

// This code is contributed
// by Shashank
```

## java 描述语言

```
<script>

// Javascript program to find the length of subsequence which has
// atleast one digit common among all its elements

// If the number contains a digit increase
// the count by 1 (even if it has multiple
// same digit the count should be increased
// by only once)
function count_(count, e)
{
    // Hash to make it sure that a digit
    // is counted only once
    var hash = Array(10).fill(false);

    // Extract the digits
    while (e > 0) {

        // If the digit did not appear before
        if (hash[e % 10] == false)

            // Increase the count
            count[e % 10]++;

        // Mark the digit as visited
        hash[e % 10] = true;

        // Delete the digit
        e /= 10;
    }
}

// Function to find the length of subsequence which has
// atleast one digit common among all its elements
function find_subsequence(arr, n)
{
    // Count of digits
    var count = Array(10).fill(0);

    for (var i = 0; i < n; i++) {

        // Extract the digits of the element
        // and increase the count
        count_(count, arr[i]);
    }

    // Longest subsequence
    var longest = 0;

    // Get the longest subsequence
    for (var i = 0; i < 10; i++)
        longest = Math.max(count[i], longest);

    // Print the length of longest subsequence
    document.write( longest);
}

// Driver code
var arr = [ 11, 12, 23, 74, 13 ];
var n = arr.length;
find_subsequence(arr, n);

</script>   
```

**Output:** 

```
3
```

**时间复杂度:** O(N)

**辅助空间:** O(N)