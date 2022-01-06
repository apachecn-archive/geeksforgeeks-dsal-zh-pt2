# 从数组

中找出所有连续数字的范围

> 原文:[https://www . geesforgeks . org/find-数组中连续数字的所有范围/](https://www.geeksforgeeks.org/find-all-ranges-of-consecutive-numbers-from-array/)

给定一个由没有任何重复的 **N** 整数组成的排序数组 **arr[]** ，任务是从该数组中找到连续数字的范围。
**例:**

> **输入:** arr[] = {1，2，3，6，7}
> **输出:** 1- > 3，6- > 7
> **解释:**
> 该数组有两个连续数字范围。
> 范围 1 = 1 - > 3
> 范围 2 = 6 - > 7
> **输入:** arr[] = {-1，0，1，2，5，6，8}
> **输出:** -1- > 2，5- > 6，8
> **说明:**
> 该数组有三个连续数的范围。
> 范围 1 = -1 - > 2
> 范围 2 = 5 - > 6
> 范围 3 = 8

**方法:**想法是[从初始位置遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于数组中的每个元素，检查当前元素和前一个元素之间的差异。

*   如果当前元素和前一个元素之间的差是 1，那么我们就增加长度变量。我们使用长度变量来构建范围**“A->B”**。因为只需要范围，所以我们不需要存储 A 和 b 之间的所有元素，我们只需要知道这个范围的长度。
*   如果当前元素和前一个元素之间的差不等于 1，我们将范围的第一个元素和当前前一个元素之间的范围构建为最后一个范围。

下面是上述方法的实现:

## C++

```
// C++ program to find the ranges of
// consecutive numbers from array
#include<bits/stdc++.h>
using namespace std;

// Function to find consecutive ranges
vector<string> consecutiveRanges(int a[], int n)
{
    int length = 1;
    vector<string> list;

    // If the array is empty,
    // return the list
    if (n == 0)
    {
        return list;
    }

    // Traverse the array from first position
    for(int i = 1; i <= n; i++)
    {

        // Check the difference between the
        // current and the previous elements
        // If the difference doesn't equal to 1
        // just increment the length variable.
        if (i == n || a[i] - a[i - 1] != 1)
        {

            // If the range contains
            // only one element.
            // add it into the list.
            if (length == 1)
            {
                list.push_back(to_string(a[i - length]));
            }
            else
            {

                // Build the range between the first
                // element of the range and the
                // current previous element as the
                // last range.
                string temp = to_string(a[i - length]) +
                            " -> " + to_string(a[i - 1]);
                list.push_back(temp);
            }

            // After finding the first range
            // initialize the length by 1 to
            // build the next range.
            length = 1;
        }
        else
        {
            length++;
        }
    }
    return list;
}

// Driver Code.
int main()
{

    // Test Case 1:
    int arr1[] = { 1, 2, 3, 6, 7 };
    int n = sizeof(arr1) / sizeof(arr1[0]);

    vector<string> ans = consecutiveRanges(arr1, n);
    cout << "[";
    for(int i = 0; i < ans.size(); i++)
    {
        if(i == ans.size() - 1)
            cout << ans[i] << "]" << endl;
        else
            cout << ans[i] << ", ";
    }

    // Test Case 2:
    int arr2[] = { -1, 0, 1, 2, 5, 6, 8 };
    n = sizeof(arr2) / sizeof(arr2[0]);
    ans = consecutiveRanges(arr2, n);

    cout << "[";
    for(int i = 0; i < ans.size(); i++)
    {
        if(i == ans.size() - 1)
            cout << ans[i] << "]" << endl;
        else
            cout << ans[i] << ", ";
    }

    // Test Case 3:
    int arr3[] = { -1, 3, 4, 5, 20, 21, 25 };
    n = sizeof(arr3) / sizeof(arr3[0]);
    ans = consecutiveRanges(arr3, n);

    cout << "[";
    for(int i = 0; i < ans.size(); i++)
    {
        if(i == ans.size() - 1)
            cout << ans[i] << "]" << endl;
        else
            cout << ans[i] << ", ";
    }
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the ranges of
// consecutive numbers from array

import java.util.*;

class GFG {

    // Function to find consecutive ranges
    static List<String>
    consecutiveRanges(int[] a)
    {
        int length = 1;
        List<String> list
            = new ArrayList<String>();

        // If the array is empty,
        // return the list
        if (a.length == 0) {
            return list;
        }

        // Traverse the array from first position
        for (int i = 1; i <= a.length; i++) {

            // Check the difference between the
            // current and the previous elements
            // If the difference doesn't equal to 1
            // just increment the length variable.
            if (i == a.length
                || a[i] - a[i - 1] != 1) {

                // If the range contains
                // only one element.
                // add it into the list.
                if (length == 1) {
                    list.add(
                        String.valueOf(a[i - length]));
                }
                else {

                    // Build the range between the first
                    // element of the range and the
                    // current previous element as the
                    // last range.
                    list.add(a[i - length]
                             + " -> " + a[i - 1]);
                }

                // After finding the first range
                // initialize the length by 1 to
                // build the next range.
                length = 1;
            }
            else {
                length++;
            }
        }

        return list;
    }

    // Driver Code.
    public static void main(String args[])
    {

        // Test Case 1:
        int[] arr1 = { 1, 2, 3, 6, 7 };
        System.out.print(consecutiveRanges(arr1));
        System.out.println();

        // Test Case 2:
        int[] arr2 = { -1, 0, 1, 2, 5, 6, 8 };
        System.out.print(consecutiveRanges(arr2));
        System.out.println();

        // Test Case 3:
        int[] arr3 = { -1, 3, 4, 5, 20, 21, 25 };
        System.out.print(consecutiveRanges(arr3));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find
# the ranges of consecutive
# numbers from array

# Function to find
# consecutive ranges
def consecutiveRanges(a, n):

    length = 1
    list = []

    # If the array is empty,
    # return the list
    if (n == 0):
        return list

    # Traverse the array
    # from first position
    for i in range (1, n + 1):

        # Check the difference
        # between the current
        # and the previous elements
        # If the difference doesn't
        # equal to 1 just increment
        # the length variable.
        if (i == n or a[i] -
            a[i - 1] != 1):

            # If the range contains
            # only one element.
            # add it into the list.
            if (length == 1):
                list.append(str(a[i - length]))
            else:

                # Build the range between the first
                # element of the range and the
                # current previous element as the
                # last range.
                temp = (str(a[i - length]) +
                        " -> " + str(a[i - 1]))
                list.append(temp)

            # After finding the 
            # first range initialize
            # the length by 1 to
            # build the next range.
            length = 1

        else:
            length += 1
    return list

# Driver Code.
if __name__ == "__main__":

    # Test Case 1:
    arr1 = [1, 2, 3, 6, 7]
    n = len(arr1)

    ans = consecutiveRanges(arr1, n)
    print ("[", end = "")
    for i in range(len(ans)):

        if(i == len(ans) - 1):
            print (ans[i], "]")
        else:
            print (ans[i], end = ", ")

    # Test Case 2:
    arr2 = [-1, 0, 1, 2, 5, 6, 8]
    n = len(arr2)
    ans = consecutiveRanges(arr2, n)

    print ("[", end = "")

    for i in range (len(ans)): 
        if(i == len(ans) - 1):
            print (ans[i], "]")
        else:
            print (ans[i], end = ", ")

    # Test Case 3:
    arr3 = [-1, 3, 4, 5, 20, 21, 25]
    n = len(arr3)
    ans = consecutiveRanges(arr3, n)

    print ("[", end = "")

    for i in range (len(ans)):   
        if(i == len(ans) - 1):
            print (ans[i], "]")
        else:
            print (ans[i], end = ", ")

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find the ranges of
// consecutive numbers from array
using System;
using System.Collections.Generic;

class GFG{

// Function to find consecutive ranges
static List<String> consecutiveRanges(int[] a)
{
    int length = 1;
    List<String> list = new List<String>();

    // If the array is empty,
    // return the list
    if (a.Length == 0)
    {
        return list;
    }

    // Traverse the array from first position
    for(int i = 1; i <= a.Length; i++)
    {

        // Check the difference between the
        // current and the previous elements
        // If the difference doesn't equal to 1
        // just increment the length variable.
        if (i == a.Length || a[i] - a[i - 1] != 1)
        {

            // If the range contains
            // only one element.
            // add it into the list.
            if (length == 1)
            {
                list.Add(
                    String.Join("", a[i - length]));
            }
            else
            {

                // Build the range between the first
                // element of the range and the
                // current previous element as the
                // last range.
                list.Add(a[i - length] +
                " -> " + a[i - 1]);
            }

            // After finding the first range
            // initialize the length by 1 to
            // build the next range.
            length = 1;
        }
        else
        {
            length++;
        }
    }
    return list;
}

static void print(List<String> arr)
{
    Console.Write("[");
    foreach(String i in arr)
        Console.Write(i + ", ");

    Console.Write("]");
}

// Driver Code.
public static void Main(String []args)
{

    // Test Case 1:
    int[] arr1 = { 1, 2, 3, 6, 7 };
    print(consecutiveRanges(arr1));
    Console.WriteLine();

    // Test Case 2:
    int[] arr2 = { -1, 0, 1, 2, 5, 6, 8 };
    print(consecutiveRanges(arr2));
    Console.WriteLine();

    // Test Case 3:
    int[] arr3 = { -1, 3, 4, 5, 20, 21, 25 };
    print(consecutiveRanges(arr3));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to find the ranges of
// consecutive numbers from array

// Function to find consecutive ranges
function consecutiveRanges(a)
{
    let length = 1;
        let list
            = [];

        // If the array is empty,
        // return the list
        if (a.length == 0) {
            return list;
        }

        // Traverse the array from first position
        for (let i = 1; i <= a.length; i++) {

            // Check the difference between the
            // current and the previous elements
            // If the difference doesn't equal to 1
            // just increment the length variable.
            if (i == a.length
                || a[i] - a[i - 1] != 1) {

                // If the range contains
                // only one element.
                // add it into the list.
                if (length == 1) {
                    list.push(
                        (a[i - length]).toString());
                }
                else {

                    // Build the range between the first
                    // element of the range and the
                    // current previous element as the
                    // last range.
                    list.push(a[i - length]
                             + " -> " + a[i - 1]);
                }

                // After finding the first range
                // initialize the length by 1 to
                // build the next range.
                length = 1;
            }
            else {
                length++;
            }
        }

        return list;
}

// Driver Code.

// Test Case 1:
let arr1=[ 1, 2, 3, 6, 7];
document.write("[");
document.write(consecutiveRanges(arr1));
document.write("]");
document.write("<br>");

// Test Case 2:
let arr2=[ -1, 0, 1, 2, 5, 6, 8 ];
document.write("[");
document.write(consecutiveRanges(arr2));
document.write("]");
document.write("<br>");

// Test Case 3:
let arr3=[ -1, 3, 4, 5, 20, 21, 25 ];
document.write("[");
document.write(consecutiveRanges(arr3));
document.write("]");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
[1 -> 3, 6 -> 7]
[-1 -> 2, 5 -> 6, 8]
[-1, 3 -> 5, 20 -> 21, 25]
```

**时间复杂度:** *O(N)* ，其中 N 为数组长度。