# 使整数 A 可被整数 B 整除的最小减量

> 原文:[https://www . geeksforgeeks . org/最小递减使整数 a 被整数 b 整除/](https://www.geeksforgeeks.org/minimum-decrements-to-make-integer-a-divisible-by-integer-b/)

给定两个**正整数 A 和 B** ，其中 A 大于 B。在一次移动中，可以将 A 减 1，这意味着在一次移动后，A 等于 A–1。任务是找到在恒定时间内使 A 被 B 整除所需的最小移动次数。
**例:**

```
Input : A = 10, B = 3 
Output : 1
Explanation:
Only one move is required A = A - 1 = 9,
which is divisible by 3.

Input : A = 10, B = 10
Output : 0
Explanation:
Since A is equal to B therefore zero move required. 
```

**方法:**
为了解决上面提到的问题，我们取 A % B 的数的模，结果存储在一个变量中，这个变量就是所需的答案。
以下是上述办法的实施:

## C++

```
// C++ implementation to count
// Total numbers moves to make
// integer A divisible by integer B

#include <bits/stdc++.h>
using namespace std;

// Function that print number
// of moves required
void movesRequired(int a, int b)
{
    // calculate modulo
    int total_moves = a % b;

    // print the required answer
    cout << total_moves << "\n";
}

// Driver Code
int main()
{

    // initialise A and B
    int A = 10, B = 3;

    movesRequired(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count
// total numbers moves to make
// integer A divisible by integer B
import java.util.*;

class GFG{

// Function that print number
// of moves required
static void movesRequired(int a, int b)
{

    // Calculate modulo
    int total_moves = a % b;

    // Print the required answer
    System.out.println(total_moves);
}

// Driver code
public static void main(String[] args)
{

    // Initialise A and B
    int A = 10, B = 3;

    movesRequired(A, B);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to count
# total numbers moves to make
# integer A divisible by integer B

# Function that print number
# of moves required
def movesRequired(a, b):

    # Calculate modulo
    total_moves = a % b

    # Print the required answer
    print(total_moves)

# Driver Code
if __name__ == '__main__':

    # Initialise A and B
    A = 10
    B = 3

    movesRequired(A, B)

# This code is contributed by Samarth
```

## C#

```
// C# implementation to count
// total numbers moves to make
// integer A divisible by integer B
using System;
class GFG
{

// Function that print number
// of moves required
static void movesRequired(int a, int b)
{

    // Calculate modulo
    int total_moves = a % b;

    // Print the required answer
    Console.Write(total_moves);
}

// Driver code
public static void Main(String []args)
{

    // Initialise A and B
    int A = 10, B = 3;

    movesRequired(A, B);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
    // Javascript implementation to count
    // Total numbers moves to make
    // integer A divisible by integer B

    // Function that print number
    // of moves required
    function movesRequired(a, b)
    {
        // calculate modulo
        let total_moves = a % b;

        // print the required answer
        document.write(total_moves);
    }

    // initialise A and B
    let A = 10, B = 3;

    movesRequired(A, B);

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
1
```