# 二进制表示法中以 LSB 为 0 的[L，R]范围内的数字计数

> 原文:[https://www . geeksforgeeks . org/numbers-in-range-l-r-with-LSB-as-0 在其二进制表示中/](https://www.geeksforgeeks.org/count-of-numbers-in-range-l-r-with-lsb-as-0-in-their-binary-representation/)

给定两个整数 **L** 和 **R** 。任务是找出范围**【L，R】**中所有数字的计数，这些数字在[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)中的最低有效位为 **0。**

**示例**:

> **输入** : L = 10，R = 20
> 输出 : 6
> 
> **输入** : L = 7，R = 11
> **输出** : 2

**天真方法**:解决这个问题最简单的方法就是检查**【L，R】**范围内的每个数字，如果二进制表示中的最低有效位是 **0。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of required numbers
int countNumbers(int l, int r)
{
    int count = 0;

    for (int i = l; i <= r; i++) {
        // If rightmost bit is 0
        if ((i & 1) == 0) {
            count++;
        }
    }
    // Return the required count
    return count;
}

// Driver code
int main()
{
    int l = 10, r = 20;

    // Call function countNumbers
    cout << countNumbers(l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG{

// Function to return the count
// of required numbers
static int countNumbers(int l, int r)
{
    int count = 0;
    for(int i = l; i <= r; i++)
    {

        // If rightmost bit is 0
        if ((i & 1) == 0)
            count += 1;
    }

    // Return the required count
    return count;
}

// Driver code
public static void main(String[] args)
{
    int l = 10, r = 20;

    // Call function countNumbers
    System.out.println(countNumbers(l, r));
}
}

// This code is contributed by MuskanKalra1
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of required numbers
def countNumbers(l, r):

    count = 0

    for i in range(l, r + 1):

        # If rightmost bit is 0
        if ((i & 1) == 0):
            count += 1

    # Return the required count
    return count

# Driver code
l = 10
r = 20

# Call function countNumbers
print(countNumbers(l, r))

# This code is contributed by amreshkumar3
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the count
    // of required numbers
    static int countNumbers(int l, int r)
    {
        int count = 0;
        for (int i = l; i <= r; i++) {

            // If rightmost bit is 0
            if ((i & 1) == 0)
                count += 1;
        }

        // Return the required count
        return count;
    }

    // Driver code
    public static void Main()
    {
        int l = 10, r = 20;

        // Call function countNumbers
        Console.WriteLine(countNumbers(l, r));
    }
}

// This code is contributed by subham348.
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count
// of required numbers
function countNumbers(l, r)
{
    let count = 0;

    for (let i = l; i <= r; i++) {
        // If rightmost bit is 0
        if ((i & 1) == 0) {
            count++;
        }
    }
    // Return the required count
    return count;
}

// Driver code
    let l = 10, r = 20;

    // Call function countNumbers
    document.write(countNumbers(l, r));

</script>
```

**Output**

```
6
```

***时间复杂度:**O(r–l)*
***辅助空间:** O(1)*

**高效途径**:这个问题可以通过利用钻头的[特性来解决。只有偶数最右边的位为 **0** 。计数可在 **O(1)** 时间内，用此公式**((R/2)–(L–1)/2)**求出。](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of required numbers
int countNumbers(int l, int r)
{
    // Count of numbers in range
    // which are divisible by 2
    return ((r / 2) - (l - 1) / 2);
}

// Driver code
int main()
{
    int l = 10, r = 20;
    cout << countNumbers(l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG{

// Function to return the count
// of required numbers
static int countNumbers(int l, int r)
{

    // Count of numbers in range
    //  which are divisible by 2
    return ((r / 2) - (l - 1) / 2);
}

// Driver Code
public static void main(String[] args)
{
    int l = 10;
    int r = 20;

    System.out.println(countNumbers(l, r));
}
}

// This code is contributed by MuskanKalra1
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of required numbers
def countNumbers(l, r):

    # Count of numbers in range
    #  which are divisible by 2
    return ((r // 2) - (l - 1) // 2)

# Driver code
l = 10
r = 20

print(countNumbers(l, r))

# This code is contributed by amreshkumar3
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return the count
// of required numbers
static int countNumbers(int l, int r)
{

    // Count of numbers in range
    // which are divisible by 2
    return ((r / 2) - (l - 1) / 2);
}

// Driver code
public static void Main()
{
    int l = 10, r = 20;
    Console.Write(countNumbers(l, r));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of required numbers
function countNumbers(l, r)
{

    // Count of numbers in range
    // which are divisible by 2
    return(parseInt(r / 2) -
          parseInt((l - 1) / 2));
}

// Driver code
let l = 10, r = 20;

document.write(countNumbers(l, r));

// This code is contributed by subhammahato348

</script>
```

**Output**

```
6
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)