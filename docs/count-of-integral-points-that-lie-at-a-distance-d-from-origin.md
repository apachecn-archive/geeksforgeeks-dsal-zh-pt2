# 距离原点距离为 D 的积分点的计数

> 原文:[https://www . geeksforgeeks . org/距离原点 d 点积分计数/](https://www.geeksforgeeks.org/count-of-integral-points-that-lie-at-a-distance-d-from-origin/)

给定一个正整数 **D** ，任务是找出距离原点 **D** 一定距离的**整数**坐标 **(x，y)** 的个数。

**示例:**

> **输入:** D = 1
> **输出:** 4
> **说明:**总有效点数为{1，0}、{0，1}、{-1，0}、{0，-1}
> 
> **输入:** D = 5
> **输出:** 12
> **解释:**总有效点数为{0，5}、{0，-5}、{5，0}、{-5，0}、{3，4}、{3，-4}、{-3，4}、{-3，-4}、{4，3}、{4，-3}、{-4，3}、{-3}、{-4，3 }、{-4，-3}

**方法:**这个问题可以简化为计算以原点为中心、半径为 **D** 的圆的圆周上的整数坐标，并且可以借助[毕达哥拉斯定理](https://en.wikipedia.org/wiki/Pythagorean_theorem)求解。由于点与原点的距离应该是 **D** ，所以它们都必须满足方程 **x * x + y * y = D <sup>2</sup>** ，其中(x，y)是点的坐标。
现在，要解决上述问题，请按照以下步骤操作:

*   初始化一个变量，比如说**计数**，它存储了**可能的坐标对**的总计数。
*   迭代所有可能的 **x 坐标**，计算 **y** 的对应值为**sqrt(D<sup>2</sup>–y * y)**。
*   因为 **x** 和 **y** 都是正整数的每个坐标可以形成总共 **4 个可能的有效对**作为 **{x，y}、{-x，y}、{-x，-y}、{x，-y}** ，并且通过变量**计数**中的 **4** 来增加每个可能对 **(x，y)** 的计数。
*   此外，由于圆的半径是一个整数，所以它切割 x 轴和 y 轴的圆周上总是存在一个整数坐标。所以在**数**加 4，补偿这些点。
*   完成上述步骤后，打印**计数**的值作为成对计数的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the total valid
// integer coordinates at a distance D
// from origin
int countPoints(int D)
{
    // Stores the count of valid points
    int count = 0;

    // Iterate over possible x coordinates
    for (int x = 1; x * x < D * D; x++) {

        // Find the respective y coordinate
        // with the pythagoras theorem
        int y = (int)sqrt(double(D * D - x * x));
        if (x * x + y * y == D * D) {
            count += 4;
        }
    }

    // Adding 4 to compensate the coordinates
    // present on x and y axes.
    count += 4;

    // Return the answer
    return count;
}

// Driver Code
int main()
{
    int D = 5;
    cout << countPoints(D);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// Function to find the total valid
// integer coordinates at a distance D
// from origin
static int countPoints(int D)
{

    // Stores the count of valid points
    int count = 0;

    // Iterate over possible x coordinates
    for (int x = 1; x * x < D * D; x++) {

        // Find the respective y coordinate
        // with the pythagoras theorem
        int y = (int)Math.sqrt((D * D - x * x));
        if (x * x + y * y == D * D) {
            count += 4;
        }
    }

    // Adding 4 to compensate the coordinates
    // present on x and y axes.
    count += 4;

    // Return the answer
    return count;
}

// Driver Code
public static void main (String[] args)
{
    int D = 5;
    System.out.println(countPoints(D));
}
}

// this code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# python 3 program for the above approach
from math import sqrt

# Function to find the total valid
# integer coordinates at a distance D
# from origin
def countPoints(D):

    # Stores the count of valid points
    count = 0

    # Iterate over possible x coordinates
    for x in range(1, int(sqrt(D * D)), 1):

        # Find the respective y coordinate
        # with the pythagoras theorem
        y = int(sqrt((D * D - x * x)))
        if (x * x + y * y == D * D):
            count += 4

    # Adding 4 to compensate the coordinates
    # present on x and y axes.
    count += 4

    # Return the answer
    return count

# Driver Code
if __name__ == '__main__':
    D = 5
    print(countPoints(D))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

// Function to find the total valid
// integer coordinates at a distance D
// from origin
public class GFG{
    static int countPoints(int D){

        // Stores the count of valid points
        int count = 0;

        // Iterate over possible x coordinates
        for(int x = 1; x*x < D*D; x++){
            int y = (int)Math.Sqrt((D * D - x * x));

            // Find the respective y coordinate
            // with the pythagoras theorem
            if(x * x + y * y == D * D){
              count += 4;  
            }
       }
    // Adding 4 to compensate the coordinates
    // present on x and y axes.

    count += 4;

    // Return the answer
    return count;
}

    // Driver Code

    public static void Main(){
        int D = 5;
        Console.Write(countPoints(D));
    }
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the total valid
        // integer coordinates at a distance D
        // from origin
        function countPoints(D)
        {

            // Stores the count of valid points
            let count = 0;

            // Iterate over possible x coordinates
            for (let x = 1; x * x < D * D; x++) {

                // Find the respective y coordinate
                // with the pythagoras theorem
                let y = Math.floor(Math.sqrt(D * D - x * x));
                if (x * x + y * y == D * D) {
                    count += 4;
                }
            }

            // Adding 4 to compensate the coordinates
            // present on x and y axes.
            count += 4;

            // Return the answer
            return count;
        }

        // Driver Code
        let D = 5;
        document.write(countPoints(D));

     // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
12
```

**时间复杂度:**O(R)
T3】辅助空间: O(1)