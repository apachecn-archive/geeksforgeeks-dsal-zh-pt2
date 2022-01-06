# 找到 d，最大化创建为 c[i] = d*a[i] + b[i]

的数组 c[]中的零数量

> 原文:[https://www . geeksforgeeks . org/find-d-最大化数组中的零的数量-c-created as-ci-Dai-bi/](https://www.geeksforgeeks.org/find-d-to-maximize-the-number-of-zeros-in-array-c-created-as-ci-dai-bi/)

给定两个数组 **N 个**整数。考虑一个数组 **C** ，其中第 I 个整数将是 **d*a[i] + b[i]** ，其中 d 是任意实数。任务是打印 d，使得数组 C 具有最大数量的零，并且也打印零的数量。
**举例:**

> **输入:** a[] = {1，2，3，4，5}，b[] = {2，4，7，11，3}
> **输出:**
> d 的值为:-2
> 数组 C 中的零个数为:2
> 如果我们选择 d 为-2，那么我们在数组 C 中得到两个零，这是最大可能的。
> **输入:** a[] = {13，37，39} b[] = {1，2，3}
> **输出:**
> d 的值为:-0.0769231
> 数组 C 中的零个数为:

可以按照以下步骤解决上述问题:

*   等式可以改写为 **d = -b[i]/a[i]**
*   使用散列表来计算任何实数的最大出现次数，以获得 d 的值。
*   零的数量将是最大计数+(a[I]和 b[i]对的数量，其中两者都是 0)。

以下是上述方法的实现:

## C++

```
// C++ program to implement the above
// approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the value of d
// and find the number of zeros in the array
void findDandZeros(int a[], int b[], int n)
{

    // Hash table
    unordered_map<long double, int> mpp;

    int count = 0;

    // Iterate for i-th element
    for (int i = 0; i < n; i++) {

        // If both are not 0
        if (b[i] != 0 && a[i] != 0) {
            long double val = (long double)(-1.0 * b[i]) /
                              (long double)(a[i]);
            mpp[val] += 1;
        }

        // If both are 0
        else if (b[i] == 0 && a[i] == 0)
            count += 1;
    }

    // Find max occurring d
    int maxi = 0;
    for (auto it : mpp) {
        maxi = max(it.second, maxi);
    }

    // Print the d which occurs max times
    for (auto it : mpp) {
        if (it.second == maxi) {
            cout << "Value of d is: "
                 << it.first << endl;
            break;
        }
    }

    // Print the number of zeros
    cout << "The number of zeros in array C is: "
         << maxi + count;
}

// Driver code
int main()
{
    int a[] = { 13, 37, 39 };
    int b[] = { 1, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    findDandZeros(a, b, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above
// approach
import java.util.*;

class geeks
{

    // Function to find the value of d
    // and find the number of zeros in the array
    public static void findDandZeroes(int[] a, int[] b, int n)
    {

        // Hash table
        HashMap<Double, Integer> mpp = new HashMap<>();

        int count = 0;

        // Iterate for i-th element
        for (int i = 0; i < n; i++)
        {

            // If both are not 0
            if (b[i] != 0 && a[i] != 0)
            {
                double val = (double) (-1.0 * b[i]) / (double) (a[i]);
                if (mpp.get(val) != null)
                {
                    int x = mpp.get(val);
                    mpp.put(val, ++x);
                }
                else
                    mpp.put(val, 1);
            }

            // If both are 0
            else if (b[i] == 0 && a[i] == 0)
                count += 1;
        }

        // Find max occurring d
        int maxi = 0;
        for (HashMap.Entry<Double, Integer> entry : mpp.entrySet())
        {
            maxi = Math.max(entry.getValue(), maxi);
        }

        // Print the d which occurs max times
        for (HashMap.Entry<Double, Integer> entry : mpp.entrySet())
        {
            if (entry.getValue() == maxi)
            {
                System.out.println("Value of d is: " + entry.getKey());
                break;
            }
        }

        // Print the number of zeros
        System.out.println("The number of zeros in array C is: " +
                                                (maxi + count));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a = { 13, 37, 39 };
        int[] b = { 1, 2, 3 };
        int n = a.length;

        findDandZeroes(a, b, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach

# Function to find the value of d and
# find the number of zeros in the array
def findDandZeros(a, b, n) :

    # Hash table
    mpp = {};

    count = 0;

    # Iterate for i-th element
    for i in range(n) :

        # If both are not 0
        if (b[i] != 0 and a[i] != 0) :
            val = (-1.0 * b[i]) / a[i];

            if val not in mpp :
                mpp[val] = 0;

            mpp[val] += 1;

        # If both are 0
        elif (b[i] == 0 and a[i] == 0) :
            count += 1;

    # Find max occurring d
    maxi = 0;
    for item in mpp :
        maxi = max(mpp[item], maxi);

    # Print the d which occurs max times
    for keys, values in mpp.items() :
        if (values == maxi) :
            print("Value of d is:", keys);
            break;

    # Print the number of zeros
    print("The number of zeros in array C is:",
                                 maxi + count);

# Driver code
if __name__ == "__main__" :
    a = [ 13, 37, 39 ];
    b = [ 1, 2, 3 ];

    n = len(a);
    findDandZeros(a, b, n);

# This code is contributed by Ryuga
```

## C#

```
// C# program to implement the above
// approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the value of d
    // and find the number of zeros in the array
    public static void findDandZeroes(int[] a,
                                      int[] b, int n)
    {

        // Hash table
        Dictionary<double,
                   int> mpp = new Dictionary<double,
                                             int>();
        int count = 0;

        // Iterate for i-th element
        for (int i = 0; i < n; i++)
        {

            // If both are not 0
            if (b[i] != 0 && a[i] != 0)
            {
                double val = (double)(-1.0 * b[i]) /
                             (double)(a[i]);
                if (mpp.ContainsKey(val))
                {
                    mpp[val] = ++mpp[val];
                }
                else
                    mpp.Add(val, 1);
            }

            // If both are 0
            else if (b[i] == 0 && a[i] == 0)
                count += 1;
        }

        // Find max occurring d
        int maxi = 0;
        foreach(KeyValuePair<double, int> entry in mpp)
        {
            maxi = Math.Max(entry.Value, maxi);
        }

        // Print the d which occurs max times
        foreach(KeyValuePair<double, int> entry in mpp)
        {
            if (entry.Value == maxi)
            {
                Console.WriteLine("Value of d is: " +
                                          entry.Key);
                break;
            }
        }

        // Print the number of zeros
        Console.WriteLine("The number of zeros in array C is: " +
                                                 (maxi + count));
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] a = { 13, 37, 39 };
        int[] b = { 1, 2, 3 };
        int n = a.Length;

        findDandZeroes(a, b, n);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to implement the above
// approach

// Function to find the value of d
// and find the number of zeros in the array
function findDandZeros(a, b, n)
{

    // Hash table
    var mpp = new Map();

    var count = 0;

    // Iterate for i-th element
    for (var i = 0; i < n; i++) {

        // If both are not 0
        if (b[i] != 0 && a[i] != 0) {
            var val = (-1.0 * b[i]) / (a[i]);
            if(mpp.has(val))
                mpp.set(val, mpp.get(val)+1)
            else  
                mpp.set(val, 1)
        }

        // If both are 0
        else if (b[i] == 0 && a[i] == 0)
            count += 1;
    }

    // Find max occurring d
    var maxi = 0;

    mpp.forEach((value, key) => {

        maxi = Math.max(value, maxi);
    });

    // Print the d which occurs max times
    mpp.forEach((value, key) => {
        if (value == maxi) {
            document.write( "Value of d is: "
                 + key + "<br>");

        }
    });

    // Print the number of zeros
    document.write( "The number of zeros in array C is: "
         + (maxi + count));
}

// Driver code
var a = [13, 37, 39];
var b = [1, 2, 3];
var n = a.length;
findDandZeros(a, b, n);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
Value of d is: -0.0769231
The number of zeros in array C is: 2
```