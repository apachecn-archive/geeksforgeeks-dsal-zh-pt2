# 将小盒子放在大盒子里面，减少盒子数量

> 原文:[https://www . geesforgeks . org/通过将小盒子放入大盒子中来最小化盒子数量/](https://www.geeksforgeeks.org/minimize-number-of-boxes-by-putting-small-box-inside-bigger-one/)

给定一个盒子大小的数组**size【】**，我们的任务是在将较小的盒子放入较大的盒子后，找到最后剩下的盒子数量。
***注:**一个盒子里面只能装一个小盒子。*
**示例:**

> **输入:** size[] = {1，2，3 }
> T3】输出: 1
> **说明:**
> 这里，1 号的盒子可以放在 2 号的盒子里面，2 号的盒子可以放在 3 号的盒子里面。所以最后我们只有一个 3 号的盒子。
> 
> **输入:**大小[] = {1，2，2，3，7，4，2，1}
> **输出:** 3
> **解释:**
> 将大小为 1，2，3，4 和 7 的盒子放在一起，对于第二个盒子，将 1 和 2 放在一起。最后只剩下两个，谁也装不下。所以我们还剩 3 个盒子。

**方法:**思路是按照下面给出的步骤:

*   按递增顺序对给定的数组大小[]进行排序，并检查当前框的大小是否大于下一个框的大小。如果是，则减少初始箱号。
*   否则，如果当前框的大小等于下一个框的大小，则检查当前框是否可以放入下一个框的大小。如果是，则移动当前框指向变量，否则进一步移动下一个指向变量。

下面是上述方法的实现:

## C++

```
// C++ implementation to minimize the
// number of the box by putting small
// box inside the bigger one

#include <bits/stdc++.h>
using namespace std;

// Function to minimize the count
void minBox(int arr[], int n)
{
    // Initial number of box
    int box = n;

    // Sort array of box size
    // in increasing order
    sort(arr, arr + n);

    int curr_box = 0, next_box = 1;
    while (curr_box < n && next_box < n) {

        // check is current box size
        // is smaller than next box size
        if (arr[curr_box] < arr[next_box]) {

            // Decrement box count
            // Increment current box count
            // Increment next box count
            box--;
            curr_box++;
            next_box++;
        }

        // Check if both box
        // have same size
        else if (arr[curr_box] == arr[next_box])
            next_box++;
    }

    // Print the result
    cout << box << endl;
}

// Driver code
int main()
{
    int size[] = { 1, 2, 3 };
    int n = sizeof(size) / sizeof(size[0]);
    minBox(size, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to minimize the
// number of the box by putting small
// box inside the bigger one
import java.util.Arrays;

class GFG{

// Function to minimize the count
public static void minBox(int arr[], int n)
{

    // Initial number of box
    int box = n;

    // Sort array of box size
    // in increasing order
    Arrays.sort(arr);

    int curr_box = 0, next_box = 1;
    while (curr_box < n && next_box < n)
    {

        // Check is current box size
        // is smaller than next box size
        if (arr[curr_box] < arr[next_box])
        {

            // Decrement box count
            // Increment current box count
            // Increment next box count
            box--;
            curr_box++;
            next_box++;
        }

        // Check if both box
        // have same size
        else if (arr[curr_box] ==
                 arr[next_box])
            next_box++;
    }

    // Print the result
    System.out.println(box);
}

// Driver code
public static void main(String args[])
{
    int []size = { 1, 2, 3 };
    int n = size.length;

    minBox(size, n);
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 implementation to minimize the
# number of the box by putting small
# box inside the bigger one

# Function to minimize the count
def minBox(arr, n):

    # Initial number of box
    box = n

    # Sort array of box size
    # in increasing order
    arr.sort()

    curr_box, next_box = 0, 1
    while (curr_box < n and next_box < n):

        # Check is current box size
        # is smaller than next box size
        if (arr[curr_box] < arr[next_box]):

            # Decrement box count
            # Increment current box count
            # Increment next box count
            box = box - 1
            curr_box = curr_box + 1
            next_box = next_box + 1

        # Check if both box
        # have same size
        elif (arr[curr_box] == arr[next_box]):
            next_box = next_box + 1

    # Print the result
    print(box)

# Driver code
size = [ 1, 2, 3 ]
n = len(size)

minBox(size, n)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation to minimize the
// number of the box by putting small
// box inside the bigger one
using System;

class GFG{

// Function to minimize the count
public static void minBox(int []arr, int n)
{

    // Initial number of box
    int box = n;

    // Sort array of box size
    // in increasing order
    Array.Sort(arr);

    int curr_box = 0, next_box = 1;
    while (curr_box < n && next_box < n)
    {

        // Check is current box size
        // is smaller than next box size
        if (arr[curr_box] < arr[next_box])
        {

            // Decrement box count
            // Increment current box count
            // Increment next box count
            box--;
            curr_box++;
            next_box++;
        }

        // Check if both box
        // have same size
        else if (arr[curr_box] ==
                 arr[next_box])
            next_box++;
    }

    // Print the result
    Console.WriteLine(box);
}

// Driver code
public static void Main(String []args)
{
    int []size = { 1, 2, 3 };
    int n = size.Length;

    minBox(size, n);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// javascript implementation to minimize the
// number of the box by putting small
// box inside the bigger one

// Function to minimize the count
function minBox(arr,  n)
{

    // Initial number of box
    var box = n;

    // Sort array of box size
    // in increasing order
    arr.sort();

    var curr_box = 0, next_box = 1;
    while (curr_box < n && next_box < n)
    {

        // Check is current box size
        // is smaller than next box size
        if (arr[curr_box] < arr[next_box])
        {

            // Decrement box count
            // Increment current box count
            // Increment next box count
            box--;
            curr_box++;
            next_box++;
        }

        // Check if both box
        // have same size
        else if (arr[curr_box] ==
                 arr[next_box])
            next_box++;
    }

    // Print the result
    document.write(box);
}

// Driver code

    var size = [ 1, 2, 3 ];
    var n = size.length;

    minBox(size, n);

</script>
```

**Output**

```
1
```

***时间复杂度:** O(N*logN)为 Arrays.sort()方法使用。*
***辅助空间:** O(1)*

**逼近:**问题中的关键观察是最小盒子数与数组中任意元素的最大频率相同。因为其余的元素是相互调整的。下面是借助步骤的图示:

*   创建一个哈希映射来存储元素的频率。
*   最后，在保持频率后返回元素的最大频率。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach

import java.util.*;

public class Boxes {

    // Function to count the boxes
    // at the end
    int countBoxes(int[] A) {

        // Default value if
        // array is empty
        int count = -1;
        int n = A.length;

         // Map to store frequencies
        Map<Integer, Integer> map =
          new HashMap<>();

        // Loop to iterate over the
        // elements of the array
        for (int i=0; i<n; i++) {
            int key = A[i];
            map.put(key,
              map.getOrDefault(key, 0) + 1);
            int val = map.get(key);

            // Condition to get the maximum
            // value of the key
            if (val > count) count = val;
        }
        return count;
    }

    // Driver Code
    public static void main(
                  String[] args)
    {
        int[] a = {8, 15, 1, 10, 5, 1};
        Boxes obj = new Boxes();

        // Function Call
        int minBoxes = obj.countBoxes(a);
          System.out.println(minBoxes);
    }
}
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)