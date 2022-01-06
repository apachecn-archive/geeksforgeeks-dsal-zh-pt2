# 计算每个子阵列的两个最大元素之间的明显差异

> 原文:[https://www . geeksforgeeks . org/每子数组两个最大元素之间的差异计数/](https://www.geeksforgeeks.org/count-of-distinct-differences-between-two-maximum-elements-of-every-subarray/)

给定一个 **N** 大小的[阵](https://www.geeksforgeeks.org/array-data-structure/)T2【arr】。任务是计算给定阵列中每个大小至少为 2 的子阵列的两个最大元素之间的唯一差异数。

**示例:**

> **输入:** arr[] = {5，1，3}，N = 3
> **输出:** 2
> **说明:**子阵为{ 5，1}、{ 5，1，3}、{1，3 }。
> {5，1 }–第一最大值= 5；秒最大值= 1；差值=(5–1)= 4
> { 5，1，3 }–第一个最大值= 5；秒最大值= 3；差值=(5–3)= 2
> { 1，3 }–第一个最大值= 3；秒最大值= 1；差异=(3–1)= 2
> 唯一的高度差异是{4，2} = 2
> 
> **输入:** arr[] = {5，2，3，8}，N = 4
> **输出:** 4
> **解释:**子阵为:{5，2}，{5，2，3}，{5，2，3，8}，{2，3}，{2，3，8}，{3，8}
> {5，2 }–First max = 5；秒最大值= 2；差值=(5–2)= 3
> { 5，2，3 }–第一个最大值= 5；秒最大值= 3；差值=(5–3)= 2
> { 5，2，3，8 }–第一个最大值= 8；秒最大值= 5；差值=(8–5)= 3
> { 2，3 }–第一个最大值= 3；秒最大值= 2；差值=(3–2)= 1
> { 2，3，8 }–第一个最大值= 8；秒最大值= 3；差值=(8–3)= 5
> { 3，8 }–第一个最大值= 8；秒最大值= 3；差异=(8–3)= 5
> 唯一的高度差异是{3，2，1，5} = 4

**方法:**问题可以在以下观察的基础上解决。每个子阵列只需要第一个和第二个最大值。当子阵列中出现另一个最大元素时，需要更新最大值。 [**栈**](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/) 的概念就是用来实现这个观察的。按照下面的步骤来解决这个问题。

*   存储两个数组中每个数组元素左边的下一个大元素和右边的下一个大元素。
*   找出左边下一个较大元素与该索引处原始元素之间的差异，以及右边下一个较大元素与该索引处原始元素之间的差异，并存储在包含唯一值的集合中。
*   打印器械包的尺寸

下面是上述方法的实现。

## C++

```
// C++ code to implement above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// of unique differences
int countUnique(vector<int>& arr, int n)
{

    // Arrays to store next greater
    // to the left and next greater
    // to the right for every arr[i]
    vector<int> ngl(n, 0);
    vector<int> ngr(n, 0);
    stack<int> st;
    set<int> s;

    // Loop to find next greater element
    // to the left of arr[i]
    ngl[0] = -1;
    st.push(arr[0]);
    for (int i = 1; i < n; i++) {
        while (st.size() > 0 && arr[i] > st.top()) {
            st.pop();
        }
        if (st.size() == 0) {
            ngl[i] = -1;
        }
        else {
            ngl[i] = st.top();
        }
        st.push(arr[i]);
    }
    while (st.size() > 0) {
        st.pop();
    }

    // Loop to find next greater element
    // to the left of arr[i]
    ngr[n - 1] = -1;
    st.push(arr[n - 1]);
    for (int i = n - 2; i >= 0; i--) {
        while (st.size() > 0 && arr[i] >= st.top()) {
            st.pop();
        }
        if (st.size() != 0) {
            ngr[i] = st.top();
        }
        else {
            ngr[i] = -1;
        }
        st.push(arr[i]);
    }

    for (int i = 0; i < n; i++) {
        if (ngl[i] != -1) {
            s.insert(ngl[i] - arr[i]);
        }
        if (ngr[i] != -1) {
            s.insert(ngr[i] - arr[i]);
        }
    }

    return s.size();
}

// Driver code
int main()
{
    int N = 4;
    vector<int> arr = { 5, 2, 3, 8 };
    cout << (countUnique(arr, N));

    return 0;
}

    // This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to count the number
    // of unique differences
    public static int countUnique(int arr[], int n)
    {
        // Arrays to store next greater 
        // to the left and next greater 
        // to the right for every arr[i]
        int[] ngl = new int[n];
        int[] ngr = new int[n];
        Stack<Integer> st = new Stack<>();
        HashSet<Integer> s = new HashSet<>();

        // Loop to find next greater element 
        // to the left of arr[i]
        ngl[0] = -1;
        st.push(arr[0]);
        for (int i = 1; i < n; i++) {
            while (st.size() > 0 && 
                   arr[i] > st.peek()) {
                st.pop();
            }
            if (st.size() == 0) {
                ngl[i] = -1;
            }
            else {
                ngl[i] = st.peek();
            }
            st.push(arr[i]);
        }
        while (st.size() > 0) {
            st.pop();
        }

        // Loop to find next greater element 
        // to the left of arr[i]
        ngr[n - 1] = -1;
        st.push(arr[n - 1]);
        for (int i = n - 2; i >= 0; i--) {
            while (st.size() > 0 && 
                   arr[i] >= st.peek()) {
                st.pop();
            }
            if (st.size() != 0) {
                ngr[i] = st.peek();
            }
            else {
                ngr[i] = -1;
            }
            st.push(arr[i]);
        }

        for (int i = 0; i < n; i++) {
            if (ngl[i] != -1) {
                s.add(ngl[i] - arr[i]);
            }
            if (ngr[i] != -1) {
                s.add(ngr[i] - arr[i]);
            }
        }

        return s.size();
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 4;
        int arr[] = { 5, 2, 3, 8 };
        System.out.println(countUnique(
          arr, N));
    }
}
```

## 蟒蛇 3

```
# Python 3 code to implement above approach

# Function to count the number
# of unique differences
def countUnique(arr, n):

    # Arrays to store next greater
    # to the left and next greater
    # to the right for every arr[i]
    ngl = [0]*(n)
    ngr = [0]*(n)
    st = []
    s = set([])

    # Loop to find next greater element
    # to the left of arr[i]
    ngl[0] = -1
    st.append(arr[0])
    for i in range(1, n):
        while (len(st) > 0 and arr[i] > st[-1]):
            st.pop()

        if (len(st) == 0):
            ngl[i] = -1

        else:
            ngl[i] = st[-1]

        st.append(arr[i])

    while (len(st) > 0):
        st.pop()

    # Loop to find next greater element
    # to the left of arr[i]
    ngr[n - 1] = -1
    st.append(arr[n - 1])
    for i in range(n - 2, -1, -1):
        while (len(st) > 0 and arr[i] >= st[-1]):
            st.pop()

        if (len(st) != 0):
            ngr[i] = st[-1]

        else:
            ngr[i] = -1

        st.append(arr[i])

    for i in range(n):
        if (ngl[i] != -1):
            s.add(ngl[i] - arr[i])

        if (ngr[i] != -1):
            s.add(ngr[i] - arr[i])

    return len(s)

# Driver code
if __name__ == "__main__":

    N = 4
    arr = [5, 2, 3, 8]
    print(countUnique(arr, N))

    # This code is contributed by ukasp.
```

## C#

```
// C# code to implement above approach
using System;
using System.Collections.Generic;

class GFG {

  // Function to count the number
  // of unique differences
  public static int countUnique(int[] arr, int n)
  {
    // Arrays to store next greater 
    // to the left and next greater 
    // to the right for every arr[i]
    int[] ngl = new int[n];
    int[] ngr = new int[n];
    Stack<int> st = new Stack<int>();
    HashSet<int> s = new HashSet<int>();

    // Loop to find next greater element 
    // to the left of arr[i]
    ngl[0] = -1;
    st.Push(arr[0]);
    for (int i = 1; i < n; i++) {
      while (st.Count > 0 && 
             arr[i] > st.Peek()) {
        st.Pop();
      }
      if (st.Count == 0) {
        ngl[i] = -1;
      }
      else {
        ngl[i] = st.Peek();
      }
      st.Push(arr[i]);
    }
    while (st.Count > 0) {
      st.Pop();
    }

    // Loop to find next greater element 
    // to the left of arr[i]
    ngr[n - 1] = -1;
    st.Push(arr[n - 1]);
    for (int i = n - 2; i >= 0; i--) {
      while (st.Count > 0 && 
             arr[i] >= st.Peek()) {
        st.Pop();
      }
      if (st.Count != 0) {
        ngr[i] = st.Peek();
      }
      else {
        ngr[i] = -1;
      }
      st.Push(arr[i]);
    }

    for (int i = 0; i < n; i++) {
      if (ngl[i] != -1) {
        s.Add(ngl[i] - arr[i]);
      }
      if (ngr[i] != -1) {
        s.Add(ngr[i] - arr[i]);
      }
    }

    return s.Count;
  }

  // Driver code
  public static void Main()
  {
    int N = 4;
    int[] arr = { 5, 2, 3, 8 };
    Console.Write(countUnique(arr, N));
  }
}

// This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>
    // JavaScript code for the above approach

    // Function to count the number
    // of unique differences
    function countUnique(arr, n) {

      // Arrays to store next greater
      // to the left and next greater
      // to the right for every arr[i]
      let ngl = new Array(n).fill(0);
      let ngr = new Array(n).fill(0);
      let st = [];
      let s = new Set();

      // Loop to find next greater element
      // to the left of arr[i]
      ngl[0] = -1;
      st.push(arr[0]);
      for (let i = 1; i < n; i++) {
        while (st.length > 0 && arr[i] > st[st.length - 1]) {
          st.pop();
        }
        if (st.length == 0) {
          ngl[i] = -1;
        }
        else {
          ngl[i] = st[st.length - 1];
        }
        st.push(arr[i]);
      }
      while (st.length > 0) {
        st.pop();
      }

      // Loop to find next greater element
      // to the left of arr[i]
      ngr[n - 1] = -1;
      st.push(arr[n - 1]);
      for (let i = n - 2; i >= 0; i--) {
        while (st.length > 0 && arr[i] >= st[st.length - 1]) {
          st.pop();
        }
        if (st.length != 0) {
          ngr[i] = st[st.length - 1];
        }
        else {
          ngr[i] = -1;
        }
        st.push(arr[i]);
      }

      for (let i = 0; i < n; i++) {
        if (ngl[i] != -1) {
          s.add(ngl[i] - arr[i]);
        }
        if (ngr[i] != -1) {
          s.add(ngr[i] - arr[i]);
        }
      }

      return s.size;
    }

    // Driver code
    let N = 4;
    let arr = [5, 2, 3, 8];
    document.write(countUnique(arr, N));

  // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
4
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)