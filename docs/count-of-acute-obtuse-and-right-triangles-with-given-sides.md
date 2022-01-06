# 给定边的锐角、钝角和直角三角形的计数

> 原文:[https://www . geeksforgeeks . org/给定边的锐角、钝角和直角三角形的计数/](https://www.geeksforgeeks.org/count-of-acute-obtuse-and-right-triangles-with-given-sides/)

给定一个由 **n** 个不同的正整数组成的数组，这些整数代表可以形成三角形的线的长度。任务是从给定的数组中分别找到锐角三角形、钝角三角形和直角三角形的数量。

**示例:**

```
Input : arr[] = { 2, 3, 9, 10, 12, 15 }.
Output :
Acute Triangle: 2
Right Triangle: 1
Obtuse Triangle: 4

Acute triangles that can be formed are {10, 12, 15} 
and { 9, 10, 12 }.
Right triangles that can be formed are {9, 12, 15}.
Obtuse triangles that can be formed are {2, 9, 10}, 
{3, 9, 10}, {3, 10, 12} and {9, 10, 15}.
```

有边 a、b、c、a 的三角形<= b c. 
如果 a<sup>2</sup>+b<sup>2</sup>T21】c<sup>2</sup>，则为锐角三角形。
如果 a<sup>2</sup>+b<sup>2</sup>= c<sup>2</sup>，则为直角三角形。
如果 a<sup>2</sup>+b<sup>2</sup><c<sup>2</sup>，则为钝角三角形。

**方法 1(简单):**蛮力可以，使用三个循环，每边一个。检查上述三个条件，看三角形是否可以从三个边开始。

**方法 2(高效):**一种高效的方法是首先对数组进行排序，并为 a 面和 b 面运行两个循环(a < b)。然后在 a + b > c 处找到最远的点 q，那么，从 b 到 q 所有的三角形都是可能的。
也找一个最远的点 p，a<sup>2</sup>+b<sup>2</sup>T18】= c<sup>2</sup>。
现在，观察 a<sup>2</sup>+b<sup>2</sup>= c<sup>2</sup>，然后增加直角三角形的计数。此外，锐角三角形是 p–b–1，钝角三角形是 q–p。

## C++

```
// C++ program to count of acute, obtuse and right
// triangles in an array
#include <bits/stdc++.h>
using namespace std;

// Find the number of acute, right, obtuse triangle
// that can be formed from given array.
void findTriangle(int a[], int n)
{
    int b[n + 2];

    // Finding the square of each element of array.
    for (int i = 0; i < n; i++)
        b[i] = a[i] * a[i];

    // Sort the sides of array and their squares.
    sort(a, a + n);
    sort(b, b + n);

    // x for acute triangles
    // y for right triangles
    // z for obtuse triangles
    int x=0,y=0,z=0;
    for (int i=0; i<n; i++)
    {
        int p = i+1;
        int q = i+1;

        for (int j=i+1; j<n; j++)
        {
            // Finding the farthest point p where
            // a^2 + b^2 >= c^2.
            while (p<n-1 && b[i]+b[j]>=b[p+1])
                p++;

            q = max(q, p);

            // Finding the farthest point q where
            // a + b > c.
            while (q<n-1 && a[i]+a[j]>a[q+1])
                q++;

            // If point p make right triangle.
            if (b[i]+b[j]==b[p])
            {
                // All triangle between j and p are acute
                // triangles. So add p - j - 1 in x.
                x += max(p - j - 1, 0);

                // Increment y by 1.
                y++;

                // All triangle between q and p are acute
                // triangles. So add q - p in z.
                z += q - p;
            }

            // If no right triangle
            else
            {
                // All triangle between j and p are acute
                // triangles. So add p - j in x.
                x += max(p - j, 0);

                // All triangle between q and p are acute
                // triangles. So add q - p in z.
                z += q - p;
            }
        }
    }

    cout << "Acute Triangle: " << x << endl;
    cout << "Right Triangle: " << y << endl;
    cout << "Obtuse Triangle: " << z << endl;
}

// Driver Code
int main()
{
    int arr[] = {2, 3, 9, 10, 12, 15};
    int n = sizeof(arr)/sizeof(arr[0]);
    findTriangle(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count of
// acute, obtuse and right
// triangles in an array
import java.util.*;
class GFG{

// Find the number of acute,
// right, obtuse triangle
// that can be formed from
// given array.
static void findTriangle(int a[],
                         int n)
{
  int b[] = new int[n];

  // Finding the square of
  // each element of array.
  for (int i = 0; i < n; i++)
    b[i] = a[i] * a[i];

  // Sort the sides of array
  // and their squares.
  Arrays.sort(a);
  Arrays.sort(b);

  // x for acute triangles
  // y for right triangles
  // z for obtuse triangles
  int x = 0, y = 0, z = 0;
  for (int i = 0; i < n; i++)
  {
    int p = i + 1;
    int q = i + 1;

    for (int j = i + 1; j < n; j++)
    {
      // Finding the farthest point
      // p where a^2 + b^2 >= c^2.
      while (p < n - 1 &&
             b[i] + b[j] >= b[p + 1])
        p++;

      q = Math.max(q, p);

      // Finding the farthest point
      // q where a + b > c.
      while (q < n - 1 &&
             a[i] + a[j] > a[q + 1])
        q++;

      // If point p make right triangle.
      if (b[i] + b[j] == b[p])
      {
        // All triangle between j
        // and p are acute triangles.
        // So add p - j - 1 in x.
        x += Math.max(p - j - 1, 0);

        // Increment y by 1.
        y++;

        // All triangle between q
        // and p are acute triangles.
        // So add q - p in z.
        z += q - p;
      }

      // If no right triangle
      else
      {
        // All triangle between
        // j and p are acute triangles.
        // So add p - j in x.
        x += Math.max(p - j, 0);

        // All triangle between q
        // and p are acute triangles.
        // So add q - p in z.
        z += q - p;
      }
    }
  }

  System.out.println("Acute Triangle: " + x);
  System.out.println("Right Triangle: " + y);
  System.out.println("Obtuse Triangle: " + z);
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {2, 3, 9, 10, 12, 15};
  int n = arr.length;
  findTriangle(arr, n);
}
}

// This code is contributed by Chitranayal
```

## 蟒蛇 3

```
# Python3 program to count of acute, obtuse and right
# triangles in an array

# Find the number of acute, right, obtuse triangle
# that can be formed from given array.
def findTriangle(a, n) :

    b = []
    # Finding the square of each element of array
    for i in range(n) :
        b.append(a[i] * a[i])

    # Sort the sides of array and their squares.
    a.sort()
    b.sort()

    # x for acute triangles
    # y for right triangles
    # z for obtuse triangles
    x, y, z = 0, 0, 0

    for i in range(n) :
        p = i+1
        q = i+1
        for j in range(i + 1, n) :
            # Finding the farthest point p where
            # a^2 + b^2 >= c^2.
            while (p<n-1 and b[i]+b[j]>=b[p+1]) :
                p += 1
            q = max(q, p)
            # Finding the farthest point q where
            # a + b > c.
            while (q<n-1 and a[i]+a[j]>a[q+1]) :
                q += 1

            # If point p make right triangle.
            if (b[i]+b[j]==b[p]) :
                # All triangle between j and p are acute
                # triangles. So add p - j - 1 in x.
                x += max(p - j - 1, 0)
                # Increment y by 1.
                y += 1
                # All triangle between q and p are acute
                # triangles. So add q - p in z.
                z += q - p
            # If no right triangle
            else :
                # All triangle between j and p are acute
                # triangles. So add p - j in x.
                x += max(p - j, 0)
                # All triangle between q and p are acute
                # triangles. So add q - p in z.
                z += q - p

    print("Acute Triangle:",x )
    print("Right Triangle:", y)
    print("Obtuse Triangle:", z)

# Driver Code
if __name__ == "__main__" :

    arr = [2, 3, 9, 10, 12, 15]
    n = len(arr)
    findTriangle(arr, n)

# This code is contributed by Ryuga
```

## C#

```
// C# program to count of
// acute, obtuse and right
// triangles in an array
using System;

class GFG{

// Find the number of acute,
// right, obtuse triangle
// that can be formed from
// given array.
static void findTriangle(int []a, int n)
{
  int []b = new int[n];

  // Finding the square of
  // each element of array.
  for(int i = 0; i < n; i++)
    b[i] = a[i] * a[i];

  // Sort the sides of array
  // and their squares.
  Array.Sort(a);
  Array.Sort(b);

  // x for acute triangles
  // y for right triangles
  // z for obtuse triangles
  int x = 0, y = 0, z = 0;
  for(int i = 0; i < n; i++)
  {
    int p = i + 1;
    int q = i + 1;

    for(int j = i + 1; j < n; j++)
    {

      // Finding the farthest point
      // p where a^2 + b^2 >= c^2.
      while (p < n - 1 &&
             b[i] + b[j] >= b[p + 1])
        p++;

      q = Math.Max(q, p);

      // Finding the farthest point
      // q where a + b > c.
      while (q < n - 1 &&
             a[i] + a[j] > a[q + 1])
        q++;

      // If point p make right triangle.
      if (b[i] + b[j] == b[p])
      {

        // All triangle between j
        // and p are acute triangles.
        // So add p - j - 1 in x.
        x += Math.Max(p - j - 1, 0);

        // Increment y by 1.
        y++;

        // All triangle between q
        // and p are acute triangles.
        // So add q - p in z.
        z += q - p;
      }

      // If no right triangle
      else
      {

        // All triangle between
        // j and p are acute triangles.
        // So add p - j in x.
        x += Math.Max(p - j, 0);

        // All triangle between q
        // and p are acute triangles.
        // So add q - p in z.
        z += q - p;
      }
    }
  }

  Console.Write("Acute Triangle: " + x + "\n");
  Console.Write("Right Triangle: " + y + "\n");
  Console.Write("Obtuse Triangle: " + z + "\n");
}

// Driver Code
public static void Main(string[] args)
{
  int []arr = { 2, 3, 9, 10, 12, 15 };
  int n = arr.Length;

  findTriangle(arr, n);
}
}

// This code is contributed by rutvik_56
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count of acute, obtuse
// and right triangles in an array

// Find the number of acute, right, obtuse
// triangle that can be formed from given array.
function findTriangle($a, $n)
{
    $b[$n + 2] = array();

    // Finding the square of each
    // element of array.
    for ($i = 0; $i < $n; $i++)
        $b[$i] = $a[$i] * $a[$i];

    // Sort the sides of array and
    // their squares.
    sort($a);
    sort($b);

    // x for acute triangles
    // y for right triangles
    // z for obtuse triangles
    $x = 0;
    $y = 0;
    $z = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $p = $i + 1;
        $q = $i + 1;

        for ($j = $i + 1; $j < $n; $j++)
        {
            // Finding the farthest point p
            // where a^2 + b^2 >= c^2.
            while ($p < $n - 1 &&
                   $b[$i] + $b[$j] >= $b[$p + 1])
                $p++;

            $q = max($q, $p);

            // Finding the farthest point q
            // where a + b > c.
            while ($q < $n - 1 &&
                   $a[$i] + $a[$j] > $a[$q + 1])
                $q++;

            // If point p make right triangle.
            if ($b[$i] + $b[$j] == $b[$p])
            {
                // All triangle between j and p are acute
                // triangles. So add p - j - 1 in x.
                $x += max($p - $j - 1, 0);

                // Increment y by 1.
                $y++;

                // All triangle between q and p are
                // acute triangles. So add q - p in z.
                $z += $q - $p;
            }

            // If no right triangle
            else
            {
                // All triangle between j and p are acute
                // triangles. So add p - j in x.
                $x += max($p - $j, 0);

                // All triangle between q and p are acute
                // triangles. So add q - p in z.
                $z += $q - $p;
            }
        }
    }

    echo "Acute Triangle: ", $x, "\n";
    echo "Right Triangle: ", $y, "\n";
    echo "Obtuse Triangle: ", $z, "\n";
}

// Driver Code
$arr = array(2, 3, 9, 10, 12, 15);
$n = sizeof($arr);
findTriangle($arr, $n);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript program to count of
// acute, obtuse and right
// triangles in an array

    // Find the number of acute,
    // right, obtuse triangle
    // that can be formed from
    // given array.
    function findTriangle(a,n)
    {
        let b=new Array(n);
        for(let i=0;i<n;i++)
        {
            b[i]=0;
        }

        // Finding the square of
      // each element of array.
      for (let i = 0; i < n; i++)
        b[i] = a[i] * a[i];

      // Sort the sides of array
      // and their squares.
      a.sort(function(i,j){return i-j;});
      b.sort(function(i,j){return i-j;});

      // x for acute triangles
        // y for right triangles
        // z for obtuse triangles
        let x = 0, y = 0, z = 0;
        for (let i = 0; i < n; i++)
        {
        let p = i + 1;
        let q = i + 1;

        for (let j = i + 1; j < n; j++)
        {
          // Finding the farthest point
          // p where a^2 + b^2 >= c^2.
          while (p < n - 1 &&
                 b[i] + b[j] >= b[p + 1])
            p++;

          q = Math.max(q, p);

          // Finding the farthest point
          // q where a + b > c.
          while (q < n - 1 &&
                 a[i] + a[j] > a[q + 1])
            q++;

          // If point p make right triangle.
          if (b[i] + b[j] == b[p])
          {
            // All triangle between j
            // and p are acute triangles.
            // So add p - j - 1 in x.
            x += Math.max(p - j - 1, 0);

            // Increment y by 1.
            y++;

            // All triangle between q
            // and p are acute triangles.
            // So add q - p in z.
            z += q - p;
          }

          // If no right triangle
          else
          {
            // All triangle between
            // j and p are acute triangles.
            // So add p - j in x.
            x += Math.max(p - j, 0);

            // All triangle between q
            // and p are acute triangles.
            // So add q - p in z.
            z += q - p;
          }
        }
        }

        document.write("Acute Triangle: " + x+"<br>");
        document.write("Right Triangle: " + y+"<br>");
        document.write("Obtuse Triangle: " + z+"<br>");

    }
    // Driver Code

    let arr=[2, 3, 9, 10, 12, 15];
    let n = arr.length;
    findTriangle(arr, n);

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Acute Triangle: 2
Right Triangle: 1
Obtuse Triangle: 4
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。