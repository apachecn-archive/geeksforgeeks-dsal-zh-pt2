# 找到 n 辆自行车行驶的最大距离

> 原文:[https://www . geesforgeks . org/find-最大覆盖距离-100 辆自行车/](https://www.geeksforgeeks.org/find-maximum-distance-covered-100-bikes/)

有 n 辆自行车，每辆加满油后可行驶 100 公里。使用 n 辆自行车你能走的最大距离是多少？你可以假设所有的自行车都是相似的，一辆自行车需要 1 升才能行驶 1 公里。
你有 n 辆自行车，用一辆只能跑 100 公里。所以如果 n 辆自行车从同一点出发，同时跑，你只能跑 100 公里。让我们换个角度想，诀窍是当你想跑最大距离时，你应该总是尽量少浪费燃料。最少的燃料消耗意味着骑最少数量的自行车。你可以考虑让 n 辆自行车串行运行，而不是并行运行。这意味着如果你把最后一辆自行车的一些燃料转移到另一辆自行车上，然后扔掉最后一辆自行车，也就是说，不要在某个时间点后跑最后一辆自行车。但问题是，在什么距离之后，燃料转移必须完成，以便最大距离被覆盖，剩余自行车的油箱不会溢出。

让我们考虑以下基本情况，然后推广解决方案。

*   **基本情况 1:有一辆自行车:**这个简单，我们只能走 100 公里。
*   **基本情况 2:有两辆自行车:**当有两辆自行车时，我们能走的最大距离是多少？为了最大化距离，我们必须在某个点放下第二辆自行车，并将其燃料转移到第一辆自行车上。让我们在 x 公里后进行转移。

```
Total distance covered = Distance covered by 100 ltr in first bike +  
                         Distance covered by fuel transferred from 
                         first bike. 
```

*   第二辆自行车的剩余燃油是 100–x。如果我们将这么多燃油转移到第一辆自行车，那么总距离将变为 100+100–x，即 200–x。因此，我们的任务是最大化 200-x。限制条件是，100–x 必须小于或等于第一辆自行车在 x 公里后产生的空间，即 100–x<= x. The value of 200-x becomes maximum when x is minimum. The minimum possible value of x is 50\. So we are able to travel 150 kms. 

*   **基本情况 3:有三辆自行车:**让第一次换乘在 x 公里后完成。x 距离后，所有的自行车都含有 100 x 的燃料。如果我们从第三辆自行车上取 100 倍量的燃油，分配到第一辆和第二辆自行车上，这样第一辆和第二辆自行车的油箱就满了。所以 100-x<= 2 * x；或者，x=33.333，所以我们应该转移第三辆自行车的剩余燃油，并在正好 33.33 公里后在第一辆和第二辆自行车之间分配燃油量。

让我们概括一下。如果我们仔细看看上面的情况，我们可以观察到，如果有 n 辆自行车，那么第一次转移是在 100/n 公里后完成的(或者一辆自行车被丢弃)。更概括地说，当我们每辆自行车还有 x 升剩余燃油，并且还有 n 辆剩余自行车时，我们会在 x/n 公里后丢弃一辆自行车。

下面是一个通用函数的实现。

## C++

```
#include <stdio.h>

// Returns maximum distance that can be traveled by n bikes and given fuel
// in every bike
double maxDistance(int n, int fuel)
{
    // dist_covered is the result of this function
    double dist_covered = 0;

    while (n > 0)
    {
        // after ever fuel/n km we are discarding one bike and filling
        // all the other bikes with fuel/n liters of fuel i.e. to their
        // maximum limit (100 litre)

        dist_covered += (double)fuel / n;

        n -= 1; // reduce number of bikes
    }
    return dist_covered;
}

// Driver program to test above function
int main()
{
    int n = 3; // number of bikes
    int fuel = 100;
    printf("Maximum distance possible with %d bikes is %f",
            n, maxDistance(n, fuel));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// distance covered using n bikes
import java.io.*;

class GFG
{
    // Function that returns maximum distance that can be traveled by n bikes
    // and given fuel in every bike
    static double maxDistance(int n, int fuel)
    {
         // dist_covered is the result of this function
        double dist_covered = 0;

        while (n > 0)
        {
            // after ever fuel/n km we are discarding one bike and filling
            // all the other bikes with fuel/n liters of fuel i.e. to their
            // maximum limit (100 litre)

            dist_covered += (double)fuel / n;

            n -= 1;  // reduce number of bikes
        }
        return dist_covered;
    }

    // driver program
    public static void main (String[] args)
    {
        int n = 3; // number of bikes
        int fuel = 100;
        System.out.println("Maximum distance possible with "
                                   + n + " bikes is " + maxDistance(n, fuel));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python 3 program to find the maximum
# distance covered using n bikes

# Returns maximum distance that can be
# traveled by n bikes and given fuel
# in every bike
def maxDistance(n, fuel):

    # dist_covered is the result
    # of this function
    dist_covered = 0

    while (n > 0):

        # after ever fuel/n km we are
        # discarding one bike and filling
        # all the other bikes with fuel/n
        # liters of fuel i.e. to their
        # maximum limit (100 litre)
        dist_covered = dist_covered + (fuel / n)

        # reduce number of bikes
        n = n - 1

    return dist_covered

# Driver Code
if __name__ =='__main__':
    n = 3

    # number of bikes
    fuel = 100
    print("Maximum distance possible with",
       n, "bikes is", maxDistance(n, fuel))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the maximum
// distance covered using n bikes
using System;

class GFG {

    // Function that returns maximum distance
    // that can be travelled by n bikes
    // and given fuel in every bike
    static double maxDistance(int n, int fuel)
    {
        // dist_covered is the result of this function
        double dist_covered = 0;

        while (n > 0) {

            // after ever fuel/n km we are discarding
            // one bike and filling all the other bikes
            // with fuel/n liters of fuel i.e. to their
            // maximum limit (100 litre)
            dist_covered += (double)fuel / n;

            n -= 1; // reduce number of bikes
        }
        return dist_covered;
    }

    // driver program
    public static void Main()
    {
        // number of bikes
        int n = 3;
        int fuel = 100;
        Console.WriteLine("Maximum distance possible with " + n +
                          " bikes is " + maxDistance(n, fuel));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Returns maximum distance that can
// be traveled by n bikes and given
// fuel in every bike

function maxDistance($n, $fuel)
{
    // dist_covered is the result
    // of this function
    $dist_covered = 0;

    while ($n > 0)
    {
        // after ever fuel/n km we are
        // discarding one bike and filling
        // all the other bikes with fuel/n
        // liters of fuel i.e. to their
        // maximum limit (100 litre)

        $dist_covered += (double)$fuel / $n;

        // reduce number of bikes
        $n -= 1;
    }
    return $dist_covered;
}

// Driver Code

// number of bikes
$n = 3;
$fuel = 100;
echo "Maximum distance possible with ",
                      $n, " bikes is ",
                maxDistance($n, $fuel);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find the maximum
// distance covered using n bikes

// Function that returns maximum distance
// that can be travelled by n bikes
// and given fuel in every bike
function maxDistance(n, fuel)
{

    // dist_covered is the result of this function
    let dist_covered = 0;

    while (n > 0)
    {

        // After ever fuel/n km we are discarding
        // one bike and filling all the other bikes
        // with fuel/n liters of fuel i.e. to their
        // maximum limit (100 litre)
        dist_covered += fuel / n;

        // Reduce number of bikes
        n -= 1;
    }
    return dist_covered.toFixed(6);
}

// Driver code

// Number of bikes
let n = 3;
let fuel = 100;

document.write("Maximum distance possible with " + n +
               " bikes is " + maxDistance(n, fuel));

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
Maximum distance possible with 3 bikes is 183.333333
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)

本文由 [**Shamik Mitra**](https://www.facebook.com/shamik.mitra1) 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息