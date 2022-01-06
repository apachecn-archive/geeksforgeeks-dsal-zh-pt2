# 将排序后的数组分成 K 个部分，每个部分的最大值和最小值之和最小化–第 2 集

> 原文:[https://www . geesforgeks . org/divide-a-sorted-array-in-k-parts-with-sum-of-divide-divide-a-divide-a-sorted-in-k-parts-with-sum-divide-of-divide-a-divide-a-sorted-in-k-parts-in-divide-a](https://www.geeksforgeeks.org/divide-a-sorted-array-in-k-parts-with-sum-of-difference-of-max-and-min-minimized-in-each-part-set-2/)

给定一个大小为 **N** 的升序排序数组**arr【】**和一个整数 **K** ，任务是将给定数组划分为 **K** 个非空子数组，使得每个子数组的最大值和最小值之差之和最小。

**示例:**

> **输入:** arr[] = { 10，20，70，80}，N = 4，K = 2
> **输出:** 20
> **说明:**给定数组可以通过以下方式拆分
> {10，20}和{70，80 }。差值为(20–10)= 10 和(80–70)= 10
> 总和= 10 + 10 = 20
> 
> **输入:** arr[] = { 5，10，50，70 }，N = 4，K = 3
> **输出:** 5
> **说明:**子阵为{ 5，10}，{50}，{70}
> 差值为 10–5 = 5，50–50 = 0，70–70 = 0
> 和= 5 + 0 + 0 = 5

**方法:**其他方法在本文的[第 1 集中讨论。在这里，我们讨论的是二分搜索法方法。](https://www.geeksforgeeks.org/divide-a-sorted-array-in-k-parts-with-sum-of-difference-of-max-and-min-minimized-in-each-part/)

**空间优化途径:**思路是用[【二分搜索法】](https://www.geeksforgeeks.org/binary-search/)来寻找答案。**答案在于[ 0，(arr[N-1]–arr[0])。**见以下观察，以获得正当理由。

> *   Assuming that as many cuts as possible are allowed, the answer will be **0** , because each element can form a subarray. So the minimum value is **0** .
> *   At the other extreme, only one subarray is allowed. In this case, the answer is **(arr [n-1]–arr [0])** . These are two extreme examples, and the answer must be between them.

按照以下步骤解决问题:

*   将变量**和**初始化为 **0** 来存储答案。
*   应用二分搜索法，使**低= 0** ，而**高= arr[N-1]–arr[0]**。
*   对于 **mid** 的每个值，检查长度为 mid 的胶带是否能覆盖 **K** 切口内的所有孔。
*   如果是这样，那么我们已经得出了一个潜在的答案。存储该值，并检查是否可以对较小长度的磁带进行同样的操作。(使**高=中-1**)
*   如果不是，则为 mid 找到一个较大的值(**低= mid + 1** )。

下面是上述方法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to find the minimum sum
    static void findMinTapeLength(int[] arr, 
                                  int N, int K)
    {
        // Initialise low and high
        int high = arr[N - 1] - arr[0], low = 0;
        int ans = 0;

        // Apply Binary Search
        while (low <= high) {
            int mid = low + (high - low) / 2;

            // IsValid() function checks if
            // max value of mid is sufficient 
            // to break the array in K subarrays
            if (isValid(arr, K, mid)) {

                // If true then set this as 
                // the current answer and divide 
                // your range to [low, mid-1] 
                // to check for a lower sum
                ans = mid;
                high = mid - 1;
            }
            // If false then that means need 
            // to increase the current length 
            // so set range to [mid+1, high]
            else
                low = mid + 1;
        }
        System.out.println(ans);
    }

    static boolean isValid(int[] arr, 
                           int max_cuts, 
                           int len)
    {

        // Max_cuts is the maximum no. of 
        // allowed cuts.
        int n = arr.length;
        int start = 0;
        int i = 1;
        while (i < n) {

            // Start from covering as many holes
            // as you can from start.
            if (arr[i] - arr[start] <= 
                len) {
                i++;
            }
            else {

                // If an index is reached 
                // from where it's not possible 
                // to accomodate more elements
                // in the current subarray 
                // then end this subarray 
                // and go further.
                len = len - (arr[i - 1] - 
                             arr[start]);
                max_cuts--;
                start = i;
                i++;
            }

            // If at any point you run out 
            // of maximum subarrays or length 
            // then return false because it's
            // impossible to obtain this 
            // value of mid.
            if (max_cuts <= 0 || len <= 0)
                return false;
        }

        // Covered all subarrays within
        // the sum maxium number of subarrays
        // so return true.
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 10, 20, 70, 80 };
        int N = 4, K = 2;
        findMinTapeLength(arr, N, K);
    }
}
```

**Output**

```
20

```

***时间复杂度:** O(N*log(M))，其中 M 为数组的最大值。*
***辅助空间:** O(1)*