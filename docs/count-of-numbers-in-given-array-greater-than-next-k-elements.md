# 给定数组中大于下一个 K 元素的数字计数

> 原文:[https://www . geesforgeks . org/给定数组中大于下一个 k 元素的数字计数/](https://www.geeksforgeeks.org/count-of-numbers-in-given-array-greater-than-next-k-elements/)

给定一个大小为 **N** 的整数[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是计算其值**大于所有 **K** 元素的**右边的**元素的数量。如果第 I 个元素右边的数字少于 K，那么所有数字的值必须小于第 I 个人的值。**

**示例:**

> **输入:** arr[] = {4，3，1，2，5}，N = 5，K = 1
> **输出:** 3
> **说明:**第 1，2，5 位是值大于其右边元素的元素(由于 K = 1 只考虑下一个)。而第三个元素不能考虑，因为第四个元素的值大于第三个元素的值。
> 
> **输入:** arr[] = {9，7，7，7，4}，N = 5，K = 3
> **输出:** 3
> **说明:**第 1、4、5 个元素将是其值大于其后所有 3 个元素元素的元素。

**天真方法:**对于每个元素，检查其右侧的 K 个元素，看看它是否大于所有这些元素。

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)

**高效方法:**这个问题可以通过以下步骤解决:

*   考虑一个 [**队列**](https://www.geeksforgeeks.org/queue-data-structure/) 来存储 K 个元素。
*   将最后一个中的 K 个元素**添加到队列中，并将最后 K 个值的最大值保存在一个变量中(比如 max_value)。**
*   从位置(N–K)向后迭代剩余的数组。
    *   迭代时，从队列中弹出一个元素，并将当前元素推入队列。
    *   如果**当前元素**的值**大于**最大值，则**增加**计数，**更新**当前元素的最大值。
    *   否则如果**弹出值**与 max_value 相同**，则**从队列中找到新的 max** 。**
*   **将计数值作为其值大于其右侧所有 k 个元素的元素的计数返回。**

**下面是上述方法的实现:**

## **C++**

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find
// maximum element in queue
int find_max(queue<int> q)
{
    int ans = INT_MIN;

    // Loop to find maximum from queue
    while (!q.empty()) {
        ans = max(ans, q.front());
        q.pop();
    }
    return ans;
}

// Function to count the elements
// whose values are greater than
// all the k elements to its immediate right
int solve(int n, int k, vector<int> arr)
{
    int max_value = INT_MIN;
    queue<int> q;
    int count = 0;
    int p = n - k;

    // Checking base cases
    if (n == 0)
        return 0;
    else if (k == 0)
        return n;

    // Traversing last k elements
    for (int i = n - 1; i >= p; i--) {
        q.push(arr[i]);
        if (arr[i] > max_value) {
            max_value = arr[i];
            count++;
        }
    }

    // Traversing rest of the elements
    for (int i = p - 1; i >= 0; i--) {
        int x = q.front();
        q.pop();
        q.push(arr[i]);
        if (arr[i] > max_value) {
            count++;
            max_value = arr[i];
        }
        else {
            if (x == max_value) {
                // If popped value
                // is same as max value
                // then update max value
                max_value = find_max(q);
            }
        }
    }
    return count;
}

// Driver Code Starts.
int main()
{
    int N, K;
    N = 5;
    K = 1;
    vector<int> arr = { 4, 3, 1, 2, 5};

    cout << solve(N, K, arr) << "\n";
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code to implement the above approach
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

class GFG {

    // Function to find
    // maximum element in queue
    public static int find_max(Queue<Integer> q) {
        int ans = Integer.MIN_VALUE;

        // Loop to find maximum from queue
        while (!q.isEmpty()) {
            ans = Math.max(ans, q.peek());
            q.remove();
        }
        return ans;
    }

    // Function to count the elements
    // whose values are greater than
    // all the k elements to its immediate right
    public static int solve(int n, int k, ArrayList<Integer> arr) {
        int max_value = Integer.MIN_VALUE;
        Queue<Integer> q = new LinkedList<Integer>();
        int count = 0;
        int p = n - k;

        // Checking base cases
        if (n == 0)
            return 0;
        else if (k == 0)
            return n;

        // Traversing last k elements
        for (int i = n - 1; i >= p; i--) {
            q.add(arr.get(i));
            if (arr.get(i) > max_value) {
                max_value = arr.get(i);
                count++;
            }
        }

        // Traversing rest of the elements
        for (int i = p - 1; i >= 0; i--) {
            int x = 0;
            if (q.size() > 0) {
                x = q.peek();
                q.remove();
            }
            q.add(arr.get(i));
            if (arr.get(i) > max_value) {
                count++;
                max_value = arr.get(i);
            } else {
                if (x == max_value) {
                    // If popped value
                    // is same as max value
                    // then update max value
                    max_value = find_max(q);
                }
            }
        }
        return count;
    }

    // Driver Code Starts.
    public static void main(String args[]) {
        int N, K;
        N = 5;
        K = 1;
        ArrayList<Integer> arr = new ArrayList<>();
        arr.add(4);
        arr.add(3);
        arr.add(1);
        arr.add(2);
        arr.add(5);

        System.out.println(solve(N, K, arr));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## **蟒蛇 3**

```
# Python3 code to implement the above approach
from queue import Queue
import copy
INT_MIN = -2147483648

# Function to find
# maximum element in queue
def find_max(q):

    ans = INT_MIN

    # Loop to find maximum from queue
    while (not q.empty()):
        ans = max(ans, q.get())

    return ans

# Function to count the elements
# whose values are greater than
# all the k elements to its immediate right
def solve(n, k, arr):

    max_value = INT_MIN
    q = Queue()
    count = 0
    p = n - k

    # Checking base cases
    if (n == 0):
        return 0
    elif (k == 0):
        return n

    # Traversing last k elements
    for i in range(n - 1, p - 1, -1):
        q.put(arr[i])
        if (arr[i] > max_value):
            max_value = arr[i]
            count += 1

    # Traversing rest of the elements
    for i in range(p - 1, -1, -1):
        x = q.get()
        q.put(arr[i])

        if (arr[i] > max_value):
            count += 1
            max_value = arr[i]

        else:
            if (x == max_value):

                # If popped value is same
                # as max value then update
                # max value
                temp = Queue()
                for i in q.queue:
                    temp.put(i)

                max_value = find_max(temp)

    return count

# Driver code
if __name__ == "__main__":

    N = 5
    K = 1
    arr = [ 4, 3, 1, 2, 5 ]

    print(solve(N, K, arr))

# This code is contributed by rakeshsahni
```

## **C#**

```
// C# code to implement the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Function to find
    // maximum element in queue
    public static int find_max(Queue<int> q) {
        int ans = int.MinValue;

        // Loop to find maximum from queue
        while (q.Count != 0) {
            ans = Math.Max(ans, q.Peek());
            q.Dequeue();
        }
        return ans;
    }

    // Function to count the elements
    // whose values are greater than
    // all the k elements to its immediate right
    public static int solve(int n, int k, List<int> arr) {
        int max_value = int.MinValue;
        Queue<int> q = new Queue<int>();
        int count = 0;
        int p = n - k;

        // Checking base cases
        if (n == 0)
            return 0;
        else if (k == 0)
            return n;

        // Traversing last k elements
        for (int i = n - 1; i >= p; i--) {
            q.Enqueue(arr[i]);
            if (arr[i] > max_value) {
                max_value = arr[i];
                count++;
            }
        }

        // Traversing rest of the elements
        for (int i = p - 1; i >= 0; i--) {
            int x = 0;
            if (q.Count > 0) {
                x = q.Peek();
                q.Dequeue();
            }
            q.Enqueue(arr[i]);
            if (arr[i] > max_value) {
                count++;
                max_value = arr[i];
            } else {
                if (x == max_value) {
                    // If popped value
                    // is same as max value
                    // then update max value
                    max_value = find_max(q);
                }
            }
        }
        return count;
    }

    // Driver Code Starts.
    public static void Main(String []args) {
        int N, K;
        N = 5;
        K = 1;
        List<int> arr = new List<int>();
        arr.Add(4);
        arr.Add(3);
        arr.Add(1);
        arr.Add(2);
        arr.Add(5);

        Console.WriteLine(solve(N, K, arr));
    }
}

// This code is contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>
// Javascript code to implement the above approach

// Function to find
// maximum element in queue
function find_max(q) {
    let ans = Number.MIN_SAFE_INTEGER;

    // Loop to find maximum from queue
    while (q.length) {
        ans = Math.max(ans, q[0]);
        q.pop();
    }
    return ans;
}

// Function to count the elements
// whose values are greater than
// all the k elements to its immediate right
function solve(n, k, arr) {
    let max_value = Number.MIN_SAFE_INTEGER;
    let q = [];
    let count = 0;
    let p = n - k;

    // Checking base cases
    if (n == 0)
        return 0;
    else if (k == 0)
        return n;

    // Traversing last k elements
    for (let i = n - 1; i >= p; i--) {
        q.push(arr[i]);
        if (arr[i] > max_value) {
            max_value = arr[i];
            count++;
        }
    }

    // Traversing rest of the elements
    for (let i = p - 1; i >= 0; i--) {
        let x = q[0];
        q.pop();
        q.push(arr[i]);
        if (arr[i] > max_value) {
            count++;
            max_value = arr[i];
        }
        else {
            if (x == max_value) {
                // If popped value
                // is same as max value
                // then update max value
                max_value = find_max(q);
            }
        }
    }
    return count;
}

// Driver Code Starts.

let N, K;
N = 5;
K = 1;
let arr = [4, 3, 1, 2, 5];

document.write(solve(N, K, arr))

// This code is contributed by gfgking.
</script>
```

****Output**

```
3
```** 

****时间复杂度:**O(N)
T3】辅助空间: O(K)**

****空间优化方法:**使用[双指针方法](https://www.geeksforgeeks.org/two-pointers-technique/)可以用更小的空间解决问题。遵循下面提到的步骤。**

*   **初始化指向数组末尾的两个指针(比如“左”和“右”)。**
*   **左指针指向 K 大小窗口的起始索引，右指针指向该窗口中的最大值。**
*   **如果左指针的值大于右指针的值，则将答案计数增加 1。(因为这意味着它比它右边的所有 K 元素都大)**
*   **如果在任何时候窗口大小超过 K，将右指针减 1，并将其调整为指向当前窗口的最大值。**

**下面是上述方法的实现:**

## **C++**

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the elements
// whose values are greater than
// all k elements to its immediate right
int solve(int n, int k, vector<int> arr)
{
    int count = 1;
    int left = n - 2, right = n - 1;

    // Checking base cases
    if (n == 0)
        return 0;
    else if (k == 0)
        return n;

    // Loop to implement two-pointer approach
    for (; left >= 0; left--) {
        if (right - left > k) {
            right--;
            while (arr[left] > arr[right])
                right--;
            if (right == left)
                count++;
        }
        else if (arr[left] > arr[right]) {
            count++;
            right = left;
        }
    }

    return count;
}

// Driver Code Starts.
int main()
{
    int N, K;
    N = 5;
    K = 1;
    vector<int> arr = { 4, 3, 1, 2, 5};
    cout << solve(N, K, arr);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code to implement the above approach
import java.io.*;

class GFG{

// Function to count the elements
// whose values are greater than
// all k elements to its immediate right
static int solve(int n, int k, int[] arr)
{
    int count = 1;
    int left = n - 2, right = n - 1;

    // Checking base cases
    if (n == 0)
        return 0;
    else if (k == 0)
        return n;

    // Loop to implement two-pointer approach
    for(; left >= 0; left--)
    {
        if (right - left > k)
        {
            right--;

            while (arr[left] > arr[right])
                right--;
            if (right == left)
                count++;
        }
        else if (arr[left] > arr[right])
        {
            count++;
            right = left;
        }
    }
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int N, K;
    N = 5;
    K = 1;
    int[] arr = { 4, 3, 1, 2, 5 };

    System.out.println(solve(N, K, arr));
}
}

// This code is contributed by Potta Lokesh
```

## **蟒蛇 3**

```
# Python 3 code to implement the above approach

# Function to count the elements
# whose values are greater than
# all k elements to its immediate right
def solve(n,  k, arr):

    count = 1
    left = n - 2
    right = n - 1

    # Checking base cases
    if (n == 0):
        return 0
    elif (k == 0):
        return n

    # Loop to implement two-pointer approach
    while left >= 0:
        if (right - left > k):
            right -= 1
            while (arr[left] > arr[right]):
                right -= 1
            if (right == left):
                count += 1

        elif (arr[left] > arr[right]):
            count += 1
            right = left

        left -= 1

    return count

# Driver Code
if __name__ == "__main__":

    N = 5
    K = 1
    arr = [4, 3, 1, 2, 5]
    print(solve(N, K, arr))

    # This code is contributed by ukasp.
```

## **C#**

```
// C# code to implement the above approach
using System;

public class GFG
{

// Function to count the elements
// whose values are greater than
// all k elements to its immediate right
static int solve(int n, int k, int[] arr)
{
    int count = 1;
    int left = n - 2, right = n - 1;

    // Checking base cases
    if (n == 0)
        return 0;
    else if (k == 0)
        return n;

    // Loop to implement two-pointer approach
    for(; left >= 0; left--)
    {
        if (right - left > k)
        {
            right--;

            while (arr[left] > arr[right])
                right--;
            if (right == left)
                count++;
        }
        else if (arr[left] > arr[right])
        {
            count++;
            right = left;
        }
    }
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    int N, K;
    N = 5;
    K = 1;
    int[] arr = { 4, 3, 1, 2, 5 };

    Console.WriteLine(solve(N, K, arr));
}
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>
// javascript code to implement the above approach

// Function to count the elements
// whose values are greater than
// all k elements to its immediate right
function solve(n , k, arr)
{
    var count = 1;
    var left = n - 2, right = n - 1;

    // Checking base cases
    if (n == 0)
        return 0;
    else if (k == 0)
        return n;

    // Loop to implement two-pointer approach
    for(; left >= 0; left--)
    {
        if (right - left > k)
        {
            right--;

            while (arr[left] > arr[right])
                right--;
            if (right == left)
                count++;
        }
        else if (arr[left] > arr[right])
        {
            count++;
            right = left;
        }
    }
    return count;
}

// Driver Code
var N, K;
N = 5;
K = 1;
var arr = [ 4, 3, 1, 2, 5 ];

document.write(solve(N, K, arr));

// This code is contributed by 29AjayKumar
</script>
```

****Output**

```
3
```** 

****时间复杂度:**O(N)
T3】辅助空间: O(1)**