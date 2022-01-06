# 对四个数组中的所有四元组进行计数，使它们的异或等于‘x’

> 原文:[https://www . geesforgeks . org/count-四联-四个数组-xor-equals-x/](https://www.geeksforgeeks.org/count-quadruples-four-arrays-xor-equals-x/)

给定四个数组和一个整数 x，求满足 a^b^c^d = x 的四倍数，其中 a 属于 Arr <sub>1</sub> ，b 属于 Arr <sub>2</sub> ，c 属于 Arr <sub>3</sub> ，d 属于 Arr <sub>4</sub> 。

**示例:**

```
Input :  x = 0;
         a[] = { 1 , 10 };
         b[] = { 1 , 10 };
         c[] = { 1 , 10 };
         d[] = { 1 , 10 };
Output : 4
Explanation: There are total 8 Quadruples
with XOR value equals to 0.
{1, 1, 1, 1}, {10, 10, 10, 10}, {1, 1, 10, 10},
{10, 10, 1, 1}, {10, 1, 10, 1}, {1, 10, 1, 10},
{1, 10, 10, 1}, {10, 1, 1, 10}

Input : x = 3
        a[] = {0, 1}
        b[] = {2, 0}
        c[] = {0, 1}
        d[] = {0, 1}
Output : 4
Explanation: There are total 4 Quadruples
with XOR value equals to 3.
{0, 2, 0, 1}, {1, 2, 0, 0}, {0, 2, 1, 0},
{1, 2, 1, 1}
```

**方法 1(天真方法)**
可以用 4 个循环来完成，覆盖每四个循环，检查是否等于 x。

## C++

```
// C++ program to find number of Quadruples from four
// arrays such that their XOR equals to 'x'
#include<bits/stdc++.h>
using namespace std;

// Function to return the number of Quadruples with XOR
// equals to x such that every element of Quadruple is
// from different array.
int findQuadruples(int a[], int b[], int c[], int d[],
                    int x, int n)
{
    int count = 0;
    for (int i = 0 ; i < n ; i++)
        for (int j = 0 ; j < n ; j++)
            for (int k = 0 ; k < n ; k++)
                for (int l = 0 ; l < n ; l++)

                    // Check whether XOR is equal to x
                    if ((a[i] ^ b[j] ^ c[k] ^ d[l]) == x)
                        count++;

    return count;
}

// Driver Program
int main()
{
    int x = 3;
    int a[] = {0, 1};
    int b[] = {2, 0};
    int c[] = {0, 1};
    int d[] = {0, 1};

    int n = sizeof(a)/sizeof(a[0]);

    cout << findQuadruples(a, b, c, d, x, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of Quadruples from four
// arrays such that their XOR equals to 'x'
class GFG {

    // Function to return the number of Quadruples with XOR
    // equals to x such that every element of Quadruple is
    // from different array.
    static int findQuadruples(int a[], int b[], int c[],
                                int d[], int x, int n)
    {
        int count = 0;
        for (int i = 0 ; i < n ; i++)
            for (int j = 0 ; j < n ; j++)
                for (int k = 0 ; k < n ; k++)
                    for (int l = 0 ; l < n ; l++)

                        // Check whether XOR is equal to x
                        if ((a[i] ^ b[j] ^ c[k] ^ d[l]) == x)
                            count++;

        return count;
    }

    // Driver method
    public static void main(String[] args)
    {
        int x = 3;
        int a[] = {0, 1};
        int b[] = {2, 0};
        int c[] = {0, 1};
        int d[] = {0, 1};

        int n = a.length;

        System.out.println(findQuadruples(a, b, c, d, x, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find number of
# Quadruples from four arrays such
# that their XOR equals to 'x'

# Function to return the number of
# Quadruples with XOR equals to x
# such that every element of Quadruple
# is from different array.
def findQuadruples(a, b, c, d, x, n):

    count = 0
    for i in range(n):
        for j in range(n):
            for k in range(n):
                for l in range(n):

                    # Check whether XOR is equal to x
                    if ((a[i] ^ b[j] ^ c[k] ^ d[l]) == x):
                        count += 1
    return count

# Driver Code
x = 3
a = [0, 1]
b = [2, 0]
c = [0, 1]
d = [0, 1]
n = len(a)
print(findQuadruples(a, b, c, d, x, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find number of
// Quadruples from four arrays such
// that their XOR equals to 'x'
using System;

class GFG {

    // Function to return the number of
    // Quadruples with XOR equals to x such that
    // every element of Quadruple is from different array.
    static int findQuadruples(int []a, int []b, int []c,
                                int []d, int x, int n)
    {
        int count = 0;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                for (int k = 0; k < n; k++)
                    for (int l = 0; l < n; l++)

                        // Check whether XOR is equal to x
                        if ((a[i] ^ b[j] ^ c[k] ^ d[l]) == x)
                            count++;

        return count;
    }

    // Driver method
    public static void Main()
    {
        int x = 3;
        int []a = {0, 1};
        int []b = {2, 0};
        int []c = {0, 1};
        int []d = {0, 1};

        int n = a.Length;

        // Function calling
        Console.Write(findQuadruples(a, b, c, d, x, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// of Quadruples from four
// arrays such that their
// XOR equals to 'x'

// Function to return the number
// of Quadruples with XOR equals
// to x such that every element
// of Quadruple is from different
// array.
function findQuadruples($a, $b, $c,
                        $d, $x, $n)
{
    $count = 0;
    for ($i = 0 ; $i < $n ; $i++)
        for ($j = 0 ; $j < $n ; $j++)
            for ($k = 0 ; $k < $n ; $k++)
                for ($l = 0 ; $l < $n ; $l++)

                    // Check whether XOR
                    // is equal to x
                    if (($a[$i] ^ $b[$j] ^
                        $c[$k] ^ $d[$l]) == $x)
                        $count++;

    return $count;
}

    // Driver Code
    $x = 3;
    $a = array(0, 1);
    $b = array(2, 0);
    $c = array(0, 1);
    $d = array(0, 1);
    $n = count($a);
    echo findQuadruples($a, $b, $c, $d, $x, $n) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // Javascript program to find number of Quadruples from four
    // arrays such that their XOR equals to 'x'

    // Function to return the number of Quadruples with XOR
    // equals to x such that every element of Quadruple is
    // from different array.
    function findQuadruples(a, b, c, d, x, n)
    {
        let count = 0;
        for (let i = 0 ; i < n ; i++)
            for (let j = 0 ; j < n ; j++)
                for (let k = 0 ; k < n ; k++)
                    for (let l = 0 ; l < n ; l++)

                        // Check whether XOR is equal to x
                        if ((a[i] ^ b[j] ^ c[k] ^ d[l]) == x)
                            count++;

        return count;
    }

    let x = 3;
    let a = [0, 1];
    let b = [2, 0];
    let c = [0, 1];
    let d = [0, 1];

    let n = a.length;

    document.write(findQuadruples(a, b, c, d, x, n));

</script>
```

**输出:**

```
4
```

**时间复杂度:**O(n<sup>4</sup>)
T5】辅助空间: O(1)

**方法 2(高效方法)**
思路是用[在中间相遇算法](https://www.geeksforgeeks.org/meet-in-the-middle/)。
为此，观察以下模式:
a ^ b ^ c ^ d = x
XOR c 和 d 两边
a ^ b ^ c ^ d ^ c ^ d = x c d
因为，c c = 0 和 d d = 0
a b 0 0 = x c d
即 a b = x c d

现在，我们只需要计算一个^ b 和 x ^ c ^ d，每个都可以用 O(n <sup>2</sup> 来计算，然后使用二分搜索法来寻找元素。

## C++

```
// C++ program to find number of Quadruples from four
// arrays such that their XOR equals to 'x'
#include<bits/stdc++.h>
using namespace std;

// Function to return the number of Quadruples with XOR
// equals to x such that every element of Quadruple is
// from different array.
int findQuadruples(int a[], int b[], int c[], int d[],
                   int x, int n)
{
    int count = 0;
    vector<int> v1, v2;

    // Loop to get two different subsets
    for (int i = 0 ; i < n ; i++)
    {
        for (int j = 0 ; j < n ; j++)
        {
            // v1 for first and second array
            v1.push_back(a[i]^b[j]);

            // v2 for third and forth array.
            // x is a constant, so no need for
            // a separate loop
            v2.push_back(x ^ c[i] ^ d[j]);
        }
    }

    // Sorting the first set (Containing XOR
    // of a[] and b[]
    sort(v1.begin(), v1.end());

    // Finding the lower and upper bound of an
    // element to find its number
    for (int i = 0 ; i < v2.size() ; i++)
    {
        // Count number of occurrences of v2[i] in sorted
        // v1[] and add the count to result.
        auto low = lower_bound(v1.begin(), v1.end(), v2[i]);
        auto high = upper_bound(v1.begin(), v1.end(), v2[i]);
        count += high - low;
    }

    return count;
}

// Driver Program
int main()
{
    int  x = 3;
    int a[] = {0, 1};
    int b[] = {2, 0};
    int c[] = {0, 1};
    int d[] = {0, 1};

    int n = sizeof(a)/sizeof(a[0]);

    cout << findQuadruples(a, b, c, d, x, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
import java.util.ArrayList;
import java.util.Collections;

class GFG
{

    // Function to return the number of Quadruples with XOR
    // equals to x such that every element of Quadruple is
    // from different array.
    public static int findQuadruples(int a[], int b[],
                                     int c[], int d[],
                                     int x, int n)
    {
        int count = 0;
        ArrayList<Integer> v1 = new ArrayList<>();
        ArrayList<Integer> v2 = new ArrayList<>();

        // Loop to get two different subsets
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {

                // v1 for first and second array
                v1.add(a[i] ^ b[j]);

                // v2 for third and forth array.
                // x is a constant, so no need for
                // a separate loop
                v2.add(x ^ c[i] ^ d[j]);
            }
        }
        Collections.sort(v1);

        // Finding the lower and upper bound of an
        // element to find its number
        for (int i = 0; i < v2.size(); i++)
        {

            // Count number of occurrences of v2[i] in
            // sorted v1[] and add the count to result.
            int low
                = Collections.binarySearch(v1, v2.get(i));
            int j = low;
            for (j = low; j >= 0; j--)
            {
                if (v1.get(j) != v2.get(i))
                {
                    j++;
                    break;
                }
            }
            low = j;
            int high = Collections.binarySearch(v1, v2.get(i));
            j = high;
            for (j = high; j < v1.size(); j++)
            {
                if (v1.get(j) != v2.get(i)) {
                    break;
                }
            }
            high = j;
            count += high - low;
        }

        return count;
    }

  // Driver code
    public static void main(String[] args)
    {
        int x = 3;
        int a[] = { 0, 1 };
        int b[] = { 2, 0 };
        int c[] = { 0, 1 };
        int d[] = { 0, 1 };

        int n = 2;
        System.out.println(
            findQuadruples(a, b, c, d, x, n));
    }
}

// This code is contributed by aditya7409
```

## 蟒蛇 3

```
# Python3 program to find number of Quadruples
# from four arrays such that their XOR equals
# to 'x'
from bisect import bisect_left, bisect_right

# Function to return the number of Quadruples
# with XOR equals to x such that every element
# of Quadruple is from different array.
def findQuadruples(a, b, c, d, x, n):

    count = 0
    v1, v2 = [], []

    # Loop to get two different subsets
    for i in range(n):
        for j in range(n):

            # v1 for first and second array
            v1.append(a[i] ^ b[j])

            # v2 for third and forth array.
            # x is a constant, so no need for
            # a separate loop
            v2.append(x ^ c[i] ^ d[j])

    # Sorting the first set (Containing XOR
    # of aand b
    v1 = sorted(v1)

    # Finding the lower and upper bound of an
    # element to find its number
    for i in range(len(v2)):

        # Count number of occurrences of v2[i]
        # in sorted v1and add the count to result.
        low = bisect_left(v1, v2[i])
        high = bisect_right(v1, v2[i])
        count += high - low

    return count

# Driver code
if __name__ == '__main__':

    x = 3
    a = [ 0, 1 ]
    b = [ 2, 0 ]
    c = [ 0, 1 ]
    d = [ 0, 1 ]

    n = len(a)

    print(findQuadruples(a, b, c, d, x, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find number of Quadruples from four
// arrays such that their XOR equals to 'x'
using System;
using System.Collections.Generic;
class GFG
{

    // Function to return the number of Quadruples with XOR
    // equals to x such that every element of Quadruple is
    // from different array.
    static int findQuadruples(int[] a, int[] b,
                              int[] c, int[] d,
                              int x, int n)
    {
        int count = 0;
        List<int> v1 = new List<int>();
        List<int> v2 = new List<int>();

        // Loop to get two different subsets
        for (int i = 0 ; i < n ; i++)
        {
            for (int j = 0 ; j < n ; j++)
            {

                // v1 for first and second array
                v1.Add(a[i]^b[j]);

                // v2 for third and forth array.
                // x is a constant, so no need for
                // a separate loop
                v2.Add(x ^ c[i] ^ d[j]);
            }
        }

        // Sorting the first set (Containing XOR
        // of a[] and b[]
        v1.Sort();

        // Finding the lower and upper bound of an
        // element to find its number
        for (int i = 0 ; i < v2.Count; i++)
        {
            // Count number of occurrences of v2[i] in
            // sorted v1[] and add the count to result.
            int low = v1.BinarySearch(v2[i]);
            int j = low;
            for (j = low; j >= 0; j--)
            {
                if (v1[j] != v2[i])
                {
                    j++;
                    break;
                }
            }
            low = j;
            int high = v1.BinarySearch(v2[i]);
            j = high;
            for (j = high; j < v1.Count; j++)
            {
                if (v1[j] != v2[i])
                {
                    break;
                }
            }
            high = j;
            count += high - low;
        }    
        return count;
    }

  // Driver code
  static void Main()
  {
    int  x = 3;
    int[] a = {0, 1};
    int[] b = {2, 0};
    int[] c = {0, 1};
    int[] d = {0, 1};

    int n = a.Length;
    Console.WriteLine(findQuadruples(a, b, c, d, x, n));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // JavaScript program to find number of Quadruples from four
    // arrays such that their XOR equals to 'x'

    // Function to return the number of Quadruples with XOR
    // equals to x such that every element of Quadruple is
    // from different array.
    function findQuadruples(a, b, c, d, x, n)
    {
        let count = 0;
        let v1 = [];
        let v2 = [];

        // Loop to get two different subsets
        for (let i = 0; i < n; i++)
        {
            for (let j = 0; j < n; j++)
            {

                // v1 for first and second array
                v1.push(a[i] ^ b[j]);

                // v2 for third and forth array.
                // x is a constant, so no need for
                // a separate loop
                v2.push(x ^ c[i] ^ d[j]);
            }
        }
        v1.sort();

        // Finding the lower and upper bound of an
        // element to find its number
        for (let i = 0; i < v2.length; i++)
        {

            // Count number of occurrences of v2[i] in
            // sorted v1[] and add the count to result.
            let low = 0;
            for(let z = 0; z < v1.length; z++)
            {
                if(v1[z] == v2[i])
                {
                    low = z;
                    break;
                }
            }
            let j = low;
            for (j = low; j >= 0; j--)
            {
                if (v1[j] != v2[i])
                {
                    j++;
                    break;
                }
            }
            low = j;
            let high = 0;
            for(let z = 0; z < v1.length; z++)
            {
                if(v1[z] == v2[i])
                {
                    high = z;
                    break;
                }
            }
            j = high;
            for (j = high; j < v1.length; j++)
            {
                if (v1[j] != v2[i]) {
                    break;
                }
            }
            high = j;
            count += high - low;
        }

        return count;
    }

    let x = 3;
    let a = [ 0, 1 ];
    let b = [ 2, 0 ];
    let c = [ 0, 1 ];
    let d = [ 0, 1 ];

    let n = 2;
    document.write(
      findQuadruples(a, b, c, d, x, n));

</script>
```

**输出:**

```
4
```

**时间复杂度:**O(n<sup>2</sup>log(n)
T5】辅助空间: O(n <sup>2</sup>

本文由 [**舒巴姆·古普塔**](https://www.facebook.com/Shubh1307) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。