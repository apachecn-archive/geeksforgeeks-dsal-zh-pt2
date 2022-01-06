# 在 K 次

的情况下，通过将对的较大和较小元素分别替换为其值的一半和两倍来最小化数组和

> 原文:[https://www . geeksforgeeks . org/通过将成对的大元素和小元素分别替换为其值的一半和两倍来最小化数组和/atmat-k-times/](https://www.geeksforgeeks.org/minimize-array-sum-by-replacing-greater-and-smaller-elements-of-pairs-by-half-and-double-of-their-values-respectively-atmost-k-times/)

给定一个由 **N** 个正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是通过从给定数组中反复选择一对元素，将其中一个元素除以 **2** ，再将另一个元素乘以 **2** ，最多可以得到最小可能的数组和 **K** 。

**示例:**

> **输入:** arr[] = {5，1，10，2，3}，K = 1
> **输出:** 17
> **解释:**既然 K = 1，唯一的操作就是更新 arr[1] = arr[1] * 2 和 arr[2] = arr[2] / 2，修改 arr[] = {5，2，5，2，3}。因此，可以得到的数组的最小可能和= 17。
> 
> **输入:** arr[] = {50，1，100，100，1}，K = 2
> **输出:** 154
> **解释:**
> 操作 1:更新 arr[1] = arr[1] * 2 和 arr[3] = arr[3] / 2 修改 arr[] = {50，2，100，50，1}。
> 操作 2:更新 arr[4] = arr[4] * 2 和 arr[2] = arr[2] / 2 修改 arr[] = {50，2，50，50，2}。
> 因此，可以得到的数组的最小可能和= 154。

**天真法:**解决问题最简单的方法是每次运算选择[最小最大数组元素](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)，最小数组元素乘以 **2** ，最大数组元素除以 **2** 。最后，完成 **K** 操作后，打印所有数组元素的[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum sum of
// array elements by given operations
int minimum_possible_sum(int arr[],
                         int n, int k)
{

    // Base case
    if (n == 0) {

        // Return 0
        return 0;
    }

    // Base case
    if (n == 1) {

        return arr[0];
    }

    // Perform K operations
    for (int i = 0; i < k; i++) {

        // Stores smallest element
        // in the array
        int smallest_element
            = arr[0];

        // Stores index of the
        // smallest array element
        int smallest_pos = 0;

        // Stores largest element
        // in the array
        int largest_element = arr[0];

        // Stores index of the
        // largest array element
        int largest_pos = 0;

        // Traverse the array elements
        for (int i = 1; i < n; i++) {

            // If current element
            // exceeds largest_element
            if (arr[i] >= largest_element) {

                // Update the largest element
                largest_element = arr[i];

                // Update index of the
                // largest array element
                largest_pos = i;
            }

            // If current element is
            // smaller than smallest_element
            if (arr[i] < smallest_element) {

                // Update the smallest element
                smallest_element = arr[i];

                // Update index of the
                // smallest array element
                smallest_pos = i;
            }
        }

        // Stores the value of smallest
        // element by given operations
        int a = smallest_element * 2;

        // Stores the value of largest
        // element by given operations
        int b = largest_element / 2;

        // If the value of a + b less than
        // the sum of smallest and
        // largest element of the array
        if (a + b < smallest_element
                        + largest_element) {

            // Update smallest element
            // of the array
            arr[smallest_pos] = a;

            // Update largest element
            // of the array
            arr[largest_pos] = b;
        }
    }

    // Stores sum of elements of
    // the array by given operations
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Update ans
        ans += arr[i];
    }

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 50, 1, 100, 100, 1 };

    int K = 2;

    int n = sizeof(arr)
            / sizeof(arr[0]);
    cout << minimum_possible_sum(
        arr, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the minimum sum of
// array elements by given operations
static int minimum_possible_sum(int arr[],
                                int n, int k)
{

    // Base case
    if (n == 0)
    {

        // Return 0
        return 0;
    }

    // Base case
    if (n == 1)
    {
        return arr[0];
    }

    // Perform K operations
    for(int i = 0; i < k; i++)
    {

        // Stores smallest element
        // in the array
        int smallest_element = arr[0];

        // Stores index of the
        // smallest array element
        int smallest_pos = 0;

        // Stores largest element
        // in the array
        int largest_element = arr[0];

        // Stores index of the
        // largest array element
        int largest_pos = 0;

        // Traverse the array elements
        for(int j = 1; j < n; j++)
        {

            // If current element
            // exceeds largest_element
            if (arr[j] >= largest_element)
            {

                // Update the largest element
                largest_element = arr[j];

                // Update index of the
                // largest array element
                largest_pos = j;
            }

            // If current element is
            // smaller than smallest_element
            if (arr[j] < smallest_element)
            {

                // Update the smallest element
                smallest_element = arr[j];

                // Update index of the
                // smallest array element
                smallest_pos = j;
            }
        }

        // Stores the value of smallest
        // element by given operations
        int a = smallest_element * 2;

        // Stores the value of largest
        // element by given operations
        int b = largest_element / 2;

        // If the value of a + b less than
        // the sum of smallest and
        // largest element of the array
        if (a + b < smallest_element +
                     largest_element)
        {

            // Update smallest element
            // of the array
            arr[smallest_pos] = a;

            // Update largest element
            // of the array
            arr[largest_pos] = b;
        }
    }

    // Stores sum of elements of
    // the array by given operations
    int ans = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Update ans
        ans += arr[i];
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 50, 1, 100, 100, 1 };
    int K = 2;
    int n = arr.length;

    System.out.print(minimum_possible_sum(
                            arr, n, K));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum
# sum of array elements by
# given operations
def minimum_possible_sum(arr, n, k):

    # Base case
    if (n == 0):

        # Return 0
        return 0

    # Base case
    if (n == 1):
        return arr[0]

    # Perform K operations
    for i in range(k):

        # Stores smallest element
        # in the array
        smallest_element = arr[0]

        # Stores index of the
        # smallest array element
        smallest_pos = 0

        # Stores largest element
        # in the array
        largest_element = arr[0]

        # Stores index of the
        # largest array element
        largest_pos = 0

        # Traverse the array
        # elements
        for i in range(1, n):

            # If current element
            # exceeds largest_element
            if (arr[i] >=
                largest_element):

                # Update the largest
                # element
                largest_element = arr[i]

                # Update index of the
                # largest array element
                largest_pos = i

            # If current element is
            # smaller than smallest_element
            if (arr[i] <
                smallest_element):

                # Update the smallest element
                smallest_element = arr[i]

                # Update index of the
                # smallest array element
                smallest_pos = i

        # Stores the value of smallest
        # element by given operations
        a = smallest_element * 2

        # Stores the value of largest
        # element by given operations
        b = largest_element // 2

        # If the value of a + b less
        # than the sum of smallest and
        # largest element of the array
        if (a + b < smallest_element +
            largest_element):

            # Update smallest element
            # of the array
            arr[smallest_pos] = a

            # Update largest element
            # of the array
            arr[largest_pos] = b

    # Stores sum of elements of
    # the array by given operations
    ans = 0

    # Traverse the array
    for i in range(n):

        # Update ans
        ans += arr[i]

    return ans

# Driver Code
if __name__ == '__main__':

    arr = [50, 1, 100, 100, 1]
    K = 2
    n = len(arr)
    print(minimum_possible_sum(arr, n, K))

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find the minimum sum of
// array elements by given operations
static int minimum_possible_sum(int[] arr,
                                int n, int k)
{

    // Base case
    if (n == 0)
    {

        // Return 0
        return 0;
    }

    // Base case
    if (n == 1)
    {
        return arr[0];
    }

    // Perform K operations
    for(int i = 0; i < k; i++)
    {

        // Stores smallest element
        // in the array
        int smallest_element = arr[0];

        // Stores index of the
        // smallest array element
        int smallest_pos = 0;

        // Stores largest element
        // in the array
        int largest_element = arr[0];

        // Stores index of the
        // largest array element
        int largest_pos = 0;

        // Traverse the array elements
        for(int j = 1; j < n; j++)
        {

            // If current element
            // exceeds largest_element
            if (arr[j] >= largest_element)
            {

                // Update the largest element
                largest_element = arr[j];

                // Update index of the
                // largest array element
                largest_pos = j;
            }

            // If current element is
            // smaller than smallest_element
            if (arr[j] < smallest_element)
            {

                // Update the smallest element
                smallest_element = arr[j];

                // Update index of the
                // smallest array element
                smallest_pos = j;
            }
        }

        // Stores the value of smallest
        // element by given operations
        int a = smallest_element * 2;

        // Stores the value of largest
        // element by given operations
        int b = largest_element / 2;

        // If the value of a + b less than
        // the sum of smallest and
        // largest element of the array
        if (a + b < smallest_element +
                     largest_element)
        {

            // Update smallest element
            // of the array
            arr[smallest_pos] = a;

            // Update largest element
            // of the array
            arr[largest_pos] = b;
        }
    }

    // Stores sum of elements of
    // the array by given operations
    int ans = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Update ans
        ans += arr[i];
    }
    return ans;
}

// Driver Code
public static void Main()
{
    int[] arr = { 50, 1, 100, 100, 1 };
    int K = 2;
    int n = arr.Length;

    Console.WriteLine(minimum_possible_sum(
                            arr, n, K));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum sum of
// array elements by given operations
function minimum_possible_sum(arr, n, k)
{

    // Base case
    if (n == 0)
    {

        // Return 0
        return 0;
    }

    // Base case
    if (n == 1)
    {
        return arr[0];
    }

    // Perform K operations
    for(let i = 0; i < k; i++)
    {

        // Stores smallest element
        // in the array
        let smallest_element = arr[0];

        // Stores index of the
        // smallest array element
        let smallest_pos = 0;

        // Stores largest element
        // in the array
        let largest_element = arr[0];

        // Stores index of the
        // largest array element
        let largest_pos = 0;

        // Traverse the array elements
        for(let j = 1; j < n; j++)
        {

            // If current element
            // exceeds largest_element
            if (arr[j] >= largest_element)
            {

                // Update the largest element
                largest_element = arr[j];

                // Update index of the
                // largest array element
                largest_pos = j;
            }

            // If current element is
            // smaller than smallest_element
            if (arr[j] < smallest_element)
            {

                // Update the smallest element
                smallest_element = arr[j];

                // Update index of the
                // smallest array element
                smallest_pos = j;
            }
        }

        // Stores the value of smallest
        // element by given operations
        let a = smallest_element * 2;

        // Stores the value of largest
        // element by given operations
        let b = largest_element / 2;

        // If the value of a + b less than
        // the sum of smallest and
        // largest element of the array
        if (a + b < smallest_element +
                     largest_element)
        {

            // Update smallest element
            // of the array
            arr[smallest_pos] = a;

            // Update largest element
            // of the array
            arr[largest_pos] = b;
        }
    }

    // Stores sum of elements of
    // the array by given operations
    let ans = 0;

    // Traverse the array
    for(let i = 0; i < n; i++)
    {

        // Update ans
        ans += arr[i];
    }
    return ans;
}

// Driver Code

    let arr = [ 50, 1, 100, 100, 1 ];
    let K = 2;
    let n = arr.length;

    document.write(minimum_possible_sum(
                            arr, n, K));

</script>
```

**Output:** 

```
154
```

***时间复杂度:** O(K * N)*
***辅助空间:** O(1)*

**高效进场:**优化以上进场的思路，就是用一个[平衡二叉查找树](http://geeksforgeeks.org/convert-normal-bst-balanced-bst/)。按照以下步骤解决问题:

*   创建一个[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)，比如说 **ms** 来按照排序顺序存储所有数组元素。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将所有数组元素插入 **ms** 。
*   在每次操作中，找到最小的元素，说**最小 _ 元素**和最大的元素，说 **ms** 中的**最大 _ 元素**，更新**最小 _ 元素=最小 _ 元素* 2** 和**最大 _ 元素=最大 _ 元素/ 2 的值。**
*   最后，[迭代多集](https://www.geeksforgeeks.org/multiset-begin-and-end-function-in-c-stl/)并打印 **ms** 所有元素的总和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum sum of
// array elements by given operations
int minimum_possible_sum(int arr[],
                         int n, int k)
{

    // Base case
    if (n == 0) {

        // Return 0
        return 0;
    }

    // Base case
    if (n == 1) {

        return arr[0];
    }

    // Stores all the array elements
    // in sorted order
    multiset<int> ms;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Insert current element
        // into multiset
        ms.insert(arr[i]);
    }

    // Perform each operation
    for (int i = 0; i < k; i++) {

        // Stores smallest element
        // of ms
        int smallest_element
            = *ms.begin();

        // Stores the largest element
        // of ms
        int largest_element
            = *ms.rbegin();

        // Stores updated value of smallest
        // element of ms by given operations
        int a = smallest_element * 2;

        // Stores updated value of largest
        // element of ms by given operations
        int b = largest_element / 2;

        // If the value of a + b less than
        // the sum of smallest and
        // largest array element
        if (a + b < smallest_element
                        + largest_element) {

            // Erase the smallest element
            ms.erase(ms.begin());

            // Erase the largest element
            ms.erase(prev(ms.end()));

            // Insert the updated value
            // of the smallest element
            ms.insert(a);

            // Insert the updated value
            // of the smallest element
            ms.insert(b);
        }
    }

    // Stores sum of array elements
    int ans = 0;

    // Traverse the multiset
    for (int x : ms) {

        // Update ans
        ans += x;
    }

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 50, 1, 100, 100, 1 };

    int K = 2;

    int n = sizeof(arr)
            / sizeof(arr[0]);

    cout << minimum_possible_sum(
        arr, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function to find the minimum sum of
// array elements by given operations
static int minimum_possible_sum(int arr[],
                                int n, int k)
{

    // Base case
    if (n == 0)
    {

        // Return 0
        return 0;
    }

    // Base case
    if (n == 1)
    {
        return arr[0];
    }

    // Stores all the array elements
    // in sorted order
    Vector<Integer> ms = new Vector<>();

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Insert current element
        // into multiset
        ms.add(arr[i]);
    }
    Collections.sort(ms);

    // Perform each operation
    for(int i = 0; i < k; i++)
    {

        // Stores smallest element
        // of ms
        int smallest_element = ms.get(0);

        // Stores the largest element
        // of ms
        int largest_element = ms.get(ms.size() - 1);

        // Stores updated value of smallest
        // element of ms by given operations
        int a = smallest_element * 2;

        // Stores updated value of largest
        // element of ms by given operations
        int b = largest_element / 2;

        // If the value of a + b less than
        // the sum of smallest and
        // largest array element
        if (a + b < smallest_element +
                     largest_element)
        {

            // Erase the smallest element
            ms.remove(0);

            // Erase the largest element
            ms.remove(ms.size() - 1);

            // Insert the updated value
            // of the smallest element
            ms.add(a);

            // Insert the updated value
            // of the smallest element
            ms.add(b);
            Collections.sort(ms);
        }
    }

    // Stores sum of array elements
    int ans = 0;

    // Traverse the multiset
    for(int x : ms)
    {

        // Update ans
        ans += x;
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 50, 1, 100, 100, 1 };
    int K = 2;
    int n = arr.length;

    System.out.print(minimum_possible_sum(
        arr, n, K));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the minimum sum of
# array elements by given operations
def minimum_possible_sum(arr, n, k):

    # Base case
    if (n == 0):

        # Return 0
        return 0

    # Base case
    if (n == 1):
        return arr[0]

    # Stores all the array elements
    # in sorted order
    ms = []

    # Traverse the array
    for i in range(n):

        # Insert current element
        # into multiset
        ms.append(arr[i])

    ms.sort()

    # Perform each operation
    for i in range(k):

        # Stores smallest element
        # of ms
        smallest_element = ms[0]

        # Stores the largest element
        # of ms
        largest_element = ms[-1]

        # Stores updated value of smallest
        # element of ms by given operations
        a = smallest_element * 2

        # Stores updated value of largest
        # element of ms by given operations
        b = largest_element / 2

        # If the value of a + b less than
        # the sum of smallest and
        # largest array element
        if (a + b < smallest_element +
                    largest_element):

            # Erase the smallest element
            ms.pop(0)

            # Erase the largest element
            ms.pop()

            # Insert the updated value
            # of the smallest element
            ms.append(a)

            # Insert the updated value
            # of the smallest element
            ms.append(b)
            ms.sort()

    # Stores sum of array elements
    ans = int(sum(ms))

    return ans

# Driver Code
arr = [ 50, 1, 100, 100, 1 ]
K = 2
n = len(arr)

print(minimum_possible_sum(arr, n, K))

# This code is contributed by rag2127
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the minimum sum of
// array elements by given operations
static int minimum_possible_sum(int []arr,
                                int n, int k)
{

    // Base case
    if (n == 0)
    {

        // Return 0
        return 0;
    }

    // Base case
    if (n == 1)
    {
        return arr[0];
    }

    // Stores all the array elements
    // in sorted order
    List<int> ms = new List<int>();

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Insert current element
        // into multiset
        ms.Add(arr[i]);
    }
    ms.Sort();

    // Perform each operation
    for(int i = 0; i < k; i++)
    {

        // Stores smallest element
        // of ms
        int smallest_element = ms[0];

        // Stores the largest element
        // of ms
        int largest_element = ms[ms.Count - 1];

        // Stores updated value of smallest
        // element of ms by given operations
        int a = smallest_element * 2;

        // Stores updated value of largest
        // element of ms by given operations
        int b = largest_element / 2;

        // If the value of a + b less than
        // the sum of smallest and
        // largest array element
        if (a + b < smallest_element +
                     largest_element)
        {

            // Erase the smallest element
            ms.RemoveAt(0);

            // Erase the largest element
            ms.RemoveAt(ms.Count - 1);

            // Insert the updated value
            // of the smallest element
            ms.Add(a);

            // Insert the updated value
            // of the smallest element
            ms.Add(b);
            ms.Sort();
        }
    }

    // Stores sum of array elements
    int ans = 0;

    // Traverse the multiset
    foreach(int x in ms)
    {

        // Update ans
        ans += x;
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 50, 1, 100, 100, 1 };
    int K = 2;
    int n = arr.Length;

    Console.Write(minimum_possible_sum(
        arr, n, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the minimum sum of
// array elements by given operations
function minimum_possible_sum(arr, n, k)
{

    // Base case
    if (n == 0) {

        // Return 0
        return 0;
    }

    // Base case
    if (n == 1) {

        return arr[0];
    }

    // Stores all the array elements
    // in sorted order
    var ms = [];

    // Traverse the array
    for (var i = 0; i < n; i++) {

        // Insert current element
        // into multiset
        ms.push(arr[i]);
    }
    ms.sort((a,b)=>a-b)
    // Perform each operation
    for (var i = 0; i < k; i++) {

        // Stores smallest element
        // of ms
        var smallest_element
            = ms[0];

        // Stores the largest element
        // of ms
        var largest_element
            = ms[ms.length-1];

        // Stores updated value of smallest
        // element of ms by given operations
        var a = smallest_element * 2;

        // Stores updated value of largest
        // element of ms by given operations
        var b = largest_element / 2;

        // If the value of a + b less than
        // the sum of smallest and
        // largest array element
        if (a + b < smallest_element
                        + largest_element) {

            // Erase the smallest element
            ms.shift();

            // Erase the largest element
            ms.pop();

            // Insert the updated value
            // of the smallest element
            ms.push(a);

            // Insert the updated value
            // of the smallest element
            ms.push(b);
            ms.sort((a,b)=>a-b)
        }
    }

    // Stores sum of array elements
    var ans = 0;

    // Traverse the multiset
    ms.forEach(x => {

        // Update ans
        ans += x;
    });
    return ans;
}

// Driver Code
var arr = [50, 1, 100, 100, 1];
var K = 2;
var n = arr.length;
document.write( minimum_possible_sum(
    arr, n, K));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
154
```

***时间复杂度:**O(K * log<sub>2</sub>N)*
***辅助空间:** O(1)*