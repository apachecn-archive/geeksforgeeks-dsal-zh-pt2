# 最长交替递增递减子阵列的长度

> 原文:[https://www . geesforgeks . org/最长交替递增递减子阵列长度/](https://www.geeksforgeeks.org/length-of-the-longest-alternating-increasing-decreasing-subarray/)

给定一个[阵列](https://www.geeksforgeeks.org/array-class-c/) **arr[]，**的任务是找到最长的交替子阵列的长度。

> 子阵列{x1，x2，..xn}是一个交替递增递减序列，如果它的元素满足以下关系之一:
> 
> x1< x2 >x3< x4 >X5< …. xn or 
> x1>x2<x3>x4<X5>…。数列

**示例:**

> **输入:** arr = {1，2，3，2，5，6}
> **输出:** 4
> **解释:**构成索引 1 到 4 的第一个元素是交替的子阵列–{ 2，3，2，5}
> 
> **输入:** arr = {5，2，1 }
> T3】输出: 2

**天真方法:**天真方法是检查每个子阵列从每个索引开始的子阵列是否交替。这个想法是使用[两个嵌套的 for 循环。](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples-2/)

下面是上述方法的实现

## C++14

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

int maxAlternatingSubarray(int n, int* arr)
{

    // Initialize mx to store maximum
    // length alternating subarrays
    int i, j, max = 1, count = 1, a, b;

    // Initialize a variable to check is the
    // subarray starts with greater
    // or smaller value
    bool check;

    // If length of the array is 1
    // then return 1
    if (n == 1)
        return 1;

    // Traverse for every element
    for (i = 0; i < n; i++) {

        // Reintialize count to 1 as
        // at least one element is counted
        count = 1;

        // Subarray starting at every element
        for (j = i; j < n - 1; j++) {

            // Initialize a and b for storing
            // adjacent positions
            a = j;
            b = j + 1;

            // Check if the alternating subarray
            // starts with greater
            // or smaller element
            if (j == i) {

                // Smaller element starts first
                if (arr[a] < arr[b])
                    check = 1;

                // Greater element starts first
                else if (arr[a] > arr[b])
                    check = 0;
            }

            // If check is 1 then the next
            // element should be greater
            if (check && arr[a] < arr[b]) {

                // Increment count
                count++;
            }

            // If check is 0 then the next
            // element should be greater
            else if (!check && arr[a] > arr[b]) {

                // Increment count
                count++;
            }
            else
                break;

            // Update the value of check
            check = !check;
        }

        // Update the maximum value of count
        if (max < count)
            max = count;
    }

    // Return the maximum length
    return max;
}

// Driver code
int main()
{

    // Initialize the array
    int arr[] = { 1, 2, 3, 2, 5, 7 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Call thefunction and print the answer
    cout << maxAlternatingSubarray(n, arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG {
  static int maxAlternatingSubarray(int n, int[] arr)
  {

    // Initialize mx to store maximum
    // length alternating subarrays
    int i, j, max = 1, count = 1, a, b;

    // Initialize a variable to check is the
    // subarray starts with greater
    // or smaller value
    boolean check=false;

    // If length of the array is 1
    // then return 1
    if (n == 1)
      return 1;

    // Traverse for every element
    for (i = 0; i < n; i++) {

      // Reintialize count to 1 as
      // at least one element is counted
      count = 1;

      // Subarray starting at every element
      for (j = i; j < n - 1; j++) {

        // Initialize a and b for storing
        // adjacent positions
        a = j;
        b = j + 1;

        // Check if the alternating subarray
        // starts with greater
        // or smaller element
        if (j == i) {

          // Smaller element starts first
          if (arr[a] < arr[b])
            check = true;

          // Greater element starts first
          else if (arr[a] > arr[b])
            check = false;
        }

        // If check is 1 then the next
        // element should be greater
        if (check==true && arr[a] < arr[b]) {

          // Increment count
          count++;
        }

        // If check is 0 then the next
        // element should be greater
        else if (check==false && arr[a] > arr[b]) {

          // Increment count
          count++;
        }
        else
          break;

        // Update the value of check
        check = !check;
      }

      // Update the maximum value of count
      if (max < count)
        max = count;
    }

    // Return the maximum length
    return max;
  }

  // Driver code
  public static void main (String[] args)
  {

    // Initialize the array
    int arr[] = { 1, 2, 3, 2, 5, 7 };

    int n = arr.length;

    // Call thefunction and print the answer

    System.out.println( maxAlternatingSubarray(n, arr));
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python implementation of the above approach
def maxAlternatingSubarray(n, arr):

    # Initialize mx to store maximum
    # length alternating subarrays
    max = 1
    count = 1
    a = 0
    b = 0

    # Initialize a variable to check is the
    # subarray starts with greater
    # or smaller value
    check = 0

    # If length of the array is 1
    # then return 1
    if (n == 1):
        return 1;

    # Traverse for every element
    for i in range(n):

        # Reintialize count to 1 as
        # at least one element is counted
        count = 1;

        # Subarray starting at every element
        for j in range(i, n - 1):

            # Initialize a and b for storing
            # adjacent positions
            a = j;
            b = j + 1;

            # Check if the alternating subarray
            # starts with greater
            # or smaller element
            if (j == i):

                # Smaller element starts first
                if (arr[a] < arr[b]):
                    check = 1;

                # Greater element starts first
                elif (arr[a] > arr[b]):
                    check = 0;

            # If check is 1 then the next
            # element should be greater
            if (check and arr[a] < arr[b]):

                # Increment count
                count += 1

            # If check is 0 then the next
            # element should be greater
            elif (not check and arr[a] > arr[b]):

                # Increment count
                count += 1

            else:
                break;

            # Update the value of check
            check = not check;

        # Update the maximum value of count
        if (max < count):
            max = count;

    # Return the maximum length
    return max;

# Driver code

# Initialize the array
arr = [ 1, 2, 3, 2, 5, 7 ];

n = len(arr);

# Call thefunction and print the answer
print(maxAlternatingSubarray(n, arr));

# This code is contributed by gfgking.
```

## C#

```
// C# code for the above approach
using System;

class GFG {
  static int maxAlternatingSubarray(int n, int []arr)
  {

    // Initialize mx to store maximum
    // length alternating subarrays
    int i, j, max = 1, count = 1, a, b;

    // Initialize a variable to check is the
    // subarray starts with greater
    // or smaller value
    bool check=false;

    // If length of the array is 1
    // then return 1
    if (n == 1)
      return 1;

    // Traverse for every element
    for (i = 0; i < n; i++) {

      // Reintialize count to 1 as
      // at least one element is counted
      count = 1;

      // Subarray starting at every element
      for (j = i; j < n - 1; j++) {

        // Initialize a and b for storing
        // adjacent positions
        a = j;
        b = j + 1;

        // Check if the alternating subarray
        // starts with greater
        // or smaller element
        if (j == i) {

          // Smaller element starts first
          if (arr[a] < arr[b])
            check = true;

          // Greater element starts first
          else if (arr[a] > arr[b])
            check = false;
        }

        // If check is 1 then the next
        // element should be greater
        if (check==true && arr[a] < arr[b]) {

          // Increment count
          count++;
        }

        // If check is 0 then the next
        // element should be greater
        else if (check==false && arr[a] > arr[b]) {

          // Increment count
          count++;
        }
        else
          break;

        // Update the value of check
        check = !check;
      }

      // Update the maximum value of count
      if (max < count)
        max = count;
    }

    // Return the maximum length
    return max;
  }

  // Driver code
  public static void Main ()
  {

    // Initialize the array
    int []arr = { 1, 2, 3, 2, 5, 7 };

    int n = arr.Length;

    // Call thefunction and print the answer
    Console.Write(maxAlternatingSubarray(n, arr));
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

function maxAlternatingSubarray(n, arr)
{

    // Initialize mx to store maximum
    // length alternating subarrays
    let i, j, max = 1, count = 1, a, b;

    // Initialize a variable to check is the
    // subarray starts with greater
    // or smaller value
    let check;

    // If length of the array is 1
    // then return 1
    if (n == 1)
        return 1;

    // Traverse for every element
    for (i = 0; i < n; i++) {

        // Reintialize count to 1 as
        // at least one element is counted
        count = 1;

        // Subarray starting at every element
        for (j = i; j < n - 1; j++) {

            // Initialize a and b for storing
            // adjacent positions
            a = j;
            b = j + 1;

            // Check if the alternating subarray
            // starts with greater
            // or smaller element
            if (j == i) {

                // Smaller element starts first
                if (arr[a] < arr[b])
                    check = 1;

                // Greater element starts first
                else if (arr[a] > arr[b])
                    check = 0;
            }

            // If check is 1 then the next
            // element should be greater
            if (check && arr[a] < arr[b]) {

                // Increment count
                count++;
            }

            // If check is 0 then the next
            // element should be greater
            else if (!check && arr[a] > arr[b]) {

                // Increment count
                count++;
            }
            else
                break;

            // Update the value of check
            check = !check;
        }

        // Update the maximum value of count
        if (max < count)
            max = count;
    }

    // Return the maximum length
    return max;
}

// Driver code

// Initialize the array
let arr = [ 1, 2, 3, 2, 5, 7 ];

let n = arr.length;

// Call thefunction and print the answer
document.write(maxAlternatingSubarray(n, arr));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output:** 

```
4
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(1)

**方法:**给定的问题可以通过迭代数组并预先计算连续元素之间的差异来优化。按照以下步骤解决问题:

*   [从索引 1 开始迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，直到结束，每次迭代:
    *   如果当前元素大于前一个元素，则将**电流变大**增加 1，并将**电流变小**重置为 0
    *   否则，如果当前元素小于前一个元素，则将**电流变小**增加 1，并将**电流变大**重置为 0
    *   否则，如果当前元素和先前元素相等，则将**更大电流**和**更小电流**重置为 0
    *   交换**更大**和**更小**的值
    *   通过将最大长度值与**更大**和**更小**进行比较来更新最大长度值
*   返回计算出的最大长度值

## C++14

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum length
// of alternating subarray
int longestAltSubarray(int N, int* arr)
{

    // If length of the array is 1
    // then return 1
    if (N == 1)
        return 1;

    int maxLen = 0;
    int currGreater = 0, currSmaller = 0;

    // Traverse the temp array
    for (int i = 1; i < N; i++) {

        // If current element is greater
        // than the previous element
        if (arr[i] > arr[i - 1]) {

            // Increment currGreater by 1
            currGreater++;

            // Reset currSmaller to 0
            currSmaller = 0;
        }

        // If current element is smaller
        // than the previous element
        else if (arr[i] < arr[i - 1]) {

            // Increment currSmaller by 1
            currSmaller++;

            // Reset currGreater to 0
            currGreater = 0;
        }
        // If current element is equal
        // to previous element
        else {

            // Reset both to 0
            currGreater = 0;
            currSmaller = 0;
        }

        // Swap currGreater and currSmaller
        // for the next iteration
        int temp = currGreater;
        currGreater = currSmaller;
        currSmaller = temp;

        // Update maxLen
        maxLen = max(maxLen,
                     max(currGreater, currSmaller));
    }

    // Return the maximum length
    return maxLen + 1;
}

// Drivers code
int main()
{

    // Initialize the array
    int arr[] = { 1, 2, 3, 2, 5, 7 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Call the function and print the answer
    cout << longestAltSubarray(n, arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;
public class GFG
{

// Function to calculate maximum length
// of alternating subarray
static int longestAltSubarray(int N, int []arr)
{

    // If length of the array is 1
    // then return 1
    if (N == 1)
        return 1;

    int maxLen = 0;
    int currGreater = 0, currSmaller = 0;

    // Traverse the temp array
    for (int i = 1; i < N; i++) {

        // If current element is greater
        // than the previous element
        if (arr[i] > arr[i - 1]) {

            // Increment currGreater by 1
            currGreater++;

            // Reset currSmaller to 0
            currSmaller = 0;
        }

        // If current element is smaller
        // than the previous element
        else if (arr[i] < arr[i - 1]) {

            // Increment currSmaller by 1
            currSmaller++;

            // Reset currGreater to 0
            currGreater = 0;
        }

        // If current element is equal
        // to previous element
        else {

            // Reset both to 0
            currGreater = 0;
            currSmaller = 0;
        }

        // Swap currGreater and currSmaller
        // for the next iteration
        int temp = currGreater;
        currGreater = currSmaller;
        currSmaller = temp;

        // Update maxLen
        maxLen = Math.max(maxLen,
                     Math.max(currGreater, currSmaller));
    }

    // Return the maximum length
    return maxLen + 1;
}

// Drivers code
public static void main(String args[])
{

    // Initialize the array
    int []arr = { 1, 2, 3, 2, 5, 7 };

    int n = arr.length;

    // Call the function and print the answer
    System.out.println(longestAltSubarray(n, arr));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python3 implementation for the above approach
from builtins import range

# Function to calculate maximum length
# of alternating subarray
def longestAltSubarray(N, arr):

    # If length of the array is 1
    # then return 1
    if (N == 1):
        return 1

    maxLen = 0
    currGreater = 0
    currSmaller = 0

    # Traverse the temp array
    for i in range(1, N, 1):

        # If current element is greater
        # than the previous element
        if (arr[i] > arr[i - 1]):

            # Increment currGreater by 1
            currGreater += 1

            # Reset currSmaller to 0
            currSmaller = 0

        # If current element is smaller
        # than the previous element
        elif (arr[i] < arr[i - 1]):

            # Increment currSmaller by 1
            currSmaller += 1

            # Reset currGreater to 0
            currGreater = 0

        # If current element is equal
        # to previous element
        else:

            # Reset both to 0
            currGreater = 0
            currSmaller = 0

        # Swap currGreater and currSmaller
        # for the next iteration
        temp = currGreater
        currGreater = currSmaller
        currSmaller = temp

        # Update maxLen
        maxLen = max(maxLen, max(currGreater,
                                 currSmaller))

    # Return the maximum length
    return maxLen + 1

# Driver code
if __name__ == '__main__':

    # Initialize the array
    arr = [ 1, 2, 3, 2, 5, 7 ]

    n = len(arr)

    # Call the function and print the answer
    print(longestAltSubarray(n, arr))

# This code is contributed by shikhasingrajput
```

## C#

```
// C# implementation for the above approach
using System;
class GFG
{

// Function to calculate maximum length
// of alternating subarray
static int longestAltSubarray(int N, int []arr)
{

    // If length of the array is 1
    // then return 1
    if (N == 1)
        return 1;

    int maxLen = 0;
    int currGreater = 0, currSmaller = 0;

    // Traverse the temp array
    for (int i = 1; i < N; i++) {

        // If current element is greater
        // than the previous element
        if (arr[i] > arr[i - 1]) {

            // Increment currGreater by 1
            currGreater++;

            // Reset currSmaller to 0
            currSmaller = 0;
        }

        // If current element is smaller
        // than the previous element
        else if (arr[i] < arr[i - 1]) {

            // Increment currSmaller by 1
            currSmaller++;

            // Reset currGreater to 0
            currGreater = 0;
        }

        // If current element is equal
        // to previous element
        else {

            // Reset both to 0
            currGreater = 0;
            currSmaller = 0;
        }

        // Swap currGreater and currSmaller
        // for the next iteration
        int temp = currGreater;
        currGreater = currSmaller;
        currSmaller = temp;

        // Update maxLen
        maxLen = Math.Max(maxLen,
                     Math.Max(currGreater, currSmaller));
    }

    // Return the maximum length
    return maxLen + 1;
}

// Drivers code
public static void Main()
{

    // Initialize the array
    int []arr = { 1, 2, 3, 2, 5, 7 };

    int n = arr.Length;

    // Call the function and print the answer
    Console.Write(longestAltSubarray(n, arr));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to calculate maximum length
// of alternating subarray
function longestAltSubarray(N, arr) {

  // If length of the array is 1
  // then return 1
  if (N == 1)
    return 1;

  let maxLen = 0;
  let currGreater = 0, currSmaller = 0;

  // Traverse the temp array
  for (let i = 1; i < N; i++) {

    // If current element is greater
    // than the previous element
    if (arr[i] > arr[i - 1]) {

      // Increment currGreater by 1
      currGreater++;

      // Reset currSmaller to 0
      currSmaller = 0;
    }

    // If current element is smaller
    // than the previous element
    else if (arr[i] < arr[i - 1]) {

      // Increment currSmaller by 1
      currSmaller++;

      // Reset currGreater to 0
      currGreater = 0;
    }
    // If current element is equal
    // to previous element
    else {

      // Reset both to 0
      currGreater = 0;
      currSmaller = 0;
    }

    // Swap currGreater and currSmaller
    // for the next iteration
    let temp = currGreater;
    currGreater = currSmaller;
    currSmaller = temp;

    // Update maxLen
    maxLen = Math.max(maxLen,
      Math.max(currGreater, currSmaller));
  }

  // Return the maximum length
  return maxLen + 1;
}

// Drivers code

// Initialize the array
let arr = [1, 2, 3, 2, 5, 7];

let n = arr.length

// Call the function and let the answer
document.write(longestAltSubarray(n, arr))

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)