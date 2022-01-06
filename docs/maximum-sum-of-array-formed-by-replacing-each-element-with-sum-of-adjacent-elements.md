# 用相邻元素之和替换每个元素形成的数组的最大和

> 原文:[https://www . geesforgeks . org/通过用相邻元素之和替换每个元素形成的最大数组之和/](https://www.geeksforgeeks.org/maximum-sum-of-array-formed-by-replacing-each-element-with-sum-of-adjacent-elements/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是找到通过用相邻元素的和替换原始数组的每个元素而形成的数组的最大和。
**例:**

> **输入:**arr =【4，2，1，3】
> **输出:** 23
> **解释:**
> 用相邻元素之和替换原数组的每个元素:
> 4+2 = 6
> 6+1 = 7
> 7+3 = 10
> 用相邻元素之和替换原数组的每个元素形成的数组:【6，7，10】
> 因此， 总和= 6 + 7 + 10 = 23
> **输入:** arr = [2，3，9，8， 4]
> **输出:** 88
> **说明:**
> 用相邻元素之和替换原数组的每个元素得到最大和:
> 9+8 = 17
> 17+4 = 21
> 21+3 = 24
> 24+2 = 26
> 用相邻元素之和替换原数组的每个元素形成的数组:[17，21，24，26]

**进场:**

*   扫描整个阵列，选择具有最高总和的相邻对。
*   从那里开始，使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)，选择左边或右边的整数，以较大者为准。
*   重复这个过程，直到数组中只剩下一个元素。

以下是上述方法的实现:

## C++

