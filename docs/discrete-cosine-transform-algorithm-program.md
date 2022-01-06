# 离散余弦变换(算法和程序)

> 原文:[https://www . geesforgeks . org/discrete-余弦变换-算法-程序/](https://www.geeksforgeeks.org/discrete-cosine-transform-algorithm-program/)

**图像压缩:**存储或传输具有像素值的图像。可以通过减少每个像素包含的值来压缩它。图像压缩基本上有两种类型:
**1。**无损压缩:在这种类型的压缩中，恢复后的图像与应用压缩技术之前完全相同，因此其质量没有降低。
**2。**有损压缩:在这种类型的压缩中，恢复后我们无法获得与旧数据完全相同的数据，这就是图像质量显著降低的原因。但是这种类型的压缩导致非常高的图像数据压缩，并且在通过网络传输图像时非常有用。
**离散余弦变换**用于有损图像压缩，因为它具有非常强的能量压缩，即它的大量信息存储在信号的非常低的频率分量中，而剩余的其他频率具有非常小的数据，可以通过使用非常少的比特数(通常最多 2 或 3 比特)来存储。
要对图像执行离散余弦变换，首先我们必须提取图像文件信息(以范围为 0–255 整数表示的像素值)，将其划分为 8×8 矩阵的块，然后对该数据块应用离散余弦变换。
应用离散余弦变换后，我们会看到其 90%以上的数据将处于低频分量。为简单起见，我们取一个大小为 8×8 的矩阵，所有值为 255(考虑图像完全为白色)，我们将对其执行二维离散余弦变换以观察输出。

**算法:**假设在应用离散余弦变换后，我们有一个包含图像信息的名为 8×8 维矩阵的二维变量和一个包含信息的名为 dct 的同维二维变量。因此，我们有公式
dct[i][j] = ci * cj (sum(k=0 到 m-1) sum(l=0 到 n-1)矩阵[k][l]* cos((2 * k+1)* I * pi/2 * m)* cos((2 * l+1)* j * pi/2 * n)
其中，如果 i=0，则 ci= 1/sqrt(m ),否则 ci= sqrt(2)/sqrt(m)和
类似，cj= 1
在本代码中，m 和 n 均等于 **8** ， **pi** 定义为 3.142857。

## C++

```
// CPP program to perform discrete cosine transform
#include <bits/stdc++.h>
using namespace std;
#define pi 3.142857
const int m = 8, n = 8;

// Function to find discrete cosine transform and print it
int dctTransform(int matrix[][n])
{
    int i, j, k, l;

    // dct will store the discrete cosine transform
    float dct[m][n];

    float ci, cj, dct1, sum;

    for (i = 0; i < m; i++) {
        for (j = 0; j < n; j++) {

            // ci and cj depends on frequency as well as
            // number of row and columns of specified matrix
            if (i == 0)
                ci = 1 / sqrt(m);
            else
                ci = sqrt(2) / sqrt(m);
            if (j == 0)
                cj = 1 / sqrt(n);
            else
                cj = sqrt(2) / sqrt(n);

            // sum will temporarily store the sum of
            // cosine signals
            sum = 0;
            for (k = 0; k < m; k++) {
                for (l = 0; l < n; l++) {
                    dct1 = matrix[k][l] *
                           cos((2 * k + 1) * i * pi / (2 * m)) *
                           cos((2 * l + 1) * j * pi / (2 * n));
                    sum = sum + dct1;
                }
            }
            dct[i][j] = ci * cj * sum;
        }
    }

    for (i = 0; i < m; i++) {
        for (j = 0; j < n; j++) {
            printf("%f\t", dct[i][j]);
        }
        printf("\n");
    }
}

// Driver code
int main()
{
    int matrix[m][n] = { { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 } };
    dctTransform(matrix);
    return 0;
}

//This code is contributed by SoumikMondal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to perform discrete cosine transform

import java.util.*;

class GFG
{
    public static int n = 8,m = 8;
    public static double pi = 3.142857;

    // Function to find discrete cosine transform and print it
    static strictfp void dctTransform(int matrix[][])
    {
        int i, j, k, l;

        // dct will store the discrete cosine transform
        double[][] dct = new double[m][n];

        double ci, cj, dct1, sum;

        for (i = 0; i < m; i++)
        {
            for (j = 0; j < n; j++)
            {
                // ci and cj depends on frequency as well as
                // number of row and columns of specified matrix
                if (i == 0)
                    ci = 1 / Math.sqrt(m);
                else
                    ci = Math.sqrt(2) / Math.sqrt(m);

                if (j == 0)
                    cj = 1 / Math.sqrt(n);
                else
                    cj = Math.sqrt(2) / Math.sqrt(n);

                // sum will temporarily store the sum of
                // cosine signals
                sum = 0;
                for (k = 0; k < m; k++)
                {
                    for (l = 0; l < n; l++)
                    {
                        dct1 = matrix[k][l] *
                               Math.cos((2 * k + 1) * i * pi / (2 * m)) *
                               Math.cos((2 * l + 1) * j * pi / (2 * n));
                        sum = sum + dct1;
                    }
                }
                dct[i][j] = ci * cj * sum;
            }
        }

        for (i = 0; i < m; i++)
        {
            for (j = 0; j < n; j++)
                System.out.printf("%f\t", dct[i][j]);
            System.out.println();
        }
    }

    // driver program
    public static void main (String[] args)
    {
        int matrix[][] = { { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 },
                         { 255, 255, 255, 255, 255, 255, 255, 255 } };
        dctTransform(matrix);
    }
}

// Contributed by Pramod Kumar
```

## C#

```
// C# program to perform discrete cosine transform
using System;

class GFG
{

  // Function to find discrete cosine transform and print it
  public static void dctTransform(int[,] matrix, int m, int n)
  {
    double pi = 3.142857;      
    int i, j, k, l;

    // dct will store the discrete cosine transform
    double[,] dct = new double[m, n];
    double ci, cj, dct1, sum;
    for (i = 0; i < m; i++)
    {
      for (j = 0; j < n; j++)
      {

        // ci and cj depends on frequency as well as
        // number of row and columns of specified matrix
        if (i == 0)
          ci = 1 / Math.Sqrt(m);
        else
          ci = Math.Sqrt(2) / Math.Sqrt(m);
        if (j == 0)
          cj = 1 / Math.Sqrt(n);
        else
          cj = Math.Sqrt(2) /Math.Sqrt(n);

        // sum will temporarily store the sum of
        // cosine signals
        sum = 0;
        for (k = 0; k < m; k++)
        {
          for (l = 0; l < n; l++)
          {
            dct1 = matrix[k, l] *
              Math.Cos((2 * k + 1) * i * pi / (2 * m)) *
              Math.Cos((2 * l + 1) * j * pi / (2 * n));
            sum = sum + dct1;
          }
        }
        dct[i,j] = ci * cj * sum;
      }
    }

    for (i = 0; i < m; i++)
    {
      for (j = 0; j < n; j++)
      {
        Console.Write(dct[i,j]);
      }
      Console.WriteLine();
    }
  }

  // Driver code
  static void Main()
  {
    const int m = 8, n = 8;
    int[,] matrix = new int[m, n] {
      { 255, 255, 255, 255, 255, 255, 255, 255 },
      { 255, 255, 255, 255, 255, 255, 255, 255 },
      { 255, 255, 255, 255, 255, 255, 255, 255 },
      { 255, 255, 255, 255, 255, 255, 255, 255 },
      { 255, 255, 255, 255, 255, 255, 255, 255 },
      { 255, 255, 255, 255, 255, 255, 255, 255 },
      { 255, 255, 255, 255, 255, 255, 255, 255 },
      { 255, 255, 255, 255, 255, 255, 255, 255 }
    };
    dctTransform(matrix, m, n);
  }
}

// This code is contributed by SoumikMondal
```

输出:

```
2039.999878    -1.168211    1.190998    -1.230618    1.289227    -1.370580    1.480267    -1.626942    
-1.167731       0.000664    -0.000694    0.000698    -0.000748    0.000774    -0.000837    0.000920    
1.191004       -0.000694    0.000710    -0.000710    0.000751    -0.000801    0.000864    -0.000950    
-1.230645       0.000687    -0.000721    0.000744    -0.000771    0.000837    -0.000891    0.000975    
1.289146       -0.000751    0.000740    -0.000767    0.000824    -0.000864    0.000946    -0.001026    
-1.370624       0.000744    -0.000820    0.000834    -0.000858    0.000898    -0.000998    0.001093    
1.480278       -0.000856    0.000870    -0.000895    0.000944    -0.001000    0.001080    -0.001177    
-1.626932       0.000933    -0.000940    0.000975    -0.001024    0.001089    -0.001175    0.001298
```

本文由[阿迪蒂亚·库马尔](https://www.linkedin.com/in/aditya-kumar-837315100/)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。