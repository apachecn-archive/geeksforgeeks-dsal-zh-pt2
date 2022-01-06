# 每个阵列元素存在于左侧和右侧的不同元素的计数差异

> 原文:[https://www . geeksforgeeks . org/每个数组元素从左到右的不同元素计数差异/](https://www.geeksforgeeks.org/difference-of-count-of-distinct-elements-present-to-left-and-right-for-each-array-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，每个数组元素的任务是找出给定数组**arr【】**中其左右不同元素[个数的绝对差。](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)

**示例:**

> **输入:** arr[] = {7，7，3，2，3}
> **输出:** 2 2 0 1 2
> **解释:**
> 出现在每个索引左侧的不同元素的数量由[0，0，1，1，2]给出，出现在每个索引右侧的不同元素的数量为[2，2，1，0，0]。取两者的绝对差值就得到上面的输出。
> 
> **输入:** arr[] = {4，3，2，3}
> **输出:** 2 0 1 2

**天真方法:**给定的问题可以使用[集合数据结构](https://www.geeksforgeeks.org/hashset-in-java/)来解决，思路是[迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，I–1】**找到每个元素左边的不同元素的计数，类似地[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)到范围**【I+1，N–1】**找到每个元素右边的不同元素。按照以下步骤解决给定的问题:

*   初始化一个数组 **res[]** ，该数组存储每个数组元素的不同元素的绝对差值。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于索引 **i** 处的每个元素，执行以下操作:
    *   迭代范围**【0，I–1】**并插入集合中的所有元素，比如 **S1** 。
    *   迭代范围**【I+1，N–1】**并插入集合中的所有元素，比如 **S2** 。
    *   将**RES【I】**的值更新为[套](https://www.geeksforgeeks.org/setsize-c-stl/)套**套【S1】套**套**套**套的绝对差。
*   完成以上步骤后，[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **res[]** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to find the difference of
// count of distince elements to the
// left and right for each array elements
void findDifferenceArray(int arr[], int N)
{

    // Stores distinct array element
    // in the left and right
    set<int> S1;
    set<int> S2;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Insert all element to the left
        // in the set S1
        for (int j = 0; j < i; j++) {
            S1.insert(arr[j]);
        }

        // Insert all element to the right
        // in the set S2
        for (int j = i + 1; j < N; j++) {
            S2.insert(arr[j]);
        }

        // Print the difference
        cout << abs((int)S1.size()
                    - (int)S2.size())
             << ' ';

        S1.clear();
        S2.clear();
    }
}

// Driver Code
int main()
{
    int arr[] = { 7, 7, 3, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    findDifferenceArray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashSet;
class GFG{

// Function to find the difference of
// count of distince elements to the
// left and right for each array elements
public static void findDifferenceArray(int arr[], int N)
{

    // Stores distinct array element
    // in the left and right
    HashSet<Integer> S1 = new HashSet<Integer>();
    HashSet<Integer> S2 = new HashSet<Integer>();

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Insert all element to the left
        // in the set S1
        for (int j = 0; j < i; j++) {
            S1.add(arr[j]);
        }

        // Insert all element to the right
        // in the set S2
        for (int j = i + 1; j < N; j++) {
            S2.add(arr[j]);
        }

        // Print the difference
        System.out.print(Math.abs(S1.size() - S2.size()) + " ");

        S1.clear();
        S2.clear();
    }
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 7, 7, 3, 2, 3 };
    int N = arr.length;
    findDifferenceArray(arr, N);
}
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the difference of
# count of distince elements to the
# left and right for each array elements
def findDifferenceArray(arr, N) :

    # Stores distinct array element
    # in the left and right
    S1 = set();
    S2 = set();

    # Traverse the array
    for i in range(N) :

        # Insert all element to the left
        # in the set S1
        for j in range(i) :
            S1.add(arr[j]);

        # Insert all element to the right
        # in the set S2
        for j in range(i + 1, N) :
            S2.add(arr[j]);

        # Print the difference
        print(abs(len(S1) - len(S2)),end=' ');

        S1.clear();
        S2.clear();

# Driver Code
if __name__ == "__main__" :

    arr = [ 7, 7, 3, 2, 3 ];
    N = len(arr);
    findDifferenceArray(arr, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to find the difference of
// count of distince elements to the
// left and right for each array elements
public static void findDifferenceArray(int[] arr, int N)
{

    // Stores distinct array element
    // in the left and right
    HashSet<int> S1 = new HashSet<int>();
    HashSet<int> S2 = new HashSet<int>();

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Insert all element to the left
        // in the set S1
        for (int j = 0; j < i; j++) {
            S1.Add(arr[j]);
        }

        // Insert all element to the right
        // in the set S2
        for (int j = i + 1; j < N; j++) {
            S2.Add(arr[j]);
        }

        // Print the difference
        Console.Write(Math.Abs(S1.Count - S2.Count) + " ");

        S1.Clear();
        S2.Clear();
    }
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { 7, 7, 3, 2, 3 };
    int N = arr.Length;
    findDifferenceArray(arr, N);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the difference of
        // count of distince elements to the
        // left and right for each array elements
        function findDifferenceArray(arr, N) {

            // Stores distinct array element
            // in the left and right
            let S1 = new Set();
            let S2 = new Set();

            // Traverse the array
            for (let i = 0; i < N; i++) {

                // Insert all element to the left
                // in the set S1
                for (let j = 0; j < i; j++) {
                    S1.add(arr[j]);
                }

                // Insert all element to the right
                // in the set S2
                for (let j = i + 1; j < N; j++) {
                    S2.add(arr[j]);
                }

                // Print the difference
                document.write(Math.abs(S1.size
                    - S2.size)
                    + ' ');

                S1.clear();
                S2.clear();
            }
        }

        // Driver Code

        let arr = [7, 7, 3, 2, 3];
        let N = arr.length;
        findDifferenceArray(arr, N);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
3 1 1 1 3
```

***时间复杂度:**O((N<sup>2</sup>)* log N)*
***辅助空间:** O(N)*

**高效方法:**上述方法也可以通过存储每个数组元素左右不同元素的频率，然后找到每个数组元素的合成差来优化。按照以下步骤解决给定的问题:

*   初始化两个[无序 _ 地图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **左地图**和**右地图**分别存储每个索引左右的不同元素。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将所有数组元素插入到**右映射**中。
*   使用变量 **i** 遍历给定数组，并执行以下步骤:
    *   计算当前元素左侧的不同元素(比如**计算左侧**)作为地图的大小**左侧地图**。
    *   通过 **1** 减少当前元素在地图**右侧地图**的频率。
    *   计算当前元素右侧的不同元素(比如 **countRight** )作为地图的[大小**右地图**。](https://www.geeksforgeeks.org/mapsize-c-stl/)
    *   将地图**左侧地图**中当前元素的频率增加 **1** 。
    *   插入地图 **左地图**和**右地图**大小的绝对差值。
*   完成以上步骤后，[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **res[]** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to find the difference of
// count of distince elements to the
// left and right for each array elements
void findDifferenceArray(int arr[], int N)
{

    // Stores the frequency of array
    // element to the left and the right
    unordered_map<int, int> leftMap, rightMap;

    // Stores the frequency of array
    // element in the map rightMap
    for (int i = 0; i < N; i++) {
        rightMap[arr[i]]++;
    }

    // Stores the resultant differences
    vector<int> res;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Find the count in the left
        int countLeft = leftMap.size();

        // Decrement the frequency
        if (rightMap[arr[i]] > 1) {
            rightMap[arr[i]]--;
        }
        else {
            rightMap.erase(arr[i]);
        }

        // Find the count in the left
        int countRight = rightMap.size();

        // Insert the resultant difference
        res.push_back(abs(countRight - countLeft));

        // Increment the frequency
        leftMap[arr[i]]++;
    }

    // Print the result
    for (auto& it : res) {
        cout << it << ' ';
    }
}

// Driver Code
int main()
{
    int arr[] = { 7, 7, 3, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    findDifferenceArray(arr, N);

    return 0;
}
```

**Output:** 

```
3 1 1 1 3
```

***时间复杂度:**O(N)*
T5**辅助** **空间:** O(N)