```
// C++ program to find the maximum sum
// of Array formed by replacing each
// element with sum of adjacent elements

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the possible
// maximum cost of the array
int getTotalTime(vector<int>& arr)
{

    // Check if array size is 0
    if (arr.size() == 0)
        return 0;

    // Initialise left and right variables
    int l = -1, r = -1;

    for (int i = 1; i < arr.size(); i++) {
        if (l == -1
            || (arr[i - 1] + arr[i])
                   > (arr[l] + arr[r])) {
            l = i - 1;
            r = i;
        }
    }

    // Calculate the current cost
    int currCost = arr[l] + arr[r];

    int totalCost = currCost;

    l--;
    r++;

    // Iterate until left variable reaches 0
    // and right variable is less than array size
    while (l >= 0 || r < arr.size()) {

        int left = l < 0
                       ? INT_MIN
                       : arr[l];
        int right = r >= arr.size()
                        ? INT_MIN
                        : arr[r];

        // Check if left integer is greater
        // than the right then add left integer
        // to the current cost and
        // decrement the left variable
        if (left > right) {
            currCost += left;

            totalCost += currCost;

            l--;
        }

        // Executes if right integer is
        // greater than left then add
        // right integer to the current cost
        // and increment the right variable
        else {

            currCost += right;
            totalCost += currCost;
            r++;
        }
    }

    // Return the final answer
    return totalCost;
}

// Driver code
int main(int argc, char* argv[])
{
    vector<int> arr = { 2, 3, 9, 8, 4 };

    cout << getTotalTime(arr) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum sum
// of array formed by replacing each
// element with sum of adjacent elements
class GFG{

// Function to calculate the possible
// maximum cost of the array
static int getTotalTime(int []arr)
{

    // Check if array size is 0
    if (arr.length == 0)
        return 0;

    // Initialise left and right variables
    int l = -1, r = -1;

    for(int i = 1; i < arr.length; i++)
    {
       if (l == -1 || (arr[i - 1] + arr[i]) >
                          (arr[l] + arr[r]))
       {
           l = i - 1;
           r = i;
       }
    }

    // Calculate the current cost
    int currCost = arr[l] + arr[r];

    int totalCost = currCost;

    l--;
    r++;

    // Iterate until left variable reaches 0
    // and right variable is less than array size
    while (l >= 0 || r < arr.length)
    {
        int left = (l < 0 ?
                    Integer.MIN_VALUE : arr[l]);
        int right = (r >= arr.length ?
                    Integer.MIN_VALUE : arr[r]);

        // Check if left integer is greater
        // than the right then add left integer
        // to the current cost and
        // decrement the left variable
        if (left > right)
        {
            currCost += left;
            totalCost += currCost;
            l--;
        }

        // Executes if right integer is
        // greater than left then add
        // right integer to the current cost
        // and increment the right variable
        else
        {
            currCost += right;
            totalCost += currCost;
            r++;
        }
    }

    // Return the final answer
    return totalCost;
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 2, 3, 9, 8, 4 };

    System.out.print(getTotalTime(arr) + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find the maximum sum
# of Array formed by replacing each
# element with sum of adjacent elements
import sys

# Function to calculate the possible
# maximum cost of the array
def getTotalTime(arr):

    # Check if array size is 0
    if (len(arr) == 0):
        return 0

    # Initialise left and right variables
    l = -1
    r = -1

    for i in range(1, len(arr), 1):
        if (l == -1 or (arr[i - 1] + arr[i]) > (arr[l] + arr[r])):
            l = i - 1
            r = i

    # Calculate the current cost
    currCost = arr[l] + arr[r]

    totalCost = currCost

    l -= 1
    r += 1

    # Iterate until left variable reaches 0
    # and right variable is less than array size
    while (l >= 0 or r < len(arr)):
        if(l < 0):
            left = sys.maxsize
        else:
            left = arr[l]
        if (r >= len(arr)):
            right = -sys.maxsize - 1
        else:
            right = arr[r]

        # Check if left integer is greater
        # than the right then add left integer
        # to the current cost and
        # decrement the left variable
        if (left > right):
            currCost += left

            totalCost += currCost

            l -= 1

        # Executes if right integer is
        # greater than left then add
        # right integer to the current cost
        # and increment the right variable
        else:
            currCost += right
            totalCost += currCost
            r += 1

    # Return the final answer
    return totalCost

# Driver code
if __name__ == '__main__':
    arr = [2, 3, 9, 8, 4]

    print(getTotalTime(arr))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to find the maximum sum
// of array formed by replacing each
// element with sum of adjacent elements
using System;

class GFG{

// Function to calculate the possible
// maximum cost of the array
static int getTotalTime(int []arr)
{

    // Check if array size is 0
    if (arr.Length == 0)
        return 0;

    // Initialise left and right variables
    int l = -1, r = -1;

    for(int i = 1; i < arr.Length; i++)
    {
       if (l == -1 || (arr[i - 1] + arr[i]) >
                          (arr[l] + arr[r]))
       {
           l = i - 1;
           r = i;
       }
    }

    // Calculate the current cost
    int currCost = arr[l] + arr[r];

    int totalCost = currCost;

    l--;
    r++;

    // Iterate until left variable reaches 0
    // and right variable is less than array size
    while (l >= 0 || r < arr.Length)
    {
        int left = (l < 0 ?
                    int.MinValue : arr[l]);
        int right = (r >= arr.Length ?
                    int.MinValue : arr[r]);

        // Check if left integer is greater
        // than the right then add left integer
        // to the current cost and
        // decrement the left variable
        if (left > right)
        {
            currCost += left;
            totalCost += currCost;
            l--;
        }

        // Executes if right integer is
        // greater than left then add
        // right integer to the current cost
        // and increment the right variable
        else
        {
            currCost += right;
            totalCost += currCost;
            r++;
        }
    }

    // Return the readonly answer
    return totalCost;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 9, 8, 4 };

    Console.Write(getTotalTime(arr) + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the maximum sum
// of Array formed by replacing each
// element with sum of adjacent elements

// Function to calculate the possible
// maximum cost of the array
function getTotalTime(arr)
{

    // Check if array size is 0
    if (arr.length == 0)
        return 0;

    // Initialise left and right variables
    var l = -1, r = -1;

    for (var i = 1; i < arr.length; i++) {
        if (l == -1
            || (arr[i - 1] + arr[i])
                   > (arr[l] + arr[r])) {
            l = i - 1;
            r = i;
        }
    }

    // Calculate the current cost
    var currCost = arr[l] + arr[r];

    var totalCost = currCost;

    l--;
    r++;

    // Iterate until left variable reaches 0
    // and right variable is less than array size
    while (l >= 0 || r < arr.length) {

        var left = l < 0
                       ? -1000000000
                       : arr[l];
        var right = r >= arr.length
                        ? -1000000000
                        : arr[r];

        // Check if left integer is greater
        // than the right then add left integer
        // to the current cost and
        // decrement the left variable
        if (left > right) {
            currCost += left;

            totalCost += currCost;

            l--;
        }

        // Executes if right integer is
        // greater than left then add
        // right integer to the current cost
        // and increment the right variable
        else {

            currCost += right;
            totalCost += currCost;
            r++;
        }
    }

    // Return the final answer
    return totalCost;
}

// Driver code
var arr = [2, 3, 9, 8, 4];
document.write( getTotalTime(arr));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
88
```

***时间复杂度:** O(N)*
***空间复杂度:** O(N)*