# 从阵列中删除所有奇数频率元素

> 原文:[https://www . geesforgeks . org/delete-all-奇数频率-从数组中删除元素/](https://www.geeksforgeeks.org/delete-all-odd-frequency-elements-from-an-array/)

给定一个包含大小为 **N** 的整数的数组 **arr** ，任务是从数组中删除所有具有奇数频率的元素。
**例:**

> **输入:** arr[] = {3，3，3，2，2，4，7，7}
> **输出:** {2，2，7，7}
> **解释:**
> 频率为 3 = 3
> 频率为 2 = 2
> 频率为 4 = 1
> 频率为 7 = 2
> 因此，元素 3 和 4 具有奇数频率，因此被移除。
> **输入:** arr[] = {1，3，3，1，2，5，6，5}
> **输出:** {1，3，3，1，5，5}

**进场:**

*   创建一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)并将数组中每个元素的[频率存储到同一个图中。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   然后，[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，借助地图找出哪些元素有奇频。
*   忽略所有具有奇数频率的元素，打印其余的

以下是上述方法的实现:

## C++

```
// C++ program to removes all odd
// frequency elements from an Array

#include <bits/stdc++.h>
using namespace std;

// Function that removes the
// elements which have odd
// frequencies in the array
void remove(int arr[], int n)
{
    // Create a map to store the
    // frequency of each element
    unordered_map<int, int> m;
    for (int i = 0; i < n; i++) {
        m[arr[i]]++;
    }

    // Remove the elements which
    // have odd frequencies
    for (int i = 0; i < n; i++) {

        // If the element has
        // odd frequency then skip
        if ((m[arr[i]] & 1))
            continue;

        cout << arr[i] << ", ";
    }
}

// Driver code
int main()
{
    int arr[]
        = { 3, 3, 3, 2,
            2, 4, 7, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    remove(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to removes all odd
// frequency elements from an Array
import java.util.*;

class GFG {

    // Function that removes the
    // elements which have odd
    // frequencies in the array
    static void remove(int arr[], int n) {
        // Create a map to store the
        // frequency of each element
        HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>();
        for (int i = 0; i < n; i++) {
            if (mp.containsKey(arr[i])) {
                mp.put(arr[i], mp.get(arr[i]) + 1);
            } else {
                mp.put(arr[i], 1);
            }
        }

        // Remove the elements which
        // have odd frequencies
        for (int i = 0; i < n; i++) {

            // If the element has
            // odd frequency then skip
            if ((mp.containsKey(arr[i]) && mp.get(arr[i]) % 2 == 1))
                continue;

            System.out.print(arr[i] + ", ");
        }
    }

    // Driver code
    public static void main(String[] args) {
        int arr[] = { 3, 3, 3, 2, 2, 4, 7, 7 };
        int n = arr.length;

        // Function call
        remove(arr, n);

    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to removes all odd
# frequency elements from an Array

# Function that removes the
# elements which have odd
# frequencies in the array
def remove(arr,  n) :

    # Create a map to store the
    # frequency of each element
    m = dict.fromkeys(arr,0);
    for i in range(n) :
        m[arr[i]] += 1;

    # Remove the elements which
    # have odd frequencies
    for i in range(n) :

        # If the element has
        # odd frequency then skip
        if ((m[arr[i]] & 1)) :
            continue;

        print(arr[i],end= ", ");

# Driver code
if __name__ == "__main__" :

    arr    = [ 3, 3, 3, 2,
            2, 4, 7, 7 ];
    n = len(arr);

    # Function call
    remove(arr, n);

# This code is contributed by Yash_R
```

## C#

```
// C# program to removes all odd
// frequency elements from an Array
using System;
using System.Collections.Generic;

class GFG {

    // Function that removes the
    // elements which have odd
    // frequencies in the array
    static void remove(int []arr, int n) {

        // Create a map to store the
        // frequency of each element
        Dictionary<int, int> mp = new Dictionary<int, int>();
        for (int i = 0; i < n; i++) {
            if (mp.ContainsKey(arr[i])) {
                mp[arr[i]] =  mp[arr[i]] + 1;
            } else {
                mp.Add(arr[i], 1);
            }
        }

        // Remove the elements which
        // have odd frequencies
        for (int i = 0; i < n; i++) {

            // If the element has
            // odd frequency then skip
            if ((mp.ContainsKey(arr[i]) && mp[arr[i]] % 2 == 1))
                continue;

            Console.Write(arr[i] + ", ");
        }
    }

    // Driver code
    public static void Main(String[] args) {
        int []arr = { 3, 3, 3, 2, 2, 4, 7, 7 };
        int n = arr.Length;

        // Function call
        remove(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to removes all odd
// frequency elements from an Array

    // Function that removes the
    // elements which have odd
    // frequencies in the array
    function remove(arr, n) {
        // Create a map to store the
        // frequency of each element
        let mp = new Map();
        for (let i = 0; i < n; i++) {
            if (mp.has(arr[i])) {
                mp.set(arr[i], mp.get(arr[i]) + 1);
            } else {
                mp.set(arr[i], 1);
            }
        }

        // Remove the elements which
        // have odd frequencies
        for (let i = 0; i < n; i++) {

            // If the element has
            // odd frequency then skip
            if ((mp.has(arr[i]) && mp.get(arr[i]) % 2 == 1))
                continue;

            document.write(arr[i] + ", ");
        }
    }

// Driver code

      let arr = [ 3, 3, 3, 2, 2, 4, 7, 7 ];
        let n = arr.length;

        // Function call
        remove(arr, n);

</script>
```

**Output**

```
2, 2, 7, 7, 
```

**时间复杂度:O(N)**

**辅助空间:O(N)**