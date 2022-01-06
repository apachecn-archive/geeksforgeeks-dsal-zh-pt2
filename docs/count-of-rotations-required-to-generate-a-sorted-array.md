# 生成排序数组所需的旋转次数

> 原文:[https://www . geeksforgeeks . org/生成排序数组所需的旋转次数/](https://www.geeksforgeeks.org/count-of-rotations-required-to-generate-a-sorted-array/)

给定一个**数组 arr[]** ，任务是找到将给定数组转换为排序形式所需的旋转次数。
**例:**

> **输入:** arr[] = {4，5，1，2，3}
> **输出:** 2
> **解释:**
> 逆时针旋转 2 圈后排序数组{1，2，3，4，5}。
> 
> **输入:** arr[] = {2，1，2，2，2}
> **输出:** 1
> **解释:**
> 逆时针旋转 1 圈后排序数组{1，2，2，2，2}。

**天真方法:**
要解决上面提到的问题，第一个观察是如果我们在数组中有 **n** 个元素，那么在排序之后，最大的元素位于(n–1)<sup>第</sup>个位置。逆时针旋转 k 次后，最大的元素将位于索引处(k–1)(k<sup>第</sup>个元素从开始)。这里要注意的另一件事是，在旋转之后，最大元素的下一个元素将总是最小的元素(除非最大的元素在最后一个索引处，如果没有旋转，这是可能的)。
因此，

> 旋转数(k) = **数组中最小元素(k)的索引**

下面是上述方法的实现:

## C++

```
// C++ program to find the
// count of rotations
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of rotations
int countRotation(int arr[], int n)
{
    for(int i = 1; i < n; i++)
    {

       // Find the smallest element
       if (arr[i] < arr[i - 1])
       {
           // Return its index
           return i;
       }
    }

    // If array is not
    // rotated at all
    return 0;
}

// Driver Code
int main()
{
    int arr1[] = { 4, 5, 1, 2, 3 };
    int n = sizeof(arr1) / sizeof(int);

    cout << countRotation(arr1, n);
}

// This code is contributed by jrishabh99
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// count of rotations
public class GFG {

    // Function to return the count of
    // rotations
    public static int countRotation(int[] arr,
                                    int n)
    {
        for (int i = 1; i < n; i++) {
            // Find the smallest element
            if (arr[i] < arr[i - 1]) {
                // Return its index
                return i;
            }
        }
        // If array is not
        // rotated at all
        return 0;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr1 = { 4, 5, 1, 2, 3 };

        System.out.println(
            countRotation(
                arr1,
                arr1.length));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the
# count of rotations

# Function to return the count
# of rotations
def countRotation(arr, n):

    for i in range (1, n):

        # Find the smallest element
        if (arr[i] < arr[i - 1]):

            # Return its index
            return i

    # If array is not
    # rotated at all
    return 0

# Driver Code
if __name__ == "__main__":

    arr1 = [ 4, 5, 1, 2, 3 ]
    n = len(arr1)

    print(countRotation(arr1, n))

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the count of rotations
using System;
class GFG{

// Function to return the count of
// rotations
public static int countRotation(int[] arr,
                                int n)
{
    for(int i = 1; i < n; i++)
    {

    // Find the smallest element
    if (arr[i] < arr[i - 1])
    {

        // Return its index
        return i;
    }
    }

    // If array is not
    // rotated at all
    return 0;
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr1 = { 4, 5, 1, 2, 3 };

    Console.WriteLine(countRotation(arr1,
                                    arr1.Length));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program to find the
// count of rotations

// Function to return the count of
// rotations
function countRotation(arr, n)
{
    for(let i = 1; i < n; i++)
    {

        // Find the smallest element
        if (arr[i] < arr[i - 1])
        {

            // Return its index
            return i;
        }
    }

    // If array is not
    // rotated at all
    return 0;
}

// Driver Code
let arr1 = [ 4, 5, 1, 2, 3 ];

document.write(countRotation(
    arr1, arr1.length));

// This code is contributed by sanjoy_62

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效途径:**
为了优化上述途径，我们将使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。我们可以注意到，在排序和旋转之后，给定的数组被分成两部分，其中包含不递减的元素，这是二分搜索法的唯一先决条件。在数组中执行递归二分搜索法运算，找到最小元素的索引。

下面是上述方法的实现:

## C++

```
// C++ program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// count of rotations
int countRotation(int arr[], int low,
                             int high)
{

    // If array is not rotated
    if (low > high)
    {
        return 0;
    }

    int mid = low + (high - low) / 2;

    // Check if current element is
    // greater than the next
    // element
    if (mid < high && arr[mid] > arr[mid + 1])
    {

        // The next element is
        // the smallest
        return mid + 1;
    }

    // Check if current element is
    // smaller than it's previous
    // element
    if (mid > low && arr[mid] < arr[mid - 1])
    {

        // Current element is
        // the smallest
        return mid;
    }

    // Check if current element is
    // greater than lower bound
    if (arr[mid] > arr[low])
    {

        // The sequence is increasing
        // so far
        // Search for smallest
        // element on the right
        // subarray
        return countRotation(arr, mid + 1,
                             high);
    }

    if (arr[mid] < arr[high])
    {

        // Smallest element lies on the
        // left subarray
        return countRotation(arr, low,
                             mid - 1);
    }
    else
    {

        // Search for the smallest
        // element on both subarrays
        int rightIndex = countRotation(arr,
                                       mid + 1,
                                       high);
        int leftIndex = countRotation(arr, low,
                                      mid - 1);
        if (rightIndex == 0)
        {
            return leftIndex;
        }
        return rightIndex;
    }
}

// Driver code   
int main()
{
    int arr1[] = { 4, 5, 1, 2, 3 };
    int N = sizeof(arr1) / sizeof(arr1[0]);

    cout << countRotation(arr1, 0, N - 1);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

public class GFG {

    // Function to return the
    // count of rotations
    public static int countRotation(int[] arr,
                                    int low,
                                    int high)
    {
        // If array is not rotated
        if (low > high) {
            return 0;
        }

        int mid = low + (high - low) / 2;

        // Check if current element is
        // greater than the next
        // element

        if (mid < high
            && arr[mid] > arr[mid + 1]) {
            // the next element is
            // the smallest
            return mid + 1;
        }

        // Check if current element is
        // smaller than it's previous
        // element
        if (mid > low
            && arr[mid] < arr[mid - 1]) {
            // Current element is
            // the smallest
            return mid;
        }

        // Check if current element is
        // greater than lower bound

        if (arr[mid] > arr[low]) {
            // The sequence is increasing
            // so far
            // Search for smallest
            // element on the right
            // subarray
            return countRotation(arr,
                                mid + 1,
                                high);
        }

        if (arr[mid] < arr[high]) {
            // Smallest element lies on the
            // left subarray
            return countRotation(arr,
                                low,
                                mid - 1);
        }

        else {
            // Search for the smallest
            // element on both subarrays
            int rightIndex = countRotation(arr,
                                        mid + 1,
                                        high);
            int leftIndex = countRotation(arr,
                                        low,
                                        mid - 1);

            if (rightIndex == 0) {
                return leftIndex;
            }

            return rightIndex;
        }
    }

    // Driver Program
    public static void main(String[] args)
    {
        int[] arr1 = { 4, 5, 1, 2, 3 };

        System.out.println(
            countRotation(
                arr1,
                0, arr1.length
                    - 1));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach

# Function to return the
# count of rotations
def countRotation(arr, low, high):

    # If array is not rotated
    if (low > high):
        return 0

    mid = low + (high - low) // 2

    # Check if current element is
    # greater than the next
    # element
    if (mid < high and arr[mid] > arr[mid + 1]):

        # The next element is
        # the smallest
        return mid + 1

    # Check if current element is
    # smaller than it's previous
    # element
    if (mid > low and arr[mid] < arr[mid - 1]):

        # Current element is
        # the smallest
        return mid

    # Check if current element is
    # greater than lower bound
    if (arr[mid] > arr[low]):

        # The sequence is increasing
        # so far
        # Search for smallest
        # element on the right
        # subarray
        return countRotation(arr, mid + 1, high)

    if (arr[mid] < arr[high]):

        # Smallest element lies on the
        # left subarray
        return countRotation(arr, low, mid - 1)

    else:

        # Search for the smallest
        # element on both subarrays
        rightIndex = countRotation(arr,
                                   mid + 1,
                                   high)
        leftIndex = countRotation(arr, low,
                                  mid - 1)

        if (rightIndex == 0):
            return leftIndex

        return rightIndex

# Driver code
if __name__ == '__main__':

    arr1 = [ 4, 5, 1, 2, 3 ]
    N = len(arr1)

    print(countRotation(arr1, 0, N - 1))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to return the
// count of rotations
public static int countRotation(int[] arr,
                                int low,
                                int high)
{

    // If array is not rotated
    if (low > high)
    {
        return 0;
    }

    int mid = low + (high - low) / 2;

    // Check if current element is
    // greater than the next
    // element
    if (mid < high &&
        arr[mid] > arr[mid + 1])
    {

        // The next element is
        // the smallest
        return mid + 1;
    }

    // Check if current element is
    // smaller than it's previous
    // element
    if (mid > low &&
        arr[mid] < arr[mid - 1])
    {

        // Current element is
        // the smallest
        return mid;
    }

    // Check if current element is
    // greater than lower bound
    if (arr[mid] > arr[low])
    {

        // The sequence is increasing
        // so far
        // Search for smallest
        // element on the right
        // subarray
        return countRotation(arr,
                             mid + 1,
                             high);
    }

    if (arr[mid] < arr[high])
    {

        // Smallest element lies on the
        // left subarray
        return countRotation(arr, low,
                             mid - 1);
    }

    else
    {

        // Search for the smallest
        // element on both subarrays
        int rightIndex = countRotation(arr,
                                       mid + 1,
                                       high);
        int leftIndex = countRotation(arr, low,
                                      mid - 1);

        if (rightIndex == 0)
        {
            return leftIndex;
        }
        return rightIndex;
    }
}

// Driver code
public static void Main(String[] args)
{
    int[] arr1 = { 4, 5, 1, 2, 3 };

    Console.WriteLine(countRotation(arr1, 0,
                            arr1.Length - 1));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Function to return the
    // count of rotations
function countRotation(arr,low,high)
{

    // If array is not rotated
        if (low > high) {
            return 0;
        }

        let mid = low + Math.floor((high - low) / 2);

        // Check if current element is
        // greater than the next
        // element

        if (mid < high
            && arr[mid] > arr[mid + 1]) {
            // the next element is
            // the smallest
            return mid + 1;
        }

        // Check if current element is
        // smaller than it's previous
        // element
        if (mid > low
            && arr[mid] < arr[mid - 1]) {
            // Current element is
            // the smallest
            return mid;
        }

        // Check if current element is
        // greater than lower bound

        if (arr[mid] > arr[low]) {
            // The sequence is increasing
            // so far
            // Search for smallest
            // element on the right
            // subarray
            return countRotation(arr,
                                mid + 1,
                                high);
        }

        if (arr[mid] < arr[high])
        {

            // Smallest element lies on the
            // left subarray
            return countRotation(arr,
                                low,
                                mid - 1);
        }

        else
        {

            // Search for the smallest
            // element on both subarrays
            let rightIndex = countRotation(arr,
                                        mid + 1,
                                        high);
            let leftIndex = countRotation(arr,
                                        low,
                                        mid - 1);

            if (rightIndex == 0) {
                return leftIndex;
            }

            return rightIndex;
        }
}

 // Driver Program
let arr1=[4, 5, 1, 2, 3 ];
document.write(
            countRotation(
                arr1,
                0, arr1.length
                    - 1));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
*对于无重复的数组，复杂度为 O(logN)。但是如果数组包含重复项，那么它将递归地调用对两部分的搜索。所以最坏的情况是 O(N)。*

***辅助空间:** O(N)*
*最坏的情况下，递归调用栈一次会有 N/2 个递归调用。*