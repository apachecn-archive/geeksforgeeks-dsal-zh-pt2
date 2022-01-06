# 三角形第三条边的最小和最大可能长度

> 原文:[https://www . geeksforgeeks . org/三角形第三边的最小和最大可能长度/](https://www.geeksforgeeks.org/minimum-and-maximum-possible-length-of-the-third-side-of-a-triangle/)

给定三角形的两条边 **s1** 和 **s2** ，任务是找到给定三角形第三条边的最小和最大可能长度。如果不可能用给定的边长做三角形，打印 **-1** 。**注意**所有边的长度必须是整数。
**举例:**

> **输入:** s1 = 3，s2 = 6
> **输出:**
> Max = 8
> Min = 4
> **输入:** s1 = 5，s2 = 8
> **输出:**
> Max = 12
> Min = 4

**逼近:**让 **s1** 、 **s2** 和 **s3** 成为给定三角形的边，其中 **s1** 和 **s2** 被给定。我们知道，在三角形中，两条边的和必须总是大于第三条边。因此，必须满足以下等式:

1.  s1 + s2 > s3
2.  s1 + s3 > s2
3.  s2 + s3 > s1

求解 **s3** ，得到 **s3 < s1 + s2** 、**S3>S2–S1**和**S3>S1–S2**。
现在很明显，第三边的长度必须在**(最大(s1，s2)–最小(s1，S2)，s1 + s2)**
的范围内，所以最小可能值将是**最大(s1，S2)–最小(s1，s2) + 1** ，最大可能值将是**S1+S2–1**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to find the minimum and the
// maximum possible length of the third
// side of the given triangle
void find_length(int s1, int s2)
{

    // Not a valid triangle
    if (s1 <= 0 || s2 <= 0) {
        cout << -1;
        return;
    }
    int max_length = s1 + s2 - 1;
    int min_length = max(s1, s2) - min(s1, s2) + 1;

    // Not a valid triangle
    if (min_length > max_length) {
        cout << -1;
        return;
    }

    cout << "Max = " << max_length << endl;
    cout << "Min = " << min_length;
}

// Driver code
int main()
{
    int s1 = 8, s2 = 5;
    find_length(s1, s2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to find the minimum and the
// maximum possible length of the third
// side of the given triangle
static void find_length(int s1, int s2)
{

    // Not a valid triangle
    if (s1 <= 0 || s2 <= 0)
    {
        System.out.print(-1);
        return;
    }
    int max_length = s1 + s2 - 1;
    int min_length = Math.max(s1, s2) - Math.min(s1, s2) + 1;

    // Not a valid triangle
    if (min_length > max_length)
    {
        System.out.print(-1);
        return;
    }

    System.out.println("Max = " + max_length);
    System.out.print("Min = " + min_length);
}

// Driver code
public static void main (String[] args)
{
    int s1 = 8, s2 = 5;
    find_length(s1, s2);
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the minimum and the
# maximum possible length of the third
# side of the given triangle
def find_length(s1, s2) :

    # Not a valid triangle
    if (s1 <= 0 or s2 <= 0) :
        print(-1, end = "");
        return;

    max_length = s1 + s2 - 1;
    min_length = max(s1, s2) - min(s1, s2) + 1;

    # Not a valid triangle
    if (min_length > max_length) :
        print(-1, end = "");
        return;

    print("Max =", max_length);
    print("Min =", min_length);

# Driver code
if __name__ == "__main__" :

    s1 = 8;
    s2 = 5;

    find_length(s1, s2);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the minimum and the
// maximum possible length of the third
// side of the given triangle
static void find_length(int s1, int s2)
{

    // Not a valid triangle
    if (s1 <= 0 || s2 <= 0)
    {
        Console.Write(-1);
        return;
    }
    int max_length = s1 + s2 - 1;
    int min_length = Math.Max(s1, s2) - Math.Min(s1, s2) + 1;

    // Not a valid triangle
    if (min_length > max_length)
    {
        Console.WriteLine(-1);
        return;
    }

    Console.WriteLine("Max = " + max_length);
    Console.WriteLine("Min = " + min_length);
}

// Driver code
public static void Main ()
{
    int s1 = 8, s2 = 5;
    find_length(s1, s2);
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to find the minimum and the
    // maximum possible length of the third
    // side of the given triangle
    function find_length(s1 , s2)
    {

        // Not a valid triangle
        if (s1 <= 0 || s2 <= 0)
        {
            document.write(-1);
            return;
        }
        var max_length = s1 + s2 - 1;
        var min_length = Math.max(s1, s2) - Math.min(s1, s2) + 1;

        // Not a valid triangle
        if (min_length > max_length)
        {
            document.write(-1);
            return;
        }

        document.write("Max = " + max_length+"<br/>");
        document.write("Min = " + min_length);
    }

    // Driver code
    var s1 = 8, s2 = 5;
    find_length(s1, s2);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
Max = 12
Min = 4
```