# 形成立方体所需的最小立方体数量

> 原文:[https://www . geesforgeks . org/minimum-cuboids-to-form-a-cube/](https://www.geeksforgeeks.org/minimum-cuboids-to-form-a-cube/)

给定[长方体](https://en.wikipedia.org/wiki/Cuboid)的 **L** 、 **B** 和表示**长度**、**宽度**和**高度**的 **H** ，任务是找出可以放在一起形成[立方体](https://en.wikipedia.org/wiki/Cube)的指定尺寸长方体的最小数量。

**示例:**

> **输入:** L = 1，B = 1，H = 2
> **输出:** 4
> **说明:**
> 给定尺寸长方体的体积= 1 * 1 * 2 = 2。
> 由这些长方体组合而成的正方体的体积= 2 * 2 * 2 = 8。
> 因此，所需长方体数= 8 / 2 = 4。
> 
> **输入:** L = 2，B = 5，H = 10
> T3】输出: 10

**天真方法:**找到给定维度的[最大值，并从获得的**最大值**开始迭代整数值。对于每个整数，检查它是否是由给定立方体形成的立方体的可能维度。为此，计算立方体](https://www.geeksforgeeks.org/stdmax-in-cpp/)的[体积和给定尺寸形成的长方体](https://www.geeksforgeeks.org/program-volume-surface-area-cube/)的[体积。检查前者是否能被后者整除。如果发现为真，则打印商数作为所需答案。](https://www.geeksforgeeks.org/program-for-volume-and-surface-area-of-cuboid/)

***时间复杂度:**O(L * B * H)*
T5**辅助空间:** O(1)

**高效方法:**为了优化上述方法，该想法基于以下观察:

*   给定尺寸的**长方体**组合得到的**立方体**的**最小长度**等于 **L、B、**和 **H** 的[*T8】LCMT10】T11。这是因为立方体的维度必须能被 **L** 、 **B** 和 **H** 整除。*](https://www.geeksforgeeks.org/lcm-gq/)
*   为了找到所需的长方体数，计算立方体 **( = LCM(L，B，H) <sup>3</sup> )** 和**长方体(= L * B * H)** 的**体积，打印 ***(立方体体积)/(长方体体积)** a 所需答案。***

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate and
// return LCM of a, b, and c
int find_lcm(int a, int b, int c)
{
    // Find GCD of a and b
    int g = __gcd(a, b);

    // Find LCM of a and b
    int LCM1 = (a * b) / g;

    // LCM(a, b, c) = LCM(LCM(a, b), c)
    g = __gcd(LCM1, c);

    // Finding LCM of a, b, c
    int LCM = (LCM1 * c) / g;

    // return LCM(a, b, c)
    return LCM;
}

// Function to find the minimum
// number of cuboids required to
// make the volume of a valid cube
void minimumCuboids(int L, int B, int H)
{
    // Find the LCM of L, B, H
    int lcm = find_lcm(L, B, H);

    // Volume of the cube
    int volume_cube = lcm * lcm * lcm;

    // Volume of the cuboid
    int volume_cuboid = L * B * H;

    // Minimum number cuboids required
    // to form a cube
    cout << (volume_cube / volume_cuboid);
}

// Driver Code
int main()
{
    // Given dimensions of cuboid
    int L = 1, B = 1, H = 2;

    // Function Call
    minimumCuboids(L, B, H);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to calculate and
// return LCM of a, b, and c
static int find_lcm(int a, int b, int c)
{

    // Find GCD of a and b
    int g = __gcd(a, b);

    // Find LCM of a and b
    int LCM1 = (a * b) / g;

    // LCM(a, b, c) = LCM(LCM(a, b), c)
    g = __gcd(LCM1, c);

    // Finding LCM of a, b, c
    int LCM = (LCM1 * c) / g;

    // return LCM(a, b, c)
    return LCM;
}

// Function to find the minimum
// number of cuboids required to
// make the volume of a valid cube
static void minimumCuboids(int L, int B, int H)
{

    // Find the LCM of L, B, H
    int lcm = find_lcm(L, B, H);

    // Volume of the cube
    int volume_cube = lcm * lcm * lcm;

    // Volume of the cuboid
    int volume_cuboid = L * B * H;

    // Minimum number cuboids required
    // to form a cube
    System.out.print((volume_cube / volume_cuboid));
}
static int __gcd(int a, int b) 
{ 
    return b == 0 ? a:__gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{

    // Given dimensions of cuboid
    int L = 1, B = 1, H = 2;

    // Function Call
    minimumCuboids(L, B, H);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate and
# return LCM of a, b, and c
def find_lcm(a, b, c):

    # Find GCD of a and b
    g = __gcd(a, b);

    # Find LCM of a and b
    LCM1 = (a * b) // g;

    # LCM(a, b, c) = LCM(LCM(a, b), c)
    g = __gcd(LCM1, c);

    # Finding LCM of a, b, c
    LCM = (LCM1 * c) // g;

    # return LCM(a, b, c)
    return LCM;

# Function to find the minimum
# number of cuboids required to
# make the volume of a valid cube
def minimumCuboids(L, B, H):

    # Find the LCM of L, B, H
    lcm = find_lcm(L, B, H);

    # Volume of the cube
    volume_cube = lcm * lcm * lcm;

    # Volume of the cuboid
    volume_cuboid = L * B * H;

    # Minimum number cuboids required
    # to form a cube
    print((volume_cube // volume_cuboid));
def __gcd(a, b):
    if(b == 0):
        return a;
    else:
        return __gcd(b, a % b);

# Driver Code
if __name__ == '__main__':

    # Given dimensions of cuboid
    L = 1; B = 1; H = 2;

    # Function Call
    minimumCuboids(L, B, H);

# This code contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to calculate and
// return LCM of a, b, and c
static int find_lcm(int a, int b, int c)
{

    // Find GCD of a and b
    int g = __gcd(a, b);

    // Find LCM of a and b
    int LCM1 = (a * b) / g;

    // LCM(a, b, c) = LCM(LCM(a, b), c)
    g = __gcd(LCM1, c);

    // Finding LCM of a, b, c
    int LCM = (LCM1 * c) / g;

    // return LCM(a, b, c)
    return LCM;
}

// Function to find the minimum
// number of cuboids required to
// make the volume of a valid cube
static void minimumCuboids(int L, int B, int H)
{

    // Find the LCM of L, B, H
    int lcm = find_lcm(L, B, H);

    // Volume of the cube
    int volume_cube = lcm * lcm * lcm;

    // Volume of the cuboid
    int volume_cuboid = L * B * H;

    // Minimum number cuboids required
    // to form a cube
    Console.Write((volume_cube / volume_cuboid));
}
static int __gcd(int a, int b) 
{ 
    return b == 0 ? a:__gcd(b, a % b);    
}

// Driver Code
public static void Main(String[] args)
{

    // Given dimensions of cuboid
    int L = 1, B = 1, H = 2;

    // Function Call
    minimumCuboids(L, B, H);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate and
// return LCM of a, b, and c
function find_lcm(a, b, c)
{

    // Find GCD of a and b
    let g = __gcd(a, b);

    // Find LCM of a and b
    let LCM1 = (a * b) / g;

    // LCM(a, b, c) = LCM(LCM(a, b), c)
    g = __gcd(LCM1, c);

    // Finding LCM of a, b, c
    let LCM = (LCM1 * c) / g;

    // return LCM(a, b, c)
    return LCM;
}

// Function to find the minimum
// number of cuboids required to
// make the volume of a valid cube
function minimumCuboids(L, B, H)
{

    // Find the LCM of L, B, H
    let lcm = find_lcm(L, B, H);

    // Volume of the cube
    let volume_cube = lcm * lcm * lcm;

    // Volume of the cuboid
    let volume_cuboid = L * B * H;

    // Minimum number cuboids required
    // to form a cube
    document.write((volume_cube /
                    volume_cuboid));
}

function __gcd(a, b) 
{ 
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code

// Given dimensions of cuboid
let L = 1, B = 1, H = 2;

// Function Call
minimumCuboids(L, B, H);

// This code is contributed by splevel62

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(log(min(L，B，H))*
***辅助空间:** O(1)*