# 根据相邻数组元素的绝对值最大化移除它们

> 原文:[https://www . geeksforgeeks . org/基于绝对值最大化移除相邻数组元素/](https://www.geeksforgeeks.org/maximize-removal-of-adjacent-array-elements-based-on-their-absolute-value/)

给定一个由正整数和负整数组成的**数组 arr[]** ，任务是从数组的最后一个索引开始移除相邻的数组元素后打印该数组。
可以根据以下条件移除数组元素:

*   符号相反的两个相邻元素只需要比较。
*   符号相反的两个相邻元素的较小绝对值将被丢弃。
*   符号相反的两个相等的绝对值相邻元素都将被丢弃。
*   如果结果数组为空，则打印-1。

**例:**

> **输入:** arr[] = { 2，7，-6，3，8，-5 }
> **输出:** 2 7 3 8
> **解释:**
> 比较 arr[4]和 arr[5]后，arr[5]因为|8| > |-6|而被丢弃。
> 比较 arr[1]和 arr[2]后，arr[2]被丢弃，因为|7| > |-6|。
> **输入:** arr[] = { 2，7，-9，3，8，-5 }
> **输出:** -9 3 8
> **解释:**
> 比较 arr[4]和 arr[5]后，arr[5]因为|8| > |-5|而被丢弃。
> 比较 arr[1]和 arr[2]后，arr[1]被丢弃，因为|7| < |-9|。
> 在比较 arr[0]和 arr[2]之后，arr[0]被丢弃，因为|2| < |-9|。

**方法:**
要解决上述问题，请按照以下步骤操作:

*   遍历给定的输入数组，如果元素为正，则将它插入向量中。
*   如果元素是负的，那么通过以相反的方式遍历最终向量来找到这个整数的正确状态，并检查向量中的最后一个元素是正的还是负的。
*   如果是正数，我们通过比较两个整数的绝对值来检查哪一个会被丢弃。
*   如果向量是空的或者其中的最后一个元素是负的，那么我们将当前元素放入最终向量中。
*   如果通过比较两个整数的绝对值，我们得到相同的值，那么向量的最后一个元素被丢弃。

以下是上述方法的实现:

## C++

```
// C++ Program to maximize removals
// of adjacent array elements based
// on their absolute value
#include <bits/stdc++.h>
using namespace std;

// Function to find remaining
// array elements after removals
void removals(int arr[], int n)
{
    vector<int> v;

    for (int i = 0; i < n; i++) {
        // If i-th element is having
        // positive value (moving right)
        if (arr[i] > 0)
            // Push them into
            // the vector
            v.push_back(arr[i]);

        else {
            // If the last element of the vector
            // is of opposite sign and is less
            // than the value of current
            // integer then pop that element
            while (!v.empty() && (v.back() > 0)
                   && v.back() < abs(arr[i]))
                v.pop_back();

            // Check if vector is empty or the
            // last element has same sign
            if (v.empty() || v.back() < 0)
                v.push_back(arr[i]);

            // Check if the value is same
            else if (v.back() == abs(arr[i]))
                v.pop_back();
        }
    }

    // If vector is empty
    if (v.size() == 0) {
        cout << -1;
        return;
    }

    // Print the final array
    for (int i = 0; i < v.size(); i++) {
        cout << v[i] << " ";
    }

    return;
}

// Driver Code
int main()
{
    int arr[] = { 2, 7, -9, 3, 8, -5 };

    int n = sizeof(arr) / sizeof(arr[0]);

    removals(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to maximize removals
// of adjacent array elements based
// on their absolute value
import java.util.*;
class GFG{

// Function to find remaining
// array elements after removals
static void removals(int arr[], int n)
{
    Vector<Integer> v = new Vector<Integer>();

    for (int i = 0; i < n; i++)
    {
        // If i-th element is having
        // positive value (moving right)
        if (arr[i] > 0)

            // Push them into
            // the vector
            v.add(arr[i]);

        else
        {

            // If the last element of the vector
            // is of opposite sign and is less
            // than the value of current
            // integer then pop that element
            while (!v.isEmpty() && (v.lastElement() > 0) &&
                    v.lastElement() < Math.abs(arr[i]))
                v.remove(v.size()-1);

            // Check if vector is empty or the
            // last element has same sign
            if (v.isEmpty() || v.lastElement() < 0)
                v.add(arr[i]);

            // Check if the value is same
            else if (v.lastElement() == Math.abs(arr[i]))
                v.remove(v.size() - 1);
        }
    }

    // If vector is empty
    if (v.size() == 0)
    {
        System.out.print(-1);
        return;
    }

    // Print the final array
    for (int i = 0; i < v.size(); i++)
    {
        System.out.print(v.get(i) + " ");
    }
    return;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 7, -9, 3, 8, -5 };

    int n = arr.length;

    removals(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to maximize removals
# of adjacent array elements based
# on their absolute value

# Function to find remaining
# array elements after removals
def removals(arr, n):

    v = []

    for i in range(n):

        # If i-th element is having
        # positive value (moving right)
        if (arr[i] > 0):

            # Push them into
            # the vector
            v.append(arr[i])

        else:

            # If the last element of the vector
            # is of opposite sign and is less
            # than the value of current
            # integer then pop that element
            while (len(v) != 0 and v[-1] > 0 and
                                   v[-1] < abs(arr[i])):
                v.pop()

            # Check if vector is empty or the
            # last element has same sign
            if (len(v) == 0 or v[-1] < 0):
                v.append(arr[i])

            # Check if the value is same
            elif (v[-1] == abs(arr[i])):
                v.pop()

    # If vector is empty
    if (len(v) == 0):
        print(-1)
        return

    # Print the final array
    for i in range(len(v)):
        print(v[i], end = " ")

    return

# Driver Code
if __name__ == "__main__":

    arr = [ 2, 7, -9, 3, 8, -5 ]
    n = len(arr)

    removals(arr, n)

# This code is contributed by chitranayal
```

## C#

```
// C# program to maximize removals
// of adjacent array elements based
// on their absolute value
using System;
using System.Collections.Generic;

class GFG{

// Function to find remaining
// array elements after removals
static void removals(int []arr, int n)
{
    List<int> v = new List<int>();

    for(int i = 0; i < n; i++)
    {

        // If i-th element is having
        // positive value (moving right)
        if (arr[i] > 0)

            // Push them into
            // the vector
            v.Add(arr[i]);

        else
        {

            // If the last element of the vector
            // is of opposite sign and is less
            // than the value of current
            // integer then pop that element
            while (v.Count != 0 && (v[v.Count - 1] > 0) &&
                 v[v.Count - 1] < Math.Abs(arr[i]))
                v.RemoveAt(v.Count - 1);

            // Check if vector is empty or the
            // last element has same sign
            if (v.Count == 0 || v[v.Count - 1] < 0)
                v.Add(arr[i]);

            // Check if the value is same
            else if (v[v.Count - 1] == Math.Abs(arr[i]))
                v.RemoveAt(v.Count - 1);
        }
    }

    // If vector is empty
    if (v.Count == 0)
    {
        Console.Write(-1);
        return;
    }

    // Print the readonly array
    for(int i = 0; i < v.Count; i++)
    {
        Console.Write(v[i] + " ");
    }
    return;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 7, -9, 3, 8, -5 };

    int n = arr.Length;

    removals(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript Program to maximize removals
// of adjacent array elements based
// on their absolute value

// Function to find remaining
// array elements after removals
function removals(arr,n)
{
    let v = [];

    for (let i = 0; i < n; i++)
    {
        // If i-th element is having
        // positive value (moving right)
        if (arr[i] > 0)

            // Push them into
            // the vector
            v.push(arr[i]);

        else
        {

            // If the last element of the vector
            // is of opposite sign and is less
            // than the value of current
            // integer then pop that element
            while (v.length!=0 && (v[v.length-1] > 0) &&
                    v[v.length-1] < Math.abs(arr[i]))
                v.pop();

            // Check if vector is empty or the
            // last element has same sign
            if (v.length==0 || v[v.length-1] < 0)
                v.push(arr[i]);

            // Check if the value is same
            else if (v[v.length-1] == Math.abs(arr[i]))
                v.pop();
        }
    }

    // If vector is empty
    if (v.length == 0)
    {
        document.write(-1);
        return;
    }

    // Print the final array
    for (let i = 0; i < v.length; i++)
    {
        document.write(v[i] + " ");
    }
    return;
}

// Driver Code
let arr=[ 2, 7, -9, 3, 8, -5];
let n = arr.length;
removals(arr, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
-9 3 8
```