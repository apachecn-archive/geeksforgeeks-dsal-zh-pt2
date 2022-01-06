# 通过移除对并用它们的平均值替换它们来最小化剩余的数组元素

> 原文:[https://www . geeksforgeeks . org/通过移除对并用它们的平均值替换它们来最小化剩余的数组元素/](https://www.geeksforgeeks.org/minimize-remaining-array-element-by-removing-pairs-and-replacing-them-with-their-average/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过从数组中重复移除一对，比如 **(arr[i]，arr[j])** 并插入它们平均值的[上限值](https://www.geeksforgeeks.org/find-ceil-ab-without-using-ceil-function/)来找到最小可能的剩余数组元素。

**示例:**

> **输入:** arr[] = { 1，2，3 }
> **输出:**
> **解释:**
> 从 arr[]中移除对(arr[1]，arr[2])并将(arr[1] + arr[2] + 1) / 2 插入 arr[]将 arr[]修改为{ 1，2 }。
> 从 arr[]中移除对(arr[0]，arr[1])并将(arr[0] + arr[1] + 1) / 2 插入 arr[]将 arr[]修改为{ 2 }。
> 因此，要求输出为 2。
> 
> **输入:** arr[] = { 30，16，40 }
> **输出:** 26
> **解释:**
> 从 arr[]中移除对(arr[0]，arr[2])并将(arr[0] + arr[2] + 1) / 2 插入 arr[]将 arr[]修改为{ 16，35 }。
> 从 arr[]中移除对(arr[0]，arr[1])并将(arr[0] + arr[1] + 1) / 2 插入 arr[]将 arr[]修改为{ 26 }。
> 因此，所需输出为 26。

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。其思想是重复移除第一个和第二个最大的数组元素，并插入它们的平均值。最后，打印数组中剩余的最小元素。

*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)，比如说 **PQ** ，来存储数组元素，这样最大的元素总是出现在 **PQ** 的顶部。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将所有数组元素存储在 **PQ** 中。
*   [迭代**优先级队列**](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/) 的元素，而**优先级队列**中的元素计数大于 **1** 。在每次迭代中，[从 **PQ** 弹出](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)前两个元素，并插入它们平均值的**上限值**。
*   最后打印 **PQ** 中剩下的元素。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest element
// left in the array by removing pairs
// and inserting their average
int findSmallestNumLeft(int arr[], int N)
{
    // Stores array elements such that the
    // largest element present at top of PQ
    priority_queue<int> PQ;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Insert arr[i] into PQ
        PQ.push(arr[i]);
    }

    // Iterate over elements of PQ while count
    // of elements in PQ greater than 1
    while (PQ.size() > 1) {

        // Stores largest element of PQ
        int top1 = PQ.top();

        // Pop the largest element of PQ
        PQ.pop();

        // Stores largest element of PQ
        int top2 = PQ.top();

        // Pop the largest element of PQ
        PQ.pop();

        // Insert the ceil value of average
        // of top1 and top2
        PQ.push((top1 + top2 + 1) / 2);
    }

    return PQ.top();
}

