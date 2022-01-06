# 执行给定操作后每个盒子中放置的包的数量

> 原文:[https://www . geeksforgeeks . org/执行给定操作后每个盒子中放置的数据包计数/](https://www.geeksforgeeks.org/count-of-packets-placed-in-each-box-after-performing-given-operations/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和**运算[]** ，由 **N** 和 **M** 整数和一个整数 **C** 组成。[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**代表 **N** 盒中的初始包数，每个容量为 **C** 。从位置 **1** 开始，按照数组**操作【】**指定的顺序执行以下类型的操作:

*   **键入 1:** 移至左框。
*   **键入 2:** 移至右框。
*   **类型 3:** 从当前框中选择一个包。
*   **类型 4:** 从当前框中丢出一个包。
*   **键入 5:** 打印每个盒子里的包数，退出。

在下列情况下，任何操作都会被忽略:

*   **向左移动**如果当前位置为 **1** ，则忽略操作。
*   **向右移动**如果当前位置为 **N** ，则忽略操作。
*   **如果数据包已经被拾取但尚未丢弃，或者当前盒子是空的，则拾取数据包**操作被忽略。
*   **如果没有选择数据包或当前盒子已经有 **C** 数据包，则丢弃数据包**操作被忽略

**示例:**

> **输入:** N = 3，C = 5，arr[] = {2，5，2}，M = 6，运算[] = {3，2，4，1，4，5}
> **输出:** {1，5，2}
> **解释:**
> 运算可以从位置 1 开始执行如下:
> 类型 3:挑包。位置= 1，arr[] = {1，5，2}。
> 类型 2:向右移动。位置= 2，arr[] = {1，5，2}
> 类型 4:丢弃数据包。位置= 2 和 arr[] = {1，5，2}
> 类型 1:向左移动。位置= 1，arr[] = {1，5，2}。
> 类型 4:丢弃数据包。位置= 1，arr[] = {2，5，2}。
> 类型 5:打印数组 arr[] = {2，5，2}。
> 
> **输入:** N = 3，C = 1，arr[] = {1，1，1}，M = 4，运算[] = {3，2，4，5}
> **输出:** {0，1，1}
> **解释:**
> 运算可以从位置 1 开始执行如下:
> 类型 3:挑包。位置= 1，arr[] = {0，1，1}。
> 类型 2:向右移动。位置= 2，arr[] = {0，1，1}
> 类型 4:丢弃数据包。位置= 2，arr[] = {0，1，1}
> 类型 5:打印数组 arr[] = {0，1，1}。

**方法:**想法是为每个任务分配变量，这样对于当前索引，用 **0** 初始化 **curr** 。要检查元素是否被拾取，用**假**初始化拾取的**。按照以下步骤解决问题:**

1.  **保留一个布尔变量**选择的**来跟踪某个数据包是否已经被选择。**
2.  **如果操作类型为**1****curr**不是 **0** ，向左移动，将 **curr** 减 **1** 。**
3.  **如果操作类型为**2****电流**不是**(N-1)**，向右移动，将电流**电流**增加 **1** 。**
4.  **如果操作类型为 **3** 、**拾取**为**假**且当前箱不为空，则在当前箱中减少 **1** 并将**拾取**标记为**真**。**
5.  **如果操作类型为 **4** 、**拾取的**为**真**且当前盒未满，则在当前盒中增加 **1** 并将**拾取的**标记为**假**。**
6.  **如果操作类型为 **5** ，打印数组**arr【】**中的当前值并退出。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <iostream>
using namespace std;
#define ll long long int

// Function to print final array after
// performing all the operations
int printFinalArray(int* a, int n,
                    int* operations,
                    int p, int capacity)
{

    // Initialize variables
    int i, curr = 0;
    bool picked = false;

    // Traverse through all operations
    for (i = 0; i < p; i++) {

        // Operation Type
        int s = operations[i];
        bool flag = false;

        switch (s) {

        // Move left
        case 1:
            if (curr != 0)
                curr--;
            break;

        // Move right
        case 2:
            if (curr != n - 1)
                curr++;
            break;

        // Pick a packet
        case 3:
            if (picked == false
                && a[curr] != 0) {
                picked = true;
                a[curr]--;
            }
            break;

        // Drop a packet
        case 4:
            if (picked == true
                && a[curr] != capacity) {
                picked = false;
                a[curr]++;
            }
            break;

        // Exit
        default:
            flag = true;
        }

        if (flag == true)
            break;
    }

    // Print final array
    for (i = 0; i < n; i++) {
        cout << a[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given capacity
    int capacity = 5;

    // Given array with initial values
    int a[] = { 2, 5, 2 };

    // Array size
    int N = sizeof(a) / sizeof(a[0]);

    // Operations
    int operations[] = { 3, 2, 4, 1, 4, 5 };

    // Number of operations
    int M = sizeof(operations)
            / sizeof(operations[0]);

    // Function call
    printFinalArray(a, N, operations,
                    M, capacity);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print final array after
// performing all the operations
static void printFinalArray(int []a, int n,
                            int []operations,
                            int p, int capacity)
{

    // Initialize variables
    int i, curr = 0;
    boolean picked = false;

    // Traverse through all operations
    for(i = 0; i < p; i++)
    {

        // Operation Type
        int s = operations[i];
        boolean flag = false;

        switch(s)
        {

            // Move left
            case 1:
                if (curr != 0)
                    curr--;
                break;

            // Move right
            case 2:
                if (curr != n - 1)
                    curr++;
                break;

            // Pick a packet
            case 3:
                if (picked == false &&
                    a[curr] != 0)
                {
                    picked = true;
                    a[curr]--;
                }
                break;

            // Drop a packet
            case 4:
                if (picked == true && 
                    a[curr] != capacity)
                {
                    picked = false;
                    a[curr]++;
                }
                break;

            // Exit
            default:
                flag = true;
        }

        if (flag == true)
            break;
    }

    // Print final array
    for(i = 0; i < n; i++)
    {
        System.out.print(a[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given capacity
    int capacity = 5;

    // Given array with initial values
    int a[] = { 2, 5, 2 };

    // Array size
    int N = a.length;

    // Operations
    int operations[] = { 3, 2, 4, 1, 4, 5 };

    // Number of operations
    int M = operations.length;

    // Function call
    printFinalArray(a, N, operations,
                    M, capacity);
}
}

// This code is contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to print final array after
# performing all the operations
def printFinalArray(a, n,
                    operations, p, capacity):

    # Initialize variables
    curr = 0
    picked = False

    # Traverse through all operations
    for i in range(p):

        # Operation Type
        s = operations[i]
        flag = False

        # Move left
        if (curr != 0):
            curr -= 1
            break

        # Move right
        if (curr != n - 1):
            curr += 1
            break

        # Pick a packet
        if (picked == False
                and a[curr] != 0):
            picked = True
            a[curr] -= 1
            break

        # Drop a packet
        if (picked == True
                and a[curr] != capacity):
            picked = False
            a[curr] += 1
            break

        # Exit
        else:
            flag = True

        if (flag == True):
            break

    # Print final array
    for i in range(n):
        print(a[i], end=" ")

# Driver Code
if __name__ == "__main__":

    # Given capacity
    capacity = 5

    # Given array with initial values
    a = [2, 5, 2]

    # Array size
    N = len(a)

    # Operations
    operations = [3, 2, 4, 1, 4, 5]

    # Number of operations
    M = len(operations)

    # Function call
    printFinalArray(a, N, operations,
                    M, capacity)

# This code is contributed by chitranayal
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to print final array after
// performing all the operations
static void printFinalArray(int []a, int n,
                            int []operations,
                            int p, int capacity)
{

    // Initialize variables
    int i, curr = 0;
    bool picked = false;

    // Traverse through all operations
    for(i = 0; i < p; i++)
    {

        // Operation Type
        int s = operations[i];
        bool flag = false;

        switch(s)
        {

            // Move left
            case 1:
                if (curr != 0)
                    curr--;
                break;

            // Move right
            case 2:
                if (curr != n - 1)
                    curr++;
                break;

            // Pick a packet
            case 3:
                if (picked == false &&
                    a[curr] != 0)
                {
                    picked = true;
                    a[curr]--;
                }
                break;

            // Drop a packet
            case 4:
                if (picked == true && 
                    a[curr] != capacity)
                {
                    picked = false;
                    a[curr]++;
                }
                break;

            // Exit
            default:
                flag = true;
            break;
        }

        if (flag == true)
            break;
    }

    // Print final array
    for(i = 0; i < n; i++)
    {
        Console.Write(a[i] + " ");
    }
}

// Driver Code
public static void Main()
{

    // Given capacity
    int capacity = 5;

    // Given array with initial values
    int[] a = { 2, 5, 2 };

    // Array size
    int N = a.Length;

    // Operations
    int[] operations = { 3, 2, 4, 1, 4, 5 };

    // Number of operations
    int M = operations.Length;

    // Function call
    printFinalArray(a, N, operations,
                    M, capacity);
}
}

// This code is contributed by sanjoy_62
```

## **java 描述语言**

```
<script>
// javascript program for the above approach

    // Function to print final array after
    // performing all the operations
    function printFinalArray(a, n,  operations, p, capacity)
    {

        // Initialize variables
        var i, curr = 0;
        var picked = false;

        // Traverse through all operations
        for (i = 0; i < p; i++)
        {

            // Operation Type
            var s = operations[i];
            var flag = false;

            switch (s)
            {

            // Move left
            case 1:
                if (curr != 0)
                    curr--;
                break;

            // Move right
            case 2:
                if (curr != n - 1)
                    curr++;
                break;

            // Pick a packet
            case 3:
                if (picked == false && a[curr] != 0)
                {
                    picked = true;
                    a[curr]--;
                }
                break;

            // Drop a packet
            case 4:
                if (picked == true && a[curr] != capacity)
                {
                    picked = false;
                    a[curr]++;
                }
                break;

            // Exit
            default:
                flag = true;
            }

            if (flag == true)
                break;
        }

        // Print final array
        for (i = 0; i < n; i++) {
            document.write(a[i] + " ");
        }
    }

    // Driver Code

        // Given capacity
        var capacity = 5;

        // Given array with initial values
        var a = [ 2, 5, 2 ];

        // Array size
        var N = a.length;

        // Operations
        var operations = [ 3, 2, 4, 1, 4, 5 ];

        // Number of operations
        var M = operations.length;

        // Function call
        printFinalArray(a, N, operations, M, capacity);

// This code is contributed by todaysgaurav.
</script>
```

****Output:** 

```
2 5 2
```** 

*****时间复杂度:** O(M + N)*
***辅助空间:** O(M + N)***