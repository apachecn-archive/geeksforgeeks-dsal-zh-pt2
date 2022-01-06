# 寻找数组中 k 个最小差 d 的有序对

> 原文:[https://www . geesforgeks . org/find-k-最小差阵列中的有序对-d/](https://www.geeksforgeeks.org/find-k-ordered-pairs-in-array-with-minimum-difference-d/)

给定一个数组 **arr[]** 和两个整数 **K** 和 **D** ，任务是从数组中精确找到 **K** 对 **(arr[i]，arr[j])** ，使得**| arr[I]–arr[j]|≥D**和 **i！= j** 。如果无法获得这样的配对，则打印 **-1** 。**注意**单个元素只能参与单个对。
**示例:**

> **输入:** arr[] = {4，6，10，23，14，7，2，20，9}，K = 4，D = 3
> **输出:**
> (2，10)
> (4，14)
> (6，20)
> (7，23)
> **输入:** arr[] = {2，10，4，6，12，5，7，3，1，9

**方法:**如果我们必须只找到 1 对，那么我们将只检查数组中的最大和最小元素。同样，为了获得 **K** 对，我们可以将**最小 K** 元素与对应的**最大 K** 元素进行比较。[排序](https://www.geeksforgeeks.org/sorting-algorithms/)可用于获取最小和最大元素。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required pairs
void findPairs(int arr[], int n, int k, int d)
{

    // There has to be atleast 2*k elements
    if (n < 2 * k) {
        cout << -1;
        return;
    }

    // To store the pairs
    vector<pair<int, int> > pairs;

    // Sort the given array
    sort(arr, arr + n);

    // For every possible pair
    for (int i = 0; i < k; i++) {

        // If the current pair is valid
        if (arr[n - k + i] - arr[i] >= d) {

            // Insert it into the pair vector
            pair<int, int> p = make_pair(arr[i], arr[n - k + i]);
            pairs.push_back(p);
        }
    }

    // If k pairs are not possible
    if (pairs.size() < k) {
        cout << -1;
        return;
    }

    // Print the pairs
    for (auto v : pairs) {
        cout << "(" << v.first << ", "
             << v.second << ")" << endl;
    }
}

// Driver code
int main()
{
    int arr[] = { 4, 6, 10, 23, 14, 7, 2, 20, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4, d = 3;

    findPairs(arr, n, k, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    static class pair
    {
        int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

    // Function to find the required pairs
    static void findPairs(int arr[], int n,
                          int k, int d)
    {

        // There has to be atleast 2*k elements
        if (n < 2 * k)
        {
            System.out.print(-1);
            return;
        }

        // To store the pairs
        Vector<pair> pairs = new Vector<pair>();

        // Sort the given array
        Arrays.sort(arr);

        // For every possible pair
        for (int i = 0; i < k; i++)
        {

            // If the current pair is valid
            if (arr[n - k + i] - arr[i] >= d)
            {

                // Insert it into the pair vector
                pair p = new pair(arr[i],
                                  arr[n - k + i]);
                pairs.add(p);
            }
        }

        // If k pairs are not possible
        if (pairs.size() < k)
        {
            System.out.print(-1);
            return;
        }

        // Print the pairs
        for (pair v : pairs)
        {
            System.out.println("(" + v.first +
                               ", " + v.second + ")");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 4, 6, 10, 23, 14, 7, 2, 20, 9 };
        int n = arr.length;
        int k = 4, d = 3;

        findPairs(arr, n, k, d);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the required pairs
def findPairs(arr, n, k, d):

    # There has to be atleast 2*k elements
    if (n < 2 * k):
        print("-1")
        return

    # To store the pairs
    pairs=[]

    # Sort the given array
    arr=sorted(arr)

    # For every possible pair
    for i in range(k):

        # If the current pair is valid
        if (arr[n - k + i] - arr[i] >= d):

            # Insert it into the pair vector
            pairs.append([arr[i], arr[n - k + i]])

    # If k pairs are not possible
    if (len(pairs) < k):
        print("-1")
        return

    # Print the pairs
    for v in pairs:
        print("(",v[0],", ",v[1],")")

# Driver code

arr = [4, 6, 10, 23, 14, 7, 2, 20, 9]
n = len(arr)
k = 4
d = 3

findPairs(arr, n, k, d)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    public class pair
    {
        public int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

    // Function to find the required pairs
    static void findPairs(int []arr, int n,
                          int k, int d)
    {

        // There has to be atleast 2*k elements
        if (n < 2 * k)
        {
            Console.Write(-1);
            return;
        }

        // To store the pairs
        List<pair> pairs = new List<pair>();

        // Sort the given array
        Array.Sort(arr);

        // For every possible pair
        for (int i = 0; i < k; i++)
        {

            // If the current pair is valid
            if (arr[n - k + i] - arr[i] >= d)
            {

                // Insert it into the pair vector
                pair p = new pair(arr[i],
                                  arr[n - k + i]);
                pairs.Add(p);
            }
        }

        // If k pairs are not possible
        if (pairs.Count < k)
        {
            Console.Write(-1);
            return;
        }

        // Print the pairs
        foreach (pair v in pairs)
        {
            Console.WriteLine ("(" + v.first +
                               ", " + v.second + ")");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 4, 6, 10, 23,
                      14, 7, 2, 20, 9 };
        int n = arr.Length;
        int k = 4, d = 3;

        findPairs(arr, n, k, d);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to find the required pairs
function findPairs(arr, n, k, d) {

    // There has to be atleast 2*k elements
    if (n < 2 * k) {
        document.write(-1);
        return;
    }

    // To store the pairs
    let pairs = [];

    // Sort the given array
    arr.sort((a, b) => a - b);

    // For every possible pair
    for (let i = 0; i < k; i++) {

        // If the current pair is valid
        if (arr[n - k + i] - arr[i] >= d) {

            // Insert it into the pair vector
            let p = [arr[i], arr[n - k + i]];
            pairs.push(p);
        }
    }

    // If k pairs are not possible
    if (pairs.length < k) {
        document.write(-1);
        return;
    }

    // Print the pairs
    for (let v of pairs) {
        document.write("(" + v[0] + ", " + v[1] + ")" + "<br>");
    }
}

// Driver code

let arr = [4, 6, 10, 23, 14, 7, 2, 20, 9];
let n = arr.length;
let k = 4, d = 3;

findPairs(arr, n, k, d);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
(2, 10)
(4, 14)
(6, 20)
(7, 23)
```