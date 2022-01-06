# 找到新数组中给定数组中每个元素最大的元素加到其左边形成的数组

> 原文:[https://www . geesforgeks . org/find-array-通过将给定数组的每个元素在其左侧添加新数组中最大的元素而形成/](https://www.geeksforgeeks.org/find-array-formed-by-adding-each-element-of-given-array-with-largest-element-in-new-array-to-its-left/)

给定一个大小为 **N** 的数组 **A** ，任务是找到给定数组中每个元素与其左边新数组中最大元素相加形成的结果数组。
**例:**

> **输入:** arr[] = {5，1，6，-3，2}
> **输出:** {5，6，12，9，14}
> 元素 A <sub>0</sub> :如果在其左侧没有元素。因此，结果数组第 0 个索引处的元素= 5
> 元素 A <sub>1</sub> :结果数组中其左侧最大的元素= 5。因此，结果数组第 1 个索引处的元素= 1 + 5 = 6
> 元素 A <sub>2</sub> :结果数组中最左边的元素= 6。因此，结果数组第二个索引处的元素= 6 + 6 = 12
> 元素 A <sub>3</sub> :结果数组中最左边的元素= 12。因此结果数组第三个索引处的元素= -3 + 12 = 9
> 元素 A <sub>4</sub> :结果数组中最左边的元素= 12。因此结果数组第 4 个索引处的元素= 2 + 12 = 14
> 因此结果数组= {5，6，12，9，14}
> **输入:** arr[] = {40，12，62}
> **输出:** {40，52，114}

**方法:**
为了找到这样的数组，新数组的每个元素将根据以下规则为[0，N-1]范围内的每个索引逐一计算:

1.  对于起始索引，即 0，新数组将为空。因此不会有任何最大的元素。在这种情况下，给定数组中第 0 个索引处的元素被复制到新数组中，即

```
B0 = A0

where A is the given array and 
      B is the new array
```

2.对于范围[1，N-1]中的每隔一个索引，首先在新数组中找到它左边的最大元素，然后将其添加到原始数组的相应元素中，即

```
Bi = Ai + max(B0, B1, ..., Bi-1)

where A is the given array, 
      B is the new array, and
      i is the current index
```

以下是上述方法的实现:

## C++

```
// C++ program to find Array formed by adding
// each element of given array with largest
// element in new array to its left

#include <bits/stdc++.h>
using namespace std;

// Function to find array B from array
// A such that Ai = Bi – max(B0…Bi-1)
void find_array(int a[], int n)
{
    // Initialising as 0 as first
    // element will remain same
    int x = 0;

    for (int i = 0; i < n; i++) {

        // restoring values of B
        a[i] += x;

        cout << a[i] << ' ';

        // Find max value
        x = max(x, a[i]);
    }
}

// Driver code
int main()
{
    int a[] = {40, 12, 62};
    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    find_array(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Array formed by adding
// each element of given array with largest
// element in new array to its left

public class GFG
{

// Function to find array B from array
// A such that Ai = Bi – max(B0…Bi-1)
static void find_array(int []a, int n)
{
    // Initialising as 0 as first
    // element will remain same
    int x = 0;

    for (int i = 0; i < n; i++) {

        // restoring values of B
        a[i] += x;

        System.out.print(a[i] + " ");

        // Find max value
        x = Math.max(x, a[i]);
    }
}

// Driver code
public static void main(String []args)
{
    int []a = {40, 12, 62};
    int n = a.length ;

    // Function call
    find_array(a, n);
}
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 program to find Array formed by adding
# each element of given array with largest
# element in new array to its left

# Function to find array B from array
# A such that Ai = Bi – max(B0…Bi-1)
def find_array(a,  n) :

    # Initialising as 0 as first
    # element will remain same
    x = 0;

    for i in range(n) :

        # restoring values of B
        a[i] += x;

        print(a[i],end= ' ');

        # Find max value
        x = max(x, a[i]);

# Driver code
if __name__ == "__main__" :

    a = [40, 12, 62];
    n = len(a);

    # Function call
    find_array(a, n);

# This code is contributed by Yash_R
```

## C#

```
// C# program to find Array formed by adding
// each element of given array with largest
// element in new array to its left
using System;

class gfg
{

// Function to find array B from array
// A such that Ai = Bi – max(B0…Bi-1)
static void find_array(int []a, int n)
{
    // Initialising as 0 as first
    // element will remain same
    int x = 0;

    for (int i = 0; i < n; i++) {

        // restoring values of B
        a[i] += x;

        Console.Write(a[i] + " ");

        // Find max value
        x = Math.Max(x, a[i]);
    }
}

// Driver code
public static void Main(string []args)
{
    int []a = {40, 12, 62};
    int n = a.Length ;

    // Function call
    find_array(a, n);
}
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// Javascript program to find Array formed by adding
// each element of given array with largest
// element in new array to its left

// Function to find array B from array
// A such that Ai = Bi – max(B0…Bi-1)
function find_array(a, n)
{
    // Initialising as 0 as first
    // element will remain same
    let x = 0;

    for (let i = 0; i < n; i++) {

        // restoring values of B
        a[i] += x;

        document.write(a[i] + ' ');

        // Find max value
        x = Math.max(x, a[i]);
    }
}

// Driver code

    let a = [40, 12, 62];
    let n = a.length;

    // Function call
    find_array(a, n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
40 52 114
```

**时间复杂度:** O(N)

**辅助空间:** O(1)