// Driver Code
int main()
{
    int arr[] = { 30, 16, 40 };
    int N = sizeof(arr)
            / sizeof(arr[0]);

    cout << findSmallestNumLeft(
        arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.PriorityQueue;

class GFG{

// Function to find the smallest element
// left in the array by removing pairs
// and inserting their average
static int findSmallestNumLeft(int arr[], int N)
{

    // Stores array elements such that the
    // largest element present at top of PQ
    PriorityQueue<Integer> PQ = new PriorityQueue<Integer>((a,b)->b-a);

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // Insert arr[i] into PQ
        PQ.add(arr[i]);
    }

    // Iterate over elements of PQ while count
    // of elements in PQ greater than 1
    while (PQ.size() > 1)
    {

        // Stores largest element of PQ
        int top1 = PQ.peek();

        // Pop the largest element of PQ
        PQ.remove();

        // Stores largest element of PQ
        int top2 = PQ.peek();

        // Pop the largest element of PQ
        PQ.remove();

        // Insert the ceil value of average
        // of top1 and top2
        PQ.add((top1 + top2 + 1) / 2);
    }

    return PQ.peek();
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 30, 16, 40 };
    int N = arr.length;

    System.out.print(findSmallestNumLeft(
        arr, N));

}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the smallest element
# left in the array by removing pairs
# and inserting their average
def findSmallestNumLeft(arr, N):

    # Stores array elements such that the
    # largest element present at top of PQ
    PQ = []

    # Traverse the array
    for i in range(N):

        # Insert arr[i] into PQ
        PQ.append(arr[i])

    # Iterate over elements of PQ while count
    # of elements in PQ greater than 1
    PQ = sorted(PQ)

    while (len(PQ) > 1):

        # Stores largest element of PQ
        top1 = PQ[-1]

        # Pop the largest element of PQ
        del PQ[-1]

        # Stores largest element of PQ
        top2 = PQ[-1]

        # Pop the largest element of PQ
        del PQ[-1]

        # Insert the ceil value of average
        # of top1 and top2
        PQ.append((top1 + top2 + 1) // 2)
        PQ = sorted(PQ)

    return PQ[-1]

# Driver Code
if __name__ == '__main__':

    arr = [ 30, 16, 40 ]
    N = len(arr)

    print (findSmallestNumLeft(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GfG
{
    // Function to find the smallest element
    // left in the array by removing pairs
    // and inserting their average
    static int findSmallestNumLeft(int[] arr, int N)
    {
        // Stores array elements such that the
        // largest element present at top of PQ
        List<int> PQ = new List<int>();

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Insert arr[i] into PQ
            PQ.Add(arr[i]);
        }

        PQ.Sort();
        PQ.Reverse();

        // Iterate over elements of PQ while count
        // of elements in PQ greater than 1
        while (PQ.Count > 1) {

            // Stores largest element of PQ
            int top1 = PQ[0];

            // Pop the largest element of PQ
            PQ.RemoveAt(0);

            // Stores largest element of PQ
            int top2 = PQ[0];

            // Pop the largest element of PQ
            PQ.RemoveAt(0);

            // Insert the ceil value of average
            // of top1 and top2
            PQ.Add((top1 + top2 + 1) / 2);

            PQ.Sort();
            PQ.Reverse();
        }

        return PQ[0];
    }

  // Driver code
    public static void Main()
    {
        int[] arr = { 30, 16, 40 };
        int N = arr.Length;

        Console.Write(findSmallestNumLeft(arr, N));
    }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the smallest element
// left in the array by removing pairs
// and inserting their average
function  findSmallestNumLeft(arr, N)
{

    // Stores array elements such that the
    // largest element present at top of PQ
    let PQ = [];

    // Traverse the array
    for (let i = 0; i < N; i++)
    {

        // Insert arr[i] into PQ
        PQ.push(arr[i]);
    }

    PQ.sort(function(a,b){return b-a;});

    // Iterate over elements of PQ while count
    // of elements in PQ greater than 1
    while (PQ.length > 1)
    {

        // Stores largest element of PQ
        let top1 = PQ[0];

        // Pop the largest element of PQ
        PQ.shift();

        // Stores largest element of PQ
        let top2 = PQ[0];

        // Pop the largest element of PQ
        PQ.shift();

        // Insert the ceil value of average
        // of top1 and top2
        PQ.push(Math.floor((top1 + top2 + 1) / 2));
        PQ.sort(function(a,b){return b-a;});
    }

    return PQ[0];
}

// Driver Code
let arr = [ 30, 16, 40];
let N = arr.length;
document.write(findSmallestNumLeft(
        arr, N));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
26
```

***时间复杂度:*** O(N * log(N))
***辅助空间:*** O(N)