# 所有 Y 尺寸子阵列中最大和最小元素之间的最小差异

> 原文:[https://www . geesforgeks . org/min-全 y 尺寸子阵中最大和最小元素之差/](https://www.geeksforgeeks.org/min-difference-between-maximum-and-minimum-element-in-all-y-size-subarrays/)

给定一个大小为 **N** 和整数 **Y** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出大小为 **Y** 的所有子数组中最大和最小元素之间的所有差异的最小值。

**示例:**

> **输入:** arr[] = { 3，2，4，5，6，1，9 } Y = 3
> **输出:** 2
> **解释:**
> 所有长度= 3 的子阵为:
> {3，2，4}其中最大元素= 4，最小元素= 2 差= 2
> {2，4，5}其中最大元素= 5，最小元素= 2 差= 3
> {4，5， 6}其中最大元素= 6，最小元素= 4 差= 2
> {5，6，1}其中最大元素= 6，最小元素= 1 差= 5
> {6，1，9}其中最大元素= 9，最小元素= 6 差= 3
> 其中，最小值为 2。
> 
> **输入:** arr[] = { 1，2，3，3，2，2} Y = 4
> **输出:** 1
> **解释:**
> 所有长度= 4 的子阵为:
> {1，2，3，3}最大元素= 3 和最小元素= 1 差= 2
> {2，3，3，2 }最大元素= 3 和最小元素= 2 差= 1
> {3，3，2，2 }最大元素= 1

**天真方法:**天真的想法是遍历范围内的每个索引 I**【0，N–Y】**使用另一个循环从 i <sup>第</sup>个索引遍历到(I+Y–1)<sup>第</sup>个索引，然后计算大小为 **Y** 的子阵列中的最小和最大元素，从而计算第 i <sup>次</sup>迭代的最大和最小元素之差。最后，通过检查差异，评估最小差异。

**时间复杂度:***O(N * Y)*
T5】辅助空间: *O(1)*

**高效方法:**想法是使用**[**下一个更大元素**](https://www.geeksforgeeks.org/next-greater-element/) 文章**中讨论的方法的概念。**以下是步骤:**

1.  **构建两个数组**maxarr【】**和**minar【】**，其中**maxarr【】**将存储下一个大于 **i <sup>th</sup> index** 的元素的索引，而**minar【】**将存储下一个小于 **i <sup>th</sup> index** 的元素的索引。**
2.  **用 **0** 初始化一个堆栈，以存储上述两种情况下的索引。**
3.  **对于每个索引， **i** 在**【0，N–Y】**范围内，使用嵌套循环和[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)方法形成两个数组*子矩阵*和*子矩阵。*这些数组将在 **i <sup>th</sup>** 迭代中存储子数组中的最大和最小元素。**
4.  **最后，计算最小差值。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the maximum of all
// the subarrays of size Y
vector<int> get_submaxarr(int* arr,
                        int n, int y)
{
    int j = 0;
    stack<int> stk;

    // ith index of maxarr array
    // will be the index upto which
    // Arr[i] is maximum
    vector<int> maxarr(n);
    stk.push(0);

    for (int i = 1; i < n; i++) {

        // Stack is used to find the
        // next larger element and
        // keeps track of index of
        // current iteration
        while (stk.empty() == false
            and arr[i] > arr[stk.top()]) {

            maxarr[stk.top()] = i - 1;
            stk.pop();
        }
        stk.push(i);
    }

    // Loop for remaining indexes
    while (!stk.empty()) {

        maxarr[stk.top()] = n - 1;
        stk.pop();
    }
    vector<int> submax;

    for (int i = 0; i <= n - y; i++) {

        // j < i used to keep track
        // whether jth element is
        // inside or outside the window
        while (maxarr[j] < i + y - 1
            or j < i) {
            j++;
        }

        submax.push_back(arr[j]);
    }

    // Return submax
    return submax;
}

// Function to get the minimum for
// all subarrays of size Y
vector<int> get_subminarr(int* arr,
                        int n, int y)
{
    int j = 0;

    stack<int> stk;

    // ith index of minarr array
    // will be the index upto which
    // Arr[i] is minimum
    vector<int> minarr(n);
    stk.push(0);

    for (int i = 1; i < n; i++) {

        // Stack is used to find the
        // next smaller element and
        // keeping track of index of
        // current iteration
        while (stk.empty() == false
            and arr[i] < arr[stk.top()]) {

            minarr[stk.top()] = i;
            stk.pop();
        }
        stk.push(i);
    }

    // Loop for remaining indexes
    while (!stk.empty()) {

        minarr[stk.top()] = n;
        stk.pop();
    }

    vector<int> submin;

    for (int i = 0; i <= n - y; i++) {

        // j < i used to keep track
        // whether jth element is inside
        // or outside the window

        while (minarr[j] <= i + y - 1
            or j < i) {
            j++;
        }

        submin.push_back(arr[j]);
    }

    // Return submin
    return submin;
}

// Function to get minimum difference
void getMinDifference(int Arr[], int N,
                    int Y)
{
    // Create submin and submax arrays
    vector<int> submin
        = get_subminarr(Arr, N, Y);

    vector<int> submax
        = get_submaxarr(Arr, N, Y);

    // Store initial difference
    int minn = submax[0] - submin[0];
    int b = submax.size();

    for (int i = 1; i < b; i++) {

        // Calculate temporary difference
        int dif = submax[i] - submin[i];
        minn = min(minn, dif);
    }

    // Final minimum difference
    cout << minn << "\n";
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 3, 2, 2 };
    int N = sizeof arr / sizeof arr[0];

    // Given subarray size
    int Y = 4;

    // Function Call
    getMinDifference(arr, N, Y);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to get the maximum of all
// the subarrays of size Y
static Vector<Integer> get_submaxarr(int[] arr, int n,
                                     int y)
{
    int j = 0;
    Stack<Integer> stk = new Stack<Integer>();

    // ith index of maxarr array
    // will be the index upto which
    // Arr[i] is maximum
    int[] maxarr = new int[n];
    Arrays.fill(maxarr,0);
    stk.push(0);

    for(int i = 1; i < n; i++)
    {

        // Stack is used to find the
        // next larger element and
        // keeps track of index of
        // current iteration
        while (stk.size() != 0 &&
               arr[i] > arr[stk.peek()])
        {
            maxarr[stk.peek()] = i - 1;
            stk.pop();
        }
        stk.push(i);
    }

    // Loop for remaining indexes
    while (stk.size() != 0)
    {
        maxarr[stk.size()] = n - 1;
        stk.pop();
    }
    Vector<Integer> submax = new Vector<Integer>();

    for(int i = 0; i <= n - y; i++)
    {

        // j < i used to keep track
        // whether jth element is
        // inside or outside the window
        while (maxarr[j] < i + y - 1 || j < i)
        {
            j++;
        }
        submax.add(arr[j]);
    }

    // Return submax
    return submax;
}

// Function to get the minimum for
// all subarrays of size Y
static Vector<Integer> get_subminarr(int[] arr, int n,
                                     int y)
{
    int j = 0;

    Stack<Integer> stk = new Stack<Integer>();

    // ith index of minarr array
    // will be the index upto which
    // Arr[i] is minimum
    int[] minarr = new int[n];
    Arrays.fill(minarr,0);
    stk.push(0);

    for(int i = 1; i < n; i++)
    {

        // Stack is used to find the
        // next smaller element and
        // keeping track of index of
        // current iteration
        while (stk.size() != 0 &&
               arr[i] < arr[stk.peek()])
        {
            minarr[stk.peek()] = i;
            stk.pop();
        }
        stk.push(i);
    }

    // Loop for remaining indexes
    while (stk.size() != 0)
    {
        minarr[stk.peek()] = n;
        stk.pop();
    }

    Vector<Integer> submin = new Vector<Integer>();

    for(int i = 0; i <= n - y; i++)
    {

        // j < i used to keep track
        // whether jth element is inside
        // or outside the window

        while (minarr[j] <= i + y - 1 || j < i)
        {
            j++;
        }
        submin.add(arr[j]);
    }

    // Return submin
    return submin;
}

// Function to get minimum difference
static void getMinDifference(int[] Arr, int N, int Y)
{

    // Create submin and submax arrays
    Vector<Integer> submin = get_subminarr(Arr, N, Y);

    Vector<Integer> submax = get_submaxarr(Arr, N, Y);

    // Store initial difference
    int minn = submax.get(0) - submin.get(0);
    int b = submax.size();

    for(int i = 1; i < b; i++)
    {

        // Calculate temporary difference
        int dif = submax.get(i) - submin.get(i) + 1;
        minn = Math.min(minn, dif);
    }

    // Final minimum difference
    System.out.print(minn);
}

// Driver code
public static void main(String[] args)
{

    // Given array arr[]
    int[] arr = { 1, 2, 3, 3, 2, 2 };
    int N = arr.length;

    // Given subarray size
    int Y = 4;

    // Function Call
    getMinDifference(arr, N, Y);
}
}

// This code is contributed by decode2207
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to get the maximum of all
# the subarrays of size Y
def get_submaxarr(arr, n, y):

    j = 0
    stk = []

    # ith index of maxarr array
    # will be the index upto which
    # Arr[i] is maximum
    maxarr = [0] * n
    stk.append(0)

    for i in range(1, n):

        # Stack is used to find the
        # next larger element and
        # keeps track of index of
        # current iteration
        while (len(stk) > 0 and
                 arr[i] > arr[stk[-1]]):
            maxarr[stk[-1]] = i - 1
            stk.pop()

        stk.append(i)

    # Loop for remaining indexes
    while (stk):
        maxarr[stk[-1]] = n - 1
        stk.pop()

    submax = []

    for i in range(n - y + 1):

        # j < i used to keep track
        # whether jth element is
        # inside or outside the window
        while (maxarr[j] < i + y - 1 or
                       j < i):
            j += 1

        submax.append(arr[j])

    # Return submax
    return submax

# Function to get the minimum for
# all subarrays of size Y
def get_subminarr(arr, n, y):

    j = 0
    stk = []

    # ith index of minarr array
    # will be the index upto which
    # Arr[i] is minimum
    minarr = [0] * n
    stk.append(0)

    for i in range(1 , n):

        # Stack is used to find the
        # next smaller element and
        # keeping track of index of
        # current iteration
        while (stk and arr[i] < arr[stk[-1]]):
            minarr[stk[-1]] = i
            stk.pop()

        stk.append(i)

    # Loop for remaining indexes
    while (stk):
        minarr[stk[-1]] = n
        stk.pop()

    submin = []

    for i in range(n - y + 1):

        # j < i used to keep track
        # whether jth element is inside
        # or outside the window
        while (minarr[j] <= i + y - 1 or
                      j < i):
            j += 1

        submin.append(arr[j])

    # Return submin
    return submin

# Function to get minimum difference
def getMinDifference(Arr, N, Y):

    # Create submin and submax arrays
    submin = get_subminarr(Arr, N, Y)
    submax = get_submaxarr(Arr, N, Y)

    # Store initial difference
    minn = submax[0] - submin[0]
    b = len(submax)

    for i in range(1, b):

        # Calculate temporary difference
        diff = submax[i] - submin[i]
        minn = min(minn, diff)

    # Final minimum difference
    print(minn)

# Driver code

# Given array arr[]
arr = [ 1, 2, 3, 3, 2, 2 ]
N = len(arr)

# Given subarray size
Y = 4

# Function call
getMinDifference(arr, N, Y)

# This code is contributed by Stuti Pathak
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to get the maximum of all
    // the subarrays of size Y
    static List<int> get_submaxarr(int[] arr, int n, int y)
    {
        int j = 0;
        Stack<int> stk = new Stack<int>();

        // ith index of maxarr array
        // will be the index upto which
        // Arr[i] is maximum
        int[] maxarr = new int[n];
        Array.Fill(maxarr,0);
        stk.Push(0);

        for (int i = 1; i < n; i++) {

            // Stack is used to find the
            // next larger element and
            // keeps track of index of
            // current iteration
            while (stk.Count!=0 && arr[i] > arr[stk.Peek()]) {

                maxarr[stk.Peek()] = i - 1;
                stk.Pop();
            }
            stk.Push(i);
        }

        // Loop for remaining indexes
        while (stk.Count!=0) {

            maxarr[stk.Count] = n - 1;
            stk.Pop();
        }
        List<int> submax = new List<int>();

        for (int i = 0; i <= n - y; i++) {

            // j < i used to keep track
            // whether jth element is
            // inside or outside the window
            while (maxarr[j] < i + y - 1
                || j < i) {
                j++;
            }

            submax.Add(arr[j]);
        }

        // Return submax
        return submax;
    }

    // Function to get the minimum for
    // all subarrays of size Y
    static List<int> get_subminarr(int[] arr, int n, int y)
    {
        int j = 0;

        Stack<int> stk = new Stack<int>();

        // ith index of minarr array
        // will be the index upto which
        // Arr[i] is minimum
        int[] minarr = new int[n];
        Array.Fill(minarr,0);
        stk.Push(0);

        for (int i = 1; i < n; i++) {

            // Stack is used to find the
            // next smaller element and
            // keeping track of index of
            // current iteration
            while (stk.Count!=0
                && arr[i] < arr[stk.Peek()]) {

                minarr[stk.Peek()] = i;
                stk.Pop();
            }
            stk.Push(i);
        }

        // Loop for remaining indexes
        while (stk.Count!=0) {

            minarr[stk.Peek()] = n;
            stk.Pop();
        }

        List<int> submin = new List<int>();

        for (int i = 0; i <= n - y; i++) {

            // j < i used to keep track
            // whether jth element is inside
            // or outside the window

            while (minarr[j] <= i + y - 1
                || j < i) {
                j++;
            }

            submin.Add(arr[j]);
        }

        // Return submin
        return submin;
    }

    // Function to get minimum difference
    static void getMinDifference(int[] Arr, int N, int Y)
    {
        // Create submin and submax arrays
        List<int> submin
            = get_subminarr(Arr, N, Y);

        List<int> submax
            = get_submaxarr(Arr, N, Y);

        // Store initial difference
        int minn = submax[0] - submin[0];
        int b = submax.Count;

        for (int i = 1; i < b; i++) {

            // Calculate temporary difference
            int dif = submax[i] - submin[i] + 1;
            minn = Math.Min(minn, dif);
        }

        // Final minimum difference
        Console.WriteLine(minn);
    }

  static void Main() {
    // Given array arr[]
    int[] arr = { 1, 2, 3, 3, 2, 2 };
    int N = arr.Length;

    // Given subarray size
    int Y = 4;

    // Function Call
    getMinDifference(arr, N, Y);
  }
}

