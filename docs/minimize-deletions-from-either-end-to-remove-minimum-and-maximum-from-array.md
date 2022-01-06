# 从任一端最小化删除，从数组中删除最小值和最大值

> 原文:[https://www . geeksforgeeks . org/最小化-从任一端删除-从阵列中删除最小和最大值/](https://www.geeksforgeeks.org/minimize-deletions-from-either-end-to-remove-minimum-and-maximum-from-array/)

给定大小为 **N、**的整数数组 **arr[]** ，任务是找到从数组中移除**最小**和**最大**元素的**最小**删除操作数。元素只能从数组的任一端删除****。****

****示例:****

> ****输入:**arr =【2，10，7，5，4，1，8，6】
> **输出:** 5
> **说明:**最小元素为 1，最大元素为 10。我们可以将删除操作可视化如下:
> 【2、10、7、5、4、1、8】**6**
> 【2、10、7、5、4、1、**8**
> 【2、10、7、5、4、**1**
> 【**2**、10、7、5、4】
> 【**
> 
> ****总共执行了 5 次删除操作。没有其他删除次数较少的序列可以删除最小值和最大值。****
> 
>  ******输入:**arr =【56】
> **输出:** 1
> **说明:**因为数组只有一个条目，所以同时作为最低值和最高值。只需一次删除，我们就可以消除它。
> 
> **输入:** arr = [2，5，8，3，6，4]
> **输出:** 3
> **说明:**最小元素为 2，最大元素为 8。我们可以将删除操作可视化如下:
> 【**2**、5、8、3、6、4】
> 【**5**、8、3、6、4】
> 【**8**、3、6、4】
> 【3、6、4】
> 
> 总共进行了 3 次删除。这是可能的最小删除次数。****

******方法:**上述问题可以通过以下观察来解决:****

****假设最大和最小元素存在于索引 I 和 j 处，反之亦然，如下所示:****

```
****[ _ _ _ _ _ min/max _ _ _ _ _ _ max/min _ _ _ _ _ _ ]**
 **<-- a -->   (i)   <---  b --->  (j)  <---- c ---->**
**<-----------------------N ------------------------->****
```

****哪里，****

*   ******i，j** :数组最大或最小元素的索引****
*   ******a** :最小(或最大)元素**距起点**的距离****
*   ******b** :最小和最大元素之间的距离****
*   ********c** :最大(或最小)元素**与终点**之间的距离******
*   ******N** :数组长度****

****现在让我们看看不同的可能删除方式:****

*   ****从开始移除一个**，从结束**移除另一个**:******

> ****删除数量=(a+c)=((I+1)+(n–j))****

*   ****为了从阵列的开始移除这两个**:******

> ****删除数量= (a + b) = (j + 1)****

*   ****为了从阵列的**端**移除它们两个**:******

> ****删除数量=(b+c)=(n–I)****

****使用上面的等式，我们现在可以很容易地使用最小和最大元素的索引来获得距离。答案是这三种情况中最少的****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ code to implement the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return
// the minimum number of deletions
int minDeletions(vector<int>& nums)
{
    int n = nums.size();

    // Index of minimum element
    int minindex
      = min_element(nums.begin(), nums.end())
                   - nums.begin();

    // Index of maximum element
    int maxindex
      = max_element(nums.begin(), nums.end())
                   - nums.begin();

    // Assume that minimum element
    // always occur before maximum element.
    // If not, then swap its index.
    if (minindex > maxindex)
        swap(minindex, maxindex);

    // Deletion operations for case-1
    int bothend = (minindex + 1) +
      (n - maxindex);

    // Deletion operations for case-2
    int frontend = (maxindex + 1);

    // Deletion operations for case-3
    int backend = (n - minindex);

    // Least number of deletions is the answer
    int ans = min(bothend,
                  min(frontend, backend));

    return ans;
}

// Driver code
int main()
{
    vector<int> arr{ 2, 10, 7, 5, 4, 1, 8, 6 };
    cout << minDeletions(arr) << endl;

    vector<int> arr2{ 56 };
    cout << minDeletions(arr2);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java code to implement the above approach
import java.util.Arrays;
import java.util.stream.IntStream;

class GFG{

// Function to return the
// minimum number of deletions
int minDeletions(int[] nums)
{
    int n = nums.length;

    // Index of minimum element
    int minindex = findIndex(nums,
    Arrays.stream(nums).min().getAsInt());

    // Index of maximum element
    int maxindex = findIndex(
        nums, Arrays.stream(nums).max().getAsInt());

    // Assume that minimum element
    // always occur before maximum element.
    // If not, then swap its index.
    if (minindex > maxindex)
    {
        minindex = minindex + maxindex;
        maxindex = minindex - maxindex;
        minindex = minindex - maxindex;
    }

    // Deletion operations for case-1
    int bothend = (minindex + 1) + (n - maxindex);

    // Deletion operations for case-2
    int frontend = (maxindex + 1);

    // Deletion operations for case-3
    int backend = (n - minindex);

    // Least number of deletions is the answer
    int ans = Math.min(
        bothend, Math.min(frontend, backend));

    return ans;
}

// Function to find the index of an element
public static int findIndex(int arr[], int t)
{
    int len = arr.length;
    return IntStream.range(0, len)
        .filter(i -> t == arr[i])
        .findFirst() // first occurrence
        .orElse(-1); // No element found
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 2, 10, 7, 5, 4, 1, 8, 6 };
    System.out.print(new GFG().minDeletions(arr) + "\n");

    int []arr2 = { 56 };
    System.out.print(new GFG().minDeletions(arr2));
}
}

// This code is contributed by 29AjayKumar**
```

## ****蟒蛇 3****

```
**# Python 3 code to implement the above approach

# Function to return
# the minimum number of deletions
def minDeletions(nums):

    n = len(nums)

    # Index of minimum element
    minindex = nums.index(min(nums))

    # Index of maximum element
    maxindex = nums.index(max(nums))

    # Assume that minimum element
    # always occur before maximum element.
    # If not, then swap its index.
    if (minindex > maxindex):
        minindex, maxindex = maxindex, minindex

    # Deletion operations for case-1
    bothend = (minindex + 1) + (n - maxindex)

    # Deletion operations for case-2
    frontend = (maxindex + 1)

    # Deletion operations for case-3
    backend = (n - minindex)

    # Least number of deletions is the answer
    ans = min(bothend,
              min(frontend, backend))

    return ans

# Driver code
if __name__ == "__main__":

    arr = [2, 10, 7, 5, 4, 1, 8, 6]
    print(minDeletions(arr))

    arr2 = [56]
    print(minDeletions(arr2))

    # This code is contributed by ukasp.**
```

## ****C#****

```
**// C# code to implement the above approach
using System;
using System.Linq;

public class GFG{

// Function to return the
// minimum number of deletions
int minDeletions(int[] nums)
{
    int n = nums.Length;

    // Index of minimum element
    int minindex = findIndex(nums,
    nums.Min());

    // Index of maximum element
    int maxindex = findIndex(
        nums, nums.Max());

    // Assume that minimum element
    // always occur before maximum element.
    // If not, then swap its index.
    if (minindex > maxindex)
    {
        minindex = minindex + maxindex;
        maxindex = minindex - maxindex;
        minindex = minindex - maxindex;
    }

    // Deletion operations for case-1
    int bothend = (minindex + 1) + (n - maxindex);

    // Deletion operations for case-2
    int frontend = (maxindex + 1);

    // Deletion operations for case-3
    int backend = (n - minindex);

    // Least number of deletions is the answer
    int ans = Math.Min(
        bothend, Math.Min(frontend, backend));

    return ans;
}

// Function to find the index of an element
public static int findIndex(int []arr, int t)
{
    int len = arr.Length;
    return  Array.IndexOf(arr, t);
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { 2, 10, 7, 5, 4, 1, 8, 6 };
    Console.Write(new GFG().minDeletions(arr) + "\n");

    int []arr2 = { 56 };
    Console.Write(new GFG().minDeletions(arr2));
}
}

// This code is contributed by 29AjayKumar**
```

## ****java 描述语言****

```
**<script>
    // JavaScript code to implement the above approach

    // Function to return
    // the minimum number of deletions
    const minDeletions = (nums) => {
        let n = nums.length;

        // Index of minimum element
        let minindex = nums.indexOf(Math.min(...nums));

        // Index of maximum element
        let maxindex = nums.indexOf(Math.max(...nums));

        // Assume that minimum element
        // always occur before maximum element.
        // If not, then swap its index.
        if (minindex > maxindex) {
            let temp = minindex;
            minindex = maxindex;
            maxindex = temp;
        }

        // Deletion operations for case-1
        let bothend = (minindex + 1) + (n - maxindex);

        // Deletion operations for case-2
        let frontend = (maxindex + 1);

        // Deletion operations for case-3
        let backend = (n - minindex);

        // Least number of deletions is the answer
        let ans = Math.min(bothend, Math.min(frontend, backend));

        return ans;
    }

    // Driver code
    let arr = [2, 10, 7, 5, 4, 1, 8, 6];
    document.write(`${minDeletions(arr)}<br/>`);

    let arr2 = [56];
    document.write(minDeletions(arr2));

    // This code is contributed by rakeshsahni

</script>**
```

******Output**

```
5
1
```**** 

******时间复杂度:**O(N)
T3】辅助空间: O(1)****