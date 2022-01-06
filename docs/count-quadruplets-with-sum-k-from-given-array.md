# 用给定数组的和 K 计数四胞胎

> 原文:[https://www . geeksforgeeks . org/count-四胞胎-带给定数组的和-k/](https://www.geeksforgeeks.org/count-quadruplets-with-sum-k-from-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **S** ，任务是找出给定数组中存在的四胞胎的数量，其和为 **S** 。

**示例:**

> **输入:** arr[] = {1，5，3，1，2，10}，S = 20
> **输出:** 1
> **说明:**只有满足条件的四胞胎才是 arr[1]+arr[2]+arr[4]+arr[5]= 5+3+2+10 = 20。
> 
> **输入:** N = 6，S = 13，arr[] = {4，5，3，1，2，4}
> **输出:** 3
> **说明:**三个四胞胎，和 13 为:
> 
> 1.  arr[0]+arr[2]+arr[4]+arr[5]= 4+3+2+4 = 13
> 2.  arr[0]+arr[1]+arr[2]+arr[3]= 4+5+3+1 = 13
> 3.  arr[1]+arr[2]+arr[3]+arr[5]= 5+3+1+4 = 13

**天真方法:**想法是[从给定的数组中生成长度为 4](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/) 的所有可能组合。对于每个四胞胎，如果总和等于 **S** ，那么将**计数器**增加 **1** 。检查完所有四胞胎后，将**计数器**打印为四胞胎总数的总和 **S** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to return the number of
// quadruplets with the given sum
int countSum(int a[], int n, int sum)
{
    // Initialize variables
    int i, j, k, l;

    // Initialize answer
    int count = 0;

    // All possible first elements
    for (i = 0; i < n - 3; i++) {

        // All possible second elements
        for (j = i + 1; j < n - 2; j++) {

            // All possible third elements
            for (k = j + 1; k < n - 1; k++) {

                // All possible fourth elements
                for (l = k + 1; l < n; l++) {

                    // Increment counter by 1
                    // if quadruplet sum is S
                    if (a[i] + a[j]
                            + a[k] + a[l]
                        == sum)
                        count++;
                }
            }
        }
    }

    // Return the final count
    return count;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 4, 5, 3, 1, 2, 4 };

    // Given sum S
    int S = 13;

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countSum(arr, N, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to return the number of
// quadruplets with the given sum
static int countSum(int a[], int n, int sum)
{

    // Initialize variables
    int i, j, k, l;

    // Initialize answer
    int count = 0;

    // All possible first elements
    for(i = 0; i < n - 3; i++)
    {

        // All possible second elements
        for(j = i + 1; j < n - 2; j++)
        {

            // All possible third elements
            for(k = j + 1; k < n - 1; k++)
            {

                // All possible fourth elements
                for(l = k + 1; l < n; l++)
                {

                    // Increment counter by 1
                    // if quadruplet sum is S
                    if (a[i] + a[j] +
                        a[k] + a[l] == sum)
                        count++;
                }
            }
        }
    }

    // Return the final count
    return count;
}

// Driver Code
public static void main(String args[])
{

    // Given array arr[]
    int arr[] = { 4, 5, 3, 1, 2, 4 };

    // Given sum S
    int S = 13;

    int N = arr.length;

    // Function Call
    System.out.print(countSum(arr, N, S));
}
}

// This code is contributed by bgangwar59
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the number of
# quadruplets with the given sum
def countSum(a, n, sum):

    # Initialize variables
    # i, j, k, l

    # Initialize answer
    count = 0

    # All possible first elements
    for i in range(n - 3):

        # All possible second elements
        for j in range(i + 1, n - 2):

            # All possible third elements
            for k in range(j + 1, n - 1):

                # All possible fourth elements
                for l in range(k + 1, n):

                    # Increment counter by 1
                    # if quadruplet sum is S
                    if (a[i] + a[j] + a[k] + a[l]== sum):
                        count += 1

    # Return the final count
    return count

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 4, 5, 3, 1, 2, 4 ]

    # Given sum S
    S = 13

    N = len(arr)

    # Function Call
    print(countSum(arr, N, S))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
