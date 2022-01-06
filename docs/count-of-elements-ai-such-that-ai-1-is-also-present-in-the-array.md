# 元素 A[i]的计数，使得阵列中也存在 A[I]+1

> 原文:[https://www . geesforgeks . org/元素计数-ai-so-ai-1-也存在于阵列中/](https://www.geeksforgeeks.org/count-of-elements-ai-such-that-ai-1-is-also-present-in-the-array/)

给定一个整数数组 **arr** ，任务是计算元素‘A[I]’的数量，这样 A[i] + 1 也出现在数组中。
**注:**若阵中有重复，则分别统计。
**例:**

> **输入:**arr =【1，2，3】
> **输出:** 2
> **说明:**
> 1 和 2 被计数，因为 2 和 3 在 arr 中。
> **输入:** arr = [1，1，3，3，5，5，7，7]
> **输出:** 0

**<u>方法 1:蛮力解</u>**
对于数组中的所有元素，检查完所有元素后返回总计数

*   对于当前元素 x，计算 x + 1，并搜索 x + 1 的当前值前后的所有位置。
*   如果你找到 x + 1，把总数加 1

以下是上述方法的实现:

## C++

```
// C++ program to count of elements
// A[i] such that A[i] + 1
// is also present in the Array
#include <bits/stdc++.h>
using namespace std;

// Function to find the countElements
int countElements(int* arr, int n)
{
    // Initialize count as zero
    int count = 0;

    // Iterate over each element
    for (int i = 0; i < n; i++) {

        // Store element in int x
        int x = arr[i];

        // Calculate x + 1
        int xPlusOne = x + 1;

        // Initialize found as false
        bool found = false;

        // Run loop to search for x + 1
        // after the current element
        for (int j = i + 1; j < n; j++) {
            if (arr[j] == xPlusOne) {
                found = true;
                break;
            }
        }

        // Run loop to search for x + 1
        // before the current element
        for (int k = i - 1;
             !found && k >= 0; k--) {
            if (arr[k] == xPlusOne) {
                found = true;
                break;
            }
        }

        // if found is true, increment count
        if (found == true) {
            count++;
        }
    }

    return count;
}

// Driver program
int main()
{
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // call countElements function on array
    cout << countElements(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count of elements
// A[i] such that A[i] + 1
// is also present in the Array
import java.io.*;
import java.util.Arrays;

class GFG{

// Function to find the countElements
public static int countElements(int[] arr, int n)
{

    // Initialize count as zero
    int count = 0;

    // Iterate over each element
    for (int i = 0; i < n; i++)
    {

        // Store element in int x
        int x = arr[i];

        // Calculate x + 1
        int xPlusOne = x + 1;

        // Initialize found as false
        boolean found = false;

        // Run loop to search for x + 1
        // after the current element
        for (int j = i + 1; j < n; j++)
        {
            if (arr[j] == xPlusOne)
            {
                found = true;
                break;
            }
        }

        // Run loop to search for x + 1
        // before the current element
        for (int k = i - 1; !found && k >= 0; k--)
        {
            if (arr[k] == xPlusOne)
            {
                found = true;
                break;
            }
        }

        // If found is true, increment count
        if (found == true)
        {
            count++;
        }
    }
        return count;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 3 };
    int n = arr.length;

    // Call countElements function on array
    System.out.println(countElements(arr, n));
}
}

//This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 program to count of elements
# A[i] such that A[i] + 1
# is also present in the Array

# Function to find the countElements
def countElements(arr,n):
    # Initialize count as zero
    count = 0

    # Iterate over each element
    for i in range(n):

        # Store element in int x
        x = arr[i]

        # Calculate x + 1
        xPlusOne = x + 1

        # Initialize found as false
        found = False

        # Run loop to search for x + 1
        # after the current element
        for j in range(i + 1,n,1):
            if (arr[j] == xPlusOne):
                found = True
                break

        # Run loop to search for x + 1
        # before the current element
        k = i - 1
        while(found == False and k >= 0):
            if (arr[k] == xPlusOne):
                found = True
                break
            k -= 1

        # if found is true, increment count
        if (found == True):
            count += 1

    return count

# Driver program
if __name__ == '__main__':
    arr = [1, 2, 3]
    n = len(arr)

    # call countElements function on array
    print(countElements(arr, n))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to count of elements
// A[i] such that A[i] + 1
// is also present in the Array
using System;

class GFG{

    // Function to find the countElements
    static int countElements(int[] arr, int n)
    {
        // Initialize count as zero
        int count = 0;

        // Iterate over each element
        for (int i = 0; i < n; i++) {

            // Store element in int x
            int x = arr[i];

            // Calculate x + 1
            int xPlusOne = x + 1;

            // Initialize found as false
            bool found = false;

            // Run loop to search for x + 1
            // after the current element
            for (int j = i + 1; j < n; j++) {
                if (arr[j] == xPlusOne) {
                    found = true;
                    break;
                }
            }

            // Run loop to search for x + 1
            // before the current element
            for (int k = i - 1;
                !found && k >= 0; k--) {
                if (arr[k] == xPlusOne) {
                    found = true;
                    break;
                }
            }

            // if found is true,
            // increment count
            if (found == true) {
                count++;
            }
        }

        return count;
    }

    // Driver program
    static public void Main ()
    {
        int[] arr = { 1, 2, 3 };
        int n = arr.Length;

        // call countElements function on array
        Console.WriteLine(countElements(arr, n));

    }
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>
// JavaScript program to count of elements
// A[i] such that A[i] + 1
// is also present in the Array

// Function to find the countElements
function countElements(arr, n)
{
    // Initialize count as zero
    let count = 0;

    // Iterate over each element
    for (let i = 0; i < n; i++) {

        // Store element in int x
        let x = arr[i];

        // Calculate x + 1
        let xPlusOne = x + 1;

        // Initialize found as false
        let found = false;

        // Run loop to search for x + 1
        // after the current element
        for (let j = i + 1; j < n; j++)
        {
            if (arr[j] == xPlusOne)
            {
                found = true;
                break;
            }
        }

        // Run loop to search for x + 1
        // before the current element
        for (let k = i - 1;
            !found && k >= 0; k--) {
            if (arr[k] == xPlusOne) {
                found = true;
                break;
            }
        }

        // if found is true, increment count
        if (found == true) {
            count++;
        }
    }
    return count;
}

// Driver program
    let arr = [ 1, 2, 3 ];
    let n = arr.length;

    // call countElements function on array
    document.write(countElements(arr, n));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
2
```

**时间复杂度**:在上面的方法中，对于给定的元素，我们检查所有其他元素，所以时间复杂度是 **O(N*N)** ，其中 N 是元素的个数。
**辅助空间复杂度**:在上面的做法中，我们没有使用任何额外的空间，所以辅助空间复杂度为 **O(1)** 。
**<u>方法二:使用</u>** [**<u>地图</u>**](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)

*   对于数组中的所有元素，比如 x，将 x-1 添加到映射中
*   同样，对于数组中的所有元素，比如 x，检查它是否存在于映射中。如果存在，递增计数器
*   检查地图中的所有关键点后，返回总计数

以下是上述方法的实现:

## C++

```
// C++ program to count of elements
// A[i] such that A[i] + 1
// is also present in the Array

#include <bits/stdc++.h>
using namespace std;

// Function to find the countElements
int countElements(vector<int>& arr)
{
    int size = arr.size();

    // Initialize result as zero
    int res = 0;

    // Create map
    map<int, bool> dat;

    // First loop to fill the map
    for (int i = 0; i < size; ++i) {
        dat[arr[i] - 1] = true;
    }

    // Second loop to check the map
    for (int i = 0; i < size; ++i) {
        if (dat[arr[i]] == true) {
            res++;
        }
    }
    return res;
}

// Driver program
int main()
{
    // Input Array
    vector<int> arr = { 1, 3, 2, 3, 5, 0 };

    // Call the countElements function
    cout << countElements(arr) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count of elements
// A[i] such that A[i] + 1 is 
// also present in the Array
import java.util.*;

class GFG{

// Function to find the countElements
public static int countElements(int[] arr)
{
    int size = arr.length;

    // Initialize result as zero
    int res = 0;

    // Create map
    Map<Integer, Boolean> dat = new HashMap<>();

    // First loop to fill the map
    for(int i = 0; i < size; ++i)
    {
       dat.put((arr[i] - 1), true);
    }

    // Second loop to check the map
    for(int i = 0; i < size; ++i)
    {
       if (dat.containsKey(arr[i]) == true)
       {
           res++;
       }
    }
    return res;
}

// Driver code
public static void main(String[] args)
{

    // Input Array
    int[] arr = { 1, 3, 2, 3, 5, 0 };

    // Call the countElements function
    System.out.println(countElements(arr));

}
}

// This code is contributed by shad0w1947
```

## 蟒蛇 3

```
# Python program to count of elements
# A[i] such that A[i] + 1
# is also present in the Array

# Function to find the countElements
def countElements(arr):

    size = len(arr)

    # Initialize result as zero
    res = 0

    # Create map
    dat={}

    # First loop to fill the map
    for i in range(size):
        dat[arr[i] - 1] = True

    # Second loop to check the map
    for i in range(size):
        if (arr[i] in dat):
            res += 1

    return res

# Driver program

# Input Array
arr =  [1, 3, 2, 3, 5, 0]

# Call the countElements function
print(countElements(arr))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to count of elements
// A[i] such that A[i] + 1 is
// also present in the Array
using System;
using System.Collections.Generic;
class GFG{

// Function to find the countElements
public static int countElements(int[] arr)
{
    int size = arr.Length;

    // Initialize result as zero
    int res = 0;

    // Create map
    Dictionary<int,
               Boolean> dat = new Dictionary<int,
                                             Boolean>();

    // First loop to fill the map
    for(int i = 0; i < size; ++i)
    {
       if(!dat.ContainsKey(arr[i] - 1))
          dat.Add((arr[i] - 1), true);
    }

    // Second loop to check the map
    for(int i = 0; i < size; ++i)
    {
       if (dat.ContainsKey(arr[i]) == true)
       {
           res++;
       }
    }
    return res;
}

// Driver code
public static void Main(String[] args)
{

    // Input Array
    int[] arr = { 1, 3, 2, 3, 5, 0 };

    // Call the countElements function
    Console.WriteLine(countElements(arr));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to count of elements
// A[i] such that A[i] + 1 is 
// also present in the Array

    // Function to find the countElements
    function countElements(arr) {
        var size = arr.length;

        // Initialize result as zero
        var res = 0;

        // Create map
        var dat = new Map();

        // First loop to fill the map
        for (i = 0; i < size; ++i) {
            dat.set((arr[i] - 1), true);
        }

        // Second loop to check the map
        for (i = 0; i < size; ++i) {
            if (dat.has(arr[i]) == true) {
                res++;
            }
        }
        return res;
    }

        // Input Array
        var arr = [ 1, 3, 2, 3, 5, 0 ];

        // Call the countElements function
        document.write(countElements(arr));

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
3
```

**时间复杂度**:在上面的方法中，我们迭代数组两次。一次用于填充地图，第二次用于检查地图中的元素，因此时间复杂度为 **O(N)** ，其中 N 为元素个数。
**辅助空间复杂度**:在上面的方法中，我们使用了一个可以包含 N 个元素的附加地图，所以辅助空间复杂度为 **O(N)** 。