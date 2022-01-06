# 通过在阵列的每次迭代中重复移除阵列中的最小峰值元素

> 原文:[https://www . geeksforgeeks . org/数组每次迭代重复移除数组中的最小峰值元素/](https://www.geeksforgeeks.org/minimum-peak-elements-from-an-array-by-their-repeated-removal-at-every-iteration-of-the-array/)

给定一个由 **N** 个不同正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是重复[从给定数组](https://www.geeksforgeeks.org/find-a-peak-in-a-given-array/)中找到**个最小峰值元素**，并移除该元素，直到所有数组元素都被移除。

> **峰元素:**基于以下条件，数组中的任何元素都被称为**峰元素**:
> 
> *   如果 arr[I–1]< arr[i] >arr[I+1]，其中 1 < I < N–1，那么 arr[i]就是峰元素。
> *   如果 arr[0] > arr[1]，那么 arr[0]就是峰值元素，其中 N 是数组的大小。
> *   如果 arr[N–2]< arr[N–1]，那么 arr[N–1]是峰元素，其中 N 是数组的大小。
> 
> 如果数组中存在多个峰值元素，则需要打印其中的最小值。

**示例:**

> **输入:** arr[] = {1，9，7，8，2，6}
> **输出**:【6，8，9，7，2，1】
> **解释:**
> 首个最小峰值= 6，为 2 < 6。
> 去除 min 峰后的数组将为[1，9，7，8，2]。
> 第二个最小峰值= 8，为 7 < 8 > 2。
> 去除最小峰后的数组将为[1，9，7，2]
> 第三个最小峰= 9，作为 1 < 9 > 7。
> 去除最小峰后的阵列将为[1，7，2]
> 第四个最小峰= 7，作为 1 < 7 > 2。
> 去除最小峰后的阵列将为[1，2]
> 第五个最小峰= 2，为 1 < 2。
> 去除最小峰后的阵列将为[1]
> 第六个最小峰= 1。
> 因此，最小峰值列表为[6，8，9，7，2，1]。
> 
> **输入:** arr []= {1，5，3，7，2}
> **输出:**【5，7，3，2，1】
> **解释:**
> 第一个最小峰值= 5，为 1 < 5 > 3。
> 去除最小峰值后的阵列将是[1，3，7，2]
> 第二个最小峰值= 7，作为 3 < 7 > 2。
> 去除最小峰后的阵列将为[1，3，2]
> 第三个最小峰= 3，作为 1 < 3 > 2。
> 去除最小峰后的阵列将为[1，2]
> 第四个最小峰= 2，为 1 < 2。
> 去除最小峰后的阵列将为[1]
> 第五个最小峰= 1。
> 因此，最小峰值列表为[5，7，3，2，1]

**方法:**思路是通过[使用两个嵌套循环迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)来找到数组的最小峰值元素，其中外部循环指向当前元素，内部循环执行以找到最小峰值元素的索引，从数组中移除该峰值元素并将当前峰值元素存储在结果列表中。完成上述步骤后，打印列表中存储的所有最小峰值元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the list of
// minimum peak elements
void minPeaks(vector<int>list)
{

    // Length of original list
    int n = list.size();

    // Initialize resultant list
    vector<int>result;

    // Traverse each element of list
    for(int i = 0; i < n; i++)
    {
        int min = INT_MAX;
        int index = -1;

        // Length of original list after
        // removing the peak element
        int size = list.size();

        // Traverse new list after removal
        // of previous min peak element
        for(int j = 0; j < size; j++)
        {

            // Update min and index,
            // if first element of
            // list > next element
            if (j == 0 && j + 1 < size)
            {
                if (list[j] > list[j + 1] &&
                        min > list[j])
                {
                    min = list[j];
                    index = j;
                }
            }

            else if (j == size - 1 &&
                     j - 1 >= 0)
            {

                // Update min and index,
                // if last element of
                // list > previous one
                if (list[j] > list[j - 1] &&
                        min > list[j])
                {
                    min = list[j];
                    index = j;
                }
            }

            // Update min and index, if
            // list has single element
            else if (size == 1)
            {
                min = list[j];
                index = j;
            }

            // Update min and index,
            // if current element >
            // adjacent elements
            else if (list[j] > list[j - 1] &&
                     list[j] > list[j + 1] &&
                         min > list[j])
            {
                min = list[j];
                index = j;
            }
        }

        // Remove current min peak
        // element from list
        list.erase(list.begin() + index);

        // Insert min peak into
        // resultant list
        result.push_back(min);
    }

    // Print resultant list
    cout << "[";
    for(int i = 0; i < result.size(); i++)
    {
        cout << result[i] << ", ";
    }
    cout << "]";
}

// Driver Code
int main()
{

    // Given array arr[]
    vector<int> arr = { 1, 9, 7, 8, 2, 6 };

    // Function call
    minPeaks(arr);
}

// This code is contributed by bikram2001jha
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to return the list of
    // minimum peak elements
    static void
    minPeaks(ArrayList<Integer> list)
    {

        // Length of original list
        int n = list.size();

        // Initialize resultant list
        ArrayList<Integer> result
            = new ArrayList<>();

        // Traverse each element of list
        for (int i = 0; i < n; i++) {

            int min = Integer.MAX_VALUE;
            int index = -1;

            // Length of original list after
            // removing the peak element
            int size = list.size();

            // Traverse new list after removal
            // of previous min peak element
            for (int j = 0; j < size; j++) {

                // Update min and index,
                // if first element of
                // list > next element
                if (j == 0 && j + 1 < size) {

                    if (list.get(j) > list.get(j + 1)
                        && min > list.get(j)) {
                        min = list.get(j);
                        index = j;
                    }
                }

                else if (j == size - 1
                         && j - 1 >= 0) {

                    // Update min and index,
                    // if last element of
                    // list > previous one
                    if (list.get(j)
                            > list.get(j - 1)
                        && min
                               > list.get(j)) {
                        min = list.get(j);
                        index = j;
                    }
                }

                // Update min and index, if
                // list has single element
                else if (size == 1) {

                    min = list.get(j);
                    index = j;
                }

                // Update min and index,
                // if current element >
                // adjacent elements
                else if (list.get(j)
                             > list.get(j - 1)
                         && list.get(j)
                                > list.get(j + 1)
                         && min
                                > list.get(j)) {

                    min = list.get(j);
                    index = j;
                }
            }

            // Remove current min peak
            // element from list
            list.remove(index);

            // Insert min peak into
            // resultant list
            result.add(min);
        }

        // Print resultant list
        System.out.println(result);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        ArrayList<Integer> arr = new ArrayList<>(
            Arrays.asList(1, 9, 7, 8, 2, 6));

        // Function Call
        minPeaks(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
import sys

# Function to return the list of
# minimum peak elements
def minPeaks(list1):

    # Length of original list
    n = len(list1)

    # Initialize resultant list
    result = []

    # Traverse each element of list
    for i in range (n):
        min = sys.maxsize
        index = -1

        # Length of original list
        # after removing the peak
        # element
        size = len(list1)

        # Traverse new list after removal
        # of previous min peak element
        for j in range (size):

            # Update min and index,
            # if first element of
            # list > next element
            if (j == 0 and j + 1 < size):

                if (list1[j] > list1[j + 1] and
                    min > list1[j]):
                    min = list1[j];
                    index = j;

            elif (j == size - 1 and
                  j - 1 >= 0):

                # Update min and index,
                # if last element of
                # list > previous one
                if (list1[j] > list1[j - 1] and
                    min > list1[j]):
                    min = list1[j]
                    index = j

            # Update min and index, if
            # list has single element
            elif (size == 1):
                min = list1[j]
                index = j

            # Update min and index,
            # if current element >
            # adjacent elements
            elif (list1[j] > list1[j - 1] and
                  list1[j] > list1[j + 1] and
                  min > list1[j]):
                min = list1[j]
                index = j

        # Remove current min peak
        # element from list
        list1.pop(index)

        # Insert min peak into
        # resultant list
        result.append(min)

    # Print resultant list
    print (result)

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [1, 9, 7, 8, 2, 6]

    # Function call
    minPeaks(arr)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to return the list of
// minimum peak elements
static void minPeaks(List<int> list)
{
  // Length of original list
  int n = list.Count;

  // Initialize resultant list
  List<int> result = new List<int>();

  // Traverse each element of list
  for (int i = 0; i < n; i++)
  {
    int min = int.MaxValue;
    int index = -1;

    // Length of original list after
    // removing the peak element
    int size = list.Count;

    // Traverse new list after removal
    // of previous min peak element
    for (int j = 0; j < size; j++)
    {
      // Update min and index,
      // if first element of
      // list > next element
      if (j == 0 && j + 1 < size)
      {
        if (list[j] > list[j + 1] &&
            min > list[j])
        {
          min = list[j];
          index = j;
        }
      }

      else if (j == size - 1 && j - 1 >= 0)
      {
        // Update min and index,
        // if last element of
        // list > previous one
        if (list[j] > list[j - 1] &&
            min > list[j])
        {
          min = list[j];
          index = j;
        }
      }

      // Update min and index, if
      // list has single element
      else if (size == 1)
      {
        min = list[j];
        index = j;
      }

      // Update min and index,
      // if current element >
      // adjacent elements
      else if (list[j] > list[j - 1] &&
               list[j] > list[j + 1] &&
               min > list[j])
      {
        min = list[j];
        index = j;
      }
    }

    // Remove current min peak
    // element from list
    list.RemoveAt(index);

    // Insert min peak into
    // resultant list
    result.Add(min);
  }

  // Print resultant list
  for (int i = 0; i < result.Count; i++)
    Console.Write(result[i] +", ");
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  List<int> arr = new List<int>{1, 9, 7,
                                8, 2, 6};

  // Function Call
  minPeaks(arr);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return the list of
// minimum peak elements
function minPeaks(list)
{

    // Length of original list
    var n = list.length;

    // Initialize resultant list
    var result = [];

    // Traverse each element of list
    for(var i = 0; i < n; i++)
    {
        var min = 1000000000;
        var index = -1;

        // Length of original list after
        // removing the peak element
        var size = list.length;

        // Traverse new list after removal
        // of previous min peak element
        for(var j = 0; j < size; j++)
        {

            // Update min and index,
            // if first element of
            // list > next element
            if (j == 0 && j + 1 < size)
            {
                if (list[j] > list[j + 1] &&
                        min > list[j])
                {
                    min = list[j];
                    index = j;
                }
            }

            else if (j == size - 1 &&
                     j - 1 >= 0)
            {

                // Update min and index,
                // if last element of
                // list > previous one
                if (list[j] > list[j - 1] &&
                        min > list[j])
                {
                    min = list[j];
                    index = j;
                }
            }

            // Update min and index, if
            // list has single element
            else if (size == 1)
            {
                min = list[j];
                index = j;
            }

            // Update min and index,
            // if current element >
            // adjacent elements
            else if (list[j] > list[j - 1] &&
                     list[j] > list[j + 1] &&
                         min > list[j])
            {
                min = list[j];
                index = j;
            }
        }

        // Remove current min peak
        // element from list

        list.splice(index, 1);

        // Insert min peak into
        // resultant list
        result.push(min);
    }

    // Print resultant list
    document.write( "[");
    for(var i = 0; i < result.length; i++)
    {
        document.write( result[i] + ", ");
    }
    document.write( "]");
}

// Driver Code
// Given array arr[]
var arr = [1, 9, 7, 8, 2, 6];

// Function call
minPeaks(arr);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
[6, 8, 9, 7, 2, 1]
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*