class GFG{

// Function to return the number of
// quadruplets with the given sum
static int countSum(int []a, int n, int sum)
{

    // Initialize variables
    int i, j, k, l;

    // Initialize answer
    int count = 0;

    // All possible first elements
    for(i = 0; i < n - 3; i++)
    {

        // All possible second elements
        for(j = i + 1; j < n - 2; j++)
        {

            // All possible third elements
            for(k = j + 1; k < n - 1; k++)
            {

                // All possible fourth elements
                for(l = k + 1; l < n; l++)
                {

                    // Increment counter by 1
                    // if quadruplet sum is S
                    if (a[i] + a[j] +
                        a[k] + a[l] == sum)
                        count++;
                }
            }
        }
    }

    // Return the final count
    return count;
}

// Driver Code
public static void Main()
{

    // Given array arr[]
    int []arr = { 4, 5, 3, 1, 2, 4 };

    // Given sum S
    int S = 13;

    int N = arr.Length;

    // Function Call
    System.Console.Write(countSum(arr, N, S));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to return the number of
// quadruplets with the given sum
function countSum(a, n, sum)
{

    // Initialize variables
    let i, j, k, l;

    // Initialize answer
    let count = 0;

    // All possible first elements
    for(i = 0; i < n - 3; i++)
    {

        // All possible second elements
        for(j = i + 1; j < n - 2; j++)
        {

            // All possible third elements
            for(k = j + 1; k < n - 1; k++)
            {

                // All possible fourth elements
                for(l = k + 1; l < n; l++)
                {

                    // Increment counter by 1
                    // if quadruplet sum is S
                    if (a[i] + a[j] +
                        a[k] + a[l] == sum)
                        count++;
                }
            }
        }
    }

    // Return the final count
    return count;
}

    // Driver Code

    // Given array arr[]
    let arr = [ 4, 5, 3, 1, 2, 4 ];

    // Given sum S
    let S = 13;

    let N = arr.length;

    // Function Call
    document.write(countSum(arr, N, S));

</script>
```

**输出:**

```
3
```

***时间复杂度:**O(N<sup>4</sup>)*
***辅助空间:** O(1)*

**更好的方法:**为了优化上述方法，想法是使用一个[地图数据结构](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。按照以下步骤解决问题:

*   用 **0** 初始化计数器**计数**存储四胞胎的数量。
*   [使用变量 **i** 在范围**【0，N–3】**内遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。对于每个元素**arr【I】**，使用变量 **j** 在范围**【I+1，N–2)**内再次遍历数组，并执行以下操作:
    *   求所需总和的值(如 **req** )为**(S–arr[I]–arr[j])**。
    *   用 **0** 初始化**count _ two**，将上述子阵列中有序对的[计数存储为总和](https://www.geeksforgeeks.org/count-pairs-with-given-sum/)**(S–arr[I]–arr[j])**。
    *   找到**计数 _ 两次**后，通过**计数 _ 两次/ 2** 更新计数。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述想法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
#include <unordered_map>
using namespace std;

// Function to return the number of
// quadruplets having given sum
int countSum(int a[], int n, int sum)
{

    // Initialize variables
    int i, j, k, l;

    // Initialize answer
    int count = 0;

    // All possible first elements
    for (i = 0; i < n - 3; i++) {

        // All possible second element
        for (j = i + 1; j < n - 2; j++) {
            int req = sum - a[i] - a[j];

            // Use map to find the
            // fourth element
            unordered_map<int, int> m;

            // All possible third elements
            for (k = j + 1; k < n; k++)
                m[a[k]]++;

            int twice_count = 0;

            // Calculate number of valid
            // 4th elements
            for (k = j + 1; k < n; k++) {

                // Update the twice_count
                twice_count += m[req - a[k]];

                if (req - a[k] == a[k])
                    twice_count--;
            }

            // Unordered pairs
            count += twice_count / 2;
        }
    }

    // Return answer
    return count;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 4, 5, 3, 1, 2, 4 };

    // Given sum S
    int S = 13;

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countSum(arr, N, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to return the number of
// quadruplets having given sum
static int countSum(int a[], int n, int sum)
{

    // Initialize variables
    int i, j, k, l;

    // Initialize answer
    int count = 0;

    // All possible first elements
    for(i = 0; i < n - 3; i++)
    {

        // All possible second element
        for(j = i + 1; j < n - 2; j++)
        {
            int req = sum - a[i] - a[j];

            // Use map to find the
            // fourth element
            HashMap<Integer, Integer> m = new HashMap<>();

            // All possible third elements
            for(k = j + 1; k < n; k++)
                if (m.containsKey(a[k]))
                {
                    m.put(a[k], m.get(a[k]) + 1);
                }
                else
                {
                    m.put(a[k], 1);
                }

            int twice_count = 0;

            // Calculate number of valid
            // 4th elements
            for(k = j + 1; k < n; k++)
            {

                // Update the twice_count
                if (m.containsKey(req - a[k]))
                    twice_count += m.get(req - a[k]);

                if (req - a[k] == a[k])
                    twice_count--;
            }

            // Unordered pairs
            count += twice_count / 2;
        }
    }

    // Return answer
    return count;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 4, 5, 3, 1, 2, 4 };

    // Given sum S
    int S = 13;

    int N = arr.length;

    // Function Call
    System.out.print(countSum(arr, N, S));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the number of
# quadruplets having given sum
def countSum(a, n, sum):

    # Initialize variables
    # Initialize answer
    count = 0

    # All possible first elements
    for i in range(n - 3):

        # All possible second element
        for j in range(i + 1, n - 2, 1):
            req = sum - a[i] - a[j]

            # Use map to find the
            # fourth element
            m = {}

            # All possible third elements
            for k in range(j + 1, n, 1):
                m[a[k]] = m.get(a[k], 0) + 1

            twice_count = 0

            # Calculate number of valid
            # 4th elements
            for k in range(j + 1, n, 1):

                # Update the twice_count
                twice_count += m.get(req - a[k], 0)

                if (req - a[k] == a[k]):
                    twice_count -= 1

            # Unordered pairs
            count += twice_count // 2

    # Return answer
    return count

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr =  [ 4, 5, 3, 1, 2, 4 ]

    # Given sum S
    S = 13

    N =  len(arr)

    # Function Call
    print(countSum(arr, N, S))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return the number of
// quadruplets having given sum
static int countSum(int []a, int n,
                    int sum)
{

    // Initialize variables
    int i, j, k;
    //int l;

    // Initialize answer
    int count = 0;

    // All possible first elements
    for(i = 0; i < n - 3; i++)
    {

        // All possible second element
        for(j = i + 1; j < n - 2; j++)
        {
            int req = sum - a[i] - a[j];

            // Use map to find the
            // fourth element
            Dictionary<int,
                       int> m = new Dictionary<int,
                                               int>();

            // All possible third elements
            for(k = j + 1; k < n; k++)
                if (m.ContainsKey(a[k]))
                {
                    m[a[k]]++;
                }
                else
                {
                    m.Add(a[k], 1);
                }

            int twice_count = 0;

            // Calculate number of valid
            // 4th elements
            for(k = j + 1; k < n; k++)
            {

                // Update the twice_count
                if (m.ContainsKey(req - a[k]))
                    twice_count += m[req - a[k]];

                if (req - a[k] == a[k])
                    twice_count--;
            }

            // Unordered pairs
            count += twice_count / 2;
        }
    }

    // Return answer
    return count;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 4, 5, 3, 1, 2, 4 };

    // Given sum S
    int S = 13;

    int N = arr.Length;

    // Function Call
    Console.Write(countSum(arr, N, S));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to return the number of
// quadruplets having given sum
function countSum(a, n, sum)
{

    // Initialize variables
    var i, j, k, l;

    // Initialize answer
    var count = 0;

    // All possible first elements
    for (i = 0; i < n - 3; i++) {

        // All possible second element
        for (j = i + 1; j < n - 2; j++) {
            var req = sum - a[i] - a[j];

            // Use map to find the
            // fourth element
            var m = new Map();

            // All possible third elements
            for (k = j + 1; k < n; k++)
            {
                if(m.has(a[k]))
                    m.set(a[k], m.get(a[k])+1)
                else
                    m.set(a[k], 1)
            }

            var twice_count = 0;

            // Calculate number of valid
            // 4th elements
            for (k = j + 1; k < n; k++) {

                // Update the twice_count
                if(m.has(req - a[k]))
                    twice_count += m.get(req - a[k]);

                if ((req - a[k]) == a[k])
                    twice_count--;
            }

            // Unordered pairs
            count += parseInt(twice_count / 2);
        }
    }

    // Return answer
    return count;
}

// Driver Code

// Given array arr[]
var arr = [4, 5, 3, 1, 2, 4];

// Given sum S
var S = 13;
var N = arr.length;

// Function Call
document.write( countSum(arr, N, S));

</script>
```

**输出:**

```
3
```

***时间复杂度:** O(N <sup>3</sup> )其中 N 是给定数组的大小，*
***辅助空间:** O(N)*

**高效方法:**这个想法类似于上面使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)的方法。在这种方法中，固定 **3 <sup>rd</sup>** 元素，然后找到并存储给定数组的任何四元组的所有可能的前两个元素的和的频率。按照以下步骤解决问题:

1.  初始化计数器**计数**以存储给定总和的总四胞胎 **S** 和一张[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)以存储每个可能四胞胎的前两个元素的所有可能总和。
2.  [使用变量 **i** 在范围**【0，N–1】**内遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，其中**arr【I】**是固定的 **3 <sup>rd</sup>** 元素。
3.  然后，对于上述步骤中的每个元素 **arr[i]** ，[使用变量 j 在范围**【I+1，N–1】**上遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并通过**映射【arr[I]+arr[j]】**增加计数器**计数**。
4.  从上述循环遍历后，对于每个元素 **arr[i]** ，[从 **j = 0 到 I–1**遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并将任何可能的四元组的前两个元素的任意和 **arr[i] + arr[j]** 的频率增加 **1** ，即将**映射【arr[I]+arr[j]】**增加 **1**
5.  对每个元素重复上述步骤**arr【I】**，然后打印计数器**计数**作为给定总和的四胞胎总数 **S** 。

下面是上述想法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
#include <unordered_map>
using namespace std;

// Function to return the number of
// quadruplets having the given sum
int countSum(int a[], int n, int sum)
{

    // Initialize variables
    int i, j, k;

    // Initialize answer
    int count = 0;

    // Store the frequency of sum
    // of first two elements
    unordered_map<int, int> m;

    // Traverse from 0 to N-1, where
    // arr[i] is the 3rd element
    for (i = 0; i < n - 1; i++) {

        // All possible 4th elements
        for (j = i + 1; j < n; j++) {

            // Sum of last two element
            int temp = a[i] + a[j];

            // Frequency of sum of first
            // two elements
            if (temp < sum)
                count += m[sum - temp];
        }
        for (j = 0; j < i; j++) {

            // Store frequency of all possible
            // sums of first two elements
            int temp = a[i] + a[j];

            if (temp < sum)
                m[temp]++;
        }
    }

    // Return the answer
    return count;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 4, 5, 3, 1, 2, 4 };

    // Given sum S
    int S = 13;

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countSum(arr, N, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to return the number of
// quadruplets having the given sum
static int countSum(int a[], int n, int sum)
{

    // Initialize variables
    int i, j, k;

    // Initialize answer
    int count = 0;

    // Store the frequency of sum
    // of first two elements
    HashMap<Integer, Integer> m = new HashMap<>();

    // Traverse from 0 to N-1, where
    // arr[i] is the 3rd element
    for(i = 0; i < n - 1; i++)
    {

        // All possible 4th elements
        for(j = i + 1; j < n; j++)
        {

            // Sum of last two element
            int temp = a[i] + a[j];

            // Frequency of sum of first
            // two elements
            if (temp < sum && m.containsKey(sum - temp))
                count += m.get(sum - temp);
        }
        for(j = 0; j < i; j++)
        {

            // Store frequency of all possible
            // sums of first two elements
            int temp = a[i] + a[j];

            if (temp < sum)
                if (m.containsKey(temp))
                    m.put(temp, m.get(temp) + 1);
                else
                    m.put(temp, 1);
        }
    }

    // Return the answer
    return count;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 4, 5, 3, 1, 2, 4 };

    // Given sum S
    int S = 13;

    int N = arr.length;

    // Function Call
    System.out.print(countSum(arr, N, S));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function to return the number of
# quadruplets having the given sum
def countSum(a, n, sum):

    # Initialize answer
    count = 0

    # Store the frequency of sum
    # of first two elements
    m = defaultdict(int)

    # Traverse from 0 to N-1, where
    # arr[i] is the 3rd element
    for i in range(n - 1):

        # All possible 4th elements
        for j in range(i + 1, n):

            # Sum of last two element
            temp = a[i] + a[j]

            # Frequency of sum of first
            # two elements
            if (temp < sum):
                count += m[sum - temp]

        for j in range(i):

            # Store frequency of all possible
            # sums of first two elements
            temp = a[i] + a[j]

            if (temp < sum):
                m[temp] += 1

    # Return the answer
    return count

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [ 4, 5, 3, 1, 2, 4 ]

    # Given sum S
    S = 13

    N = len(arr)

    # Function Call
    print(countSum(arr, N, S))

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return the number of
// quadruplets having the given sum
static int countSum(int []a, int n, int sum)
{

    // Initialize variables
    int i, j;

    // Initialize answer
    int count = 0;

    // Store the frequency of sum
    // of first two elements
    Dictionary<int,
               int> m = new Dictionary<int,
                                       int>();

    // Traverse from 0 to N-1, where
    // arr[i] is the 3rd element
    for(i = 0; i < n - 1; i++)
    {

        // All possible 4th elements
        for(j = i + 1; j < n; j++)
        {

            // Sum of last two element
            int temp = a[i] + a[j];

            // Frequency of sum of first
            // two elements
            if (temp < sum && m.ContainsKey(sum - temp))
                count += m[sum - temp];
        }

        for(j = 0; j < i; j++)
        {

            // Store frequency of all possible
            // sums of first two elements
            int temp = a[i] + a[j];

            if (temp < sum)
                if (m.ContainsKey(temp))
                    m[temp]++;
                else
                    m.Add(temp, 1);
        }
    }

    // Return the answer
    return count;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 4, 5, 3, 1, 2, 4 };

    // Given sum S
    int S = 13;

    int N = arr.Length;

    // Function Call
    Console.Write(countSum(arr, N, S));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return the number of
// quadruplets having the given sum
function countSum(a, n, sum)
{

    // Initialize variables
    let i, j, k;

    // Initialize answer
    let count = 0;

    // Store the frequency of sum
    // of first two elements
    let m = new Map();

    // Traverse from 0 to N-1, where
    // arr[i] is the 3rd element
    for(i = 0; i < n - 1; i++)
    {

        // All possible 4th elements
        for(j = i + 1; j < n; j++)
        {

            // Sum of last two element
            let temp = a[i] + a[j];

            // Frequency of sum of first
            // two elements
            if (temp < sum && m.has(sum - temp))
                count += m.get(sum - temp);
        }
        for(j = 0; j < i; j++)
        {

            // Store frequency of all possible
            // sums of first two elements
            let temp = a[i] + a[j];

            if (temp < sum)
                if (m.has(temp))
                    m.set(temp, m.get(temp) + 1);
                else
                    m.set(temp, 1);
        }
    }

    // Return the answer
    return count;
}

// Driver Code

// Given array arr[]
let arr = [ 4, 5, 3, 1, 2, 4 ];

 // Given sum S
let S = 13;
let  N = arr.length;

// Function Call
document.write(countSum(arr, N, S));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*