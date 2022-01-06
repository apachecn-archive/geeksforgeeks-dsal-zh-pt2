# 查找与所有其他数组元素奇偶性不同的元素的索引

> 原文:[https://www . geeksforgeeks . org/find-元素索引-与所有其他数组元素奇偶性不同/](https://www.geeksforgeeks.org/find-index-of-the-element-differing-in-parity-with-all-other-array-elements/)

给定一个大小为***(N>3)*的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到与所有其他数组元素奇偶性(奇数/偶数)不同的元素的位置。
***注:**保证总有一个数在奇偶性上不同于所有其他元素。***

****示例:****

> ****输入:** arr[] = {2，4，7，8，10}
> **输出:** 2
> **解释:**数组中唯一的奇数元素是 7 (= arr[2])。因此，所需输出为 2。**
> 
> ****输入:** arr[] = {2，1，1 }
> T3】输出: 0**

****天真方法:**解决这个问题最简单的方法是将所有偶数和奇数及其索引存储在一个[多地图](https://www.geeksforgeeks.org/multimap-associative-containers-the-c-standard-template-library-stl/)中，并打印大小为 **1** 的**地图**中存在的元素的索引。按照以下步骤解决问题:**

1.  **初始化两个**多重映射**，用于偶数和奇数。**
2.  **[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将数组元素及其索引存储在各自的**多映射**中。**
3.  **现在找到[大小](https://www.geeksforgeeks.org/multimap-size-function-in-c-stl/)等于 **1** 的**多地图**。打印存储在**多映射**中的数组元素的索引。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the array
// element which differs in parity
// with the remaining array elements
int OddOneOut(int arr[], int N)
{

    // Multimaps to store even
    // and odd numbers along
    // with their indices
    multimap<int, int> e, o;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If array element is even
        if (arr[i] % 2 == 0) {
            e.insert({ arr[i], i });
        }

        // Otherwise
        else {
            o.insert({ arr[i], i });
        }
    }

    // If only one even element
    // is present in the array
    if (e.size() == 1) {
        cout << e.begin()->second;
    }

    // If only one odd element
    // is present in the array
    else {
        cout << o.begin()->second;
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 4, 7, 8, 10 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    OddOneOut(arr, N);

    return 0;
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to print the array
# element which differs in parity
# with the remaining array elements
def OddOneOut(arr, N) :

    # Multimaps to store even
    # and odd numbers along
    # with their indices
    e, o = {}, {}

    # Traverse the array
    for i in range(N) :

        # If array element is even
        if (arr[i] % 2 == 0) :
            e[arr[i]] = i

        # Otherwise
        else :
            o[arr[i]] = i

    # If only one even element
    # is present in the array
    if (len(e) == 1) :
        print(list(e.values())[0] )

    # If only one odd element
    # is present in the array
    else :
        print(list(o.values())[0] )

# Given array
arr = [ 2, 4, 7, 8, 10 ]

# Size of the array
N = len(arr)

OddOneOut(arr, N)

# This code is contributed by divyesh072019.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;
class GFG {

  // Function to print the array
  // element which differs in parity
  // with the remaining array elements
  static void OddOneOut(int[] arr, int N)
  {

    // Multimaps to store even
    // and odd numbers along
    // with their indices
    Dictionary<int, int> e = new Dictionary<int, int>();
    Dictionary<int, int> o = new Dictionary<int, int>();

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // If array element is even
      if (arr[i] % 2 == 0) {
        e[arr[i]] = i;
      }

      // Otherwise
      else {
        o[arr[i]] = i;
      }
    }

    // If only one even element
    // is present in the array
    if (e.Count == 1) {
      Console.Write(e.First().Value);
    }

    // If only one odd element
    // is present in the array
    else {
      Console.Write(o.First().Value);
    }
  }

  // Driver Code
  public static void Main(string[] args)
  {

    // Given array
    int[] arr = { 2, 4, 7, 8, 10 };

    // Size of the array
    int N = arr.Length;

    OddOneOut(arr, N);
  }
}

// This code is contributed by chitranayal.
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to print the array
// element which differs in parity
// with the remaining array elements
function OddOneOut(arr,N)
{
    // Multimaps to store even
    // and odd numbers along
    // with their indices
    let e = new Map();
    let o = new Map();

    // Traverse the array
    for (let i = 0; i < N; i++) {

      // If array element is even
      if (arr[i] % 2 == 0) {
        e.set(arr[i] , i);
      }

      // Otherwise
      else {
        o.set(arr[i] , i);
      }
    }

    // If only one even element
    // is present in the array
    if (e.size == 1) {
        document.write(Array.from(e.values())[0])    ;

    }

    // If only one odd element
    // is present in the array
    else {
    document.write(Array.from(o.values())[0])    ;

    }
}

// Driver Code
// Given array
let arr=[2, 4, 7, 8, 10];
// Size of the array
let N = arr.length;
OddOneOut(arr, N);

// This code is contributed by avanitrachhadiya2155
</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:** O(N*logN)*
***辅助空间:** O(N)***

****高效方法:**对上述方法进行优化，思路是在两个变量中保留偶数和奇数数组元素的计数，并检查哪个计数等于 **1** 。按照以下步骤解决问题:**

1.  **保持四个变量**偶数，奇数**，以保持数组中**偶数**和**奇数**数组元素的计数，以及**最后一个奇数，最后一个偶数**以存储最后一个**奇数**和**偶数**数组元素的索引。**
2.  **[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)后，如果发现**奇数**为 **1** ，则打印**最后一个奇数**。**
3.  **否则，打印**最后一个**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the element
// which differs in parity
int oddOneOut(int arr[], int N)
{
    // Stores the count of odd and
    // even array elements encountered
    int odd = 0, even = 0;

    // Stores the indices of the last
    // odd and even array elements encountered
    int lastOdd = 0, lastEven = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If array element is even
        if (arr[i] % 2 == 0) {
            even++;
            lastEven = i;
        }

        // Otherwise
        else {
            odd++;
            lastOdd = i;
        }
    }

    // If only one odd element
    // is present in the array
    if (odd == 1) {
        cout << lastOdd << endl;
    }

    // If only one even element
    // is present in the array
    else {
        cout << lastEven << endl;
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 4, 7, 8, 10 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    oddOneOut(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to print the element
// which differs in parity
static void oddOneOut(int arr[], int N)
{

    // Stores the count of odd and
    // even array elements encountered
    int odd = 0, even = 0;

    // Stores the indices of the last
    // odd and even array elements encountered
    int lastOdd = 0, lastEven = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If array element is even
        if (arr[i] % 2 == 0) {
            even++;
            lastEven = i;
        }

        // Otherwise
        else {
            odd++;
            lastOdd = i;
        }
    }

    // If only one odd element
    // is present in the array
    if (odd == 1) {
        System.out.println(lastOdd);
    }

    // If only one even element
    // is present in the array
    else {
       System.out.println(lastEven);
    }
}

// Driver Code
public static void main(String args[])
{

    // Given array
    int arr[] = { 2, 4, 7, 8, 10 };

    // Size of the array
    int N = arr.length;
    oddOneOut(arr, N);
}
}

// This code is contributed by jana_sayantan.
```

## **蟒蛇 3**

```
# Python program for the above approach

# Function to print the element
# which differs in parity
def oddOneOut(arr, N) :

    # Stores the count of odd and
    # even array elements encountered
    odd = 0
    even = 0

    # Stores the indices of the last
    # odd and even array elements encountered
    lastOdd = 0
    lastEven = 0

    # Traverse the array
    for i in range(N):

        # If array element is even
        if (arr[i] % 2 == 0) :
            even += 1
            lastEven = i

        # Otherwise
        else :
            odd += 1
            lastOdd = i

    # If only one odd element
    # is present in the array
    if (odd == 1) :
        print(lastOdd)

    # If only one even element
    # is present in the array
    else :
        print(lastEven)

# Driver Code

# Given array
arr = [ 2, 4, 7, 8, 10 ]

# Size of the array
N = len(arr)

oddOneOut(arr, N)

# This code is contributed by susmitakundugoaldanga.
```

## **C#**

```
// C# program for the above approach
using System;
class GFG
{

    // Function to print the element
    // which differs in parity
    static void oddOneOut(int[] arr, int N)
    {

        // Stores the count of odd and
        // even array elements encountered
        int odd = 0, even = 0;

        // Stores the indices of the last
        // odd and even array elements encountered
        int lastOdd = 0, lastEven = 0;

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // If array element is even
            if (arr[i] % 2 == 0)
            {
                even++;
                lastEven = i;
            }

            // Otherwise
            else
            {
                odd++;
                lastOdd = i;
            }
        }

        // If only one odd element
        // is present in the array
        if (odd == 1)
        {
            Console.WriteLine(lastOdd);
        }

        // If only one even element
        // is present in the array
        else
        {
            Console.WriteLine(lastEven);
        }
    }

  // Driver code
  static void Main()
  {

    // Given array
    int[] arr = { 2, 4, 7, 8, 10 };

    // Size of the array
    int N = arr.Length;
    oddOneOut(arr, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to print the element
// which differs in parity
function oddOneOut(arr, N)
{

    // Stores the count of odd and
    // even array elements encountered
    let odd = 0, even = 0;

    // Stores the indices of the last
    // odd and even array elements encountered
    let lastOdd = 0, lastEven = 0;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // If array element is even
        if (arr[i] % 2 == 0)
        {
            even++;
            lastEven = i;
        }

        // Otherwise
        else
        {
            odd++;
            lastOdd = i;
        }
    }

    // If only one odd element
    // is present in the array
    if (odd == 1)
    {
        document.write(lastOdd);
    }

    // If only one even element
    // is present in the array
    else
    {
        document.write(lastEven);
    }
}

// Driver code

// Given array
let arr = [ 2, 4, 7, 8, 10 ];

// Size of the array
let N = arr.length;

oddOneOut(arr, N);

// This code is contributed by suresh07 

</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**