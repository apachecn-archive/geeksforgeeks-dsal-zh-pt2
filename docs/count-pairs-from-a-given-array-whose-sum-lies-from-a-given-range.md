# 对给定数组中的配对进行计数，这些配对的和位于给定范围内

> 原文:[https://www . geesforgeks . org/count-pairs-from-a-给定数组-其和位于给定范围内/](https://www.geeksforgeeks.org/count-pairs-from-a-given-array-whose-sum-lies-from-a-given-range/)

给定一个由 **N** 整数和两个整数 **L** 和 **R** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算其和在**【L，R】**范围内的对的数量。

**示例:**

> ***输入:** arr[] =* {5，1，2}，L = 4，R = 7
> ***输出:** 2*
> **说明:**
> 满足必要条件的对如下:
> 
> 1.  **(5，1):** Sum = 5 + 1 = 6，在[4，7]范围内。
> 2.  **(5，2):** Sum = 5 + 2 = 7，在[4，7]范围内。
> 
> 因此，这种对的计数是 2。
> 
> ***输入:** arr[] =* {5，1，2，4，3}，L = 5，R = 8
> ***输出:** 7*

**天真方法:**解决给定问题的最简单方法是[生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，并计算那些和位于范围**【L，R】**内的对。检查所有配对后，打印配对总数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法也可以通过[排序数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)然后执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来找到每个数组元素的元素数量**arr【I】**来优化，使得总和不会超过给定的范围。按照以下步骤解决问题:

*   [按递增顺序排列数组**arr[]**](https://www.geeksforgeeks.org/sort-c-stl/)。
*   初始化变量，说**右**为**N–1**，**计数**为 **0** ，存储其和在**【L，R】**范围内的对的数量。
*   [迭代直到**右侧**大于 **0** 并执行以下步骤:](https://www.geeksforgeeks.org/java-while-loop-with-examples/)
    *   找到与 **arr【右】**之和大于等于 **L** 的元素的起始索引，并存储在变量中，比如 **start** 。
    *   找到与 **arr【右】**之和小于或等于 **R** 的 **arr【右】**之前元素的结束索引，然后存储在变量中，比如 **end** 。
    *   如果**结束**大于等于**开始**，那么将**(结束–开始+ 1)** 加到**计数**上，表示与当前元素之和在范围**【L，R】**内的元素数量，然后将**右减**1**。**
*   **完成上述步骤后，打印**计数**的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count pairs whose
// sum lies over the range [L, R]
int countPairSum(int arr[], int L,
                 int R, int N)
{
    // Sort the given array
    sort(arr, arr + N);

    int right = N - 1, count = 0;

    // Iterate until right > 0
    while (right > 0) {

        // Starting index of element
        // whose sum with arr[right] >= L
        auto it1
            = lower_bound(arr, arr + N,
                          L - arr[right]);

        int start = it1 - arr;

        // Ending index of element
        // whose sum with arr[right] <= R
        auto it2
            = upper_bound(arr, arr + N,
                          R - arr[right]);

        --it2;

        int end = it2 - arr;

        // Update the value of end
        end = min(end, right - 1);

        // Add the count of elements
        // to the variable count
        if (end - start >= 0) {
            count += (end - start + 1);
        }

        right--;
    }

    // Return the value of count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 5, 1, 2, 4, 3 };
    int L = 5, R = 8;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << countPairSum(arr, L, R, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{
    static int lowerBound(int[] a, int low, int high, int element){
        while(low < high){
            int middle = low + (high - low)/2;
            if(element > a[middle])
                low = middle + 1;
            else
                high = middle;
        }
        return low;
    }

    static int upperBound(int[] a, int low, int high, int element){
        while(low < high){
            int middle = low + (high - low)/2;
            if(a[middle] > element)
                high = middle;
            else
                low = middle + 1;
        }
        return low;
    }
// Function to count pairs whose
// sum lies over the range [L, R]
static int countPairSum(int arr[], int L,
                 int R, int N)
{
    // Sort the given array
    Arrays.sort(arr);

    int right = N - 1, count = 0;

    // Iterate until right > 0
    while (right > 0) {

        // Starting index of element
        // whose sum with arr[right] >= L
        int it1
            = lowerBound(arr, 0,N,
                          L - arr[right]);
       it1++;
        int start = it1 - arr[0];

        // Ending index of element
        // whose sum with arr[right] <= R
        int it2
            = upperBound(arr, 0,N,
                          R - arr[right]);

        int end = it2 - arr[0];

        // Update the value of end
        end = Math.min(end, right - 1);

        // Add the count of elements
        // to the variable count
        if (end - start >= 0) {
            count += (end - start +1);
        }

        right--;
    }

    // Return the value of count
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 1, 2, 4, 3 };
    int L = 5, R = 8;
    int N = arr.length;
    System.out.print(countPairSum(arr, L, R, N));

}
}

// This code is contributed by gauravrajput1
```

## **蟒蛇 3**

```
# Python3 program for the above approach
from bisect import bisect_left, bisect_right

# Function to count pairs whose
# sum lies over the range [L, R]
def countPairSum(arr, L, R, N):

    # Sort the given array
    arr.sort()

    right = N - 1
    count = 0

    # Iterate until right > 0
    while (right > 0):

        # Starting index of element
        # whose sum with arr[right] >= L
        it1 = bisect_left(arr, L - arr[right])

        start = it1

        # Ending index of element
        # whose sum with arr[right] <= R
        it2 = bisect_right(arr, R - arr[right])

        it2 -= 1
        end = it2

        # Update the value of end
        end = min(end, right - 1)

        # Add the count of elements
        # to the variable count
        if (end - start >= 0):
            count += (end - start + 1)

        right -= 1

    # Return the value of count
    return count

# Driver Code
if __name__ == '__main__':

    arr = [ 5, 1, 2, 4, 3 ]
    L = 5
    R = 8
    N = len(arr)

    print(countPairSum(arr, L, R, N))

# This code is contributed by SURENDRA_GANGWAR
```

## **C#**

```
// C# program for the above approach
using System;

public class GFG {
    static int lowerBound(int[] a, int low, int high, int element) {
        while (low < high) {
            int middle = low + (high - low) / 2;
            if (element > a[middle])
                low = middle + 1;
            else
                high = middle;
        }
        return low;
    }

    static int upperBound(int[] a, int low, int high, int element) {
        while (low < high) {
            int middle = low + (high - low) / 2;
            if (a[middle] > element)
                high = middle;
            else
                low = middle + 1;
        }
        return low;
    }

    // Function to count pairs whose
    // sum lies over the range [L, R]
    static int countPairSum(int []arr, int L, int R, int N)
    {

        // Sort the given array
        Array.Sort(arr);

        int right = N - 1, count = 0;

        // Iterate until right > 0
        while (right > 0) {

            // Starting index of element
            // whose sum with arr[right] >= L
            int it1 = lowerBound(arr, 0, N, L - arr[right]);
            it1++;
            int start = it1 - arr[0];

            // Ending index of element
            // whose sum with arr[right] <= R
            int it2 = upperBound(arr, 0, N, R - arr[right]);

            int end = it2 - arr[0];

            // Update the value of end
            end = Math.Min(end, right - 1);

            // Add the count of elements
            // to the variable count
            if (end - start >= 0) {
                count += (end - start + 1);
            }

            right--;
        }

        // Return the value of count
        return count;
    }

    // Driver Code
    public static void Main(String[] args) {
        int []arr = { 5, 1, 2, 4, 3 };
        int L = 5, R = 8;
        int N = arr.Length;
        Console.Write(countPairSum(arr, L, R, N));

    }
}

// This code is contributed by gauravrajput1
```

## **java 描述语言**

```
<script>
// javascript program for the above approach
    function lowerBound(a , low , high , element) {
        while (low < high) {
            var middle = low + parseInt((high - low) / 2);
            if (element > a[middle])
                low = middle + 1;
            else
                high = middle;
        }
        return low;
    }

    function upperBound(a , low , high , element) {
        while (low < high) {
            var middle = low + parseInt((high - low) / 2);
            if (a[middle] > element)
                high = middle;
            else
                low = middle + 1;
        }
        return low;
    }

    // Function to count pairs whose
    // sum lies over the range [L, R]
    function countPairSum(arr , L , R , N)
    {

        // Sort the given array
        arr.sort((a,b)=>a-b);

        var right = N - 1, count = 0;

        // Iterate until right > 0
        while (right > 0) {

            // Starting index of element
            // whose sum with arr[right] >= L
            var it1 = lowerBound(arr, 0, N, L - arr[right]);
            it1++;
            var start = it1 - arr[0];

            // Ending index of element
            // whose sum with arr[right] <= R
            var it2 = upperBound(arr, 0, N, R - arr[right]);
            var end = it2 - arr[0];

            // Update the value of end
            end = Math.min(end, right - 1);

            // Add the count of elements
            // to the variable count
            if (end - start >= 0) {
                count += (end - start + 1);
            }

            right--;
        }

        // Return the value of count
        return count;
    }

    // Driver Code
        var arr = [ 5, 1, 2, 4, 3 ];
        var L = 5, R = 8;
        var N = arr.length;
        document.write(countPairSum(arr, L, R, N));

// This code is contributed by gauravrajput1
</script>
```

****Output:** 

```
7
```** 

*****时间复杂度:** O(N*log N)*
***辅助空间:** O(1)***