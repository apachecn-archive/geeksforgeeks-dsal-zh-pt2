# 通过删除或追加任意数字

来减少将 N 变为 2 的幂的步骤

> 原文:[https://www . geeksforgeeks . org/通过删除或追加任意数字来最小化更改 n 次方的步骤/](https://www.geeksforgeeks.org/minimize-steps-to-change-n-to-power-of-2-by-deleting-or-appending-any-digit/)

给定一个整数 **N** ，任务是使用以下步骤找到将数字 **N** 更改为 **2** 的[完美幂](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)所需的最小步数:

*   从数字中删除任意一个数字 **d** 。
*   在数字 **N** 的末尾加上任意数字 **d** 。

**示例:**

> **输入:** N = 1092
> **输出:** 2
> **说明:**
> 以下为执行步骤:
> 
> 1.  从数字 N(= 1092)中删除数字 9 会将其修改为 102。
> 2.  将数字 4 加到数字 N(= 102)的末尾会将其修改为 1024。
> 
> 经过以上运算，数字 N 转化为 2 的完美幂，需要的移动次数是 2，这是最小值。因此，打印 2。
> 
> **输入:**N = 4444
> T3】输出: 3

**方法:**给定问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决，其思想是存储所有 2 的幂且小于 **10 <sup>20</sup>** 的数字，并检查每个数字将给定数字转换为 **2 的幂的最小步骤。**按照以下步骤解决问题:

*   [初始化一个数组](https://www.geeksforgeeks.org/python-initialize-empty-array-of-given-length/)并存储所有为 **2** 幂且小于 **10 <sup>20</sup>** 的数字。
*   将答案变量**最佳**初始化为**长度+ 1** 作为所需的最大步数。
*   [使用变量 **x** 迭代范围](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)**【0，len)** ，其中 **len** 是数组[的长度](https://www.geeksforgeeks.org/how-to-determine-length-or-size-of-an-array-in-java/)，并执行以下步骤:
    *   初始化变量，将**位置**设为 **0** 。
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)**【0，len)** ，其中 **len** 是数字的长度，如果**位置**小于 **len(x)** 且 **x【位置】**等于**num【I】**，则将**位置**的值增加 **1** 。
    *   将**最佳**的值更新为**最佳**或**镜头(x) +镜头(num)–2 *位置**的最小值。
*   执行上述步骤后，打印**最佳**的值作为结果。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum number of
# steps required to reduce N to perfect
# power of 2 by performing given steps
def findMinimumSteps(N):

    num = str(N)
    c = 1
    a = []

    # Stores all the perfect power of 2
    while True:
        if (c > 10 ** 20):
            break
        a.append(str(c))
        c = c * 2

    # Maximum number of steps required
    best = len(num) + 1

    # Iterate for each perfect power of 2
    for x in a:
        position = 0

        # Comparing with all numbers
        for i in range(len(num)):

            if position < len(x) and x[position] == num[i]:
                position += 1

        # Update the minimum number of
        # steps required
        best = min(best, len(x) + len(num) - 2 * position)

    # Print the result
    print(best)

# Driver Code
N = 1092

# Function Call
findMinimumSteps(N)
```

## java 描述语言

```
<script>

        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum number of
        // steps required to reduce N to perfect
        // power of 2 by performing given steps
        function findMinimumSteps(N)
        {
            num = N.toString()
            c = 1
            a = []

            // Stores all the perfect power of 2
            while (1) {
                if (c > Math.pow(10, 20)) {
                    break;
                }
                a.push(c.toString())
                c = c * 2
            }

            // Maximum number of steps required
            best = num.length + 1

            // Iterate for each perfect power of 2
            for (x of a) {
                position = 0

                // Comparing with all numbers
                for (let i = 0; i < num.length; i++) {

                    if (position < x.length && x[position] == num[i])
                        position += 1
                }

                // Update the minimum number of
                // steps required
                best = Math.min(best, x.length + num.length - 2 * position)
            }

            // Print the result
            document.write(best)
        }

        // Driver Code
        let N = 1092

        // Function Call
        findMinimumSteps(N)

    // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)