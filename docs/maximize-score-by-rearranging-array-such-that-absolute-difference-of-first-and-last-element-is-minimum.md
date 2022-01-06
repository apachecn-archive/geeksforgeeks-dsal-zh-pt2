# 通过重新排列数组，使第一个和最后一个元素的绝对差值最小，从而最大化得分

> 原文:[https://www . geeksforgeeks . org/通过重新排列数组来最大化分数，这样第一个和最后一个元素的绝对差值就是最小值/](https://www.geeksforgeeks.org/maximize-score-by-rearranging-array-such-that-absolute-difference-of-first-and-last-element-is-minimum/)

给定一个大小为 **N** 的数组**arr【】**，任务是重新排列数组以达到**最大**可能得分，尽可能将**第一个**和**最后一个**元素的**绝对差**保持为**最小**。分数分布如下:

*   如果 **arr[i] < arr[i+1]** ，则按 **1** 增加分数。
*   否则保持分数**不变**。

**示例:**

> **输入:** N = 5，arr[] = {5，7，9，5，8}
> **输出:** {5，7，8，9，5}
> **解释:**重新排列数组后，第一个和最后一个元素的绝对差= ABS(5–5)= 0，这是最小可能。
> 可以达到的最高分:
> 
> *   arr[0] < arr[1]，得分= 1
> *   arr[1] < arr[2]，得分= 2
> *   arr[2] > arr[3]，得分= 3
> *   arr[3] > arr[4]，得分= 3
> 
> **输入:** N = 4，arr[] = {6，4，1，3}
> **输出:** {3，6，1，4}

**方法:**给定的问题可以通过[贪婪的](https://www.geeksforgeeks.org/greedy-algorithms/)方法解决。按照以下步骤解决问题:

1.  [对数组](https://www.geeksforgeeks.org/sorting-algorithms/)进行排序，找出每对**相邻**元素之间**最小**的绝对差，并存储其索引，如 **ind** 。
2.  现在，在索引处只使用这两个元素之外的元素(**ind–1**和 **ind** )。这两个元素将是所需数组的第一个**元素和最后一个**元素。****
3.  通过以下两种方式存储剩余元素来解决问题:
    *   首先在 res 数组中存储大于索引**(ind–1)**处元素的**。**
    *   **然后，将**小于**或等于索引 **(ind)处的元素存储在 res 数组中。****
4.  **最后，推送最后一个元素，即索引处的元素(ind)，并返回 res 向量。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the array to
// achieve the maximum score
vector<int> rearrangeArray(vector<int> arr)
{
    int min_diff = INT_MAX;
    int ind = -1;
    int n = arr.size();

    // Sort the array
    sort(arr.begin(), arr.end());

    // Iterate the array and find the
    // minimum difference between two
    // elements along with its index
    for (int i = 1; i < n; i++) {
        if (abs(arr[i] - arr[i - 1]) < min_diff) {
            min_diff = abs(arr[i] - arr[i - 1]);
            ind = i;
        }
    }

    // Vector to store the rearranged
    // elements
    vector<int> res;

    // Push the element at (ind - 1)
    res.push_back(arr[ind - 1]);

    // Traverse the array and push the
    // elements in res which are greater
    // than the element at index (ind - 1)
    for (int i = 0; i < n; i++) {
        if (i == ind || i == ind - 1) {
            continue;
        }
        if (arr[i] > arr[ind - 1]) {
            res.push_back(arr[i]);
        }
    }

    // Again traverse the array and push the
    // elements in res which are less or equal
    // to the element at index (ind)
    for (int i = 0; i < n; i++) {
        if (i == ind || i == ind - 1) {
            continue;
        }
        if (arr[i] <= arr[ind]) {
            res.push_back(arr[i]);
        }
    }

    // At the end, push the element at (ind)
    res.push_back(arr[ind]);

    // Return res vector
    return res;
}

// Driver Code
int main()
{
    vector<int> arr = { 5, 7, 9, 5, 8 };

    vector<int> res = rearrangeArray(arr);
    for (auto it : res)
        cout << it << " ";

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the above approach
import java.util.*;

public class GFG
{

// Function to rearrange the array to
// achieve the maximum score
static ArrayList<Integer> rearrangeArray(ArrayList<Integer> arr)
{
    int min_diff = Integer.MAX_VALUE;
    int ind = -1;
    int n = arr.size();

    // Sort the array
    Collections.sort(arr);

    // Iterate the array and find the
    // minimum difference between two
    // elements along with its index
    for (int i = 1; i < n; i++) {
        if (Math.abs(arr.get(i) - arr.get(i - 1)) < min_diff) {
            min_diff = Math.abs(arr.get(i) - arr.get(i - 1));
            ind = i;
        }
    }

    // Vector to store the rearranged
    // elements
    ArrayList<Integer> res = new ArrayList<Integer>();

    // Push the element at (ind - 1)
    res.add(arr.get(ind - 1));

    // Traverse the array and push the
    // elements in res which are greater
    // than the element at index (ind - 1)
    for (int i = 0; i < n; i++) {
        if (i == ind || i == ind - 1) {
            continue;
        }
        if (arr.get(i) > arr.get(ind - 1)) {
            res.add(arr.get(i));
        }
    }

    // Again traverse the array and push the
    // elements in res which are less or equal
    // to the element at index (ind)
    for (int i = 0; i < n; i++) {
        if (i == ind || i == ind - 1) {
            continue;
        }
        if (arr.get(i) <= arr.get(ind)) {
            res.add(arr.get(i));
        }
    }

    // At the end, push the element at (ind)
    res.add(arr.get(ind));

    // Return res
    return res;
}

// Driver Code
public static void main(String args[])
{
    ArrayList<Integer> arr
            = new ArrayList<Integer>();

    arr.add(5);
    arr.add(7);
    arr.add(9);
    arr.add(5);
    arr.add(8);

    ArrayList<Integer> res = rearrangeArray(arr);
    for (int i = 0; i < res.size(); i++) {
        System.out.print(res.get(i) + " ");
    }

}
}

// This code is contributed by Samim Hossain Mondal.
```

## **蟒蛇 3**

```
# Python code for the above approach

# Function to rearrange the array to
# achieve the maximum score
def rearrangeArray(arr):

     min_diff = 9999999
     ind = -1
     n = len(arr)

    # Sort the array
     arr.sort()

    # Iterate the array and find the
    # minimum difference between two
    # elements along with its index
     for i in range(n):
        if abs(arr[i] - arr[i - 1]) < min_diff:
            min_diff = abs(arr[i] - arr[i - 1])
            ind = i

    # Vector to store the rearranged
    # elements
     res = []

    # Push the element at (ind - 1)
     res.append(arr[ind - 1])

    # Traverse the array and push the
    # elements in res which are greater
    # than the element at index (ind - 1)
     for i in range(n):
        if i == ind or i == ind - 1:
            continue

        if arr[i] > arr[ind - 1]:
            res.append(arr[i])

    # Again traverse the array and push the
    # elements in res which are less or equal
    # to the element at index (ind)
     for i in range(n):
        if i == ind or i == ind - 1 :
            continue;

        if arr[i] <= arr[ind] :
            res.append(arr[i])

    # At the end, push the element at (ind)
     res.append(arr[ind])

    # Return res vector
     return res

# Driver Code
arr = [ 5, 7, 9, 5, 8 ]
res = rearrangeArray(arr)
for i in range(len(res)):
    print(str(res[i]),end =" ")

# This code is contributed by Potta Lokesh
```

## **C#**

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to rearrange the array to
// achieve the maximum score
static List<int> rearrangeArray(List<int> arr)
{
    int min_diff = Int32.MaxValue;
    int ind = -1;
    int n = arr.Count;

    // Sort the array
    arr.Sort();

    // Iterate the array and find the
    // minimum difference between two
    // elements along with its index
    for (int i = 1; i < n; i++) {
        if (Math.Abs(arr[i] - arr[i - 1]) < min_diff) {
            min_diff = Math.Abs(arr[i] - arr[i - 1]);
            ind = i;
        }
    }

    // Vector to store the rearranged
    // elements
    List<int> res = new List<int>();

    // Push the element at (ind - 1)
    res.Add(arr[ind - 1]);

    // Traverse the array and push the
    // elements in res which are greater
    // than the element at index (ind - 1)
    for (int i = 0; i < n; i++) {
        if (i == ind || i == ind - 1) {
            continue;
        }
        if (arr[i] > arr[ind - 1]) {
            res.Add(arr[i]);
        }
    }

    // Again traverse the array and push the
    // elements in res which are less or equal
    // to the element at index (ind)
    for (int i = 0; i < n; i++) {
        if (i == ind || i == ind - 1) {
            continue;
        }
        if (arr[i] <= arr[ind]) {
            res.Add(arr[i]);
        }
    }

    // At the end, push the element at (ind)
    res.Add(arr[ind]);

    // Return res
    return res;
}

// Driver Code
public static void Main()
{
    List<int> arr
            = new List<int>();

    arr.Add(5);
    arr.Add(7);
    arr.Add(9);
    arr.Add(5);
    arr.Add(8);

    List<int> res = rearrangeArray(arr);
    foreach(int k in res)
        Console.Write(k + " ");
}
}
// This code is contributed by Samim Hossain Mondal.
```

## **java 描述语言**

```
<script>
// Javascript implementation of the above approach

// Function to rearrange the array to
// achieve the maximum score
function rearrangeArray(arr)
{
    let min_diff = Number.MAX_SAFE_INTEGER;
    let ind = -1;
    let n = arr.length;

    // Sort the array
    arr.sort();

    // Iterate the array and find the
    // minimum difference between two
    // elements along with its index
    for (let i = 1; i < n; i++) {
        if (Math.abs(arr[i] - arr[i - 1]) < min_diff) {
            min_diff = Math.abs(arr[i] - arr[i - 1]);
            ind = i;
        }
    }

    // Vector to store the rearranged
    // elements
    let res = [];

    // Push the element at (ind - 1)
    res.push(arr[ind - 1]);

    // Traverse the array and push the
    // elements in res which are greater
    // than the element at index (ind - 1)
    for (let i = 0; i < n; i++) {
        if (i == ind || i == ind - 1) {
            continue;
        }
        if (arr[i] > arr[ind - 1]) {
            res.push(arr[i]);
        }
    }

    // Again traverse the array and push the
    // elements in res which are less or equal
    // to the element at index (ind)
    for (let i = 0; i < n; i++) {
        if (i == ind || i == ind - 1) {
            continue;
        }
        if (arr[i] <= arr[ind]) {
            res.push(arr[i]);
        }
    }

    // At the end, push the element at (ind)
    res.push(arr[ind]);

    // Return res vector
    return res;
}

// Driver Code
let arr = [ 5, 7, 9, 5, 8 ];

let res = rearrangeArray(arr);
for (let i = 0; i < res.length; i++)
    document.write(res[i] + " ");

// This code is contributed by Samim Hossain Mundal.
</script>
```

****Output**

```
5 7 8 9 5 
```** 

*****时间复杂度:**T3】O(n logn)
T5】T6】辅助空间:T8】O(n)***