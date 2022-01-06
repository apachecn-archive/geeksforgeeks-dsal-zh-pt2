# 计算给定范围内的发音数

> 原文:[https://www . geeksforgeeks . org/count-pronic-numbers-from-a-给定范围/](https://www.geeksforgeeks.org/count-pronic-numbers-from-a-given-range/)

给定两个整数 **A** 和 **B** ，任务是计算**【A，B】**范围内出现的[音位数字](https://www.geeksforgeeks.org/check-given-number-pronic/)的数量。

**示例:**

> **输入:** A = 3，B = 20
> **输出:** 3
> **说明:**范围[3，20]内的音位数字是 6，12，20
> 
> **输入:** A = 5000，B = 990000000
> T3】输出: 31393

**天真方法:**按照给定的步骤解决问题:

1.  将[发音数字](https://www.geeksforgeeks.org/check-given-number-pronic/)的计数初始化为 **0** 。
2.  对于**【A，B】**[范围内的每一个数字，检查**它**是否为正整数](https://www.geeksforgeeks.org/check-given-number-pronic/)
3.  如果发现为真，则增加计数。
4.  最后，打印计数

下面是上述方法的实现:

## C++14

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if x
// is a Pronic Number or not
bool checkPronic(int x)
{

    for (int i = 0; i <= (int)(sqrt(x));
         i++) {

        // Check for Pronic Number by
        // multiplying consecutive
        // numbers
        if (x == i * (i + 1)) {
            return true;
        }
    }
    return false;
}

// Function to count pronic
// numbers in the range [A, B]
void countPronic(int A, int B)
{
    // Initialise count
    int count = 0;

    // Iterate from A to B
    for (int i = A; i <= B; i++) {

        // If i is pronic
        if (checkPronic(i)) {

            // Increment count
            count++;
        }
    }

    // Print count
    cout << count;
}

// Driver Code
int main()
{
    int A = 3, B = 20;

    // Function call to count pronic
    // numbers in the range [A, B]
    countPronic(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check if x
// is a Pronic Number or not
static boolean checkPronic(int x)
{

    for (int i = 0; i <= (int)(Math.sqrt(x));
         i++) {

        // Check for Pronic Number by
        // multiplying consecutive
        // numbers
        if ((x == i * (i + 1)) != false) {
            return true;
        }
    }
    return false;
}

// Function to count pronic
// numbers in the range [A, B]
static void countPronic(int A, int B)
{
    // Initialise count
    int count = 0;

    // Iterate from A to B
    for (int i = A; i <= B; i++) {

        // If i is pronic
        if (checkPronic(i) != false) {

            // Increment count
            count++;
        }
    }

    // Print count
    System.out.print(count);
}

// Driver Code
public static void main(String args[])
{
    int A = 3, B = 20;

    // Function call to count pronic
    // numbers in the range [A, B]
    countPronic(A, B);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check if x
# is a Pronic Number or not
def checkPronic(x) :
    for i in range(int(math.sqrt(x)) + 1):

        # Check for Pronic Number by
        # multiplying consecutive
        # numbers
        if (x == i * (i + 1)) :
            return True
    return False

# Function to count pronic
# numbers in the range [A, B]
def countPronic(A, B) :

    # Initialise count
    count = 0

    # Iterate from A to B
    for i in range(A, B + 1):

        # If i is pronic
        if (checkPronic(i) != 0) :

            # Increment count
            count += 1

    # Prcount
    print(count)

# Driver Code
A = 3
B = 20

# Function call to count pronic
# numbers in the range [A, B]
countPronic(A, B)

# This code is contributed by susmitakundugoaldanga.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to check if x
// is a Pronic Number or not
static bool checkPronic(int x)
{

    for (int i = 0; i <= (int)(Math.Sqrt(x));
         i++)
    {

        // Check for Pronic Number by
        // multiplying consecutive
        // numbers
        if ((x == i * (i + 1)) != false)
        {
            return true;
        }
    }
    return false;
}

// Function to count pronic
// numbers in the range [A, B]
static void countPronic(int A, int B)
{

    // Initialise count
    int count = 0;

    // Iterate from A to B
    for (int i = A; i <= B; i++)
    {

        // If i is pronic
        if (checkPronic(i) != false)
        {

            // Increment count
            count++;
        }
    }

    // Print count
    Console.Write(count);
}

// Driver Code
public static void Main(String[] args)
{
    int A = 3, B = 20;

    // Function call to count pronic
    // numbers in the range [A, B]
    countPronic(A, B);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach

// Function to check if x
// is a Pronic Number or not
function checkPronic(x)
{

    for (let i = 0; i <= parseInt(Math.sqrt(x));
         i++) {

        // Check for Pronic Number by
        // multiplying consecutive
        // numbers
        if (x == i * (i + 1)) {
            return true;
        }
    }
    return false;
}

// Function to count pronic
// numbers in the range [A, B]
function countPronic(A, B)
{
    // Initialise count
    let count = 0;

    // Iterate from A to B
    for (let i = A; i <= B; i++) {

        // If i is pronic
        if (checkPronic(i)) {

            // Increment count
            count++;
        }
    }

    // Print count
    document.write(count);
}

// Driver Code
let A = 3, B = 20;

// Function call to count pronic
// numbers in the range [A, B]
countPronic(A, B);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O((B–A)*√(B–A))*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤解决问题:

1.  定义一个函数 **pronic(N)** 求 [pronic 整数](https://www.geeksforgeeks.org/check-given-number-pronic/)的个数，它们是 **≤ N** 。
2.  [计算**N**](https://www.geeksforgeeks.org/square-root-of-an-integer/)的平方根，说 **X** 。
3.  如果 **X** 和**X–1**的乘积小于或等于 **N** ，则返回 **N** 。
4.  否则，返回**N–1**。
5.  打印**pronic(B)–pronic(A–1)**获得范围内的 pronic 整数的计数**【A，B】**

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count pronic
// numbers in the range [A, B]
int pronic(int num)
{
    // Check upto sqrt N
    int N = (int)sqrt(num);

    // If product of consecutive
    // numbers are less than equal to num
    if (N * (N + 1) <= num) {
        return N;
    }

    // Return N - 1
    return N - 1;
}

// Function to count pronic
// numbers in the range [A, B]
int countPronic(int A, int B)
{
    // Subtract the count of pronic numbers
    // which are <= (A - 1) from the count
    // f pronic numbers which are <= B
    return pronic(B) - pronic(A - 1);
}

// Driver Code
int main()
{
    int A = 3;
    int B = 20;

    // Function call to count pronic
    // numbers in the range [A, B]
    cout << countPronic(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to count pronic
// numbers in the range [A, B]
static int pronic(int num)
{

    // Check upto sqrt N
    int N = (int)Math.sqrt(num);

    // If product of consecutive
    // numbers are less than equal to num
    if (N * (N + 1) <= num)
    {
        return N;
    }

    // Return N - 1
    return N - 1;
}

// Function to count pronic
// numbers in the range [A, B]
static int countPronic(int A, int B)
{

    // Subtract the count of pronic numbers
    // which are <= (A - 1) from the count
    // f pronic numbers which are <= B
    return pronic(B) - pronic(A - 1);
}

// Driver Code
public static void main(String[] args)
{
    int A = 3;
    int B = 20;

    // Function call to count pronic
    // numbers in the range [A, B]
    System.out.print(countPronic(A, B));

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count pronic
# numbers in the range [A, B]
def pronic(num) :

    # Check upto sqrt N
    N = int(num ** (1/2));

    # If product of consecutive
    # numbers are less than equal to num
    if (N * (N + 1) <= num) :
        return N;

    # Return N - 1
    return N - 1;

# Function to count pronic
# numbers in the range [A, B]
def countPronic(A, B) :

    # Subtract the count of pronic numbers
    # which are <= (A - 1) from the count
    # f pronic numbers which are <= B
    return pronic(B) - pronic(A - 1);

# Driver Code
if __name__ == "__main__" :

    A = 3;
    B = 20;

    # Function call to count pronic
    # numbers in the range [A, B]
    print(countPronic(A, B));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to count pronic
// numbers in the range [A, B]
static int pronic(int num)
{

    // Check upto sqrt N
    int N = (int)Math.Sqrt(num);

    // If product of consecutive
    // numbers are less than equal to num
    if (N * (N + 1) <= num)
    {
        return N;
    }

    // Return N - 1
    return N - 1;
}

// Function to count pronic
// numbers in the range [A, B]
static int countPronic(int A, int B)
{

    // Subtract the count of pronic numbers
    // which are <= (A - 1) from the count
    // f pronic numbers which are <= B
    return pronic(B) - pronic(A - 1);
}

// Driver Code
public static void Main(String[] args)
{
    int A = 3;
    int B = 20;

    // Function call to count pronic
    // numbers in the range [A, B]
    Console.Write(countPronic(A, B));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count pronic
// numbers in the range [A, B]
function pronic(num)
{

    // Check upto sqrt N
    var N = parseInt(Math.sqrt(num));

    // If product of consecutive
    // numbers are less than equal to num
    if (N * (N + 1) <= num) {
        return N;
    }

    // Return N - 1
    return N - 1;
}

// Function to count pronic
// numbers in the range [A, B]
function countPronic(A, B)
{

    // Subtract the count of pronic numbers
    // which are <= (A - 1) from the count
    // f pronic numbers which are <= B
    return pronic(B) - pronic(A - 1);
}

// Driver Code
var A = 3;
var B = 20;

// Function call to count pronic
// numbers in the range [A, B]
document.write(countPronic(A, B));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(log<sub>2</sub>(B))*
***辅助空间:** O(1)*