# 通过给定的操作最小化数组的偏差

> 原文:[https://www . geeksforgeeks . org/按给定操作最小化数组偏差/](https://www.geeksforgeeks.org/minimize-deviation-of-an-array-by-given-operations/)

给定一个由正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** ，任务是在执行以下任意次数的操作后，计算给定数组 **A[]** 的最小可能[偏差:](https://www.geeksforgeeks.org/program-for-variance-and-standard-deviation-of-an-array/)

*   **操作 1:** [如果阵元为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，除以 **2** 。
*   **操作 2:** [如果阵元为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则乘以 **2** 。

数组 **A[]** 的偏差是数组中存在的[最大元素和最小元素 **A[]** 之间的差值。](https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/)

**示例:**

> **输入:** A[] = {4，1，5，20，3}
> **输出:** 3
> **解释:**数组在执行给定操作后修改为{4，2，5，5，3}。因此，偏差= 5–2 = 3。
> 
> **输入** : A[] = {1，2，3，4}
> **输出** : 1
> **说明:**数组经过两次运算修改为{2，2，3，2}。因此，偏差= 3–2 = 1。

**方法:**根据以下观察结果可以解决问题:

*   偶数可以被多次除，直到它转换成奇数。
*   奇数转换为偶数时只能加倍一次。
*   因此，偶数永远不能增加。

按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并加倍所有奇数数组元素。这就取消了第二次<sup>和第三次</sup>操作的要求。
*   现在，偶数时减少[最大数组元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。
*   要以排序方式存储数组元素，[将所有数组元素插入一个集合](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)。
*   贪婪地减少[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中存在的最大元素
*   如果集合中存在的最大元素是奇数，[断开循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   打印获得的最小偏差。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// deviation of the array A[]
void minimumDeviation(int A[], int N)
{
    // Store all array elements
    // in sorted order
    set<int> s;

    for (int i = 0; i < N; i++) {

        if (A[i] % 2 == 0)
            s.insert(A[i]);

        // Odd number are transformed
        // using 2nd operation
        else
            s.insert(2 * A[i]);
    }

    // (Maximum - Minimum)
    int diff = *s.rbegin() - *s.begin();

    // Check if the size of set is > 0 and
    // the maximum element is divisible by 2
    while ((int)s.size()
           && *s.rbegin() % 2 == 0) {

        // Maximum element of the set
        int maxEl = *s.rbegin();

        // Erase the maximum element
        s.erase(maxEl);

        // Using operation 1
        s.insert(maxEl / 2);

        // (Maximum - Minimum)
        diff = min(diff, *s.rbegin() - *s.begin());
    }

    // Print the Minimum
    // Deviation Obtained
    cout << diff;
}

// Driver Code
int main()
{
    int A[] = { 4, 1, 5, 20, 3 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call to find
    // Minimum Deviation of A[]
    minimumDeviation(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

// Function to find the minimum
// deviation of the array A[]
static void minimumDeviation(int A[], int N)
{

    // Store all array elements
    // in sorted order
    TreeSet<Integer> s = new TreeSet<Integer>();
    for (int i = 0; i < N; i++)
    {

        if (A[i] % 2 == 0)
            s.add(A[i]);

        // Odd number are transformed
        // using 2nd operation
        else
            s.add(2 * A[i]);
    }

    // (Maximum - Minimum)
    int diff =  s.last() -  s.first() ;

    // Check if the size of set is > 0 and
    // the maximum element is divisible by 2
    while ((s.last() % 2 == 0))
    {

        // Maximum element of the set
        int maxEl = s.last();

        // Erase the maximum element
        s.remove(maxEl);

        // Using operation 1
        s.add(maxEl / 2);

        // (Maximum - Minimum)
        diff = Math.min(diff, s.last() -  s.first());
    }

    // Print the Minimum
    // Deviation Obtained
    System.out.print(diff);
}

// Driver code
public static void main(String[] args)
{
    int A[] = { 4, 1, 5, 20, 3 };
    int N = A.length;

    // Function Call to find
    // Minimum Deviation of A[]
    minimumDeviation(A, N);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach

# Function to find the minimum
# deviation of the array A[]
def minimumDeviation(A, N):

    # Store all array elements
    # in sorted order
    s = set([])

    for i in range(N):
        if (A[i] % 2 == 0):
            s.add(A[i])

        # Odd number are transformed
        # using 2nd operation
        else:
            s.add(2 * A[i])

    # (Maximum - Minimum)

    s = list(s)
    diff = s[-1] - s[0]

    # Check if the size of set is > 0 and
    # the maximum element is divisible by 2
    while (len(s) and s[-1] % 2 == 0):

        # Maximum element of the set
        maxEl = s[-1]

        # Erase the maximum element
        s.remove(maxEl)

        # Using operation 1
        s.append(maxEl // 2)

        # (Maximum - Minimum)
        diff = min(diff, s[-1] - s[0])

    # Print the Minimum
    # Deviation Obtained
    print(diff)

# Driver Code
if __name__ == "__main__":
    A = [4, 1, 5, 20, 3]
    N = len(A)

    # Function Call to find
    # Minimum Deviation of A[]
    minimumDeviation(A, N)

    # This code is contributed by chitranayal.
```

## C#

```
// C# implementation of the
// above approach
using System;
using System.Collections.Generic;
using System.Linq;
class GFG
{

    // Function to find the minimum
    // deviation of the array A[]
    static void minimumDeviation(int[] A, int N)
    {

        // Store all array elements
        // in sorted order
        HashSet<int> s = new HashSet<int>();
        for (int i = 0; i < N; i++)
        {
            if (A[i] % 2 == 0)
                s.Add(A[i]);

            // Odd number are transformed
            // using 2nd operation
            else
                s.Add(2 * A[i]);
        }
        List<int> S = s.ToList();
        S.Sort();

        // (Maximum - Minimum)
        int diff = S[S.Count - 1] - S[0];

        // Check if the size of set is > 0 and
        // the maximum element is divisible by 2
        while ((int)S.Count != 0 && S[S.Count - 1] % 2 == 0) {

            // Maximum element of the set
            int maxEl = S[S.Count - 1];

            // Erase the maximum element
            S.RemoveAt(S.Count - 1);

            // Using operation 1
            S.Add(maxEl / 2);

            S.Sort();

            // (Maximum - Minimum)
            diff = Math.Min(diff, S[S.Count - 1] - S[0]);
        }

        // Print the Minimum
        // Deviation Obtained
        Console.Write(diff);
    }

  // Driver code
  static void Main()
  {
    int[] A = { 4, 1, 5, 20, 3 };
    int N = A.Length;

    // Function Call to find
    // Minimum Deviation of A[]
    minimumDeviation(A, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

// Function to find the minimum
// deviation of the array A[]
function minimumDeviation(A, N)
{
    // Store all array elements
    // in sorted order
    var s = new Set();

    for (var i = 0; i < N; i++) {

        if (A[i] % 2 == 0)
            s.add(A[i]);

        // Odd number are transformed
        // using 2nd operation
        else
            s.add(2 * A[i]);
    }

    var tmp = [...s].sort((a,b)=>a-b);
    // (Maximum - Minimum)
    var diff = tmp[tmp.length-1] - tmp[0];

    // Check if the size of set is > 0 and
    // the maximum element is divisible by 2
    while (s.size
           && tmp[tmp.length-1] % 2 == 0) {

        // Maximum element of the set
        var maxEl = tmp[tmp.length-1];

        // Erase the maximum element
        s.delete(maxEl);

        // Using operation 1
        s.add(parseInt(maxEl / 2));
        tmp = [...s].sort((a,b)=>a-b);
        // (Maximum - Minimum)
        diff = Math.min(diff, tmp[tmp.length-1] - tmp[0]);
    }

    // Print the Minimum
    // Deviation Obtained
    document.write( diff);
}

// Driver Code

var A = [4, 1, 5, 20, 3];
var N = A.length;

// Function Call to find
// Minimum Deviation of A[]
minimumDeviation(A, N);

</script>
```

**Output:** 

```
3
```

***时间复杂度** : O(N * log(N))*
***辅助空间** : O(N)*