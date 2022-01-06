# 用给定的异或对所有对进行计数

> 原文:[https://www.geeksforgeeks.org/count-pairs-given-xor/](https://www.geeksforgeeks.org/count-pairs-given-xor/)

给定一个不同正整数的数组和一个数 x，求数组中异或等于 x 的整数对的个数。

**示例:**

```
Input : arr[] = {5, 4, 10, 15, 7, 6}, x = 5
Output : 1
Explanation :  (10 ^ 15) = 5

Input : arr[] = {3, 6, 8, 10, 15, 50}, x = 5
Output : 2
Explanation : (3 ^ 6) = 5 and (10 ^ 15) = 5 
```

一个**简单的解决方案**是遍历每个元素，检查是否有另一个数与它的异或等于 x，这个解决方案需要 O(n <sup>2</sup> )时间。这个问题的有效解决方案需要 0(n)时间。这个想法是基于这样一个事实，即当且仅当 arr[i] ^ x 等于 arr[j]时，arr[i] ^ arr[j]等于 x。

```
1) Initialize result as 0.
2) Create an empty hash set "s".
3) Do following for each element arr[i] in arr[]
   (a)    If x ^ arr[i] is in "s", then increment result by 1.
   (b)    Insert arr[i] into the hash set "s".
3) return result.
```

## C++

```
// C++ program to Count all pair with given XOR
// value x
#include<bits/stdc++.h>

using namespace std;

// Returns count of pairs in arr[0..n-1] with XOR
// value equals to x.
int xorPairCount(int arr[], int n, int x)
{
    int result = 0; // Initialize result

    // create empty set that stores the visiting
    // element of array.
    // Refer below post for details of unordered_set
    // https://www.geeksforgeeks.org/unorderd_set-stl-uses/
    unordered_set<int> s;

    for (int i=0; i<n ; i++)
    {
        // If there exist an element in set s
        // with XOR equals to x^arr[i], that means
        // there exist an element such that the
        // XOR of element with arr[i] is equal to
        // x, then increment count.
        if (s.find(x^arr[i]) != s.end())
            result++;

        // Make element visited
        s.insert(arr[i]);
    }

    // return total count of pairs with XOR equal to x
    return result;
}

// driver program
int main()
{
    int arr[] = {5 , 4 ,10, 15, 7, 6};
    int n = sizeof(arr)/sizeof(arr[0]);
    int x = 5;
    cout << "Count of pairs with given XOR = "
         << xorPairCount(arr, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count all pair with
// given XOR value x
import java.util.*;

class GFG
{

    // Returns count of pairs in arr[0..n-1] with XOR
    // value equals to x.
    static int xorPairCount(int arr[], int n, int x)
    {
        int result = 0; // Initialize result

        // create empty set that stores the visiting
        // element of array.
        // Refer below post for details of unordered_set
        // https://www.geeksforgeeks.org/unorderd_set-stl-uses/
        HashSet<Integer> s = new HashSet<Integer>();

        for (int i = 0; i < n; i++)
        {
            // If there exist an element in set s
            // with XOR equals to x^arr[i], that means
            // there exist an element such that the
            // XOR of element with arr[i] is equal to
            // x, then increment count.
            if (s.contains(x ^ arr[i]) &&
                    (x ^ arr[i]) == (int) s.toArray()[s.size() - 1])
            {
                result++;
            }

            // Make element visited
            s.add(arr[i]);
        }

        // return total count of
        // pairs with XOR equal to x
        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {5, 4, 10, 15, 7, 6};
        int n = arr.length;
        int x = 5;
        System.out.print("Count of pairs with given XOR = "
                + xorPairCount(arr, n, x));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to count all the pair
# with given xor

# Returns count of pairs in arr[0..n-1]
# with XOR value equals to x.
def xorPairCount(arr, n, x):
    result = 0 # Initialize result

    # create empty set that stores the
    # visiting element of array.
    s = set()
    for i in range(0, n):

        # If there exist an element in set s
        # with XOR equals to x^arr[i], that
        # means there exist an element such
        # that the XOR of element with arr[i] 
        # is equal to x, then increment count.
        if(x ^ arr[i] in s):
            result = result + 1

        # Make element visited
        s.add(arr[i])
    return result

# Driver Code
if __name__ == "__main__":
    arr = [5, 4, 10, 15, 7, 6]
    n = len(arr)
    x = 5
    print("Count of pair with given XOR = " +
                str(xorPairCount(arr, n, x)))

# This code is contributed by Anubhav Natani
```

## C#

```
// C# program to Count all pair with
// given XOR value x
using System;
using System.Collections.Generic;

class GFG
{

    // Returns count of pairs in arr[0..n-1] with XOR
    // value equals to x.
    static int xorPairCount(int []arr, int n, int x)
    {
        int result = 0; // Initialize result

        // create empty set that stores the visiting
        // element of array.
        // Refer below post for details of unordered_set
        // https://www.geeksforgeeks.org/unorderd_set-stl-uses/
        HashSet<int> s = new HashSet<int>();

        for (int i = 0; i < n; i++)
        {
            // If there exist an element in set s
            // with XOR equals to x^arr[i], that means
            // there exist an element such that the
            // XOR of element with arr[i] is equal to
            // x, then increment count.
            if (s.Contains(x ^ arr[i]))
            {
                result++;
            }

            // Make element visited
            s.Add(arr[i]);
        }

        // return total count of
        // pairs with XOR equal to x
        return result;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {5, 4, 10, 15, 7, 6};
        int n = arr.Length;
        int x = 5;
        Console.WriteLine("Count of pairs with given XOR = "
                + xorPairCount(arr, n, x));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// Javascript program to Count all pair with
// given XOR value x

     // Returns count of pairs in arr[0..n-1] with XOR
    // value equals to x.
    function xorPairCount(arr,n,x)
    {
        let result = 0; // Initialize result

        // create empty set that stores the visiting
        // element of array.
        // Refer below post for details of unordered_set
        // https://www.geeksforgeeks.org/unorderd_set-stl-uses/
        let s = new Set();

        for (let i = 0; i < n; i++)
        {
            // If there exist an element in set s
            // with XOR equals to x^arr[i], that means
            // there exist an element such that the
            // XOR of element with arr[i] is equal to
            // x, then increment count.
            if (s.has(x ^ arr[i]) )
            {
                result++;
            }

            // Make element visited
            s.add(arr[i]);
        }

        // return total count of
        // pairs with XOR equal to x
        return result;
    }

    // Driver code
    let arr=[5, 4, 10, 15, 7, 6];
    let n = arr.length;
    let x = 5;
    document.write("Count of pairs with given XOR = "
                + xorPairCount(arr, n, x));

    // This code is contributed by unknown2108
</script>
```

**输出:**

```
Count of pairs with given XOR = 1
```

**时间复杂度:** O(n)

**辅助空间:**O(n)
T3】

**如何处理重复？**
如果输入数组中存在重复项，上述高效解决方案将不起作用。例如，上述解决方案对{2，2，5}和{5，2，2}产生不同的结果。为了处理重复，我们存储所有元素出现的次数。我们用无序映射代替无序集。

## C++

```
// C++ program to Count all pair with given XOR
// value x
#include<bits/stdc++.h>

using namespace std;

// Returns count of pairs in arr[0..n-1] with XOR
// value equals to x.
int xorPairCount(int arr[], int n, int x)
{
    int result = 0; // Initialize result

    // create empty map that stores counts of
    // individual elements of array.
    unordered_map<int, int> m;

    for (int i=0; i<n ; i++)
    {
        int curr_xor =  x^arr[i];

        // If there exist an element in map m
        // with XOR equals to x^arr[i], that means
        // there exist an element such that the
        // XOR of element with arr[i] is equal to
        // x, then increment count.
        if (m.find(curr_xor) != m.end())
            result += m[curr_xor];

        // Increment count of current element
        m[arr[i]]++;
    }

    // return total count of pairs with XOR equal to x
    return result;
}

// driver program
int main()
{
    int arr[] = {2, 5, 2};
    int n = sizeof(arr)/sizeof(arr[0]);
    int x = 0;
    cout << "Count of pairs with given XOR = "
         << xorPairCount(arr, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count all pair with given XOR
// value x
import java.util.*;

class GFG
{

// Returns count of pairs in arr[0..n-1] with XOR
// value equals to x.
static int xorPairCount(int arr[], int n, int x)
{
    int result = 0; // Initialize result

    // create empty map that stores counts of
    // individual elements of array.
    Map<Integer,Integer> m = new HashMap<>();

    for (int i = 0;  i < n ; i++)
    {
        int curr_xor = x^arr[i];

        // If there exist an element in map m
        // with XOR equals to x^arr[i], that means
        // there exist an element such that the
        // XOR of element with arr[i] is equal to
        // x, then increment count.
        if (m.containsKey(curr_xor))
            result += m.get(curr_xor);

        // Increment count of current element
        if(m.containsKey(arr[i]))
        {
            m.put(arr[i], m.get(arr[i]) + 1);
        }
        else{
            m.put(arr[i], 1);
        }
    }
    // return total count of pairs with XOR equal to x
    return result;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {2, 5, 2};
    int n = arr.length;
    int x = 0;
    System.out.println("Count of pairs with given XOR = "
        + xorPairCount(arr, n, x));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to Count all pair with
# given XOR value x

# Returns count of pairs in arr[0..n-1]
# with XOR value equals to x.
def xorPairCount(arr, n, x):

    result = 0 # Initialize result

    # create empty map that stores counts
    # of individual elements of array.
    m = dict()

    for i in range(n):

        curr_xor = x ^ arr[i]

        # If there exist an element in map m
        # with XOR equals to x^arr[i], that
        # means there exist an element such that
        # the XOR of element with arr[i] is equal
        # to x, then increment count.
        if (curr_xor in m.keys()):
            result += m[curr_xor]

        # Increment count of current element
        if arr[i] in m.keys():
            m[arr[i]] += 1
        else:
            m[arr[i]] = 1

    # return total count of pairs
    # with XOR equal to x
    return result

# Driver Code
arr = [2, 5, 2]
n = len(arr)
x = 0
print("Count of pairs with given XOR = ",
                 xorPairCount(arr, n, x))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to Count all pair with given XOR
// value x
using System;
using System.Collections.Generic;

class GFG
{

// Returns count of pairs in arr[0..n-1] with XOR
// value equals to x.
static int xorPairCount(int []arr, int n, int x)
{
    int result = 0; // Initialize result

    // create empty map that stores counts of
    // individual elements of array.
    Dictionary<int,int> m = new Dictionary<int,int>();

    for (int i = 0; i < n ; i++)
    {
        int curr_xor = x^arr[i];

        // If there exist an element in map m
        // with XOR equals to x^arr[i], that means
        // there exist an element such that the
        // XOR of element with arr[i] is equal to
        // x, then increment count.
        if (m.ContainsKey(curr_xor))
            result += m[curr_xor];

        // Increment count of current element
        if(m.ContainsKey(arr[i]))
        {
            var val = m[arr[i]];
            m.Remove(arr[i]);
            m.Add(arr[i], val + 1);
        }
        else
        {
            m.Add(arr[i], 1);
        }
    }

    // return total count of pairs with XOR equal to x
    return result;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = {2, 5, 2};
    int n = arr.Length;
    int x = 0;
    Console.WriteLine("Count of pairs with given XOR = "
        + xorPairCount(arr, n, x));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to Count all pair with given XOR
// value x

// Returns count of pairs in arr[0..n-1] with XOR
// value equals to x.
function xorPairCount(arr, n, x)
{
    let result = 0; // Initialize result

    // create empty map that stores counts of
    // individual elements of array.
    let m = new Map();

    for (let i = 0;  i < n ; i++)
    {
        let curr_xor = x^arr[i];

        // If there exist an element in map m
        // with XOR equals to x^arr[i], that means
        // there exist an element such that the
        // XOR of element with arr[i] is equal to
        // x, then increment count.
        if (m.has(curr_xor))
            result += m.get(curr_xor);

        // Increment count of current element
        if(m.has(arr[i]))
        {
            m.set(arr[i], m.get(arr[i]) + 1);
        }
        else{
            m.set(arr[i], 1);
        }
    }
    // return total count of pairs with XOR equal to x
    return result;
}

// Driver program

    let arr = [2, 5, 2];
    let n = arr.length;
    let x = 0;
    document.write("Count of pairs with given XOR = "
        + xorPairCount(arr, n, x));

</script>
```

**输出:**

```
Count of pairs with given XOR = 1
```

**时间复杂度:** O(n)

**辅助空间:** O(n)

本文由 **Nishant_singh(pintu)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。