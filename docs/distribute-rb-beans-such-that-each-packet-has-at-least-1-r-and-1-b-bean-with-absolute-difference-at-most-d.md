# 分配 R、B 豆，使得每个包至少有 1 个 R 和 1 个 B 豆，绝对差值最多为 D

> 原文:[https://www . geeksforgeeks . org/distribute-Rb-beans-这样-每个包至少有-1-r-和-1-b-bean-最多有绝对差异-d/](https://www.geeksforgeeks.org/distribute-rb-beans-such-that-each-packet-has-at-least-1-r-and-1-b-bean-with-absolute-difference-at-most-d/)

给定两个正整数 **R** 和 **B** 代表 **R** 红色和 **B** 蓝色的豆子和一个整数 **D** ，任务是检查是否有可能根据以下规则在几个(可能是一个)包之间分配豆子:

*   每包至少有一颗红豆。
*   每个包至少有一个蓝色的豆子。
*   **每包**中红豆和蓝豆的数量相差不超过 **D (** 或 **|R-B| < = D)**

如果可能，打印**是**。否则，打印**否**。

**示例**

> **输入:** R = 1，B = 1，D = 0
> **输出:**是
> **说明:**1 红 1 蓝豆组成一包。绝对差**| 1 1 | = 0≤D**。
> 
> **输入:** R = 6，B = 1，D = 4
> T3】输出:否

**进场:**观察**(R****B)**的最大值是 **D + 1** 乘以 **R** 和 **B** 的最小值，就可以轻松解决这个问题。按照下面给出的步骤解决问题:

*   求 **R 和 b 的[最大值.](https://www.geeksforgeeks.org/compute-the-minimum-or-maximum-max-of-two-integers-without-branching/)** 和[R 和 b 的](https://www.geeksforgeeks.org/compute-the-minimum-or-maximum-max-of-two-integers-without-branching/)**最小值**
*   **为了满足给定的 3 个约束条件， **max(R，B)** 的值最多应该是 **(D + 1)** 乘以 **min(R，B)** ，因为 **(D + 1)** 豆可以保存在每个包中，一种类型的 1 个豆，另一种类型的 **D** 豆。**
*   **完成上述步骤后，如果**最大值(R，B)** 小于或等于**(D+1)*最小值(R，B)** ，则打印**“是”**。否则，打印**“否”**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to distribute R red and B blue beans
// in packets such that the difference
// between the beans in each packet is
// atmost D
void checkDistribution(int R, int B, int D)
{
    // Check for the condition to
    // distributing beans
    if (max(R, B) <= min(R, B) * (D + 1)) {

        // Print the answer
        cout << "Yes";
    }

    // Distribution is not possible
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    int R = 1, B = 1, D = 0;
    checkDistribution(R, B, D);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to check if it is possible
    // to distribute R red and B blue beans
    // in packets such that the difference
    // between the beans in each packet is
    // atmost D
    static void checkDistribution(int R, int B, int D)
    {

        // Check for the condition to
        // distributing beans
        if (Math.max(R, B) <= Math.min(R, B) * (D + 1)) {

            // Print the answer
            System.out.println("Yes");
        }

        // Distribution is not possible
        else {
            System.out.println("No");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int R = 1, B = 1, D = 0;
        checkDistribution(R, B, D);
    }
}

// This code is contributed by Potta Lokesh
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to check if it is possible
# to distribute R red and B blue beans
# in packets such that the difference
# between the beans in each packet is
# atmost D
def checkDistribution(R, B, D):

    # Check for the condition to
    # distributing beans
    if (max(R, B) <= min(R, B) * (D + 1)):

        # Print the answer
        print("Yes")

    # Distribution is not possible
    else:
        print("No")

# Driver Code
R = 1
B = 1
D = 0

checkDistribution(R, B, D)

# This code is contributed by code_hunt
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

    // Function to check if it is possible
    // to distribute R red and B blue beans
    // in packets such that the difference
    // between the beans in each packet is
    // atmost D
    static void checkDistribution(int R, int B, int D)
    {

        // Check for the condition to
        // distributing beans
        if (Math.Max(R, B) <= Math.Min(R, B) * (D + 1)) {

            // Print the answer
            Console.WriteLine("Yes");
        }

        // Distribution is not possible
        else {
            Console.WriteLine("No");
        }
    }

// Driver code
static public void Main()
{
    int R = 1, B = 1, D = 0;
    checkDistribution(R, B, D);
}
}

// This code is contributed by target_2.
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

    // Function to check if it is possible
    // to distribute R red and B blue beans
    // in packets such that the difference
    // between the beans in each packet is
    // atmost D
   function checkDistribution(R, B, D)
    {

        // Check for the condition to
        // distributing beans
        if (Math.max(R, B) <= Math.min(R, B) * (D + 1)) {

            // Print the answer
            document.write("Yes");
        }

        // Distribution is not possible
        else {
            document.write("No");
        }
    }

// Driver Code

    let R = 1, B = 1, D = 0;
    checkDistribution(R, B, D);

// This code is contributed by sanjoy_62.
</script>
```

****Output**

```
Yes
```** 

*****时间复杂度:**O(1)*
T5**辅助空间:** O(1)**