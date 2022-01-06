# 最大化可以选择的元素的数量，这些元素的和与 K 之间的差值最小

> 原文:[https://www . geeksforgeeks . org/最大化可选择元素的数量-它们的和与 k 之间的差异最小/](https://www.geeksforgeeks.org/maximize-count-of-elements-that-can-be-selected-having-minimum-difference-between-their-sum-and-k/)

给定一个数组 **arr[]** 和一个整数值 **K** ，任务是计算可以选择的数组元素的最大数量，以便:

*   所选数组元素之和小于 **K** 。
*   **K**–(所选元素的总和)大于或等于 **0** 和最小可能值。

**示例:**

> **示例:**
> **输入:** arr[] = {20，90，40，90}，K = 100
> **输出:** 2
> **说明:** {20，40}被选择为它们的总和(= 60)小于 K，K–总和(= 40)大于 0 且最小可能。
> 
> **示例:**
> **输入:** arr[] = {30，30，10，10}，K = 50
> **输出:** 3
> **说明:** {10，10，30}被选择<使得它们的总和(= 50)等于 K 和 K–总和为 0 且最小可能。

**进场:**解决这个问题的主要思路是用一个[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)。按照以下步骤解决此问题:

*   [给定数组排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   现在，从第一个数组元素开始，将当前元素添加到总和中。
*   将计数增加 1。
*   检查总和是否大于 **K** 。
    *   如果发现是真的，不要再选择任何元素。
    *   否则，重复上述过程，直到遍历完数组的最后一个元素。
*   答案是所选元素的总数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count maximum number
// of elements that can be selected
int CountMaximum(int arr[], int n, int k)
{

    // Sort he array
    sort(arr, arr + n);

    int sum = 0, count = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {
        // Add current element
        // to the sum
        sum += arr[i];

        // IF sum exceeds k
        if (sum > k)
            break;

        // Increment count
        count++;
    }

    // Return the count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 30, 30, 10, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 50;

    cout << CountMaximum(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;

public class GFG {
    // Function to count maximum number
    // of elements that can be selected
    static int CountMaximum(int arr[], int n, int k)
    {
        // Sorting the array
        Arrays.sort(arr);

        int sum = 0, count = 0;

        // Traverse the array
        for (int i = 0; i < n; i++) {
            // Add the current
            // element to the sum
            sum += arr[i];

            // If sum exceeds k
            if (sum > k)
                break;

            // Increment count
            count++;
        }

        // Returning the count
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 30, 30, 10, 10 };
        int n = 4;
        int k = 50;

        // Function call
        System.out.println(
            CountMaximum(arr, n, k));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to count maximum number
# of elements that can be selected
def CountMaximum(arr, n, k) :

    # Sort he array
    arr.sort()
    Sum, count = 0, 0

    # Traverse the array
    for i in range(0, n) :

        # Add current element
        # to the sum
        Sum += arr[i]

        # IF sum exceeds k
        if (Sum > k) :
            break

        # Increment count
        count += 1

    # Return the count
    return count

  # Driver code
arr = [ 30, 30, 10, 10 ]
n = len(arr)
k = 50

print(CountMaximum(arr, n, k))

# This code is contributed by divyesh072019
```

## C#

```
// C# implementation of the above approach
using System;
class GFG
{

  // Function to count maximum number
  // of elements that can be selected
  static int CountMaximum(int[] arr, int n, int k)
  {
    // Sorting the array
    Array.Sort(arr);
    int sum = 0, count = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // Add the current
      // element to the sum
      sum += arr[i];

      // If sum exceeds k
      if (sum > k)
        break;

      // Increment count
      count++;
    }

    // Returning the count
    return count;
  }

  // Driver code
  static public void Main()
  {
    int[] arr = new int[] { 30, 30, 10, 10 };
    int n = 4;
    int k = 50;

    // Function call
    Console.WriteLine(CountMaximum(arr, n, k));
  }
}

// This code is contributed by dharanendralv23
```

## java 描述语言

```
<script>

// Javascript program of the above approach

    // Function to count maximum number
    // of elements that can be selected
    function CountMaximum(arr, n, k)
    {
        // Sorting the array
        arr.sort();

        let sum = 0, count = 0;

        // Traverse the array
        for (let i = 0; i < n; i++) {
            // Add the current
            // element to the sum
            sum += arr[i];

            // If sum exceeds k
            if (sum > k)
                break;

            // Increment count
            count++;
        }

        // Returning the count
        return count;
    }

    // Driver Code

        let arr = [ 30, 30, 10, 10 ];
        let n = 4;
        let k = 50;

        // Function call
        document.write(
        CountMaximum(arr, n, k));

</script>
```

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count maximum number
// of elements that can be selected
int CountMaximum(int arr[], int n, int k)
{

    // Sort the array
    sort(arr, arr + n);

    int sum = 0, count = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {
        // Add current element
        // to the sum
        sum += arr[i];

        // IF sum exceeds k
        if (sum > k)
            break;

        // Increment count
        count++;
    }

    // Return the count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 30, 30, 10, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 50;

    cout << CountMaximum(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;

public class GFG {
    // Function to count maximum number
    // of elements that can be selected
    static int CountMaximum(int arr[], int n, int k)
    {
        // Sorting the array
        Arrays.sort(arr);

        int sum = 0, count = 0;

        // Traverse the array
        for (int i = 0; i < n; i++) {
            // Add the current
            // element to the sum
            sum += arr[i];

            // If sum exceeds k
            if (sum > k)
                break;

            // Increment count
            count++;
        }

        // Returning the count
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 30, 30, 10, 10 };
        int n = 4;
        int k = 50;

        // Function call
        System.out.println(
            CountMaximum(arr, n, k));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to count maximum number
# of elements that can be selected
def CountMaximum(arr, n, k) :

    # Sort he array
    arr.sort()
    Sum, count = 0, 0

    # Traverse the array
    for i in range(0, n) :

        # Add current element
        # to the sum
        Sum += arr[i]

        # IF sum exceeds k
        if (Sum > k) :
            break

        # Increment count
        count += 1

    # Return the count
    return count

  # Driver code
arr = [ 30, 30, 10, 10 ]
n = len(arr)
k = 50

print(CountMaximum(arr, n, k))

# This code is contributed by divyesh072019
```

## C#

```
// C# implementation of the above approach
using System;
class GFG
{

  // Function to count maximum number
  // of elements that can be selected
  static int CountMaximum(int[] arr, int n, int k)
  {
    // Sorting the array
    Array.Sort(arr);
    int sum = 0, count = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // Add the current
      // element to the sum
      sum += arr[i];

      // If sum exceeds k
      if (sum > k)
        break;

      // Increment count
      count++;
    }

    // Returning the count
    return count;
  }

  // Driver code
  static public void Main()
  {
    int[] arr = new int[] { 30, 30, 10, 10 };
    int n = 4;
    int k = 50;

    // Function call
    Console.WriteLine(CountMaximum(arr, n, k));
  }
}

// This code is contributed by dharanendralv23
```

## java 描述语言

```
<script>

    // Javascript implementation of
    // the above approach

    // Function to count maximum number
    // of elements that can be selected
    function CountMaximum(arr, n, k)
    {

        // Sort the array
        arr.sort(function(a, b){return a - b});

        let sum = 0, count = 0;

        // Traverse the array
        for (let i = 0; i < n; i++) {
            // Add current element
            // to the sum
            sum += arr[i];

            // IF sum exceeds k
            if (sum > k)
                break;

            // Increment count
            count++;
        }

        // Return the count
        return count;
    }

    let arr = [ 30, 30, 10, 10 ];
    let n = arr.length;
    let k = 50;

    document.write(CountMaximum(arr, n, k));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(1)*