// This code is contributed by rameshtravel07.
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to get the maximum of all
// the subarrays of size Y
function get_submaxarr(arr, n, y)
{
    var j = 0;
    var stk = [];

    // ith index of maxarr array
    // will be the index upto which
    // Arr[i] is maximum
    var maxarr = Array(n);
    stk.push(0);

    for (var i = 1; i < n; i++) {

        // Stack is used to find the
        // next larger element and
        // keeps track of index of
        // current iteration
        while (stk.length!=0
            && arr[i] > arr[stk[stk.length-1]]) {

            maxarr[stk[stk.length-1]] = i - 1;
            stk.pop();
        }
        stk.push(i);
    }

    // Loop for remaining indexes
    while (stk.length!=0) {

        maxarr[stk[stk.length-1]] = n - 1;
        stk.pop();
    }
    var submax = [];

    for (var i = 0; i <= n - y; i++) {

        // j < i used to keep track
        // whether jth element is
        // inside or outside the window
        while (maxarr[j] < i + y - 1
            || j < i) {
            j++;
        }

        submax.push(arr[j]);
    }

    // Return submax
    return submax;
}

// Function to get the minimum for
// all subarrays of size Y
function get_subminarr(arr, n, y)
{
    var j = 0;

    var stk = [];

    // ith index of minarr array
    // will be the index upto which
    // Arr[i] is minimum
    var minarr = Array(n);
    stk.push(0);

    for (var i = 1; i < n; i++) {

        // Stack is used to find the
        // next smaller element and
        // keeping track of index of
        // current iteration
        while (stk.length!=0
            && arr[i] < arr[stk[stk.length-1]]) {

            minarr[stk[stk.length-1]] = i;
            stk.pop();
        }
        stk.push(i);
    }

    // Loop for remaining indexes
    while (stk.length!=0) {

        minarr[stk[stk.length-1]] = n;
        stk.pop();
    }

    var submin = [];

    for (var i = 0; i <= n - y; i++) {

        // j < i used to keep track
        // whether jth element is inside
        // or outside the window

        while (minarr[j] <= i + y - 1
            || j < i) {
            j++;
        }

        submin.push(arr[j]);
    }

    // Return submin
    return submin;
}

// Function to get minimum difference
function getMinDifference(Arr, N, Y)
{
    // Create submin and submax arrays
    var submin
        = get_subminarr(Arr, N, Y);

    var submax
        = get_submaxarr(Arr, N, Y);

    // Store initial difference
    var minn = submax[0] - submin[0];
    var b = submax.length;

    for (var i = 1; i < b; i++) {

        // Calculate temporary difference
        var dif = submax[i] - submin[i];
        minn = Math.min(minn, dif);
    }

    // Final minimum difference
    document.write( minn + "<br>");
}

// Driver Code
// Given array arr[]
var arr = [1, 2, 3, 3, 2, 2];
var N = arr.length
// Given subarray size
var Y = 4;
// Function Call
getMinDifference(arr, N, Y);

</script>
```

****Output:** 

```
1
```** 

****时间复杂度:***O(N)*
T5】辅助空间: *O(N)***