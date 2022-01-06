# 最小化数组中相邻元素之间的最大差异

> 原文:[https://www . geeksforgeeks . org/最小化数组中相邻元素之间的最大差异/](https://www.geeksforgeeks.org/minimize-the-maximum-difference-between-adjacent-elements-in-an-array/)

给定非递减数组 **arr[]** 和整数 **K** ，任务是从数组中移除 **K** 元素，使得相邻元素之间的最大差异最小。
**注:**K<N–2

**示例:**

> **输入:** arr[] = {3，7，8，10，14}，K = 2
> **输出:** 2
> **说明:**
> 去掉元素 A[0]和 A[4]后，
> 相邻元素最大差值最小。
> 去掉元素后，剩下的数组是[7，8，10]
> 
> **输入:** arr[] = [12，16，22，31，31，38]，K = 3
> **输出:** 6
> **解释:**
> 去掉元素 A[3]、A[4]和 A[5]后，
> 相邻元素之间的最大差值最小。
> 去掉元素后，剩下的数组是[12，16，22]

**方法一:蛮力**思路是[生成大小数组**N–K**的子集](https://www.geeksforgeeks.org/finding-all-subsets-of-a-given-set-in-java/)，同时计算每个子序列中相邻元素的最大差值。最后，找出这种最大差异的最小值。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum of the maximum difference
// of the adjacent elements after
// removing K elements from the array

#include <bits/stdc++.h>

using namespace std;

// Function to find the minimum
// of the maximum difference of the
// adjacent elements after removing
// K elements from the array
int minimumAdjacentDifference(vector<int> a,
                        int n, int k)
{
    // Initialising the
    // minimum difference
    int minDiff = INT_MAX;

    // Traversing over subsets
    // in iterative manner
    for (int i = 0; i < (1 << n); i++) {

        // Number of elements to
        // be taken in the subset
        // ON bits of i represent
        // elements not to be removed
        int cnt = __builtin_popcount(i);

        // If the removed
        // set is of size k
        if (cnt == n - k) {

            // Creating the new array
            // after removing elements
            vector<int> temp;
            for (int j = 0; j < n; j++) {
                if ((i & (1 << j)) != 0)
                    temp.push_back(a[j]);
            }
            // Maximum difference of adjacent
            // elements of remaining array
            int maxDiff = INT_MIN;
            for (int j = 0; j < temp.size() - 1; j++) {
                maxDiff = max(maxDiff,
                   temp[j + 1] - temp[j]);
            }
            minDiff = min(minDiff, maxDiff);
        }
    }
    return minDiff;
}

// Driver Code
int main()
{
    int n = 5;
    int k = 2;

    vector<int> a= { 3, 7, 8, 10, 14 };

    cout << minimumAdjacentDifference(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum of the maximum difference
// of the adjacent elements after
// removing K elements from the array
import java.util.*;

class GFG{

    // Function to find the minimum
    // of the maximum difference of the
    // adjacent elements after removing
    // K elements from the array
    static int minimumAdjacentDifference(int a[],
                            int n, int k)
    {
        // Initialising the
        // minimum difference
        int minDiff = Integer.MAX_VALUE;

        // Traversing over subsets
        // in iterative manner
        for (int i = 0; i < (1 << n); i++) {

            // Number of elements to
            // be taken in the subset
            // ON bits of i represent
            // elements not to be removed
            int cnt = Integer.bitCount(i);

            // If the removed
            // set is of size k
            if (cnt == n - k) {

                // Creating the new array
                // after removing elements
                 Vector<Integer> temp = new Vector<Integer>();
                for (int j = 0; j < n; j++) {
                    if ((i & (1 << j)) != 0)
                        temp.add(a[j]);
                }

                // Maximum difference of adjacent
                // elements of remaining array
                int maxDiff = Integer.MIN_VALUE;
                for (int j = 0; j < temp.size() - 1; j++) {
                    maxDiff = Math.max(maxDiff,
                    temp.get(j + 1) - temp.get(j));
                }
                minDiff = Math.min(minDiff, maxDiff);
            }
        }
        return minDiff;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 5;
        int k = 2;

        int a[] = { 3, 7, 8, 10, 14 };

        System.out.println(minimumAdjacentDifference(a, n, k));
    }
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum of the maximum difference
# of the adjacent elements after
# removing K elements from the array
import sys

INT_MAX = sys.maxsize;
INT_MIN = -(sys.maxsize - 1)

# Function to find the minimum
# of the maximum difference of the
# adjacent elements after removing
# K elements from the array
def minimumAdjacentDifference(a, n, k) :

    # Initialising the
    # minimum difference
    minDiff = INT_MAX;

    # Traversing over subsets
    # in iterative manner
    for i in range( 1<<n) :

        # Number of elements to
        # be taken in the subset
        # ON bits of i represent
        # elements not to be removed
        cnt = bin(i).count('1');

        # If the removed
        # set is of size k
        if (cnt == n - k) :

            # Creating the new array
            # after removing elements
            temp = [];
            for j in range(n) :
                if ((i & (1 << j)) != 0) :
                    temp.append(a[j]);

            # Maximum difference of adjacent
            # elements of remaining array
            maxDiff = INT_MIN;

            for j in range(len(temp) - 1) :
                maxDiff = max(maxDiff, temp[j + 1] - temp[j]);

            minDiff = min(minDiff, maxDiff);

    return minDiff;

# Driver Code
if __name__ == "__main__" :

    n = 5;
    k = 2;

    a = [ 3, 7, 8, 10, 14 ];

    print(minimumAdjacentDifference(a, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find the
// minimum of the maximum difference
// of the adjacent elements after
// removing K elements from the array
using System;
using System.Collections.Generic;

class GFG{

    // Function to find the minimum
    // of the maximum difference of the
    // adjacent elements after removing
    // K elements from the array
    static int minimumAdjacentDifference(int []a,
                            int n, int k)
    {
        // Initialising the
        // minimum difference
        int minDiff = int.MaxValue;

        // Traversing over subsets
        // in iterative manner
        for (int i = 0; i < (1 << n); i++) {

            // Number of elements to
            // be taken in the subset
            // ON bits of i represent
            // elements not to be removed
            int cnt = countSetBits(i);

            // If the removed
            // set is of size k
            if (cnt == n - k) {

                // Creating the new array
                // after removing elements
                 List<int> temp = new List<int>();
                for (int j = 0; j < n; j++) {
                    if ((i & (1 << j)) != 0)
                        temp.Add(a[j]);
                }

                // Maximum difference of adjacent
                // elements of remaining array
                int maxDiff = int.MinValue;
                for (int j = 0; j < temp.Count - 1; j++) {
                    maxDiff = Math.Max(maxDiff,
                    temp[j + 1] - temp[j]);
                }
                minDiff = Math.Min(minDiff, maxDiff);
            }
        }
        return minDiff;
    }
     static int countSetBits(int x)
     {
         int setBits = 0;
         while (x != 0) {
             x = x & (x - 1);
             setBits++;
         }
         return setBits;
     }
    // Driver Code
    public static void Main(String []args)
    {
        int n = 5;
        int k = 2;

        int []a = { 3, 7, 8, 10, 14 };

        Console.WriteLine(minimumAdjacentDifference(a, n, k));
    }
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// minimum of the maximum difference
// of the adjacent elements after
// removing K elements from the array
function countSetBits(x)
{
    let setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Function to find the minimum
// of the maximum difference of the
// adjacent elements after removing
// K elements from the array
function minimumAdjacentDifference(a, n, k)
{

    // Initialising the
    // minimum difference
    let minDiff = Number.MAX_VALUE;

    // Traversing over subsets
    // in iterative manner
    for(let i = 0; i < (1 << n); i++)
    {

        // Number of elements to
        // be taken in the subset
        // ON bits of i represent
        // elements not to be removed
        let cnt = countSetBits(i);

        // If the removed
        // set is of size k
        if (cnt == n - k)
        {

            // Creating the new array
            // after removing elements
              let temp = [];
            for(let j = 0; j < n; j++)
            {
                if ((i & (1 << j)) != 0)
                    temp.push(a[j]);
            }

            // Maximum difference of adjacent
            // elements of remaining array
            let maxDiff = Number.MIN_VALUE;
            for(let j = 0; j < temp.length - 1; j++)
            {
                maxDiff = Math.max(
                    maxDiff, temp[j + 1] - temp[j]);
            }
            minDiff = Math.min(minDiff, maxDiff);
        }
    }
    return minDiff;
}

// Driver code
let n = 5;
let k = 2;
let a = [ 3, 7, 8, 10, 14 ];

document.write(minimumAdjacentDifference(a, n, k));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(2<sup>N</sup>* N)
T5】辅助空间:O(N)
T8】方法二:最优进场

*   仔细观察，可以注意到，如果从数组之间的某个地方移除元素(即不是末端元素)，那么剩余元素的最大差异只能增加或保持不变。
    **例如:**

```
Let the given array be {1, 5, 6},

If we remove the element 5(not the end element), 
then the maximum difference will always increase.

Therefore, It is always better to remove end elements.
```

*   这意味着移除 K 个元素后得到的阵列将是大小为 N–K 的原始阵列的子阵列
*   因此，我们可以迭代所有大小为 N–K 的[子阵列，并为每个子阵列找到相邻元素之间的最大差异。最后求相邻元素所有最大差的最小值。](https://www.geeksforgeeks.org/subarray-of-size-k-with-given-sum/)

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum of the maximum difference
// of the adjacent elements after
// removing K elements from the array

#include <bits/stdc++.h>

using namespace std;

// Function to find the minimum
// of the maximum difference of the
// adjacent elements after removing
// K elements from the array
int minimumAdjacentDifference(vector<int> a,
                        int n, int k)
{
    // Initialising the
    // minimum difference
    int minDiff = INT_MAX;

    // Iterating over all
    // subarrays of size n-k
    for (int i = 0; i <= k; i++) {

        // Maximum difference after
        // removing elements
        int maxDiff = INT_MIN;
        for (int j = 0; j < n - k - 1; j++) {
            for (int p = i; p <= i + j; p++) {
                maxDiff = max(maxDiff,
                     a[p + 1] - a[p]);
            }
        }
        // Minimum Adjacent Difference
        minDiff = min(minDiff, maxDiff);
    }
    return minDiff;
}

// Driver Code
int main()
{
    int n = 5;
    int k = 2;

    vector<int> a = { 3, 7, 8, 10, 14 };

    cout << minimumAdjacentDifference(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum of the maximum difference
// of the adjacent elements after
// removing K elements from the array
class GFG {

    // Function to find the minimum
    // of the maximum difference of the
    // adjacent elements after removing
    // K elements from the array
    static int minimumAdjacentDifference(int a[],
                            int n, int k)
    {
        // Initialising the
        // minimum difference
        int minDiff = Integer.MAX_VALUE;

        // Iterating over all
        // subarrays of size n-k
        for (int i = 0; i <= k; i++) {

            // Maximum difference after
            // removing elements
            int maxDiff = Integer.MIN_VALUE;
            for (int j = 0; j < n - k - 1; j++) {
                for (int p = i; p <= i + j; p++) {
                    maxDiff = Math.max(maxDiff,
                        a[p + 1] - a[p]);
                }
            }

            // Minimum Adjacent Difference
            minDiff = Math.min(minDiff, maxDiff);
        }
        return minDiff;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 5;
        int k = 2;

        int []a = { 3, 7, 8, 10, 14 };

        System.out.println(minimumAdjacentDifference(a, n, k));
    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum of the maximum difference
# of the adjacent elements after
# removing K elements from the array
import sys

INT_MAX = sys.maxsize;
INT_MIN = -(sys.maxsize - 1);

# Function to find the minimum
# of the maximum difference of the
# adjacent elements after removing
# K elements from the array
def minimumAdjacentDifference(a, n, k) :

    # Initialising the
    # minimum difference
    minDiff = INT_MAX;

    # Iterating over all
    # subarrays of size n-k
    for i in range(k + 1) :

        # Maximum difference after
        # removing elements
        maxDiff = INT_MIN;
        for j in range( n - k - 1) :
            for p in range(i, i + j + 1) :
                maxDiff = max(maxDiff, a[p + 1] - a[p]);

        # Minimum Adjacent Difference
        minDiff = min(minDiff, maxDiff);

    return minDiff;

# Driver Code
if __name__ == "__main__" :

    n = 5;
    k = 2;

    a = [ 3, 7, 8, 10, 14 ];

    print(minimumAdjacentDifference(a, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find the
// minimum of the maximum difference
// of the adjacent elements after
// removing K elements from the array
using System;

class GFG {

    // Function to find the minimum
    // of the maximum difference of the
    // adjacent elements after removing
    // K elements from the array
    static int minimumAdjacentDifference(int []a,
                            int n, int k)
    {
        // Initialising the
        // minimum difference
        int minDiff = int.MaxValue;

        // Iterating over all
        // subarrays of size n-k
        for (int i = 0; i <= k; i++) {

            // Maximum difference after
            // removing elements
            int maxDiff = int.MinValue;
            for (int j = 0; j < n - k - 1; j++) {
                for (int p = i; p <= i + j; p++) {
                    maxDiff = Math.Max(maxDiff,
                        a[p + 1] - a[p]);
                }
            }

            // Minimum Adjacent Difference
            minDiff = Math.Min(minDiff, maxDiff);
        }
        return minDiff;
    }

    // Driver Code
    public static void Main (string[] args)
    {
        int n = 5;
        int k = 2;

        int []a = { 3, 7, 8, 10, 14 };

        Console.WriteLine(minimumAdjacentDifference(a, n, k));
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// minimum of the maximum difference
// of the adjacent elements after
// removing K elements from the array

    // Function to find the minimum
    // of the maximum difference of the
    // adjacent elements after removing
    // K elements from the array
    function minimumAdjacentDifference(a,n,k)
    {
        // Initialising the
        // minimum difference
        let minDiff = Number.MAX_VALUE;

        // Iterating over all
        // subarrays of size n-k
        for (let i = 0; i <= k; i++) {

            // Maximum difference after
            // removing elements
            let maxDiff = Number.MIN_VALUE;
            for (let j = 0; j < n - k - 1; j++) {
                for (let p = i; p <= i + j; p++) {
                    maxDiff = Math.max(maxDiff,
                        a[p + 1] - a[p]);
                }
            }

            // Minimum Adjacent Difference
            minDiff = Math.min(minDiff, maxDiff);
        }
        return minDiff;
    }

    // Driver Code

        let n = 5;
        let k = 2;

        let a = [ 3, 7, 8, 10, 14 ];

        document.write(minimumAdjacentDifference(a, n, k));

// This code is contributed by sravan

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N * K<sup>2</sup>)
T5】辅助空间: O(1)

**方法 3:高效方法**

*   利用方法 2 的思想，我们需要找到 N–K 大小的所有子阵列的最大相邻元素差的最小值，如果我们创建一个差阵列，即初始阵列的相邻元素差的阵列，那么我们所需要做的就是找到这个差阵列的 N–K–1 大小的所有子阵列的最大值的最小元素(因为这个最大值将代表原始阵列的 N–K 大小的子阵列的最大相邻差)。

*   为了执行这个操作，我们可以使用双端队列的滑动窗口方法。参考[滑动窗口最大值(大小为 K 的所有子阵列的最大值)](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)了解该方法。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum of the maximum difference
// of the adjacent elements after
// removing K elements from the array

#include <bits/stdc++.h>

using namespace std;

// Function to find the minimum
// different in the subarrays
// of size K in the array
int findKMin(vector<int> arr, int n, int k)
{
    // Create a Double Ended Queue, Qi
    // that will store indexes
    // of array elements, queue will
    // store indexes of useful elements
    // in every window
    deque<int> Qi(k);

    // Process first k (or first window)
    // elements of array
    int i;
    for (i = 0; i < k; ++i) {
        // For every element,
        // the previous smaller elements
        // are useless so remove them from Qi
        while ((!Qi.empty()) &&
               arr[i] >= arr[Qi.back()])
            Qi.pop_back(); // Remove from rear

        // Add new element at rear of queue
        Qi.push_back(i);
    }

    int minDiff = INT_MAX;

    // Process rest of the elements,
    // i.e., from arr[k] to arr[n-1]
    for (; i < n; ++i) {
        // The element at the front
        // of the queue is the largest
        //  element of previous window
        minDiff = min(minDiff, arr[Qi.front()]);

        // Remove the elements
        // which are out of this window
        while ((!Qi.empty()) && Qi.front() <= i - k)
            Qi.pop_front();

        // Remove all elements smaller
        // than the currently being
        // added element (remove useless elements)
        while ((!Qi.empty()) &&
                arr[i] >= arr[Qi.back()])
            Qi.pop_back();

        // Add current element
        // at the rear of Qi
        Qi.push_back(i);
    }

    // compare the maximum
    // element of last window
    minDiff = min(minDiff, arr[Qi.front()]);
    return minDiff;
}

// Function to find the minimum
// of the maximum difference of the
// adjacent elements after removing
// K elements from the array
int minimumAdjacentDifference(vector<int> a,
                          int n, int k)
{

    // Create the difference array
    vector<int> diff(n-1);
    for (int i = 0; i < n - 1; i++) {
        diff[i] = a[i + 1] - a[i];
    }

    // find minimum of all maximum
    // of subarray sizes n - k - 1
    int answer = findKMin(diff,
                  n - 1, n - k - 1);
    return answer;
}

// Driver Code
int main()
{
    int n = 5;
    int k = 2;

    vector<int> a= { 3, 7, 8, 10, 14 };

    cout << minimumAdjacentDifference(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum of the maximum difference
// of the adjacent elements after
// removing K elements from the array
import java.util.*;
import java.lang.*;

class GFG{

// Function to find the minimum
// different in the subarrays
// of size K in the array
static int findKMin(int arr[], int n, int k)
{

    // Create a Double Ended Queue, Qi
    // that will store indexes
    // of array elements, queue will
    // store indexes of useful elements
    // in every window
    Deque<Integer> Qi = new LinkedList<>();

    // Process first k (or first window)
    // elements of array
    int i;
    for(i = 0; i < k; ++i)
    {

        // For every element,
        // the previous smaller elements
        // are useless so remove them from Qi
        while ((!Qi.isEmpty()) &&
               arr[i] >= arr[Qi.peekLast()])

            // Remove from rear
            Qi.pollLast();

        // Add new element at rear of queue
        Qi.addLast(i);
    }

    int minDiff = Integer.MAX_VALUE;

    // Process rest of the elements,
    // i.e., from arr[k] to arr[n-1]
    for(; i < n; ++i)
    {

        // The element at the front
        // of the queue is the largest
        //  element of previous window
        minDiff = Math.min(minDiff,
                           arr[Qi.peekFirst()]);

        // Remove the elements
        // which are out of this window
        while ((!Qi.isEmpty()) &&
                 Qi.peekFirst() <= i - k)
            Qi.pollFirst();

        // Remove all elements smaller
        // than the currently being
        // added element (remove useless elements)
        while ((!Qi.isEmpty()) &&
                arr[i] >= arr[Qi.peekLast()])
            Qi.pollLast();

        // Add current element
        // at the rear of Qi
        Qi.addLast(i);
    }

    // Compare the maximum
    // element of last window
    minDiff = Math.min(minDiff,
                       arr[Qi.peekFirst()]);
    return minDiff;
}

// Function to find the minimum
// of the maximum difference of the
// adjacent elements after removing
// K elements from the array
static int minimumAdjacentDifference(int a[],
                                     int n, int k)
{

    // Create the difference array
    int[] diff = new int[n - 1];
    for(int i = 0; i < n - 1; i++)
    {
        diff[i] = a[i + 1] - a[i];
    }

    // find minimum of all maximum
    // of subarray sizes n - k - 1
    int answer = findKMin(diff,
                          n - 1,
                          n - k - 1);
    return answer;
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    int k = 2;

    int a[] = { 3, 7, 8, 10, 14 };

    System.out.println(minimumAdjacentDifference(a, n, k));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum of the maximum difference
# of the adjacent elements after
# removing K elements from the array
import sys

# Function to find the minimum
# different in the subarrays
# of size K in the array
def findKMin(arr, n, k):

    # Create a Double Ended Queue, Qi
    # that will store indexes
    # of array elements, queue will
    # store indexes of useful elements
    # in every window
    Qi = []

    # Process first k (or first window)
    # elements of array
    i = 0

    for j in range(k):

        # For every element,
        # the previous smaller elements
        # are useless so remove them from Qi
        while ((len(Qi) != 0) and
                 arr[i] >= arr[Qi[-1]]):
            Qi.pop() # Remove from rear

        # Add new element at rear of queue
        Qi.append(i)
        i += 1

    minDiff = sys.maxsize;

    # Process rest of the elements,
    # i.e., from arr[k] to arr[n-1]
    for j in range(i, n):

        # The element at the front
        # of the queue is the largest
        #  element of previous window
        minDiff = min(minDiff, arr[Qi[0]])

        # Remove the elements
        # which are out of this window
        while ((len(Qi) != 0) and
                  Qi[0] <= i - k):
            Qi.pop(0)

        # Remove all elements smaller
        # than the currently being
        # added element (remove
        # useless elements)
        while ((len(Qi) != 0) and
                 arr[i] >= arr[Qi[-1]]):
            Qi.pop()

        # Add current element
        # at the rear of Qi
        Qi.append(i)
        i += 1

    # Compare the maximum
    # element of last window
    minDiff = min(minDiff, arr[Qi[0]])

    return minDiff

# Function to find the minimum
# of the maximum difference of the
# adjacent elements after removing
# K elements from the array
def minimumAdjacentDifference(a, n, k):

    # Create the difference array
    diff = [0 for i in range(n - 1)]

    for i in range(n - 1):
        diff[i] = a[i + 1] - a[i]

    # Find minimum of all maximum
    # of subarray sizes n - k - 1
    answer = findKMin(diff, n - 1,
                        n - k - 1)
    return answer

# Driver code   
if __name__=="__main__":

    n = 5
    k = 2

    a = [ 3, 7, 8, 10, 14 ]

    print(minimumAdjacentDifference(a, n, k))

# This code is contributed by rutvik_56
```

**Output:** 

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)