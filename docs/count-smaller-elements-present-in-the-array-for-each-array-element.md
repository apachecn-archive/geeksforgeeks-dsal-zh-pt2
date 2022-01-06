# 计算每个数组元素在数组中出现的较小元素

> 原文:[https://www . geeksforgeeks . org/count-较小元素-每个数组元素在数组中存在/](https://www.geeksforgeeks.org/count-smaller-elements-present-in-the-array-for-each-array-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，对于每个数组元素，比如**arr【I】**，任务是找出小于**arr【I】**的数组元素的数量。

**示例:**

> **输入:** arr[] = {3，4，1，1，2}
> **输出:** 3 4 0 0 2
> **解释:**
> 小于 arr[0](= 3)的元素为{1，1，2}。因此，计数为 3。
> 小于 arr[1](= 4)的元素是{1，1，2，3}。因此，计数为 4。
> 元素 arr[2](= 1)和 arr[3](= 1)是最小的可能。因此，计数为 0。
> 小于 arr[4](= 2)的元素为{1，1}。因此，计数为 2。
> 
> **输入:** arr[] = {1，2，3，4}
> **输出:** 0 1 2 3

**天真法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，计算比它们小的数组元素的[个数](https://www.geeksforgeeks.org/count-smaller-equal-elements-sorted-array/)并打印得到的个数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count for each array
// element, the number of elements
// that are smaller than that element
void smallerNumbers(int arr[], int N)
{
    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Stores the count
        int count = 0;

        // Traverse the array
        for (int j = 0; j < N; j++) {

            // Increment count
            if (arr[j] < arr[i]) {
                count++;
            }
        }

        // Print the count of smaller
        // elements for the current element
        cout << count << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 4, 1, 1, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    smallerNumbers(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count for each array
// element, the number of elements
// that are smaller than that element
static void smallerNumbers(int arr[], int N)
{

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Stores the count
        int count = 0;

        // Traverse the array
        for(int j = 0; j < N; j++)
        {

            // Increment count
            if (arr[j] < arr[i])
            {
                count++;
            }
        }

        // Print the count of smaller
        // elements for the current element
        System.out.print(count + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 4, 1, 1, 2 };
    int N = arr.length;

    smallerNumbers(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count for each array
# element, the number of elements
# that are smaller than that element
def smallerNumbers(arr, N):

    # Traverse the array
    for i in range(N):

        # Stores the count
        count = 0

        # Traverse the array
        for j in range(N):

            # Increment count
            if (arr[j] < arr[i]):
                count += 1

        # Print the count of smaller
        # elements for the current element
        print(count, end=" ")

# Driver Code
if __name__ == "__main__":

    arr = [3, 4, 1, 1, 2]
    N = len(arr)

    smallerNumbers(arr, N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to count for each array
  // element, the number of elements
  // that are smaller than that element
  static void smallerNumbers(int[] arr, int N)
  {

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

      // Stores the count
      int count = 0;

      // Traverse the array
      for(int j = 0; j < N; j++)
      {

        // Increment count
        if (arr[j] < arr[i])
        {
          count++;
        }
      }

      // Print the count of smaller
      // elements for the current element
      Console.Write(count + " ");
    }
  }

  // Driver Code
  static public void Main()
  {
    int[] arr = { 3, 4, 1, 1, 2 };
    int N = arr.Length;

    smallerNumbers(arr, N);
  }
}

// This code is contributed by sanjoy_62,
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count for each array
// element, the number of elements
// that are smaller than that element
function smallerNumbers(arr, N)
{
    var i;
    // Traverse the array
    for(i = 0; i < N; i++) {

        // Stores the count
        var count = 0;

        // Traverse the array
        for (j = 0; j < N; j++) {

            // Increment count
            if (arr[j] < arr[i]) {
                count += 1;
            }
        }

        // Print the count of smaller
        // elements for the current element
        document.write(count + " ");
    }
}

// Driver Code
    var arr = [3, 4, 1, 1, 2]
    var N = arr.length;

    smallerNumbers(arr, N);

</script>
```

**Output:** 

```
3 4 0 0 2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)进行优化。按照以下步骤解决问题:

*   初始化一个大小为**10<sup>5</sup>T5】的辅助数组 **hash[]** ，用 **0** 初始化所有数组元素，存储每个数组元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)**
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，将数组 **hash[]** 中的 **arr[i]** 的频率增加 **1** 作为**hash[arr[I]]+**。
*   找到数组 **哈希[]** 的[前缀和。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)
*   再次，[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素 **arr[]** ，打印**散列【arr[I]–1】**的值作为较小元素的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count for each array
// element, the number of elements
// that are smaller than that element
void smallerNumbers(int arr[], int N)
{
    // Stores the frequencies
    // of array elements
    int hash[100000] = { 0 };

    // Traverse the array
    for (int i = 0; i < N; i++)

        // Update frequency of arr[i]
        hash[arr[i]]++;

    // Initialize sum with 0
    int sum = 0;

    // Compute prefix sum of the array hash[]
    for (int i = 1; i < 100000; i++) {
        hash[i] += hash[i - 1];
    }

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If current element is 0
        if (arr[i] == 0) {
            cout << "0";
            continue;
        }

        // Print the resultant count
        cout << hash[arr[i] - 1]
             << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 4, 1, 1, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    smallerNumbers(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count for each array
// element, the number of elements
// that are smaller than that element
static void smallerNumbers(int arr[], int N)
{

    // Stores the frequencies
    // of array elements
    int hash[] = new int[100000];

    // Traverse the array
    for(int i = 0; i < N; i++)

        // Update frequency of arr[i]
        hash[arr[i]]++;

    // Initialize sum with 0
    int sum = 0;

    // Compute prefix sum of the array hash[]
    for(int i = 1; i < 100000; i++)
    {
        hash[i] += hash[i - 1];
    }

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If current element is 0
        if (arr[i] == 0)
        {
            System.out.println("0");
            continue;
        }

        // Print the resultant count
        System.out.print(hash[arr[i] - 1] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 4, 1, 1, 2 };
    int N = arr.length;

    smallerNumbers(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count for each array
# element, the number of elements
# that are smaller than that element
def smallerNumbers(arr, N):

    # Stores the frequencies
    # of array elements
    hash = [0] * 100000

    # Traverse the array
    for i in range(N):

        # Update frequency of arr[i]
        hash[arr[i]] += 1

    # Initialize sum with 0
    sum = 0

    # Compute prefix sum of the array hash[]
    for i in range(1, 100000):
        hash[i] += hash[i - 1]

    # Traverse the array arr[]
    for i in range(N):

        # If current element is 0
        if (arr[i] == 0):
            print("0")
            continue

        # Print the resultant count
        print(hash[arr[i] - 1], end = " ")

# Driver Code
if __name__ == "__main__":

    arr = [ 3, 4, 1, 1, 2 ]
    N = len(arr)

    smallerNumbers(arr, N)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count for each array
// element, the number of elements
// that are smaller than that element
static void smallerNumbers(int []arr, int N)
{

    // Stores the frequencies
    // of array elements
    int []hash = new int[100000];

    // Traverse the array
    for(int i = 0; i < N; i++)

        // Update frequency of arr[i]
        hash[arr[i]]++;

    // Initialize sum with 0
    //int sum = 0;

    // Compute prefix sum of the array hash[]
    for(int i = 1; i < 100000; i++)
    {
        hash[i] += hash[i - 1];
    }

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If current element is 0
        if (arr[i] == 0)
        {
            Console.WriteLine("0");
            continue;
        }

        // Print the resultant count
        Console.Write(hash[arr[i] - 1] + " ");
    }
}

// Driver Code
public static void Main(string[] args)
{
    int []arr = { 3, 4, 1, 1, 2 };
    int N = arr.Length;

    smallerNumbers(arr, N);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to count for each array
    // element, the number of elements
    // that are smaller than that element
    function smallerNumbers(arr, N)
    {

        // Stores the frequencies
        // of array elements
        let hash = new Array(100000);
        hash.fill(0);

        // Traverse the array
        for(let i = 0; i < N; i++)

            // Update frequency of arr[i]
            hash[arr[i]]++;

        // Initialize sum with 0
        let sum = 0;

        // Compute prefix sum of the array hash[]
        for(let i = 1; i < 100000; i++)
        {
            hash[i] += hash[i - 1];
        }

        // Traverse the array arr[]
        for(let i = 0; i < N; i++)
        {

            // If current element is 0
            if (arr[i] == 0)
            {
                document.write("0" + "</br>");
                continue;
            }

            // Print the resultant count
            document.write(hash[arr[i] - 1] + " ");
        }
    }

    let arr = [ 3, 4, 1, 1, 2 ];
    let N = arr.length;

    smallerNumbers(arr, N);

</script>
```

**Output:** 

```
3 4 0 0 2
```

***时间复杂度:** O(N)*
***辅助空间:** O(10 <sup>5</sup> )*