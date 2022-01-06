# 两列列车同向行驶的距离

> 原文:[https://www . geesforgeks . org/同向两列火车行驶距离/](https://www.geeksforgeeks.org/distance-traveled-by-two-trains-together-in-the-same-direction/)

给定两个数组**A【】**和**B【】**，每个数组由 **N** 个整数组成，包含两列火车在每个时间单位内同向行驶的速度，任务是找出两列火车在整个旅程中一起(并排)行驶的总距离。

**示例:**

> **输入:** A[] = {1，2，3，2，4}，B[] = {2，1，3，1，4}
> **输出:** 3
> **解释:**
> 由于 A[1] + A[0] = B[0] + B[1]，两列列车在 2 个时间单位后行驶了相同的距离。
> 现在，由于 A[2] = B[2] = 3，两列火车一起行驶了这段距离。
> 第 3 个时间单位后，列车速度不同。
> 因此，这两列火车一起行驶的总距离为 3。
> **输入:** A[] = {1，1，3，2，4}，B[] = {3，1，2，1，4}
> **输出:**

**方法:**
按照以下步骤解决问题:

*   同时遍历两个数组。
*   对于每一个 I<sup>指数，检查**和(A【0】..a[I–1])**等于**和(B[0]..B[I–1])**以及 **A[i]** 和 **B[i]** 是否相等。</sup>
*   如果满足以上两个条件，在**答案**中加上**A【I】**。
*   最后遍历完整数组后，打印**答案**。

下面是上述方法的实现:

## C++

```
// C++ Program to find the distance
// traveled together by the two trains
#include <iostream>
using namespace std;

// Function to find the distance traveled together
int calc_distance(int A[], int B[], int n)
{

    // Stores distance travelled by A
    int distance_traveled_A = 0;

    // Stpres distance travelled by B
    int distance_traveled_B = 0;

    // Stores the total distance
    // travelled together
    int answer = 0;

    for (int i = 0; i < 5; i++) {

        // Sum of distance travelled
        distance_traveled_A += A[i];
        distance_traveled_B += B[i];

        // Condition for traveling
        // together
        if ((distance_traveled_A
             == distance_traveled_B)
            && (A[i] == B[i])) {
            answer += A[i];
        }
    }
    return answer;
}

// Driver Code
int main()
{

    int A[5] = { 1, 2, 3, 2, 4 };
    int B[5] = { 2, 1, 3, 1, 4 };
    int N = sizeof(A) / sizeof(A[0]);

    cout << calc_distance(A, B, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the distance
// traveled together by the two trains
import java.util.*;
import java.lang.*;

class GFG{

// Function to find the distance traveled together
static int calc_distance(int A[], int B[], int n)
{

    // Stores distance travelled by A
    int distance_traveled_A = 0;

    // Stpres distance travelled by B
    int distance_traveled_B = 0;

    // Stores the total distance
    // travelled together
    int answer = 0;

    for(int i = 0; i < 5; i++)
    {

        // Sum of distance travelled
        distance_traveled_A += A[i];
        distance_traveled_B += B[i];

        // Condition for traveling
        // together
        if ((distance_traveled_A ==
             distance_traveled_B) &&
             (A[i] == B[i]))
        {
            answer += A[i];
        }
    }
    return answer;
}

// Driver code
public static void main (String[] args)
{
    int A[] = { 1, 2, 3, 2, 4 };
    int B[] = { 2, 1, 3, 1, 4 };
    int N = A.length;

    System.out.println(calc_distance(A, B, N));    
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the distance
# traveled together by the two trains

# Function to find the distance
# traveled together
def calc_distance(A, B, n):

    # Stores distance travelled by A
    distance_traveled_A = 0

    # Stpres distance travelled by B
    distance_traveled_B = 0

    # Stores the total distance
    # travelled together
    answer = 0

    for i in range(5):

        # Sum of distance travelled
        distance_traveled_A += A[i]
        distance_traveled_B += B[i]

        # Condition for traveling
        # together
        if ((distance_traveled_A ==
             distance_traveled_B) and
            (A[i] == B[i])):
            answer += A[i]

    return answer

# Driver Code
A = [ 1, 2, 3, 2, 4 ]
B = [ 2, 1, 3, 1, 4 ]

N = len(A)

print(calc_distance(A, B, N))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to find the distance
// traveled together by the two trains
using System;

class GFG{

// Function to find the distance
// traveled together
static int calc_distance(int []A, int []B,
                         int n)
{

    // Stores distance travelled by A
    int distance_traveled_A = 0;

    // Stpres distance travelled by B
    int distance_traveled_B = 0;

    // Stores the total distance
    // travelled together
    int answer = 0;

    for(int i = 0; i < 5; i++)
    {

        // Sum of distance travelled
        distance_traveled_A += A[i];
        distance_traveled_B += B[i];

        // Condition for traveling
        // together
        if ((distance_traveled_A ==
             distance_traveled_B) &&
             (A[i] == B[i]))
        {
            answer += A[i];
        }
    }
    return answer;
}

// Driver Code
public static void Main(string []s)
{
    int []A = { 1, 2, 3, 2, 4 };
    int []B = { 2, 1, 3, 1, 4 };
    int N = A.Length;

    Console.Write(calc_distance(A, B, N));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// javascript program to find the distance
// traveled together by the two trains
// Function to find the distance traveled together
    function calc_distance(A , B , n)
    {

        // Stores distance travelled by A
        var distance_traveled_A = 0;

        // Stpres distance travelled by B
        var distance_traveled_B = 0;

        // Stores the total distance
        // travelled together
        var answer = 0;

        for (i = 0; i < 5; i++) {

            // Sum of distance travelled
            distance_traveled_A += A[i];
            distance_traveled_B += B[i];

            // Condition for traveling
            // together
            if ((distance_traveled_A == distance_traveled_B) && (A[i] == B[i])) {
                answer += A[i];
            }
        }
        return answer;
    }

    // Driver code

        var A = [ 1, 2, 3, 2, 4 ];
        var B = [ 2, 1, 3, 1, 4 ];
        var N = A.length;

        document.write(calc_distance(A, B, N));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*