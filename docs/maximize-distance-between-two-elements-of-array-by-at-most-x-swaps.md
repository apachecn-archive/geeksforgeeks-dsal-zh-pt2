# 通过最多 X 次交换最大化数组两个元素之间的距离

> 原文:[https://www . geeksforgeeks . org/最大化最多 x 个数组元素之间的距离/](https://www.geeksforgeeks.org/maximize-distance-between-two-elements-of-array-by-at-most-x-swaps/)

给定唯一元素和三个整数的**数组 arr[]****X**、 **A** 和 **B** 。任务是在大气 **X** 中打印元素 **A** 和 **B** 之间的最大可能距离，并与相邻元素交换。
**举例:**

> **输入:** arr[] = {5，1，3，2}，X = 1，A = 2，B = 3
> **输出:** 2
> **解释:**
> 3 与其相邻的元素 1 交换。所以，元素 3 和 2 之间的距离是 2，因为 X = 1，所以不可能有更多的互换。
> **输入:** arr = {100，33，10，1}，X = 5，A = 100，B = 1
> **输出:** 3
> **说明:**
> 由于元素已经是开始和结束元素，它们之间的距离已经最大化。

**方法:**可以按照以下步骤计算结果:

*   如果给定的 X 为 0，则返回**|索引(A)-索引(B)|** 作为最终答案。
*   如果元素已经在索引 0 和 n-1，返回 **N-1** ，因为距离已经最大化。
*   否则，较大的索引元素与其相邻元素交换 **X** 次，直到它小于数组的大小。
*   到达数组末尾后如果 X > 0；然后较小的索引元素与其先前的元素交换，直到 **X** 不等于 0。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to maximize the distance
// between the two elements of the
// array by at most X swaps
void max_distance(int a[], int n, int x,
                  int A, int B)
{
    // Initialize the variables
    int g = 0, h = 0;

    // Iterate till the length of the array
    for (int i = 0; i < n; i++) {
        // Check if current element is A
        if (a[i] == A)
            // Store index
            g = i;

        // Check if current element is B
        if (a[i] == B)
            // Store index
            h = i;
    }

    // If X = 0, swapping can not be done
    if (x == 0) {
        cout << abs(g - h);
    }

    // If elements are at starting and ending
    // indices, then the distance
    // is already maximum
    else if ((g == 0) && (h == (n - 1)))
        cout << n - 1 << endl;

    else if ((g == n - 1) && (h == 0))
        cout << n - 1 << endl;

    else {

        // Greater index is incremented
        // till x > 0 and the
        // index of element < size of array
        if (h > g) {
            while ((x > 0) && (h < n - 1)) {
                h++;
                x--;
            }

            // Check if reached the size of array
            // and x > 0, then the
            // smaller index is decremented
            if (x > 0) {
                while ((x > 0) && (g > 0)) {
                    g--;
                    x--;
                }
            }
            cout << h - g << endl;
        }

        // Greater index is incremented till x>0
        // and index of element < size of array
        else {
            while ((x > 0) && (g < n - 1)) {
                g++;
                x--;
            }

            // Check if reached the size of the array
            // and x > 0 the smaller index
            // is decremented
            if (x > 0) {
                while ((x > 0) && (h > 0)) {
                    h--;
                    x--;
                }
            }
            cout << g - h << endl;
        }
    }
}

// Driver code
int main()
{
    int a[] = { 100, 33, 10, 1 };
    int x = 5, A = 100, B = 1;
    int n = sizeof(a) / sizeof(a[0]);
    max_distance(a, n, x, A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to maximize the distance
// between the two elements of the
// array by at most X swaps
static void max_distance(int a[], int n, int x,
                         int A, int B)
{

    // Initialize the variables
    int i, g = 0, h = 0;

    // Iterate till the length of the array
    for(i = 0; i < n; i++)
    {

        // Check if current element is A
        if (a[i] == A)

            // Store index
            g = i;

        // Check if current element is B
        if (a[i] == B)

            // Store index
            h = i;
    }

    // If X = 0, swapping can not be done
    if (x == 0)
    {
        System.out.print(Math.abs(g - h));
    }

    // If elements are at starting and
    // ending indices, then the distance
    // is already maximum
    else if ((g == 0) && (h == (n - 1)))
        System.out.println(n - 1);

    else if ((g == n - 1) && (h == 0))
        System.out.println(n - 1);

    else
    {

        // Greater index is incremented
        // till x > 0 and theindex of
        // element < size of array
        if (h > g)
        {
            while ((x > 0) && (h < n - 1))
            {
                h++;
                x--;
            }

            // Check if reached the size of
            // array and x > 0, then the
            // smaller index is decremented
            if (x > 0)
            {
                while ((x > 0) && (g > 0))
                {
                    g--;
                    x--;
                }
            }
            System.out.println(h - g);
        }

        // Greater index is incremented till x>0
        // and index of element < size of array
        else
        {
            while ((x > 0) && (g < n - 1))
            {
                g++;
                x--;
            }

            // Check if reached the size of the array
            // and x > 0 the smaller index
            // is decremented
            if (x > 0)
            {
                while ((x > 0) && (h > 0))
                {
                    h--;
                    x--;
                }
            }
            System.out.println(g - h);
        }
    }
}

// Driver code
public static void main (String []args)
{
    int a[] = { 100, 33, 10, 1 };
    int x = 5, A = 100, B = 1;
    int n = a.length;

    max_distance(a, n, x, A, B);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to maximize the distance
# between the two elements of the
# array by at most X swaps
def max_distance(a, n, x, A, B):

    # Initialize the variables
    g = 0
    h = 0

    for i in range(0, n):

        # Check if current element is A
        if (a[i] == A):

            # Store index
            g = i

        # Check if current element is B
        if (a[i] == B):

            # Store index
            h = i

    # If X = 0, swapping can not be done
    if (x == 0):
        print(abs(g - h))

    # If elements are at starting and
    # ending indices, then the distance
    # is already maximum
    elif ((g == 0) and (h == (n - 1))):
        print(n - 1, end = '')

    elif ((g == n - 1) and (h == 0)):
        print(n - 1, end = '')
    else:

        # Greater index is incremented
        # till x > 0 and the
        # index of element < size of array
        if (h > g):
            while ((x > 0) and (h < n - 1)):
                h += 1
                x -= 1

                # Check if reached the size
                # of array and x > 0, then the
                # smaller index is decremented
                if (x > 0):
                    while ((x > 0) and (g > 0)):
                        g -= 1
                        x -= 1

                print(h - g, end = '')

        # Greater index is incremented till x>0
        # and index of element < size of array
        else:
            while ((x > 0) and (g < n - 1)):
                g += 1
                x -= 1

            # Check if reached the size of
            # the array and x > 0 the smaller
            # index is decremented
            if (x > 0):
                while ((x > 0) and (h > 0)):
                    h -= 1
                    x -= 1

            print(g - h, end = '')

# Driver code
if __name__ == '__main__':

    a = [ 100, 33, 10, 1 ]
    x = 5
    A = 100
    B = 1
    n = len(a)

    max_distance(a, n, x, A, B)

# This code is contributed by virusbuddah_    
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to maximize the distance
// between the two elements of the
// array by at most X swaps
static void max_distance(int []a, int n, int x,
                         int A, int B)
{

    // Initialize the variables
    int i, g = 0, h = 0;

    // Iterate till the length of the array
    for(i = 0; i < n; i++)
    {

        // Check if current element is A
        if (a[i] == A)

            // Store index
            g = i;

        // Check if current element is B
        if (a[i] == B)

            // Store index
            h = i;
    }

    // If X = 0, swapping can not be done
    if (x == 0)
    {
        Console.Write(Math.Abs(g - h));
    }

    // If elements are at starting and
    // ending indices, then the distance
    // is already maximum
    else if ((g == 0) && (h == (n - 1)))
        Console.WriteLine(n - 1);

    else if ((g == n - 1) && (h == 0))
        Console.WriteLine(n - 1);

    else
    {

        // Greater index is incremented
        // till x > 0 and theindex of
        // element < size of array
        if (h > g)
        {
            while ((x > 0) && (h < n - 1))
            {
                h++;
                x--;
            }

            // Check if reached the size of
            // array and x > 0, then the
            // smaller index is decremented
            if (x > 0)
            {
                while ((x > 0) && (g > 0))
                {
                    g--;
                    x--;
                }
            }
            Console.WriteLine(h - g);
        }

        // Greater index is incremented till x>0
        // and index of element < size of array
        else
        {
            while ((x > 0) && (g < n - 1))
            {
                g++;
                x--;
            }

            // Check if reached the size of the
            // array and x > 0 the smaller index
            // is decremented
            if (x > 0)
            {
                while ((x > 0) && (h > 0))
                {
                    h--;
                    x--;
                }
            }
            Console.WriteLine(g - h);
        }
    }
}

// Driver code
public static void Main(String []args)
{
    int []a = { 100, 33, 10, 1 };
    int x = 5, A = 100, B = 1;
    int n = a.Length;

    max_distance(a, n, x, A, B);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to maximize the distance
// between the two elements of the
// array by at most X swaps
function max_distance(a,n,x,A,B)
{
    // Initialize the variables
    let i, g = 0, h = 0;

    // Iterate till the length of the array
    for(i = 0; i < n; i++)
    {

        // Check if current element is A
        if (a[i] == A)

            // Store index
            g = i;

        // Check if current element is B
        if (a[i] == B)

            // Store index
            h = i;
    }

    // If X = 0, swapping can not be done
    if (x == 0)
    {
        document.write(Math.abs(g - h));
    }

    // If elements are at starting and
    // ending indices, then the distance
    // is already maximum
    else if ((g == 0) && (h == (n - 1)))
        document.write(n - 1);

    else if ((g == n - 1) && (h == 0))
        document.write(n - 1);

    else
    {

        // Greater index is incremented
        // till x > 0 and theindex of
        // element < size of array
        if (h > g)
        {
            while ((x > 0) && (h < n - 1))
            {
                h++;
                x--;
            }

            // Check if reached the size of
            // array and x > 0, then the
            // smaller index is decremented
            if (x > 0)
            {
                while ((x > 0) && (g > 0))
                {
                    g--;
                    x--;
                }
            }
            document.write(h - g);
        }

        // Greater index is incremented till x>0
        // and index of element < size of array
        else
        {
            while ((x > 0) && (g < n - 1))
            {
                g++;
                x--;
            }

            // Check if reached the size of the array
            // and x > 0 the smaller index
            // is decremented
            if (x > 0)
            {
                while ((x > 0) && (h > 0))
                {
                    h--;
                    x--;
                }
            }
            document.write(g - h);
        }
    }
}

// Driver code
let a=[ 100, 33, 10, 1];
let x = 5, A = 100, B = 1;
let  n = a.length;
max_distance(a, n, x, A, B);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
3
```