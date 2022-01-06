# 最多改变 k 个“0”形成的“1”的最长子段|集合 2(使用队列)

> 原文:[https://www . geeksforgeeks . org/最长-1s 子段-通过最多改变 k-0s-set-2-使用队列形成/](https://www.geeksforgeeks.org/longest-subsegment-of-1s-formed-by-changing-at-most-k-0s-set-2-using-queue/)

给定一个二进制数组 **a[]** 和一个数字 **k** ，我们需要通过最多改变**k****【0】s**来找到**1 的最长子段**的**长度**。

**示例:**

> **输入** : a[] = {1，0，0，1，1，0，1}，k = 1
> **输出** : 4
> **说明**:这里我们只需要改变 1 零(0)。我们可以得到的最大可能长度是通过改变数组中的第三个零，我们得到一个[] = {1，0，0，1，1，1，1}
> 
> **输入** : a[] = {1，0，0，1，0，1，0，1，0，1}，k = 2
> **输出** : 5

**双指针进场:**关于双指针进场的实施，请参考本文的[集 1。](https://www.geeksforgeeks.org/longest-subsegment-1s-formed-changing-k-0s/) 

**队列方式:**任务可以借助[队列](https://www.geeksforgeeks.org/queue-data-structure/)解决。将目前遇到的 **0s** 的**指数**存储在**队列**中。对于每个 **0** ，检查 **K** 的值是否大于 0**如果是**非零**，**翻转**到 **1** ，并且**相应地最大化**子段**的**长度，否则**将左指针(最初在字符串的起始索引处)移动**到
按照以下步骤解决问题:**

*   声明一个队列，用于存储已访问的 **0s** 的**索引**。
*   遍历字符串，如果**当前的**字符是 **0** 并且还剩下一些法术，即 **(k！= 0)** 然后使用法术即(减量 k)。同样，**存储**出现“0”的索引。
*   如果 **k = 0** ，则取出队列的前部，并将其存储在变量中。
*   将 **i-low** 和**之前的**答案之间的长度存储为**最大**。
*   低移至第一个“0”+1 的**索引，并增加 k。**
*   最后，返回答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to Find longest subsegment of 1s
int get(int n, int k, int arr[])
{
    // Queue for storing indices of 0s
    queue<int> q;

    int low = 0;
    int ans = INT_MIN;

    int p = k;
    int i = 0;

    while (i < n) {
        // If the current character is 1
        // then increment i by 1
        if (arr[i] == 1) {
            i++;
        }

        // If the current character is 0
        // and some spells are
        // left then use them
        else if (arr[i] == 0 && k != 0) {
            q.push(i);
            k--;
            i++;
        }
        // If k == 0
        else {
            // Take out the index where
            // the first "0" was found
            int x = q.front();
            q.pop();

            // Store the length as max
            // between i-low and that
            // of the previous answer
            ans = max(ans, i - low);

            // Shift low to index
            // of first "O" + 1
            low = x + 1;

            // Increase spell by 1
            k++;
        }

        // Store the length between
        // the i-low and that of
        // previous answer
        ans = max(ans, i - low);
    }
    return ans;
}

// Driver Code
int main()
{
    int N = 10;
    int K = 2;
    int arr[] = { 1, 0, 0, 1, 0,
                  1, 0, 1, 0, 1 };

    cout << get(N, K, arr) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.LinkedList;
import java.util.Queue;

class GFG{

// Function to Find longest subsegment of 1s
static int get(int n, int k, int arr[])
{

    // Queue for storing indices of 0s
    Queue<Integer> q = new LinkedList<Integer>();

    int low = 0;
    int ans = Integer.MIN_VALUE;
    int i = 0;

    while (i < n)
    {

        // If the current character is 1
        // then increment i by 1
        if (arr[i] == 1)
        {
            i++;
        }

        // If the current character is 0
        // and some spells are
        // left then use them
        else if (arr[i] == 0 && k != 0)
        {
            q.add(i);
            k--;
            i++;
        }

        // If k == 0
        else
        {

            // Take out the index where
            // the first "0" was found
            int x = q.peek();
            q.remove();

            // Store the length as max
            // between i-low and that
            // of the previous answer
            ans = Math.max(ans, i - low);

            // Shift low to index
            // of first "O" + 1
            low = x + 1;

            // Increase spell by 1
            k++;
        }

        // Store the length between
        // the i-low and that of
        // previous answer
        ans = Math.max(ans, i - low);
    }
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int N = 10;
    int K = 2;
    int arr[] = { 1, 0, 0, 1, 0,
                  1, 0, 1, 0, 1 };

    System.out.println(get(N, K, arr));
}
}

// This code is contributed by gfking
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to Find longest subsegment of 1s
def get(n, k, arr):

    # Queue for storing indices of 0s
    q = []

    low = 0
    ans = 10 ** -9

    p = k
    i = 0

    while (i < n):

        # If the current character is 1
        # then increment i by 1
        if (arr[i] == 1):
            i += 1

        # If the current character is 0
        # and some spells are
        # left then use them
        elif (arr[i] == 0 and k != 0):
            q.append(i)
            k -= 1
            i += 1
        # If k == 0
        else:
            # Take out the index where
            # the first "0" was found
            x = q[0]
            q.pop(0)

            # Store the length as max
            # between i-low and that
            # of the previous answer
            ans = max(ans, i - low)

            # Shift low to index
            # of first "O" + 1
            low = x + 1

            # Increase spell by 1
            k += 1

        # Store the length between
        # the i-low and that of
        # previous answer
        ans = max(ans, i - low)

    return ans

# Driver Code
N = 10
K = 2
arr = [1, 0, 0, 1, 0, 1, 0, 1, 0, 1]
print(get(N, K, arr))

# This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
        // JavaScript code for the above approach

        // Function to Find longest subsegment of 1s
        function get(n, k, arr) {
            // Queue for storing indices of 0s
            let q = [];

            let low = 0;
            let ans = Number.MIN_VALUE;

            let p = k;
            let i = 0;

            while (i < n) {
                // If the current character is 1
                // then increment i by 1
                if (arr[i] == 1) {
                    i++;
                }

                // If the current character is 0
                // and some spells are
                // left then use them
                else if (arr[i] == 0 && k != 0) {
                    q.push(i);
                    k--;
                    i++;
                }
                // If k == 0
                else {
                    // Take out the index where
                    // the first "0" was found
                    let x = q[0];
                    q.shift();

                    // Store the length as max
                    // between i-low and that
                    // of the previous answer
                    ans = Math.max(ans, i - low);

                    // Shift low to index
                    // of first "O" + 1
                    low = x + 1;

                    // Increase spell by 1
                    k++;
                }

                // Store the length between
                // the i-low and that of
                // previous answer
                ans = Math.max(ans, i - low);
            }
            return ans;
        }

        // Driver Code

        let N = 10;
        let K = 2;
        let arr = [1, 0, 0, 1, 0,
            1, 0, 1, 0, 1];

        document.write(get(N, K, arr) + '<br>');

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
5
```

***时间复杂度*****:**O(N)
***辅助空间*** **:** O(k)