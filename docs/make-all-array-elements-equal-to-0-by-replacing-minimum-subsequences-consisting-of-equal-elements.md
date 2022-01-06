# 通过替换由相等元素组成的最小子序列使所有数组元素等于 0

> 原文:[https://www . geesforgeks . org/make-all-array-elements-通过替换最小子序列-由相等元素组成-等于 0/](https://www.geeksforgeeks.org/make-all-array-elements-equal-to-0-by-replacing-minimum-subsequences-consisting-of-equal-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过用任意整数最小次数替换元素相等的子序列的所有元素，使所有数组元素等于 **0** 。

**示例:**

> **输入:** arr[] = {3，7，3}，N = 3
> **输出:** 2
> **解释:**
> 选择一个子序列{ 7 }并用 0 替换其所有元素会将 arr[]修改为{3，3，3 }。
> 选择数组{ 3，3，3 }并用 0 替换其所有元素将 arr[]修改为{ 0，0，0 }
> 
> **输入:** arr[] = {1，5，1，3，2，3，1}，N = 7
> **输出:** 4

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。想法是[计算数组中不等于 0 的不同元素](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)并打印得到的计数。按照以下步骤解决问题:

*   初始化一个[设置](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)来存储数组中存在的不同元素，它不等于 **0** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 和[将数组元素插入集合](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)。
*   最后，打印器械包的[尺寸。](https://www.geeksforgeeks.org/setsize-c-stl/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count of operations
// required to convert all array elements to zero
// br replacing subsequence of equal elements to 0
void minOpsToTurnArrToZero(int arr[], int N)
{

    // Store distinct elements
    // present in the array
    unordered_set<int> st;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If arr[i] is already present in
        // the Set or arr[i] is equal to 0
        if (st.find(arr[i]) != st.end()
            || arr[i] == 0) {
            continue;
        }

        // Otherwise, increment ans by
        // 1 and insert current element
        else {
            st.insert(arr[i]);
        }
    }

    cout << st.size() << endl;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 3, 7, 3 };

    // Size of the given array
    int N = sizeof(arr) / sizeof(arr[0]);

    minOpsToTurnArrToZero(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find minimum count of operations
    // required to convert all array elements to zero
    // br replacing subsequence of equal elements to 0
    static void minOpsToTurnArrToZero(int[] arr, int N)
    {

        // Store distinct elements
        // present in the array
        Set<Integer> st = new HashSet<Integer>();
        // Traverse the array
        for (int i = 0; i < N; i++) {

            // If arr[i] is already present in
            // the Set or arr[i] is equal to 0
            if (st.contains(arr[i]) || arr[i] == 0) {
                continue;
            }

            // Otherwise, increment ans by
            // 1 and insert current element
            else {
                st.add(arr[i]);
            }
        }

        System.out.println(st.size());
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given array
        int arr[] = { 3, 7, 3 };

        // Size of the given array
        int N = arr.length;

        minOpsToTurnArrToZero(arr, N);
    }
}

// This code is contributed by 18bhupendrayadav18
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum count of
# operations required to convert all
# array elements to zero by replacing
# subsequence of equal elements to 0
def minOpsToTurnArrToZero(arr, N):

    # Store distinct elements
    # present in the array
    st = dict()

    # Traverse the array
    for i in range(N):

        # If arr[i] is already present in
        # the Set or arr[i] is equal to 0
        if (i in st.keys() or arr[i] == 0):
            continue

        # Otherwise, increment ans by
        # 1 and insert current element
        else:
            st[arr[i]] = 1

    print(len(st))

# Driver Code

# Given array
arr = [ 3, 7, 3 ]

# Size of the given array
N = len(arr)

minOpsToTurnArrToZero(arr, N)

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

  // Function to find minimum count of operations
  // required to convert all array elements to zero
  // br replacing subsequence of equal elements to 0
  static void minOpsToTurnArrToZero(int[] arr, int N)
  {

    // Store distinct elements
    // present in the array
    HashSet<int> st = new HashSet<int>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // If arr[i] is already present in
      // the Set or arr[i] is equal to 0
      if (st.Contains(arr[i]) || arr[i] == 0)
      {
        continue;
      }

      // Otherwise, increment ans by
      // 1 and insert current element
      else
      {
        st.Add(arr[i]);
      }
    }
    Console.WriteLine(st.Count);
  }

  // Driver Code
  public static void Main(String []args)
  {

    // Given array
    int []arr = { 3, 7, 3 };

    // Size of the given array
    int N = arr.Length;
    minOpsToTurnArrToZero(arr, N);
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find minimum count of operations
// required to convert all array elements to zero
// br replacing subsequence of equal elements to 0
function minOpsToTurnArrToZero(arr, N)
{

    // Store distinct elements
    // present in the array
    var st = new Set();

    // Traverse the array
    for(var i = 0; i < N; i++)
    {

        // If arr[i] is already present in
        // the Set or arr[i] is equal to 0
        if (st.has(arr[i]) || arr[i] == 0)
        {
            continue;
        }

        // Otherwise, increment ans by
        // 1 and insert current element
        else
        {
            st.add(arr[i]);
        }
    }
    document.write(st.size)
}

// Driver Code

// Given array
var arr = [ 3, 7, 3 ];

// Size of the given array
var N = arr.length;

minOpsToTurnArrToZero(arr, N);

// This code is contributed by noob2000

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)