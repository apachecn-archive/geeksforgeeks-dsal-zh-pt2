# 根据给定条件选择元素可能得到的最大修改数组和

> 原文:[https://www . geesforgeks . org/按给定条件选择元素的最大修改数组总和/](https://www.geeksforgeeks.org/maximum-modified-array-sum-possible-by-choosing-elements-as-per-the-given-conditions/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到数组元素的最大可能和，以便可以根据以下条件选择元素:

*   对于每个索引 **i** 元素的值是**arr【I】**，那么我们可以将从 **1 到 min(N，arr【I】)**的任何元素添加到总和中，否则就留下该元素。
*   如果某个元素已经加到和中，那么我们就不能再把同一个元素加到和中。

**示例:**

> ***输入:** arr[] = {1，2，2，4}*
> ***输出:** 7*
> **解释:**
> *最初，总和为 0。*
> *将索引 1 处的元素添加到 sum = 1 后的 Sum。将索引 2 处的元素添加到 sum = 3 后，添加到 sum = {1}*
> *的元素。添加到总和中的元素= {1，2}*
> 现在，从索引 3 开始，我们不能将(1 到 2)中的任何元素添加到总和中，因为我们已经将元素{1，2}添加到总和中。所以，将元素留在索引 3 处。
> 然后将索引 4 处的元素加到 sum 上，因为 4 之前没有加到 sum 上，所以我们能得到的最大和是 3+4=7。
> 
> ***输入:** arr[] = {4，4，1，5}*
> ***输出:** 13*

**进场:**这个问题可以用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是步骤:

1.  [按升序排序](https://www.geeksforgeeks.org/sorting-algorithms/)数组的元素。
2.  保持最大可能数**(比如说最大可能)**，这个最大可能数可以加到总和中。
3.  用数组的最大元素初始化**最大可能**，并将其加到总和中。
4.  [从头到尾遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查给定的元素值之前是否已经加到总和中。
5.  如果之前已经添加了元素值，那么我们将把**(元素–1)**添加到总和中，如果元素值小于**最大可能值**，那么我们将添加该数字并将**最大可能值**更改为元素值。
6.  完成上述步骤后，打印总和的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#define ll long long
using namespace std;

// Function that finds the maximum sum
// of the array elements according to
// the given condition
ll findMaxValue(int arr[], int n)
{
    // Sort the array
    sort(arr, arr + n);

    // Take the max value from the array
    ll ans = arr[n - 1];
    ll maxPossible = arr[n - 1];

    // Iterate from the end of the array
    for (int i = n - 2; i >= 0; --i) {

        if (maxPossible > 0) {

            // Check for the number had
            // come before or not
            if (arr[i] >= maxPossible) {

                // Take the value which is
                // not occured already
                ans += (maxPossible - 1);
                maxPossible = maxPossible - 1;
            }
            else {

                // Change max to new value
                maxPossible = arr[i];
                ans += maxPossible;
            }
        }
    }

    // Return the maximum sum
    return ans;
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 4, 4, 1, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << findMaxValue(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function that finds the maximum sum
// of the array elements according to
// the given condition
static int findMaxValue(int arr[], int n)
{
    // Sort the array
    Arrays.sort(arr);

    // Take the max value from the array
    int ans = arr[n - 1];
    int maxPossible = arr[n - 1];

    // Iterate from the end of the array
    for (int i = n - 2; i >= 0; --i)
    {
        if (maxPossible > 0)
        {

            // Check for the number had
            // come before or not
            if (arr[i] >= maxPossible)
            {

                // Take the value which is
                // not occured already
                ans += (maxPossible - 1);
                maxPossible = maxPossible - 1;
            }
            else
            {

                // Change max to new value
                maxPossible = arr[i];
                ans += maxPossible;
            }
        }
    }

    // Return the maximum sum
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 4, 4, 1, 5 };
    int n = arr.length;

    // Function Call
    System.out.print(findMaxValue(arr, n));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the maximum sum
# of the array elements according to
# the given condition
def findMaxValue(arr, n):

    # Sort the array
    arr.sort()

    # Take the max value from the array
    ans = arr[n - 1]
    maxPossible = arr[n - 1]

    # Iterate from the end of the array
    for i in range(n - 2, -1, -1):
        if (maxPossible > 0):

            # Check for the number had
            # come before or not
            if (arr[i] >= maxPossible):

                # Take the value which is
                # not occured already
                ans += (maxPossible - 1)
                maxPossible = maxPossible - 1
            else:

                # Change max to new value
                maxPossible = arr[i]
                ans += maxPossible

    # Return the maximum sum
    return ans

# Driver code
if __name__=='__main__':

    # Given array arr[]
    arr = [ 4, 4, 1, 5 ]
    n = len(arr)

    # Function call
    print(findMaxValue(arr,n))

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function that finds the maximum sum
// of the array elements according to
// the given condition
static int findMaxValue(int []arr, int n)
{
    // Sort the array
    Array.Sort(arr);

    // Take the max value from the array
    int ans = arr[n - 1];
    int maxPossible = arr[n - 1];

    // Iterate from the end of the array
    for (int i = n - 2; i >= 0; --i)
    {
        if (maxPossible > 0)
        {

            // Check for the number had
            // come before or not
            if (arr[i] >= maxPossible)
            {

                // Take the value which is
                // not occured already
                ans += (maxPossible - 1);
                maxPossible = maxPossible - 1;
            }
            else
            {

                // Change max to new value
                maxPossible = arr[i];
                ans += maxPossible;
            }
        }
    }

    // Return the maximum sum
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 4, 4, 1, 5 };
    int n = arr.Length;

    // Function Call
    Console.Write(findMaxValue(arr, n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that finds the maximum sum
// of the array elements according to
// the given condition
function findMaxValue(arr, n)
{
    // Sort the array
    arr.sort((a, b) => a - b);

    // Take the max value from the array
    let ans = arr[n - 1];
    let maxPossible = arr[n - 1];

    // Iterate from the end of the array
    for (let i = n - 2; i >= 0; --i) {

        if (maxPossible > 0) {

            // Check for the number had
            // come before or not
            if (arr[i] >= maxPossible) {

                // Take the value which is
                // not occured already
                ans += (maxPossible - 1);
                maxPossible = maxPossible - 1;
            }
            else {

                // Change max to new value
                maxPossible = arr[i];
                ans += maxPossible;
            }
        }
    }

    // Return the maximum sum
    return ans;
}

// Driver Code

    // Given array arr[]
    let arr = [ 4, 4, 1, 5 ];
    let n = arr.length;

    // Function Call
    document.write(findMaxValue(arr, n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
13
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*